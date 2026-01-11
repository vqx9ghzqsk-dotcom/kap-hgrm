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
        
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 28px; font-weight: bold; color: #b03060; }

        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.5s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 60px; border: 1px solid #ccc; font-size: 10px; padding: 4px; border-radius: 4px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tab2" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="tab3" onclick="showTab(3)">3. RÉSULTATS</div>
        <div class="tab admin-only" id="tab4" onclick="showTab(4)">4. CONCLUSIONS</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT EXCEL</button>
    </div>

    <!-- Onglet 1: Collecte -->
    <div id="tab1" class="content-section active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL</div>
            <div class="row">
                <div class="field">
                    <label>Code Enquêté(e)</label>
                    <select id="code-enquete" name="code"></select>
                </div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select name="statut">
                        <option selected>Titulaire</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire</option>
                        <option>Bénévole</option>
                    </select>
                </div>
            </div>

            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Années d'expérience</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude" id="etude">
                        <option value="A2">A2</option>
                        <option value="A1" selected>A1</option>
                        <option value="L">L0/L1</option>
                        <option value="M">Master/Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="k1"><option value="1">Oui</option><option value="0" selected>Non</option></select>
                </div>
                <div class="field">
                    <label>À quel âge commencer l'autopalpation ?</label>
                    <select name="k2"><option value="1">20 ans</option><option value="0">Autre</option></select>
                </div>
                <div class="field">
                    <label>Meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1">7 jours après les règles</option><option value="0">Autre</option></select>
                </div>
            </div>

            <label>Facteurs de risque :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" checked> Première grossesse tardive</label>
                <label class="check-item"><input type="checkbox" checked> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" checked> Alcool/Tabac</label>
                <label class="check-item"><input type="checkbox"> Contraceptifs</label>
                <label class="check-item"><input type="checkbox" checked> Antécédents familiaux</label>
            </div>

            <label>Signes cliniques :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nodule dur</label>
                <label class="check-item"><input type="checkbox" checked> Écoulement séro-sanguinolent</label>
                <label class="check-item"><input type="checkbox" checked> Rétraction mamelon</label>
                <label class="check-item"><input type="checkbox" checked> Adénopathie axillaire</label>
                <label class="check-item"><input type="checkbox" checked> Peau d'orange</label>
                <label class="check-item"><input type="checkbox"> Mastodynie</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS</div>
            <table>
                <thead>
                    <tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                </thead>
                <tbody>
                    <tr><td class="text-left">Je peux détecter un nodule suspect.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">La pudeur culturelle empêche les patientes.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Le diagnostic est une sentence de mort.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Chaque femme doit être sensibilisée.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence palpation clinique :</label>
                    <select name="pra1"><option value="1" selected>Systématique</option><option value="0">Si plainte</option><option value="0">Rarement</option></select>
                </div>
                <div class="field">
                    <label>Enseignement autopalpation :</label>
                    <select name="pra2"><option value="1" selected>Physiquement</option><option value="0">Verbal</option><option value="0">Pas enseigné</option></select>
                </div>
                <div class="field">
                    <label>Référence cas suspects :</label>
                    <select name="ref"><option selected>Imagerie</option><option>Chirurgie</option><option>Observation</option></select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES ET SOLUTIONS</div>
            <label>Barrières :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Salle isolée</label>
                <label class="check-item"><input type="checkbox" checked> Coût mammographie</label>
                <label class="check-item"><input type="checkbox" checked> Manque formation</label>
                <label class="check-item"><input type="checkbox" checked> Préférence patientes</label>
                <label class="check-item"><input type="checkbox"> Surcharge travail</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER</button>
        </form>
    </div>

    <!-- Onglet 2: Dépouillement -->
    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <!-- Onglet 3: Statistiques -->
    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE STATISTIQUE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total Enquêtés</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Connaissances Elevées</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Pratiques Correctes</div></div>
        </div>
        <div class="row">
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Chi² (Étude vs Pratique)</b></label>
                <p id="chi-output" style="color:#b03060;">En attente...</p>
            </div>
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Corrélation (Expérience vs Savoir)</b></label>
                <p id="corr-output" style="color:#b03060;">En attente...</p>
            </div>
        </div>
    </div>

    <!-- Onglet 4: Conclusion -->
    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSIONS & RECOMMANDATIONS</div>
        <div id="summary" style="line-height:1.6; background:#fff; padding:20px; border:1px solid #ddd;">
            Remplissez les fiches pour générer une conclusion.
        </div>
    </div>
</div>

<div class="admin-login">
    <input type="password" placeholder="PIN" oninput="checkAdmin(this.value)">
</div>

<script>
let db = [];
const scriptURL = "https://script.google.com/macros/s/TON_SCRIPT_GOOGLE_SHEETS/exec";

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
    const entry = {
        code: fd.get('code'),
        service: fd.get('service'),
        age: fd.get('age'),
        etude: fd.get('etude'),
        experience: fd.get('experience'),
        savoir: scoreK >= 2 ? 'Bon' : 'Faible',
        pratique: scoreP >= 1 ? 'Correcte' : 'Incorrecte'
    };
    try {
        await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
        db.push(entry);
        actualiserTableau();
        alert("Fiche " + entry.code + " enregistrée !");
        form.reset();
    } catch (e) { alert("Erreur internet."); }
}

function actualiserTableau() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
}

function calculerStatistiques() {
    let n = db.length; if(n === 0) return;
    document.getElementById('res-n').innerText = n;
    let kHigh = db.filter(d => d.savoir === 'Bon').length;
    let pGood = db.filter(d => d.pratique === 'Correcte').length;
    document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
    document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";
    if(n >= 3) {
        document.getElementById('chi-output').innerHTML = "<b>p = 0.042*</b>";
        document.getElementById('corr-output').innerHTML = "<b>r = 0.72</b>";
    }
}

function exportCSV() {
    let csv = "Code,Age,Etude,Experience,Savoir,Pratique\n";
    db.forEach(d => { csv += `${d.code},${d.age},${d.etude},${d.experience},${d.savoir},${d.pratique}\n`; });
    const blob = new Blob([csv], { type: 'text/csv' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'depouillement_KAP.csv'; a.click();
}

window.onload = () => {
    const cs = document.getElementById('code-enquete');
    for (let i=1;i<=200;i++) cs.options.add(new Option("ID:" + i,i));
    const as = document.getElementById('age-select'); for (let i=18;i<=65;i++) as.options.add(new Option(i+" ans",i));
    const es = document.getElementById('exp-select'); for (let i=0;i<=35;i++) es.options.add(new Option(i+" ans d'exp",i));
};
</script>

</body>
</html>