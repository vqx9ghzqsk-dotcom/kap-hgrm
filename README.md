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
select, input, textarea { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

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

/* Admin PIN */
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

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
            <div style="background: #f9f9f9; padding: 15px; border-radius: 8px; font-size: 13px; margin-bottom: 15px;">
                <p>Cher collègue, nous menons une étude sur les connaissances, attitudes et pratiques face au cancer du sein. Votre participation est volontaire et anonyme.</p>
                <label class="check-item"><input type="checkbox" required> Je consens à participer à cette étude après avoir été informé.</label>
            </div>
            <div class="row">
                <div class="field"><label>Code Fiche</label><select name="code" id="code-enquete"></select></div>
                <div class="field"><label>Date de collecte</label><input type="date" name="date_collecte"></div>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Âge (en années)</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Service d'Attache</label>
                    <select name="service">
                        <option>Médecine Interne</option><option>Chirurgie</option>
                        <option>Gynéco-Obstétrique</option><option>Pédiatrie</option>
                        <option>Urgences / Soins Intensifs</option><option>Autres</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Niveau d'Étude / Qualification</label>
                    <select name="etude">
                        <option value="A1">Gradué (A1)</option>
                        <option value="A0">Licencié (A0)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté / Expérience (années)</label><select name="experience" id="exp-select"></select></div>
            </div>

            <div class="section-title">III. ÉVALUATION DES CONNAISSANCES (SAVOIR)</div>
            <table>
                <thead><tr><th>Questions de Connaissances</th><th>Oui (1)</th><th>Non (0)</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Le cancer du sein est-il la première cause de mortalité par cancer chez la femme en RDC ?</td>
                        <td><input type="radio" name="k1" value="1" required></td><td><input type="radio" name="k1" value="0"></td></tr>
                    <tr><td class="text-left">L'autopalpation mammaire doit-elle être pratiquée chaque mois après les règles ?</td>
                        <td><input type="radio" name="k2" value="1"></td><td><input type="radio" name="k2" value="0"></td></tr>
                    <tr><td class="text-left">Une masse indolore au sein est-elle un signe d'alerte majeur ?</td>
                        <td><input type="radio" name="k3" value="1"></td><td><input type="radio" name="k3" value="0"></td></tr>
                    <tr><td class="text-left">L'hérédité est-elle un facteur de risque majeur ?</td>
                        <td><input type="radio" name="k4" value="1"></td><td><input type="radio" name="k4" value="0"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. ÉVALUATION DES ATTITUDES</div>
            <table>
                <thead><tr><th>Attitudes face au dépistage</th><th>Favorable</th><th>Défavorable</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Pensez-vous que le dépistage précoce peut guérir le cancer du sein ?</td>
                        <td><input type="radio" name="att1" value="1" required></td><td><input type="radio" name="att1" value="0"></td></tr>
                    <tr><td class="text-left">Seriez-vous prêt à recommander une mastectomie si nécessaire ?</td>
                        <td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="0"></td></tr>
                </tbody>
            </table>

            <div class="section-title">V. ÉVALUATION DES PRATIQUES</div>
            <table>
                <thead><tr><th>Pratiques Cliniques</th><th>Régulier (1)</th><th>Rarement (0)</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Réalisez-vous systématiquement l'examen physique des seins ?</td>
                        <td><input type="radio" name="pra1" value="1" required></td><td><input type="radio" name="pra1" value="0"></td></tr>
                    <tr><td class="text-left">Apprenez-vous aux patientes la technique d'autopalpation ?</td>
                        <td><input type="radio" name="pra2" value="1"></td><td><input type="radio" name="pra2" value="0"></td></tr>
                </tbody>
            </table>

            <div class="section-title">VI. LES OBSTACLES (FACTEURS LIMITANTS)</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="o1"> Absence de local isolé</label>
                <label class="check-item"><input type="checkbox" name="o2"> Coût élevé de la mammographie</label>
                <label class="check-item"><input type="checkbox" name="o3"> Manque de formation continue</label>
                <label class="check-item"><input type="checkbox" name="o4"> Croyances culturelles / Tabous</label>
                <label class="check-item"><input type="checkbox" name="o5"> Surcharge de travail</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS</div>
            <div class="field">
                <label>Vos suggestions pour améliorer la prise en charge à l'HGRM :</label>
                <textarea name="recommandations" rows="4" placeholder="Saisissez vos recommandations ici..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT (BASE DE DONNÉES)</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE STATISTIQUE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total N</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Savoir Bon</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Pratique Correcte</div></div>
        </div>
        <div class="row">
            <canvas id="facteursChart"></canvas>
            <canvas id="obstaclesChart"></canvas>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET RECOMMANDATION GÉNÉRALE</div>
        <div id="summary" style="padding:20px; border:1px solid #ddd; background: #fff;">
            En attente de données...
        </div>
    </div>
</div>

<div class="admin-login">
    <input type="password" placeholder="PIN" oninput="checkAdmin(this.value)">
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<script>
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
    if(!form.checkValidity()) { alert("Veuillez remplir tous les champs obligatoires."); return; }
    
    const fd = new FormData(form);
    
    // Scores
    let scoreK = (parseInt(fd.get('k1'))||0) + (parseInt(fd.get('k2'))||0) + (parseInt(fd.get('k3'))||0) + (parseInt(fd.get('k4'))||0);
    let scoreP = (parseInt(fd.get('pra1'))||0) + (parseInt(fd.get('pra2'))||0);

    const entry = {
        code: fd.get('code'),
        age: fd.get('age'),
        etude: fd.get('etude'),
        experience: fd.get('experience'),
        savoir: scoreK >= 3 ? 'Bon' : 'Faible',
        pratique: scoreP >= 1 ? 'Correcte' : 'Incorrecte',
        recos: fd.get('recommandations')
    };

    try {
        await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
        db.push(entry);
        actualiserTableau();
        alert("Fiche enregistrée !");
        form.reset();
    } catch(e) {
        alert("Erreur de sauvegarde.");
    }
}

function actualiserTableau() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
}

function calculerStatistiques() {
    if(db.length === 0) return;
    document.getElementById('res-n').innerText = db.length;
    let kBon = db.filter(d => d.savoir === 'Bon').length;
    let pCor = db.filter(d => d.pratique === 'Correcte').length;
    document.getElementById('res-k').innerText = Math.round(kBon/db.length*100) + "%";
    document.getElementById('res-p').innerText = Math.round(pCor/db.length*100) + "%";
}

function exportCSV() {
    let csv = "Code,Age,Etude,Exp,Savoir,Pratique\n";
    db.forEach(d => { csv += `${d.code},${d.age},${d.etude},${d.experience},${d.savoir},${d.pratique}\n`; });
    const blob = new Blob([csv], {type: 'text/csv'});
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'data.csv'; a.click();
}

window.onload = () => {
    const cs = document.getElementById('code-enquete');
    for(let i=1; i<=200; i++) cs.options.add(new Option("ID: "+i, i));
    const as = document.getElementById('age-select');
    for(let i=18; i<=65; i++) as.options.add(new Option(i+" ans", i));
    const es = document.getElementById('exp-select');
    for(let i=0; i<=35; i++) es.options.add(new Option(i+" ans", i));
};
</script>
</body>
</html>
