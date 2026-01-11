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

.section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; }

.consent-box { background: #fff3e0; border: 2px solid #ffb74d; padding: 20px; border-radius: 8px; margin-bottom: 20px; }
.row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
.field { display: flex; flex-direction: column; margin-bottom: 15px; }
label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
select, input, textarea { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

/* Tables */
table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
td { border: 1px solid #eee; padding: 12px; }

.check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
.check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }

.btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }

/* Stats */
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
        <div class="tab admin-only" id="tab2-tab" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="tab3-tab" onclick="showTab(3)">3. ANALYSE STATISTIQUE</div>
        <div class="tab admin-only" id="tab4-tab" onclick="showTab(4)">4. CONCLUSION</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
            <div class="consent-box">
                <p><strong>Note d'information :</strong> Cette enquête est réalisée dans le cadre de l'amélioration de la prise en charge du cancer du sein à l'HGRM. Vos réponses sont strictement confidentielles.</p>
                <label class="check-item"><input type="checkbox" required> Je confirme avoir été informé(e) et j'accepte de participer à cette étude.</label>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Code Fiche</label><select name="code" id="code-enquete"></select></div>
                <div class="field"><label>Service d'Attache</label><input type="text" name="service" required placeholder="ex: Chirurgie, Gynécologie..."></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge (ans)</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="etude" id="etude-select">
                        <option value="A1">Infirmier A1 (Gradué)</option>
                        <option value="A0">Infirmier A0 (Licencié)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté / Expérience</label><select name="experience" id="exp-select"></select></div>
            </div>

            <div class="section-title">III. ÉVALUATION DES CONNAISSANCES (SAVOIR GRADUÉ)</div>
            <div class="field">
                <label>1. Quels sont les facteurs de risque majeurs selon vous ?</label>
                <select name="k_facteurs">
                    <option value="0">Ignorance / Facteurs mystiques</option>
                    <option value="1">Alimentation et hygiène de vie seulement</option>
                    <option value="2">Hérédité, Nulliparité, Ménopause tardive, Mutations BRCA (Niveau Expert)</option>
                </select>
            </div>
            <div class="field">
                <label>2. Quels sont les signes cliniques précoces ?</label>
                <select name="k_signes">
                    <option value="0">Douleur intense uniquement</option>
                    <option value="1">Présence d'une boule palpable</option>
                    <option value="2">Masse indolore, fixée, modification du mamelon ou de la peau (Peau d'orange)</option>
                </select>
            </div>
            <div class="field">
                <label>3. Quel est le bilan para-clinique de choix pour le dépistage ?</label>
                <select name="k_paraclinique">
                    <option value="0">Radiographie du thorax</option>
                    <option value="1">Échographie simple</option>
                    <option value="2">Mammographie bilatérale associée à l'Écho-mammaire (Standard de référence)</option>
                </select>
            </div>
            <div class="field">
                <label>4. Quels sont les signes de gravité ou stade avancé ?</label>
                <select name="k_gravite">
                    <option value="0">Juste une rougeur</option>
                    <option value="1">Adénopathie axillaire palpable</option>
                    <option value="2">Ulcération, fixation au plan profond, adénopathies sus-claviculaires (Niveau Expert)</option>
                </select>
            </div>

            <div class="section-title">IV. ÉVALUATION DES ATTITUDES</div>
            <div class="field">
                <label>Pensez-vous que le dépistage précoce peut réduire la mortalité à l'HGRM ?</label>
                <select name="att_mortalite">
                    <option value="0">Non, c'est une maladie fatale</option>
                    <option value="1">Peut-être, mais les moyens manquent</option>
                    <option value="2">Oui, c'est le pilier de la prise en charge (Attitude Positive)</option>
                </select>
            </div>
            <div class="field">
                <label>Comment réagissez-vous face à une patiente avec une masse mammaire ?</label>
                <select name="att_reaction">
                    <option value="0">Rassurer sans examens</option>
                    <option value="1">Donner des antibiotiques</option>
                    <option value="2">Prescrire une imagerie et référer en spécialité immédiatement</option>
                </select>
            </div>

            <div class="section-title">V. ÉVALUATION DES PRATIQUES</div>
            <div class="field">
                <label>Réalisez-vous systématiquement l'examen clinique des seins (ECS) ?</label>
                <select name="pra_ecs">
                    <option value="0">Jamais</option>
                    <option value="1">Seulement si la patiente demande</option>
                    <option value="2">Régulièrement pour toute femme en âge de procréer</option>
                </select>
            </div>
            <div class="field">
                <label>Apprenez-vous l'autopalpation aux patientes ?</label>
                <select name="pra_auto">
                    <option value="0">Non, je ne maîtrise pas la technique</option>
                    <option value="1">Parfois, si j'ai le temps</option>
                    <option value="2">Oui, systématiquement avec démonstration</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES ET RECOMMANDATIONS</div>
            <label>Obstacles majeurs rencontrés :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="o1"> Coût élevé de la mammographie</label>
                <label class="check-item"><input type="checkbox" name="o2"> Manque de formation continue du personnel</label>
                <label class="check-item"><input type="checkbox" name="o3"> Absence de matériel de dépistage (Plateau technique)</label>
                <label class="check-item"><input type="checkbox" name="o4"> Pudeur et croyances des patientes</label>
            </div>
            
            <div class="field" style="margin-top:20px;">
                <label>Vos recommandations pour améliorer le service :</label>
                <textarea name="recommandations" rows="4" placeholder="Ex: Subventionner les examens, organiser des séminaires..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE CLINIQUE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Profil</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">RÉSULTATS ET ANALYSE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Total N</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div>Expertise Savoir</div></div>
        </div>
        <div class="row">
            <canvas id="canvasPie"></canvas>
            <canvas id="canvasBar"></canvas>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION</div>
        <div id="summary-box" style="padding:20px; background:#f9f9f9; border-radius:10px; line-height:1.6;">
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
        alert("Mode Admin Activé");
    }
}

function showTab(n) {
    document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
    document.getElementById('tab' + n).classList.add('active');
    document.querySelectorAll('.tab')[n-1].classList.add('active');
    if(n === 3) generateCharts();
}

async function saveData() {
    const form = document.getElementById('kapForm');
    if(!form.checkValidity()) { alert("Veuillez accepter le consentement"); return; }
    
    const fd = new FormData(form);
    
    // Calcul du score Savoir (sur 8 points max)
    let scoreK = parseInt(fd.get('k_facteurs')) + parseInt(fd.get('k_signes')) + parseInt(fd.get('k_paraclinique')) + parseInt(fd.get('k_gravite'));
    let scoreP = parseInt(fd.get('pra_ecs')) + parseInt(fd.get('pra_auto'));

    const entry = {
        code: fd.get('code'),
        profil: fd.get('etude'),
        savoir: scoreK >= 6 ? 'Expert' : (scoreK >= 4 ? 'Moyen' : 'Faible'),
        pratique: scoreP >= 3 ? 'Correcte' : 'Incorrecte'
    };

    db.push(entry);
    updateTable();
    alert("Fiche enregistrée !");
    form.reset();
}

function updateTable() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.profil}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
}

function generateCharts() {
    if(db.length === 0) return;
    document.getElementById('res-n').innerText = db.length;
    
    const kData = [
        db.filter(d => d.savoir === 'Expert').length,
        db.filter(d => d.savoir === 'Moyen').length,
        db.filter(d => d.savoir === 'Faible').length
    ];

    new Chart(document.getElementById('canvasPie'), {
        type: 'pie',
        data: {
            labels: ['Expert', 'Moyen', 'Faible'],
            datasets: [{ data: kData, backgroundColor: ['#b03060', '#f06292', '#f8bbd0'] }]
        }
    });

    new Chart(document.getElementById('canvasBar'), {
        type: 'bar',
        data: {
            labels: ['Pratique Correcte', 'Pratique Incorrecte'],
            datasets: [{ 
                label: 'Nombre',
                data: [db.filter(d=>d.pratique==='Correcte').length, db.filter(d=>d.pratique==='Incorrecte').length],
                backgroundColor: '#b03060'
            }]
        }
    });
}

function exportCSV() {
    let csv = "Code,Profil,Savoir,Pratique\n" + db.map(d => `${d.code},${d.profil},${d.savoir},${d.pratique}`).join("\n");
    const blob = new Blob([csv], { type: 'text/csv' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'data_HGRM.csv'; a.click();
}

window.onload = () => {
    const cs = document.getElementById('code-enquete');
    for(let i=1;i<=200;i++) cs.options.add(new Option("ID: "+i, i));
    const as = document.getElementById('age-select');
    for(let i=18;i<=65;i++) as.options.add(new Option(i+" ans", i));
    const es = document.getElementById('exp-select');
    for(let i=0;i<=40;i++) es.options.add(new Option(i+" ans", i));
};
</script>
</body>
</html>
