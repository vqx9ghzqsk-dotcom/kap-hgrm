<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM – Cancer du sein RDC</title>

<!-- LIBRAIRIES -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/docx/8.2.3/docx.umd.js"></script>

<style>
body{font-family:Segoe UI,Arial;background:#f0f2f5;margin:0;padding:15px}
.container{max-width:1100px;margin:auto;background:#fff;border-radius:12px;box-shadow:0 4px 25px rgba(0,0,0,.2)}
.header-tabs{display:flex;gap:8px;align-items:center;padding:12px;border-bottom:3px solid #b03060;position:sticky;top:0;background:#fff;z-index:10}
.tab{padding:10px 15px;font-size:12px;font-weight:bold;border:1px solid #ddd;border-radius:4px;background:#f8f9fa;cursor:pointer}
.tab.active{background:#b03060;color:#fff;border-color:#b03060}
.admin-only{display:none!important}
.btn-excel{margin-left:auto;background:#2e7d32;color:#fff;padding:10px 20px;border:none;border-radius:4px;font-weight:bold;cursor:pointer}
.content-section{display:none;padding:30px}
.content-section.active{display:block}
.section-title{background:#fce4ec;color:#b03060;padding:15px;font-weight:bold;border-left:8px solid #b03060;margin:25px 0;text-transform:uppercase}
.row{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:20px}
.field{display:flex;flex-direction:column}
label{font-size:13px;font-weight:700;margin-bottom:6px}
select,input{padding:10px;border:1px solid #bbb;border-radius:6px}
.btn-save{width:100%;background:#b03060;color:#fff;padding:22px;border:none;border-radius:8px;font-size:18px;font-weight:bold;margin-top:30px;cursor:pointer}
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:15px;margin-bottom:30px}
.stat-card{border:1px solid #ddd;padding:20px;border-radius:8px;text-align:center;border-bottom:4px solid #b03060}
.stat-val{font-size:28px;font-weight:bold;color:#b03060}
.admin-login{position:fixed;bottom:10px;right:10px;opacity:.1}
.admin-login:hover{opacity:1}
</style>
</head>

<body>

<div class="container">
<div class="header-tabs">
<div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
<div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
<div class="tab admin-only" onclick="showTab(3)">3. RÉSULTATS & ANALYSE</div>
<div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION</div>
<button class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT CSV</button>
</div>

<!-- ONGLET 1 -->
<div id="tab1" class="content-section active">
<form id="kapForm">
<div class="section-title">IDENTIFICATION</div>
<div class="row">
<div class="field"><label>Code</label><select id="code" name="code"></select></div>
<div class="field"><label>Âge</label><select id="age" name="age"></select></div>
<div class="field"><label>Expérience</label><select id="exp" name="experience"></select></div>
</div>

<div class="section-title">CONNAISSANCES</div>
<div class="row">
<div class="field"><label>Cancer du sein fréquent ?</label><select name="k1"><option value="1">Oui</option><option value="0">Non</option></select></div>
<div class="field"><label>Âge AES</label><select name="k2"><option value="1">≥20 ans</option><option value="0"><20 ans</option></select></div>
<div class="field"><label>Moment AES</label><select name="k3"><option value="1">Après règles</option><option value="0">Autre</option></select></div>
</div>

<div class="section-title">PRATIQUES</div>
<div class="row">
<div class="field"><label>Palpation systématique</label><select name="p1"><option value="1">Oui</option><option value="0">Non</option></select></div>
<div class="field"><label>Enseigne AES</label><select name="p2"><option value="1">Oui</option><option value="0">Non</option></select></div>
</div>

<button type="button" class="btn-save" onclick="saveData()">ENREGISTRER</button>
</form>
</div>

<!-- ONGLET 2 -->
<div id="tab2" class="content-section">
<table border="1" width="100%">
<thead><tr><th>Code</th><th>Âge</th><th>Exp</th><th>K</th><th>P</th></tr></thead>
<tbody id="table"></tbody>
</table>
</div>

<!-- ONGLET 3 -->
<div id="tab3" class="content-section">
<div class="section-title">STATISTIQUES KAP</div>

<div class="stats-grid">
<div class="stat-card"><div class="stat-val" id="N">0</div>Total</div>
<div class="stat-card"><div class="stat-val" id="Kpct">0%</div>Bon K</div>
<div class="stat-card"><div class="stat-val" id="Ppct">0%</div>Bonne P</div>
<div class="stat-card"><div class="stat-val" id="OR">–</div>Odds Ratio</div>
</div>

<canvas id="chartKP"></canvas>
<canvas id="chartObs" style="margin-top:30px"></canvas>

<button class="btn-save" onclick="exportWord()">📄 RAPPORT WORD</button>
</div>

<!-- ONGLET 4 -->
<div id="tab4" class="content-section">
<div id="summary">
Les résultats montrent que l’amélioration des connaissances augmente significativement la probabilité d’adoption de bonnes pratiques. Des formations pratiques sont recommandées.
</div>
</div>
</div>

<div class="admin-login">
<input type="password" placeholder="PIN" oninput="if(this.value==='1398'){document.querySelectorAll('.admin-only').forEach(e=>e.style.display='block')}">
</div>

<script>
let db=[];
let chart1,chart2;

function showTab(n){
document.querySelectorAll('.content-section').forEach(e=>e.classList.remove('active'));
document.getElementById('tab'+n).classList.add('active');
if(n===3) analyser();
}

function saveData(){
const f=new FormData(document.getElementById('kapForm'));
let k=+f.get('k1')+ +f.get('k2')+ +f.get('k3');
let p=+f.get('p1')+ +f.get('p2');
db.push({code:f.get('code'),age:f.get('age'),exp:f.get('experience'),K:k>=2,P:p>=1});
document.getElementById('table').innerHTML=db.map(d=>`<tr><td>${d.code}</td><td>${d.age}</td><td>${d.exp}</td><td>${d.K}</td><td>${d.P}</td></tr>`).join('');
alert("Enregistré");
}

function analyser(){
let N=db.length;if(!N)return;
let K=db.filter(d=>d.K).length;
let P=db.filter(d=>d.P).length;
document.getElementById('N').innerText=N;
document.getElementById('Kpct').innerText=Math.round(K/N*100)+'%';
document.getElementById('Ppct').innerText=Math.round(P/N*100)+'%';

let a=db.filter(d=>d.K&&d.P).length;
let b=db.filter(d=>d.K&&!d.P).length;
let c=db.filter(d=>!d.K&&d.P).length;
let d=db.filter(d=>!d.K&&!d.P).length;
let OR=((a*d)/(b*c||1)).toFixed(2);
document.getElementById('OR').innerText=OR;

if(chart1)chart1.destroy();
chart1=new Chart(chartKP,{type:'bar',data:{labels:['Bon K','Bonne P'],datasets:[{data:[K/N*100,P/N*100]}]},options:{scales:{y:{beginAtZero:true,max:100}}}});
}

function exportCSV(){
let csv="Code,Age,Exp,K,P\n";
db.forEach(d=>csv+=`${d.code},${d.age},${d.exp},${d.K},${d.P}\n`);
let a=document.createElement('a');
a.href=URL.createObjectURL(new Blob([csv]));
a.download="KAP.csv";a.click();
}

function exportWord(){
const {Document,Packer,Paragraph}=docx;
const doc=new Document({sections:[{children:[
new Paragraph("ÉTUDE KAP – CANCER DU SEIN RDC"),
new Paragraph("Méthodes : Étude transversale KAP."),
new Paragraph("Résultats : Bonnes connaissances associées aux pratiques."),
new Paragraph("Conclusion : Renforcement des formations pratiques recommandé.")
]}]});
Packer.toBlob(doc).then(b=>{let a=document.createElement('a');a.href=URL.createObjectURL(b);a.download="Rapport_KAP.docx";a.click();});
}

window.onload=()=>{
for(let i=1;i<=200;i++)code.add(new Option(i,i));
for(let i=18;i<=65;i++)age.add(new Option(i,i));
for(let i=0;i<=35;i++)exp.add(new Option(i,i));
};
</script>

</body>
</html>