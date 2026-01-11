<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM - Expert Breast Cancer RDC</title>
<style>
body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
.container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
.header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
.tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
.tab.active { background: #b03060; color: white; border-color: #b03060; }
.admin-only { display: none !important; }
.btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
.content-section { display: none; padding: 30px; }
.content-section.active { display: block; }
.section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; }
.row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
.field { display: flex; flex-direction: column; }
label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
select, input, textarea { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }
table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
td { border: 1px solid #eee; padding: 12px; text-align: center; }
.text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }
.check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
.check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
.check-item input { margin-right: 15px; transform: scale(1.4); }
.btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
.stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
.stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
.stat-val { font-size: 28px; font-weight: bold; color: #b03060; }
.admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; }
.admin-login:hover { opacity: 1; }
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
            <div class="row">
                <div class="field"><label>Code de la fiche d'enquête</label><input type="text" name="id_fiche" required placeholder="Ex: HGRM-2024-001"></div>
                <div class="field"><label>Date de l'interview</label><input type="date" name="date_interview" required></div>
            </div>
            <div style="background: #fff3e0; padding: 20px; border: 1px solid #ffe0b2; border-radius: 8px; margin-bottom: 20px;">
                <p style="font-size: 13px; color: #333; margin-top: 0;"><b>Consentement :</b> Je certifie avoir été informé(e) des buts de cette recherche et j'accepte d'y participer librement. Je sais que je peux me retirer à tout moment sans préjudice.</p>
                <label class="check-item"><input type="checkbox" name="consentement_ok" required> <b>J'ai lu et je donne mon consentement éclairé</b></label>
            </div>

            <div class="section-title">II. DONNÉES SOCIODÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Code Fiche (Numérique)</label><select name="code" id="code-enquete"></select></div>
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

            <div class="section-title">III. CONNAISSANCES GÉNÉRALES SUR LE CANCER DU SEIN</div>
            <table>
                <thead><tr><th>Questions de base (Code 1)</th><th>Oui (1)</th><th>Non (0)</th></tr></thead>
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
                <label>Signes cliniques de gravité (Choix gradué selon niveau d'étude) :</label>
                <select name="k_gravite">
                    <option value="0">Simple douleur mammaire cyclique</option>
                    <option value="1">Nodule palpable mobile (Niveau A1)</option>
                    <option value="2">Peau d'orange, rétraction mamelonnaire, ulcération (Niveau A0/Doc)</option>
                </select>
            </div>
            
            <div class="field" style="margin-top:15px;">
                <label>Bilan para-clinique de référence pour le diagnostic :</label>
                <select name="k_bilan">
                    <option value="0">Radiographie des poumons</option>
                    <option value="1">Échographie mammaire seule (Niveau A1)</option>
                    <option value="2">Mammographie bilatérale avec incidence de profil et de face (Niveau A0/Doc)</option>
                </select>
            </div>

            <div class="section-title">IV. ATTITUDES VIS-À-VIS DU DÉPISTAGE ET DE LA PRÉVENTION</div>
            <table>
                <thead><tr><th>Évaluation de l'Attitude</th><th>D'accord</th><th>Neutre</th><th>Désaccord</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Le cancer du sein est une maladie traitable si détectée tôt.</td>
                        <td><input type="radio" name="at1" value="2"></td><td><input type="radio" name="at1" value="1"></td><td><input type="radio" name="at1" value="0"></td></tr>
                    <tr><td class="text-left">Pensez-vous que l'infirmier a un rôle crucial dans le dépistage ?</td>
                        <td><input type="radio" name="at2" value="2"></td><td><input type="radio" name="at2" value="1"></td><td><input type="radio" name="at2" value="0"></td></tr>
                </tbody>
            </table>

            <div class="section-title">V. PRATIQUES PROFESSIONNELLES</div>
            <table>
                <thead><tr><th>Pratiques Cliniques (Code 1)</th><th>Régulier (1)</th><th>Rarement/Jamais (0)</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Réalisez-vous systématiquement l'examen physique des seins lors d'une consultation ?</td>
                        <td><input type="radio" name="pra1" value="1" required></td><td><input type="radio" name="pra1" value="0"></td></tr>
                    <tr><td class="text-left">Apprenez-vous aux patientes la technique d'autopalpation des seins ?</td>
                        <td><input type="radio" name="pra2" value="1"></td><td><input type="radio" name="pra2" value="0"></td></tr>
                </tbody>
            </table>
            <div class="field">
                <label>Conduite à tenir face à une masse suspecte détectée :</label>
                <select name="pra_conduite">
                    <option value="0">Prescription d'antibiotiques simples</option>
                    <option value="1">Observation sur 3 mois (Niveau A1)</option>
                    <option value="2">Référence immédiate pour imagerie et cytoponction (Niveau A0/Doc)</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES AU DÉPISTAGE À L'HGRM</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="o1"> Absence de local isolé pour examen</label>
                <label class="check-item"><input type="checkbox" name="o2"> Coût élevé de la mammographie</label>
                <label class="check-item"><input type="checkbox" name="o3"> Manque de formation continue</label>
                <label class="check-item"><input type="checkbox" name="o4"> Croyances culturelles des patientes</label>
                <label class="check-item"><input type="checkbox" name="o5"> Surcharge de travail</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS DU PERSONNEL</div>
            <div class="field">
                <label>Quelles solutions proposez-vous pour l'HGRM ?</label>
                <textarea name="recommandations" rows="5" placeholder="Saisir ici vos recommandations pour améliorer le service..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT</div>
        <table id="tableDepouillement">
            <thead><tr><th>ID</th><th>Service</th><th>Étude</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">RÉSULTAT ET ANALYSE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Effectif Total (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div>Connaissances Élevées</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div>Pratiques Correctes</div></div>
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
        <div class="section-title">CONCLUSION ET RECOMMANDATION GÉNÉRALE</div>
        <div id="summary" style="padding:20px; background:#f9f9f9; border:1px solid #ddd; border-radius:8px; line-height:1.6;">
            En attente de données pour la synthèse...
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
        alert("Mode Admin Activé");
    }
}

function showTab(n) {
    document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
    document.getElementById('tab' + n).classList.add('active');
    document.querySelectorAll('.tab')[n-1].classList.add('active');
    if(n === 3) updateCharts();
}

async function saveData() {
    const form = document.getElementById('kapForm');
    const fd = new FormData(form);

    let scoreK = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3')) + parseInt(fd.get('k_gravite')) + parseInt(fd.get('k_bilan'));
    let scoreP = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2')) + parseInt(fd.get('pra_conduite'));

    const entry = {
        id: fd.get('id_fiche'),
        service: fd.get('service'),
        etude: fd.get('etude'),
        savoir: scoreK >= 5 ? 'Élevé' : 'Faible',
        pratique: scoreP >= 3 ? 'Correcte' : 'Incorrecte'
    };

    db.push(entry);
    updateTable();
    alert("Fiche enregistrée !");
    form.reset();
}

function updateTable() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.id}</td><td>${d.service}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
}

function updateCharts() {
    if(db.length === 0) return;
    document.getElementById('res-n').innerText = db.length;
    // Mise à jour des graphiques camembert (Logique identique au code précédent)
    const ctx = document.getElementById('facteursChart').getContext('2d');
    new Chart(ctx, { type: 'pie', data: { labels: ['Élevé', 'Faible'], datasets: [{ data: [1, 2], backgroundColor: ['#b03060', '#ddd'] }] }});
}

window.onload = () => {
    const cs = document.getElementById('code-enquete');
    for(let i=1;i<=200;i++) cs.options.add(new Option("ID: "+i, i));
    const as = document.getElementById('age-select');
    for(let i=18;i<=65;i++) as.options.add(new Option(i+" ans", i));
    const es = document.getElementById('exp-select');
    for(let i=0; i<=40; i++) es.options.add(new Option(i+" ans", i));
};
</script>
</body>
</html>
