<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM - Base de Données & Analyse Expert</title>

<style>
body {font-family:'Segoe UI',Arial;background:#f0f2f5;margin:0;padding:15px}
.container{max-width:1200px;margin:auto;background:white;border-radius:12px;box-shadow:0 4px 25px rgba(0,0,0,0.2)}
.header-tabs{display:flex;background:#fff;border-bottom:3px solid #b03060;padding:12px;gap:8px;position:sticky;top:0}
.tab{padding:10px 15px;font-weight:bold;font-size:12px;border-radius:4px;border:1px solid #ddd;background:#f8f9fa;cursor:pointer}
.tab.active{background:#b03060;color:white}
.btn-excel{margin-left:auto;background:#2e7d32;color:white;padding:10px 20px;border:none;border-radius:4px;font-weight:bold}
.form-content{padding:30px;display:none}
.form-content.active{display:block}
.section-title{background:#fce4ec;color:#b03060;padding:15px;font-weight:bold;border-left:8px solid #b03060;margin:30px 0}
.row{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:20px}
.field{display:flex;flex-direction:column}
select,input{padding:10px;border:1px solid #bbb;border-radius:6px}
table{width:100%;border-collapse:collapse}
th,td{border:1px solid #ddd;padding:10px;text-align:center}
.check-group{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr))}
.btn-save{width:100%;background:#b03060;color:white;padding:20px;border:none;border-radius:8px;font-size:18px;font-weight:bold}
.bar-container{display:flex;align-items:center;margin:6px 0}
.bar-label{width:180px}
.bar-track{flex:1;background:#eee;border-radius:4px;overflow:hidden}
.bar-fill{height:18px;color:white;text-align:center;font-size:11px}
.counter-badge{background:#b03060;color:white;padding:2px 8px;border-radius:10px;margin-left:5px}
</style>
</head>

<body>

<div class="container">

<div class="header-tabs">
<button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
<button class="tab" onclick="switchTab(2)">2. DEPLOUILLEMENT</button>
<button class="tab" onclick="switchTab(3)">3. ANALYSE</button>
<button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
<button class="btn-excel" onclick="exportToCSV()">EXPORT CSV</button>
</div>

<!-- ================= COLLECTE ================= -->
<div id="content-1" class="form-content active">

<div class="section-title">PRATIQUES</div>

<div class="row">

<div class="field">
<label>Fréquence palpation</label>
<select id="pratique-freq">
<option>Systématique</option>
<option>Si plainte</option>
<option>Rarement</option>
</select>
</div>

<div class="field">
<label>Enseignement AES</label>
<select id="pratique-enseigne">
<option>Démonstration physique</option>
<option>Verbalement</option>
<option>Pas d'enseignement</option>
</select>
</div>

<div class="field">
<label>Palpé ce matin ?</label>
<select id="pratique-matin">
<option>Oui</option>
<option>Non</option>
</select>
</div>

<div class="field">
<label>Technique de palpation</label>
<select id="pratique-technique">
<option>Palpation rapide sans méthode précise</option>
<option>Méthode systématique (Quadrant par quadrant)</option>
<option>Méthode complète (Quadrant + creux axillaire + mamelon)</option>
</select>
</div>

</div>

<button class="btn-save" onclick="saveRecord()">ENREGISTRER</button>

</div>

<!-- ================= TABLEAU ================= -->
<div id="content-2" class="form-content">

<table>
<thead>
<tr>
<th>#</th>
<th>Score Pratique</th>
<th>Score KAP Global</th>
</tr>
</thead>
<tbody id="database-body"></tbody>
</table>

</div>

<!-- ================= ANALYSE ================= -->
<div id="content-3" class="form-content">

<div class="section-title">Comparaison Techniques de Palpation</div>
<div id="graph-technique"></div>

</div>

<!-- ================= CONCLUSION ================= -->
<div id="content-4" class="form-content">

<div id="final-conclusion"></div>

</div>

</div>

<script>

let database=[];

function saveRecord(){

let freq=document.getElementById("pratique-freq").value;
let enseigne=document.getElementById("pratique-enseigne").value;
let matin=document.getElementById("pratique-matin").value;
let technique=document.getElementById("pratique-technique").value;

let scorePratique=0;

if(freq=="Systématique") scorePratique+=30;
if(enseigne=="Démonstration physique") scorePratique+=30;
else if(enseigne=="Verbalement") scorePratique+=10;
if(matin=="Oui") scorePratique+=10;

if(technique.includes("rapide")) scorePratique+=10;
if(technique.includes("systématique")) scorePratique+=20;
if(technique.includes("complète")) scorePratique+=30;

if(scorePratique>100) scorePratique=100;

let scoreKAP=Math.round(scorePratique);

database.push({scorePratique,scoreKAP,technique});

document.getElementById("count-badge").textContent=database.length;

updateTable();
updateGraph();
}

function updateTable(){

let body=document.getElementById("database-body");
body.innerHTML="";

database.forEach((r,i)=>{
body.innerHTML+=`<tr>
<td>${i+1}</td>
<td>${r.scorePratique}%</td>
<td><b>${r.scoreKAP}%</b></td>
</tr>`;
});

}

function updateGraph(){

let rapide=database.filter(r=>r.technique.includes("rapide")).length;
let syst=database.filter(r=>r.technique.includes("systématique")).length;
let comp=database.filter(r=>r.technique.includes("complète")).length;

let total=database.length;

function bar(label,val,color){
let pct=total?Math.round(val/total*100):0;
return `<div class="bar-container">
<div class="bar-label">${label}</div>
<div class="bar-track">
<div class="bar-fill" style="width:${pct}%;background:${color}">${pct}%</div>
</div>
</div>`;
}

document.getElementById("graph-technique").innerHTML=
bar("Rapide",rapide,"#c62828")+
bar("Systématique",syst,"#f9a825")+
bar("Complète",comp,"#2e7d32");

document.getElementById("final-conclusion").innerHTML=
`<h3>Total fiches : ${total}</h3>
<p>Méthode complète utilisée par ${Math.round(comp/total*100||0)}%</p>`;
}

function switchTab(i){
document.querySelectorAll(".form-content").forEach(d=>d.classList.remove("active"));
document.querySelectorAll(".tab").forEach(b=>b.classList.remove("active"));
document.getElementById("content-"+i).classList.add("active");
document.querySelector(".header-tabs button:nth-child("+i+")").classList.add("active");
}

function exportToCSV(){

if(database.length==0){alert("Aucune donnée");return;}

let csv="ID,Pratique,KAP,Technique\n";

database.forEach((r,i)=>{
csv+=`${i+1},${r.scorePratique},${r.scoreKAP},"${r.technique}"\n`;
});

let a=document.createElement("a");
a.href="data:text/csv;charset=utf-8,"+encodeURIComponent(csv);
a.download="KAP_HGRM.csv";
a.click();
}

</script>

</body>
</html>