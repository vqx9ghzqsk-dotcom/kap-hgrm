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

    <div id="tab1" class="content-section active">
        <form class="form-content" id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
            <div style="background: #fff8fb; padding: 15px; border: 1px solid #f06292; border-radius: 8px; margin-bottom: 20px;">
                <p style="font-size: 13px; color: #555;">Cette étude vise à évaluer les connaissances, attitudes et pratiques des infirmiers de l'HGRM sur le cancer du sein. Les données sont anonymes.</p>
                <label class="check-item"><input type="checkbox" name="consentement" required> <b>J'accepte de participer à cette enquête après avoir été informé(e).</b></label>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Code Fiche</label><select name="code" id="code-enquete"></select></div>
                <div class="field"><label>Service d'Attache</label>
                    <select name="service">
                        <option>Médecine Interne</option><option>Chirurgie</option>
                        <option>Gynéco-Obstétrique</option><option>Pédiatrie</option>
                        <option>Urgences / Soins Intensifs</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge (ans)</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="etude" id="etude-select">
                        <option value="A1">Gradué (A1)</option>
                        <option value="A0">Licencié (A0)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté / Expérience</label><select name="experience" id="exp-select"></select></div>
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
                </tbody>
            </table>

            <div class="field">
                <label>Signes de gravité (stade avancé) :</label>
                <select name="k_gravite">
                    <option value="0">Douleur simple au bras</option>
                    <option value="1">Présence d'un nodule fixe (A1)</option>
                    <option value="2">Peau d'orange, ulcération mammaire, adénopathies sus-claviculaires (A0/Doc)</option>
                </select>
            </div>
            <div class="field" style="margin-top:15px;">
                <label>Bilan para-clinique de référence :</label>
                <select name="k_bilan">
                    <option value="0">Radiographie standard</option>
                    <option value="1">Échographie mammaire (A1)</option>
                    <option value="2">Mammographie bilatérale couplée à l'Écho-mammaire (A0/Doc)</option>
                </select>
            </div>

            <div class="section-title">IV. ÉVALUATION DES ATTITUDES</div>
            <div class="field">
                <label>Quelle est votre attitude face à une patiente suspecte ?</label>
                <select name="att_attitude">
                    <option value="0">Rassurer la patiente et attendre (Niveau élémentaire)</option>
                    <option value="1">Prescrire des anti-inflammatoires (Niveau intermédiaire)</option>
                    <option value="2">Référer immédiatement pour biopsie ou imagerie spécialisée (Niveau expert)</option>
                </select>
            </div>

            <div class="section-title">V. ÉVALUATION DES PRATIQUES PROFESSIONNELLES</div>
            <table>
                <thead><tr><th>Pratiques Cliniques</th><th>Régulier (1)</th><th>Rarement/Jamais (0)</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Réalisez-vous systématiquement l'examen physique des seins lors d'une consultation ?</td>
                        <td><input type="radio" name="pra1" value="1" required></td><td><input type="radio" name="pra1" value="0"></td></tr>
                    <tr><td class="text-left">Apprenez-vous aux patientes la technique d'autopalpation des seins ?</td>
                        <td><input type="radio" name="pra2" value="1"></td><td><input type="radio" name="pra2" value="0"></td></tr>
                </tbody>
            </table>

            <div class="section-title">VI. FACTEURS ET OBSTACLES (MULTIPLE)</div>
            <label>Facteurs de risque identifiés (Plusieurs choix possibles) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="f1"> Nulliparité / Grossesse tardive</label>
                <label class="check-item"><input type="checkbox" name="f2"> Ménopause tardive (>55 ans)</label>
                <label class="check-item"><input type="checkbox" name="f3"> Tabagisme / Alcoolisme</label>
                <label class="check-item"><input type="checkbox" name="f4"> Utilisation prolongée de contraceptifs</label>
                <label class="check-item"><input type="checkbox" name="f5"> Antécédents familiaux (Hérédité BRCA)</label>
            </div>

            <br>
            <label>Obstacles majeurs au dépistage à l'HGRM :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="o1"> Absence de local isolé pour examen</label>
                <label class="check-item"><input type="checkbox" name="o2"> Coût élevé de la mammographie</label>
                <label class="check-item"><input type="checkbox" name="o3"> Manque de formation continue</label>
                <label class="check-item"><input type="checkbox" name="o4"> Croyances culturelles des patientes</label>
                <label class="check-item"><input type="checkbox" name="o5"> Surcharge de travail</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS</div>
            <div class="field">
                <label>Vos suggestions pour améliorer la prise en charge à l'HGRM :</label>
                <textarea name="recommandations" rows="4" placeholder="Saisir vos recommandations ici..."></textarea>
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
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total Enquêtés (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Connaissances Elevées</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Pratiques Correctes</div></div>
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

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION</div>
        <div id="summary" style="line-height:1.6; background:#fff; padding:20px; border:1px solid #ddd;">
            Remplissez les fiches pour générer une conclusion.
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
    document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
    document.getElementById('tab' + n).classList.add('active');
    document.querySelectorAll('.tab')[n-1].classList.add('active');
    if(n === 3) calculerStatistiques();
}

async function saveData() {
    const form = document.getElementById('kapForm');
    const fd = new FormData(form);

    let scoreK = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3')) + parseInt(fd.get('k_gravite')) + parseInt(fd.get('k_bilan'));
    let scoreP = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));
    const facteurs = [fd.get('f1'), fd.get('f2'), fd.get('f3'), fd.get('f4'), fd.get('f5')].map(v => v === 'on');
    const obstacles = [fd.get('o1'), fd.get('o2'), fd.get('o3'), fd.get('o4'), fd.get('o5')].map(v => v === 'on');

    const entry = {
        code: fd.get('code'), service: fd.get('service'), age: fd.get('age'),
        etude: fd.get('etude'), experience: fd.get('experience'),
        savoir: scoreK >= 5 ? 'Bon' : 'Faible',
        pratique: scoreP >= 1 ? 'Correcte' : 'Incorrecte',
        facteurs, obstacles
    };

    try {
        await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
        db.push(entry);
        actualiserTableau();
        alert("Fiche Code " + entry.code + " enregistrée !");
        form.reset();
    } catch(e) { alert("Erreur."); }
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

    const fLabels = ['Nulliparité','Ménopause','Alcool/Tabac','Contraceptifs','Hérédité'];
    const fCount = [0,1,2,3,4].map(i => db.reduce((sum, d) => sum + (d.facteurs[i] ? 1 : 0), 0));
    renderChart('facteursChart', 'Facteurs de risque', fLabels, fCount);

    const oLabels = ["Salle","Coût","Formation","Culture","Surcharge"];
    const oCount = [0,1,2,3,4].map(i => db.reduce((sum, d) => sum + (d.obstacles[i] ? 1 : 0), 0));
    renderChart('obstaclesChart', 'Obstacles', oLabels, oCount);
}

function renderChart(id, title, labels, data) {
    let canvas = document.getElementById(id);
    if(canvas.chart) canvas.chart.destroy();
    canvas.chart = new Chart(canvas, {
        type: 'pie',
        data: { labels: labels, datasets: [{ label: title, data: data, backgroundColor: ['#b03060','#f06292','#f8bbd0','#e91e63','#c2185b'] }]},
        options: { responsive: true }
    });
}

function exportCSV() {
    let csv = "Code,Age,Etude,Experience,Savoir,Pratique\n";
    db.forEach(d => { csv += `${d.code},${d.age},${d.etude},${d.experience},${d.savoir},${d.pratique}\n`; });
    const blob = new Blob([csv], { type: 'text/csv' });
    const a = document.createElement('a'); a.href = window.URL.createObjectURL(blob); a.download = 'donnees.csv'; a.click();
}

window.onload = () => {
    const cs = document.getElementById('code-enquete');
    for(let i=1;i<=200;i++) cs.options.add(new Option("ID: "+i, i));
    const as = document.getElementById('age-select');
    for(let i=18;i<=65;i++) as.options.add(new Option(i+" ans", i));
    const es = document.getElementById('exp-select');
    for(let i=0; i<=35; i++) es.options.add(new Option(i+" ans d'exp", i));
};
</script>

</body>
</html>
