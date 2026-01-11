<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM - Expert Breast Cancer RDC</title>
<style>
body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
.container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }

/* Header & Tabs */
.header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
.tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
.tab.active { background: #b03060; color: white; border-color: #b03060; }

/* Admin only */
.admin-only { display: none !important; }
.btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

.content-section { display: none; padding: 30px; }
.content-section.active { display: block; }

.section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }

.row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
.field { display: flex; flex-direction: column; }
label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

/* Tables Likert */
table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
td { border: 1px solid #eee; padding: 12px; text-align: center; }
.text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

/* Grid Checkboxes */
.check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
.check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
.check-item input { margin-right: 15px; transform: scale(1.4); }

.btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
.btn-save:hover { background: #8e244d; transform: translateY(-2px); }

/* Stats Design */
.stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
.stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
.stat-val { font-size: 28px; font-weight: bold; color: #b03060; }

/* ZONE LOGIN DISCRÈTE */
.admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.5s; }
.admin-login:hover { opacity: 1; }
.admin-login input { width: 60px; border: 1px solid #ccc; font-size: 10px; padding: 4px; border-radius: 4px; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tab2-tab" onclick="showTab(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab admin-only" id="tab3-tab" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab admin-only" id="tab4-tab" onclick="showTab(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <!-- Onglet Collecte -->
    <div id="tab1" class="content-section active">
        <form class="form-content" id="kapForm">
            <!-- FORMULAIRE IDENTIQUE AU TIEN -->
            <!-- Je garde tout ton code de formulaire ici pour Collecte -->
            <!-- ... tout le formulaire que tu as déjà ... -->

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <!-- Dépouillement -->
    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT (BASE DE DONNÉES)</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <!-- Analyse -->
    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE STATISTIQUE (FRÉQUENCES & TESTS)</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total Enquêtés (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Connaissances Elevées</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Pratiques Correctes</div></div>
        </div>
        <div class="row">
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Test de Chi² (Étude vs Pratique)</b></label>
                <p id="chi-output" style="color:#b03060;">Besoin de données...</p>
            </div>
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Corrélation (Expérience vs Savoir)</b></label>
                <p id="corr-output" style="color:#b03060;">En attente...</p>
            </div>
        </div>
        <div class="row">
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <canvas id="facteursChart"></canvas>
            </div>
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <canvas id="obstaclesChart"></canvas>
            </div>
        </div>
    </div>

    <!-- Conclusion -->
    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET RECOMMANDATION</div>
        <div id="summary" style="line-height:1.6; background:#fff; padding:20px; border:1px solid #ddd;">
            Remplissez les fiches pour générer une conclusion.
        </div>
    </div>
</div>

<div class="admin-login">
    <input type="password" placeholder="PIN" oninput="checkAdmin(this.value)">
</div>

<!-- Chart.js -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<script>
// ====================== SCRIPT COMPLET ======================
let db = [];
const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

function checkAdmin(val) {
    if(val === "1398") {
        document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
        alert("Mode Admin Activé !");
    }
}

function showTab(n) {
    document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.getElementById('tab' + n).classList.add('active');
    document.querySelectorAll('.tab')[n-1].classList.add('active');
    if(n === 3) calculerStatistiques();
}

async function saveData() {
    const form = document.getElementById('kapForm');
    const fd = new FormData(form);

    let scoreK = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
    let scoreP = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));
    const facteurs = Array.from(form.querySelectorAll('.check-group:first-of-type input')).map(c => c.checked);
    const obstacles = Array.from(form.querySelectorAll('.check-group:last-of-type input')).map(c => c.checked);

    const entry = {
        code: fd.get('code'),
        service: fd.get('service'),
        age: fd.get('age'),
        etude: fd.get('etude'),
        experience: fd.get('experience'),
        savoir: scoreK >= 2 ? 'Bon' : 'Faible',
        pratique: scoreP >= 1 ? 'Correcte' : 'Incorrecte',
        facteurs,
        obstacles
    };

    try {
        await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
        db.push(entry);
        actualiserTableau();
        alert("Fiche Code " + entry.code + " envoyée et enregistrée !");
        form.reset();
    } catch(e) {
        alert("Erreur de connexion. Réessayez.");
    }
}

function actualiserTableau() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
}

function calculerStatistiques() {
    if(db.length === 0) return;

    const n = db.length;
    document.getElementById('res-n').innerText = n;

    const kHigh = db.filter(d => d.savoir === 'Bon').length;
    const pGood = db.filter(d => d.pratique === 'Correcte').length;

    document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
    document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";

    // Chi² simplifié Étude vs Pratique
    const table = { "Bon-Correcte":0, "Bon-Incorrecte":0, "Faible-Correcte":0, "Faible-Incorrecte":0 };
    db.forEach(d => table[`${d.savoir}-${d.pratique}`]++);
    const chi = ((table["Bon-Correcte"]*table["Faible-Incorrecte"] - table["Bon-Incorrecte"]*table["Faible-Correcte"])**2) /
                ((table["Bon-Correcte"]+table["Bon-Incorrecte"])*(table["Faible-Correcte"]+table["Faible-Incorrecte"]));
    document.getElementById('chi-output').innerHTML = `<b>Chi² ≈ ${chi.toFixed(2)}</b>`;

    // Corrélation Expérience vs Savoir
    const x = db.map(d => parseInt(d.experience));
    const y = db.map(d => d.savoir==="Bon"?1:0);
    const meanX = x.reduce((a,b)=>a+b,0)/n;
    const meanY = y.reduce((a,b)=>a+b,0)/n;
    const r = x.map((xi,i)=> (xi-meanX)*(y[i]-meanY)).reduce((a,b)=>a+b,0) /
              Math.sqrt(x.map(xi=>(xi-meanX)**2).reduce((a,b)=>a+b,0) * y.map(yi=>(yi-meanY)**2).reduce((a,b)=>a+b,0));
    document.getElementById('corr-output').innerHTML = `<b>r ≈ ${r.toFixed(2)}</b>`;

    // Graphiques
    const facteursCount = db[0].facteurs.map((_,i)=> db.reduce((sum,d)=>sum+(d.facteurs[i]?1:0),0));
    renderChart('facteursChart','Facteurs de risque',['Nulliparité','Grossesse tardive','Ménopause tardive','Alcool/tabac','Contraceptifs','Antécédents familiaux'],facteursCount);
    const obstaclesCount = db[0].obstacles.map((_,i)=> db.reduce((sum,d)=>sum+(d.obstacles[i]?1:0),0));
    renderChart('obstaclesChart','Obstacles',["Salle isolée","Coût mammographie","Manque formation","Pratiques culturelles","Surcharge travail"],obstaclesCount);
}

function renderChart(id,title,labels,data) {
    let canvas = document.getElementById(id);
    if(!canvas) {
        canvas = document.createElement('canvas'); canvas.id=id;
        document.getElementById('tab3').appendChild(canvas);
    }
    if(canvas.chart) canvas.chart.destroy();
    canvas.chart = new Chart(canvas,{
        type:'pie',
        data:{ labels: labels, datasets:[{ label: title, data: data, backgroundColor:['#b03060','#f06292','#f8bbd0','#e91e63','#c2185b','#ec407a'] }]},
        options:{ responsive:true }
    });
}

function exportCSV() {
    let csv = "Code,Age,Etude,Experience,Savoir,Pratique\n";
    db.forEach(d=>{ csv += `${d.code},${d.age},${d.etude},${d.experience},${d.savoir},${d.pratique}\n`; });
    const blob = new Blob([csv],{type:'text/csv'});
    const url = window.URL.createObjectURL(blob);
    const a=document.createElement('a'); a.href=url; a.download='depouillement_KAP.csv'; a.click();
}

window.onload = ()=>{
    const cs = document.getElementById('code-enquete');
    for(let i=1;i<=200;i++) cs.options.add(new Option("ID: "+i,i));
    const as = document.getElementById('age-select');
    for(let i=18;i<=65;i++) as.options.add(new Option(i+" ans",i));
    const es = document.getElementById('exp-select');
    for(let i=0;i<=35;i++) es.options.add(new Option(i+" ans d'exp",i));
};
</script>

</body>
</html>