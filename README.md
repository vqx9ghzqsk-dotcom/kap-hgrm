<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Système Expert CAP - HGRM Makala</title>

<style>
:root { --primary:#be185d; --secondary:#1e293b; --accent:#db2777; --bg:#f8fafc; --text:#334155; }
body{font-family:'Segoe UI',system-ui;background:var(--bg);margin:0}
.container{max-width:1100px;margin:20px auto;padding:20px}

/* Tabs */
.nav-tabs{display:flex;gap:5px;background:#e2e8f0;padding:5px;border-radius:10px}
.tab-btn{flex:1;padding:12px;border:none;border-radius:8px;font-weight:600;cursor:pointer}
.tab-btn.active{background:var(--primary);color:#fff}

/* Pages */
.page{display:none;background:#fff;padding:30px;border-radius:12px;margin-top:20px}
.page.active{display:block}

/* Form KAP */
.section-title{
background:#fce4ec;color:#b03060;padding:15px;font-weight:bold;
border-left:8px solid #b03060;margin:30px 0 15px;text-transform:uppercase
}
.row{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px}
.field{display:flex;flex-direction:column}
label{font-weight:600;font-size:13px;margin-bottom:6px}
select,input{padding:12px;border:1px solid #bbb;border-radius:6px}
.check-group{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:10px;border:1px solid #eee;padding:15px;border-radius:8px}
.check-item{display:flex;align-items:center;font-size:13px}
.check-item input{margin-right:10px;transform:scale(1.3)}

.btn-action{background:var(--primary);color:#fff;border:none;padding:20px;border-radius:8px;font-size:18px;font-weight:bold;width:100%;cursor:pointer}
.btn-action:hover{background:var(--accent)}
</style>
</head>

<body>
<div class="container">

<div class="nav-tabs">
<button class="tab-btn active" onclick="openPage('recolte')">1. COLLECTE</button>
<button class="tab-btn" onclick="openPage('traitement')">2. DÉPOUILLEMENT</button>
<button class="tab-btn" onclick="openPage('resultats')">3. RÉSULTATS</button>
<button class="tab-btn" onclick="openPage('discussion')">4. ANALYSE</button>
<button class="tab-btn" onclick="openPage('conclusion')">5. CONCLUSION</button>
</div>

<!-- =================== COLLECTE (REMPLACÉE) =================== -->
<div id="recolte" class="page active">

<form id="formCollecte">

<div class="section-title">I. IDENTIFICATION & PROFIL</div>
<div class="row">
<div class="field"><label>Code enquêté(e)</label><input name="code"></div>
<div class="field"><label>Service</label><input name="service"></div>
<div class="field"><label>Statut professionnel</label>
<select name="statut">
<option>Titulaire</option><option>Garde</option><option>Stagiaire</option>
</select></div>
</div>

<div class="row">
<div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
<div class="field"><label>Expérience</label><select id="exp-select" name="experience"></select></div>
<div class="field"><label>Niveau d’étude</label>
<select name="niveau">
<option>A2</option><option>A1</option><option>L0/L1</option><option>Master+</option>
</select></div>
</div>

<div class="section-title">II. CONNAISSANCES</div>
<div class="row">
<div class="field"><label>Cancer du sein = première cause en RDC ?</label>
<select name="c1"><option>Vrai</option><option>Faux</option><option>NSP</option></select></div>
<div class="field"><label>Début AES</label>
<select name="c2"><option>12 ans</option><option>20 ans</option><option>40 ans</option></select></div>
</div>

<div class="section-title">III. PRATIQUES</div>
<div class="row">
<div class="field"><label>Enseignez-vous l’AES ?</label>
<select name="p_enseigne"><option>Oui</option><option>Non</option></select></div>
<div class="field"><label>Palpation clinique</label>
<select name="palpation"><option>Systématique</option><option>Rare</option></select></div>
</div>

<div class="section-title">IV. OBSTACLES</div>
<div class="check-group">
<label class="check-item"><input type="checkbox"> Coût mammographie</label>
<label class="check-item"><input type="checkbox"> Manque formation</label>
<label class="check-item"><input type="checkbox"> Charge de travail</label>
</div>

<button type="button" class="btn-action" onclick="sauvegarderDonnees()">VALIDER LA FICHE</button>

</form>
</div>

<!-- =================== AUTRES PAGES (INCHANGÉES) =================== -->
<div id="traitement" class="page"><h2>Dépouillement</h2><div id="tableContainer"></div></div>
<div id="resultats" class="page"><h2>Résultats</h2></div>
<div id="discussion" class="page"><h2>Analyse</h2></div>
<div id="conclusion" class="page"><h2>Conclusion</h2></div>

</div>

<script>
let database = JSON.parse(localStorage.getItem('memo_makala_db')) || [];

function openPage(id){
document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
document.getElementById(id).classList.add('active');
document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
event.target.classList.add('active');
}

function sauvegarderDonnees(){
const data = Object.fromEntries(new FormData(formCollecte).entries());
database.push(data);
localStorage.setItem('memo_makala_db', JSON.stringify(database));
alert("Fiche enregistrée");
formCollecte.reset();
}

/* Auto age & expérience */
for(let i=18;i<=60;i++){ageSelect.innerHTML+=`<option>${i}</option>`}
expSelect.innerHTML+=`<option>Moins d’un an</option>`;
for(let i=1;i<=30;i++){expSelect.innerHTML+=`<option>${i} ans</option>`}
</script>

</body>
</html>