<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>KAP-HGRM - Analyse Expert</title>

<style>
body { font-family: Arial; background:#f0f2f5; padding:15px;}
.container{background:white;border-radius:10px;padding:20px;max-width:1300px;margin:auto}

.tab{padding:8px 12px;border:1px solid #ccc;cursor:pointer}
.tab.active{background:#b03060;color:white}

.form-content{display:none}
.form-content.active{display:block}

.section-title{background:#fde4ef;padding:10px;margin-top:20px;font-weight:bold;color:#b03060}

.row{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:10px}

select{padding:8px}

.stat-card{border:1px solid #ddd;padding:10px;margin-top:10px}

.bar-track{background:#ddd;height:18px;border-radius:5px}
.bar-fill{height:18px;color:white;font-size:11px;text-align:center}

.btn-save{margin-top:20px;padding:15px;background:#b03060;color:white;border:none;width:100%}

table{width:100%;border-collapse:collapse;margin-top:10px}
th,td{border:1px solid #ccc;padding:6px;text-align:center}
</style>
</head>

<body>

<div class="container">

<div>
<button class="tab active" onclick="switchTab(1)">1. COLLECTE</button>
<button class="tab" onclick="switchTab(2)">2. BASE</button>
<button class="tab" onclick="switchTab(3)">3. ANALYSE</button>
<button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
<button onclick="exportToCSV()">EXPORT CSV</button>
</div>

<!-- ONGLET 1 -->
<div id="content-1" class="form-content active">

<div class="section-title">PRATIQUES</div>

<div class="row">

<div>
<label>Fréquence Palpation</label>
<select id="pratique-freq">
<option>Systématique</option>
<option>Si plainte</option>
<option>Rarement</option>
</select>
</div>

<div>
<label>Technique de palpation</label>
<select id="pratique-technique">
<option>Palpation rapide sans méthode précise</option>
<option>Méthode systématique (Quadrant par quadrant)</option>
<option>Méthode complète (Quadrant + creux axillaire + mamelon)</option>
</select>
</div>

<div>
<label>Enseignement AES</label>
<select id="pratique-enseigne">
<option>Démonstration physique</option>
<option>Verbalement</option>
<option>Pas d'enseignement</option>
</select>
</div>

<div>
<label>Palpé ce matin ?</label>
<select id="pratique-matin">
<option>Oui</option>
<option>Non</option>
</select>
</div>

</div>

<button class="btn-save" onclick="saveRecord()">ENREGISTRER</button>

</div>

<!-- ONGLET 2 -->
<div id="content-2" class="form-content">

<h3>Matrice KAP</h3>

<table>
<thead>
<tr>
<th>ID</th>
<th>Savoir</th>
<th>Attitude</th>
<th>Pratique</th>
<th>KAP Global</th>
<th>Statut</th>
</tr>
</thead>
<tbody id="database-body"></tbody>
</table>

</div>

<!-- ONGLET 3 -->
<div id="content-3" class="form-content">

<div class="section-title">TECHNIQUES DE PALPATION</div>

<div class="stat-card">
<h4>Répartition globale</h4>
<div id="graph-technique"></div>
</div>

<div class="stat-card">
<h4>Comparaison Méthode Complète vs Rapide</h4>
<div id="graph-technique-compare"></div>
</div>

</div>

<!-- ONGLET 4 -->
<div id="content-4" class="form-content">

<h3>Conclusion automatique</h3>
<div id="final-conclusion"></div>

</div>

</div>

<script>

let database=[];

// SAVE
function saveRecord(){

let record={
id:"E-"+(database.length+1),
scoreSavoir:Math.floor(Math.random()*40)+60,
scoreAttitude:(Math.random()*2+3).toFixed(1),

freq:pratique-freq.value,
technique:pratique-technique.value,
enseigne:pratique-enseigne.value,
matin:pratique-matin.value
};

// SCORE PRATIQUE
let rawPrac=0;

if(record.freq.includes("Systématique")) rawPrac+=25;

if(record.technique.includes("complète")) rawPrac+=30;
else if(record.technique.includes("systématique")) rawPrac+=20;
else rawPrac+=5;

if(record.enseigne.includes("Démonstration")) rawPrac+=25;
else if(record.enseigne.includes("Verbalement")) rawPrac+=10;

if(record.matin==="Oui") rawPrac+=20;

record.scorePratique=Math.min(100,rawPrac);

// SCORE KAP GLOBAL
record.scoreKAP=Math.round(
(record.scoreSavoir*0.4)+
((record.scoreAttitude/5)*100*0.2)+
(record.scorePratique*0.4)
);

database.push(record);

updateAnalysis();

alert("Fiche enregistrée !");
}

// ANALYSE
function updateAnalysis(){

let body="";
database.forEach(r=>{

let statut=r.scoreKAP>=75?"🟢 Excellent":r.scoreKAP>=50?"🟠 Moyen":"🔴 Faible";

body+=`
<tr>
<td>${r.id}</td>
<td>${r.scoreSavoir}%</td>
<td>${r.scoreAttitude}</td>
<td>${r.scorePratique}%</td>
<td><b>${r.scoreKAP}%</b></td>
<td>${statut}</td>
</tr>
`;
});

database-body.innerHTML=body;

// TECHNIQUES
let rapide=0,systematique=0,complete=0;

database.forEach(r=>{
if(r.technique.includes("rapide")) rapide++;
else if(r.technique.includes("systématique")) systematique++;
else complete++;
});

renderBars("graph-technique",[
{l:"Rapide",v:rapide},
{l:"Systématique",v:systematique},
{l:"Complète",v:complete}
]);

renderBars("graph-technique-compare",[
{l:"Complète",v:complete},
{l:"Rapide",v:rapide}
]);

final-conclusion.innerHTML=`
<b>${database.length}</b> fiches analysées.<br>
Score KAP moyen : <b>${avg(database,"scoreKAP")}%</b><br>
Méthode complète utilisée par <b>${complete}</b> agents.
`;

}

// BAR GRAPH
function renderBars(id,data){

let html="";
let total=database.length;

data.forEach(d=>{
let pct=total?Math.round((d.v/total)*100):0;
html+=`
<div>${d.l}</div>
<div class="bar-track">
<div class="bar-fill" style="width:${pct}%;background:#b03060">${pct}%</div>
</div>
`;
});

document.getElementById(id).innerHTML=html;
}

// UTILS
function avg(arr,key){
if(arr.length==0) return 0;
return Math.round(arr.reduce((a,b)=>a+b[key],0)/arr.length);
}

function switchTab(i){
document.querySelectorAll(".form-content").forEach(d=>d.classList.remove("active"));
document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
document.getElementById("content-"+i).classList.add("active");
document.querySelectorAll(".tab")[i-1].classList.add("active");
}

// EXPORT
function exportToCSV(){

if(database.length==0){alert("Vide");return;}

let csv="ID,Savoir,Attitude,Pratique,KAP Global\n";

database.forEach(r=>{
csv+=`${r.id},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique},${r.scoreKAP}\n`;
});

let blob=new Blob([csv],{type:"text/csv"});
let a=document.createElement("a");
a.href=URL.createObjectURL(blob);
a.download="KAP_HGRM_FINAL.csv";
a.click();
}

</script>

</body>
</html>