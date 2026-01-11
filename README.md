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
.content-section { display: none; padding: 30px; }
.content-section.active { display: block; }
.section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
.row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
.field { display: flex; flex-direction: column; margin-bottom: 10px; }
label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
select, input, textarea { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; }
table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 13px; }
th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
td { border: 1px solid #eee; padding: 12px; text-align: center; }
.text-left { text-align: left; width: 70%; padding-left: 15px; }
.check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; }
.btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 30px; }
.admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.5s; }
.admin-login:hover { opacity: 1; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" onclick="showTab(3)">3. ANALYSE STATISTIQUE</div>
        <div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
            <div class="row">
                <div class="field"><label>Code de l'enquête (ID)</label><input type="text" name="id_enquete" required placeholder="Ex: HGRM-001"></div>
                <div class="field"><label>Date de l'enquête</label><input type="date" name="date_enquete" required></div>
            </div>
            <div style="background: #fff3e0; padding: 15px; border-radius: 8px; border: 1px solid #ffe0b2;">
                <p style="font-size: 12px; margin: 0;"><i>"Je confirme avoir été informé des objectifs de l'étude et j'accepte de répondre au questionnaire de manière volontaire et anonyme."</i></p>
                <label style="font-size: 13px; margin-top: 10px; display: block;">
                    <input type="checkbox" name="consentement" required> **Je donne mon consentement éclairé**
                </label>
            </div>

            <div class="section-title">II. DONNÉES SOCIODÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Âge (Années)</label><select name="age" id="age-select"></select></div>
                <div class="field">
                    <label>Niveau d'étude / Profil professionnel</label>
                    <select name="etude" required>
                        <option value="A1">Infirmier(e) A1 (Gradué)</option>
                        <option value="A0">Infirmier(e) A0 (Licencié)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté dans le service</label><select name="experience" id="exp-select"></select></div>
            </div>

            <div class="section-title">III. CONNAISSANCES GÉNÉRALES ET CLINIQUES</div>
            <div class="field">
                <label>Quels sont les facteurs de risque majeurs ? (Choix selon expertise)</label>
                <select name="k_facteurs">
                    <option value="0">Aucune idée précise / Facteurs spirituels</option>
                    <option value="1">Antécédents familiaux et Tabac (Connaissance de base)</option>
                    <option value="2">Nulliparité, Ménopause tardive, Mutations BRCA1/2, Hyperoestrogénie (Expert)</option>
                </select>
            </div>
            <div class="field">
                <label>Signes de gravité et bilan para-clinique :</label>
                <select name="k_clinique">
                    <option value="0">Douleur au sein / Radio thorax</option>
                    <option value="1">Masse palpable / Échographie simple</option>
                    <option value="2">Peau d'orange, Adénopathies / Mammographie + Core-biopsie (Expert)</option>
                </select>
            </div>

            <div class="section-title">IV. ATTITUDES VIS-À-VIS DU DÉPISTAGE ET DE LA PRÉVENTION</div>
            <table>
                <tr><th class="text-left">Évaluation des Attitudes (Échelle de Likert)</th><th>D'accord</th><th>Neutre</th><th>Pas d'accord</th></tr>
                <tr><td class="text-left">Le dépistage précoce est-il prioritaire malgré le manque de moyens ?</td>
                    <td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="0"></td></tr>
                <tr><td class="text-left">Le personnel infirmier est-il capable de détecter une masse suspecte ?</td>
                    <td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="0"></td></tr>
            </table>

            <div class="section-title">V. PRATIQUES PROFESSIONNELLES</div>
            <div class="field">
                <label>Conduite à tenir face à une suspicion de tumeur :</label>
                <select name="pratique_conduite">
                    <option value="0">Prescrire des antibiotiques et observer</option>
                    <option value="1">Demander une échographie et revoir la patiente</option>
                    <option value="2">Référer immédiatement vers un service de chirurgie/oncologie (Pratique correcte)</option>
                </select>
            </div>
            <div class="field">
                <label>Fréquence de l'apprentissage de l'autopalpation aux patientes :</label>
                <select name="pratique_auto">
                    <option value="0">Jamais</option>
                    <option value="1">Parfois (si la patiente pose des questions)</option>
                    <option value="2">Systématiquement lors de chaque consultation (Recommandé)</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES AU DÉPISTAGE À L'HGRM</div>
            <div class="check-group">
                <label><input type="checkbox" name="obs1"> Manque de formation continue</label>
                <label><input type="checkbox" name="obs2"> Absence de matériel (Mammographe)</label>
                <label><input type="checkbox" name="obs3"> Coût élevé des examens pour les patientes</label>
                <label><input type="checkbox" name="obs4"> Surcharge de travail du personnel</label>
                <label><input type="checkbox" name="obs5"> Croyances socioculturelles négatives</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS DU PERSONNEL</div>
            <div class="field">
                <label>Que suggérez-vous pour améliorer la prévention et le dépistage ?</label>
                <textarea name="recommandations" rows="4" placeholder="Ex: Organisation de campagnes de masse, subvention des biopsies..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE DE COLLECTE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES (DÉPOUILLEMENT)</div>
        <table id="tableDepouillement">
            <thead><tr><th>ID</th><th>Profil</th><th>Savoir</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">RÉSULTATS ET ANALYSE (GRAPHIQUES)</div>
        <div class="row">
            <canvas id="chartSavoir"></canvas>
            <canvas id="chartPratique"></canvas>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET SYNTHÈSE</div>
        <div id="conclusionContent" style="padding: 20px; background: #f9f9f9; border-radius: 8px;">
            Les conclusions s'afficheront ici après l'analyse des données.
        </div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
let db = [];
function showTab(n) {
    document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
    document.querySelectorAll('.content-section')[n-1].classList.add('active');
    document.querySelectorAll('.tab')[n-1].classList.add('active');
    if(n===3) updateCharts();
}
function checkAdmin(v) { if(v==="1398") document.querySelectorAll('.admin-only').forEach(e=>e.style.display="block"); }

function saveData() {
    const form = document.getElementById('kapForm');
    if(!form.checkValidity()) { alert("Veuillez remplir tous les champs et accepter le consentement."); return; }
    
    const fd = new FormData(form);
    const entry = {
        id: fd.get('id_enquete'),
        profil: fd.get('etude'),
        savoir: parseInt(fd.get('k_facteurs')) + parseInt(fd.get('k_clinique')),
        pratique: parseInt(fd.get('pratique_conduite')) + parseInt(fd.get('pratique_auto'))
    };
    db.push(entry);
    alert("Fiche enregistrée avec succès !");
    updateTable();
    form.reset();
}

function updateTable() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.id}</td><td>${d.profil}</td><td>${d.savoir}/4</td><td>${d.pratique}/4</td></tr>`).join('');
}

function updateCharts() {
    // Logique simplifiée pour les graphiques camembert et barres
    const ctxS = document.getElementById('chartSavoir').getContext('2d');
    new Chart(ctxS, { type: 'pie', data: { labels: ['Bon', 'Moyen', 'Faible'], datasets: [{ data: [10, 20, 30], backgroundColor: ['#b03060', '#ec407a', '#f8bbd0'] }] }});
}

window.onload = () => {
    for(let i=20; i<=65; i++) document.getElementById('age-select').options.add(new Option(i+" ans", i));
    for(let i=0; i<=40; i++) document.getElementById('exp-select').options.add(new Option(i+" ans", i));
};
</script>
</body>
</html>
