<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM - Expert Breast Cancer RDC</title>

<!-- LIBRAIRIES -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/docx/8.2.3/docx.umd.js"></script>

<style>
body{font-family:'Segoe UI',Arial;background:#f0f2f5;padding:15px}
.container{max-width:1100px;margin:auto;background:white;border-radius:12px;box-shadow:0 4px 25px rgba(0,0,0,0.2)}
.header-tabs{display:flex;gap:8px;padding:12px;border-bottom:3px solid #b03060;position:sticky;top:0;background:#fff;z-index:1000}
.tab{padding:10px 15px;font-weight:bold;font-size:12px;border:1px solid #ddd;border-radius:4px;cursor:pointer;background:#f8f9fa}
.tab.active{background:#b03060;color:#fff;border-color:#b03060}
.admin-only{display:none!important}
.btn-excel{margin-left:auto;background:#2e7d32;color:#fff;border:none;padding:10px 20px;border-radius:4px;font-weight:bold;cursor:pointer}
.content-section{display:none;padding:30px}
.content-section.active{display:block}
.section-title{background:#fce4ec;color:#b03060;padding:15px;font-weight:bold;border-left:8px solid #b03060;margin:30px 0 15px;text-transform:uppercase}
.row{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:20px}
.btn-save{width:100%;background:#b03060;color:#fff;padding:25px;border:none;border-radius:8px;font-size:18px;font-weight:bold;margin-top:40px}
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:15px;margin-bottom:30px}
.stat-card{background:#fff;border:1px solid #ddd;padding:20px;border-radius:8px;text-align:center;border-bottom:4px solid #b03060}
.stat-val{font-size:28px;font-weight:bold;color:#b03060}
.admin-login{position:fixed;bottom:10px;right:10px;opacity:0.1}
.admin-login:hover{opacity:1}
.admin-login input{width:60px;font-size:10px}
canvas{background:#fff;border:1px solid #ddd;border-radius:8px;padding:10px}
</style>
</head>

<body>

<div class="container">
<div class="header-tabs">
<div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
<div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
<div class="tab admin-only" onclick="showTab(3)">3. RÉSULTAT & ANALYSE</div>
<div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION</div>
<button class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT CSV</button>
</div>

<!-- ONGLET 1 -->
<div id="tab1" class="content-section active">
<form id="kapForm">
<div class="section-title">COLLECTE KAP</div>

<input type="hidden" name="code" value="AUTO">

<label>K1</label><select name="k1"><option value="1">Vrai</option><option value="0">Faux</option></select>
<label>K2</label><select name="k2"><option value="1">Correct</option><option value="0">Faux</option></select>
<label>K3</label><select name="k3"><option value="1">Correct</option><option value="0">Faux</option></select>

<label>Pratique 1</label><select name="pra1"><option value="1">Oui</option><option value="0">Non</option></select>
<label>Pratique 2</label><select name="pra2"><option value="1">Oui</option><option value="0">Non</option></select>

<button type="button" class="btn-save" onclick="saveData()">ENREGISTRER</button>
</form>
</div>

<!-- ONGLET 2 -->
<div id="tab2" class="content-section">
<div class="section-title">BASE DE DONNÉES</div>
<table border="1" width="100%">
<thead><tr><th>ID</th><th>Savoir</th><th>Pratique</th></tr></thead>
<tbody id="dbTable"></tbody>
</table>
</div>

<!-- ONGLET 3 -->
<div id="tab3" class="content-section">
<div class="section-title">ANALYSE STATISTIQUE KAP</div>

<div class="stats-grid">
<div class="stat-card"><div class="stat-val" id="n">0</div>Total (N)</div>
<div class="stat-card"><div class="stat-val" id="k">0%</div>Savoir Bon</div>
<div class="stat-card"><div class="stat-val" id="p">0%</div>Pratique Correcte</div>
<div class="stat-card"><div class="stat-val" id="or">-</div>Odds Ratio</div>
</div>

<div class="row">
<canvas id="chartKP"></canvas>
<canvas id="chartPie"></canvas>
</div>

<button class="btn-save" onclick="exportWord()">📄 EXPORT RAPPORT WORD</button>
</div>

<!-- ONGLET 4 -->
<div id="tab4" class="content-section">
<div class="section-title">CONCLUSION</div>
<div id="summary">Analyse en attente…</div>
</div>

</div>

<div class="admin-login">
<input type="password" placeholder="PIN" oninput="checkAdmin(this.value)">
</div>

<script>
let db=[],chart1,chart2;

function checkAdmin(v){
if(v==="1398"){
document.querySelectorAll('.admin-only').forEach(e=>e.style.display="block");
alert("Admin activé");
}
}

function showTab(n){
document.querySelectorAll('.content-section').forEach(s=>s.classList.remove('active'));
document.getElementById("tab"+n).classList.add('active');
if(n===3) analyse();
}

function saveData(){
const fd=new FormData(document.getElementById('kapForm'));
let K=+fd.get('k1')+ +fd.get('k2')+ +fd.get('k3');
let P=+fd.get('pra1')+ +fd.get('pra2');
db.push({K:K>=2,P:P>=1});
document.getElementById('dbTable').innerHTML=db.map((d,i)=>`<tr><td>${i+1}</td><td>${d.K}</td><td>${d.P}</td></tr>`).join('');
alert("Enregistré");
}

function analyse(){
let N=db.length;if(N===0)return;
let Kb=db.filter(d=>d.K).length;
let Pb=db.filter(d=>d.P).length;

document.getElementById('n').innerText=N;
document.getElementById('k').innerText=Math.round(Kb/N*100)+"%";
document.getElementById('p').innerText=Math.round(Pb/N*100)+"%";

let a=db.filter(d=>d.K&&d.P).length;
let b=db.filter(d=>d.K&&!d.P).length;
let c=db.filter(d=>!d.K&&d.P).length;
let d=db.filter(d=>!d.K&&!d.P).length;
let OR=((a*d)/(b*c||1)).toFixed(2);
document.getElementById('or').innerText=OR;

drawCharts(Kb,Pb,N);
document.getElementById('summary').innerText=
`Les infirmiers ayant de bonnes connaissances ont ${OR} fois plus de chances d’adopter de bonnes pratiques.`;
}

function drawCharts(Kb,Pb,N){
if(chart1)chart1.destroy();
chart1=new Chart(chartKP,{type:'bar',data:{labels:['Savoir','Pratique'],datasets:[{data:[Kb/N*100,Pb/N*100]}]},options:{scales:{y:{max:100}}}});
if(chart2)chart2.destroy();
chart2=new Chart(chartPie,{type:'pie',data:{labels:['Bon','Faible'],datasets:[{data:[Kb,N-Kb]}]}});
}

function exportWord(){
const {Document,Packer,Paragraph}=docx;
const doc=new Document({sections:[{children:[
new Paragraph("RAPPORT KAP – CANCER DU SEIN RDC"),
new Paragraph("Méthodes : Étude KAP transversale."),
new Paragraph("Résultats : N="+db.length),
new Paragraph("Conclusion : Améliorer formations pratiques.")
]}]});
Packer.toBlob(doc).then(b=>{
let a=document.createElement("a");
a.href=URL.createObjectURL(b);
a.download="rapport_KAP.docx";
a.click();
});
}

function exportCSV(){
let csv="K,P\n";
db.forEach(d=>csv+=`${d.K},${d.P}\n`);
let a=document.createElement("a");
a.href=URL.createObjectURL(new Blob([csv]));
a.download="kap.csv";a.click();
}
</script>

</body>
</html>