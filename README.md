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
    .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    .admin-only { display: none !important; }
    .content-section { display: none; padding: 25px; }
    .content-section.active { display: block; }
    .section-title { background: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; border-left: 6px solid #b03060; margin: 25px 0 10px 0; text-transform: uppercase; font-size: 14px; }
    .consent-box { background: #fff3e0; border: 1px solid #ffb74d; padding: 15px; border-radius: 8px; margin-bottom: 20px; font-style: italic; font-size: 13px; }
    .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; margin-bottom: 10px; }
    .field { display: flex; flex-direction: column; }
    label { font-size: 13px; font-weight: 700; margin-bottom: 5px; color: #333; }
    select, input, textarea { padding: 10px; border: 1px solid #ccc; border-radius: 5px; font-size: 13px; }
    table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 12px; }
    th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; }
    td { border: 1px solid #eee; padding: 10px; text-align: left; }
    .graduated-choice { display: block; margin: 5px 0; font-weight: normal; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; }
    .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; }
    .admin-login:hover { opacity: 1; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE (FICHE INFIRMIÈRE)</div>
        <div class="tab admin-only" id="tab2-tab" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="tab3-tab" onclick="showTab(3)">3. ANALYSE STATISTIQUE</div>
        <div class="tab admin-only" id="tab4-tab" onclick="showTab(4)">4. CONCLUSIONS</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            
            <div class="section-title">I. CONSENTEMENT ÉCLAIRÉ</div>
            <div class="consent-box">
                "Je soussigné(e), accepte volontairement de participer à cette étude sur les connaissances, attitudes et pratiques liées au cancer du sein à l'HGRM. Je comprends que mes données sont anonymes et utilisées à des fins de recherche clinique pour améliorer la prise en charge."
                <br><br>
                <label><input type="checkbox" required> **Je donne mon consentement éclairé**</label>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Code Fiche</label><select name="code" id="code-enquete"></select></div>
                <div class="field"><label>Niveau d'Étude (Profil)</label>
                    <select name="etude" id="niveau-etude">
                        <option value="A1">Infirmier(e) A1 (Gradué)</option>
                        <option value="A0">Infirmier(e) A0 (Licencié)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Service d'attache</label><input type="text" name="service" placeholder="ex: Gynécologie, Chirurgie..." required></div>
                <div class="field"><label>Ancienneté (Années)</label><select name="experience" id="exp-select"></select></div>
            </div>

            <div class="section-title">III. ÉVALUATION DES CONNAISSANCES (GRADUÉES)</div>
            <p style="font-size:11px; color:#666;">*Choisissez la réponse la plus proche de votre niveau de compétence.*</p>
            
            <div class="field">
                <label>1. Quels sont les principaux facteurs de risque ?</label>
                <label class="graduated-choice"><input type="radio" name="k1" value="0"> Facteurs mystiques ou sortilèges</label>
                <label class="graduated-choice"><input type="radio" name="k1" value="1"> Hérédité et mauvaise alimentation</label>
                <label class="graduated-choice"><input type="radio" name="k1" value="2"> Nulliparité, Ménopause tardive, Mutation BRCA1/2, Exposition hormonale</label>
            </div>

            <div class="field" style="margin-top:15px;">
                <label>2. Quels sont les signes cliniques de gravité (Stades avancés) ?</label>
                <label class="graduated-choice"><input type="radio" name="k2" value="0"> Juste une douleur au bras</label>
                <label class="graduated-choice"><input type="radio" name="k2" value="1"> Masse palpable et changement de couleur de la peau</label>
                <label class="graduated-choice"><input type="radio" name="k2" value="2"> Peau d'orange, Adénopathies axillaires fixées, Ulcération mammaire, Écoulement sanglant</label>
            </div>

            <div class="field" style="margin-top:15px;">
                <label>3. Quel est le bilan para-clinique de référence pour le dépistage ?</label>
                <label class="graduated-choice"><input type="radio" name="k3" value="0"> Une simple radiographie du thorax</label>
                <label class="graduated-choice"><input type="radio" name="k3" value="1"> Échographie mammaire uniquement</label>
                <label class="graduated-choice"><input type="radio" name="k3" value="2"> Mammographie bilatérale complétée par Écho-mammaire +/- Biopsie (Core-biopsy)</label>
            </div>

            <div class="section-title">IV. ÉVALUATION DES ATTITUDES</div>
            <table>
                <tr><th>Face à une patiente suspecte, que pensez-vous ?</th><th>D'accord</th><th>Neutre</th><th>Désaccord</th></tr>
                <tr><td>Le cancer du sein est une fatalité où l'on ne peut rien faire.</td><td><input type="radio" name="at1" value="0"></td><td><input type="radio" name="at1" value="1"></td><td><input type="radio" name="at1" value="2"></td></tr>
                <tr><td>L'information sur l'autopalpation doit être donnée à chaque femme.</td><td><input type="radio" name="at2" value="2"></td><td><input type="radio" name="at2" value="1"></td><td><input type="radio" name="at2" value="0"></td></tr>
            </table>

            <div class="section-title">V. ÉVALUATION DES PRATIQUES (SOINS ET PRÉVENTION)</div>
            <div class="field">
                <label>Fréquence de l'examen clinique des seins (ECS) en consultation :</label>
                <select name="pra1">
                    <option value="0">Jamais (Manque de temps/intimité)</option>
                    <option value="1">Rarement (Uniquement si la patiente se plaint)</option>
                    <option value="2">Systématiquement pour toute femme > 35 ans</option>
                </select>
            </div>
            <div class="field" style="margin-top:10px;">
                <label>Action immédiate devant une masse suspecte :</label>
                <select name="pra2">
                    <option value="0">Prescrire des antibiotiques/anti-inflammatoires</option>
                    <option value="1">Demander de revenir dans 3 mois pour surveiller</option>
                    <option value="2">Référer immédiatement pour Imagerie (Mammographie) et avis spécialisé</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES IDENTIFIÉS</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="o1"> Coût financier exorbitant des examens</label>
                <label class="check-item"><input type="checkbox" name="o2"> Manque de plateau technique (Mammographe en panne/absent)</label>
                <label class="check-item"><input type="checkbox" name="o3"> Absence de protocoles standardisés de prise en charge</label>
                <label class="check-item"><input type="checkbox" name="o4"> Pudeur et barrières culturelles des patientes</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS DU PERSONNEL</div>
            <textarea name="recommandations" style="width:100%; height:80px;" placeholder="Vos suggestions pour améliorer le dépistage à l'HGRM..."></textarea>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE CLINIQUE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES DES ENQUÊTES</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Profil</th><th>Savoir</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">STATISTIQUES ET GRAPHIQUES</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Total Fiches</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div>Expertise Élevée</div></div>
        </div>
        <canvas id="mainChart" style="max-height: 400px;"></canvas>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS FINALES</div>
        <div id="summary" style="background:#f9f9f9; padding:20px; border-radius:10px; line-height:1.6;">
            En attente de données pour générer la synthèse automatique...
        </div>
    </div>
</div>

<div class="admin-login">
    <input type="password" placeholder="PIN" oninput="checkAdmin(this.value)">
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
let db = [];

function checkAdmin(val) {
    if(val === "1398") {
        document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
        alert("Accès Admin Autorisé");
    }
}

function showTab(n) {
    document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
    document.getElementById('tab'+n).classList.add('active');
    document.querySelectorAll('.tab')[n-1].classList.add('active');
    if(n === 3) updateStats();
}

function saveData() {
    const form = document.getElementById('kapForm');
    const fd = new FormData(form);
    
    // Calcul des scores basés sur les choix gradués
    let scoreK = (parseInt(fd.get('k1'))||0) + (parseInt(fd.get('k2'))||0) + (parseInt(fd.get('k3'))||0);
    let scoreA = (parseInt(fd.get('at1'))||0) + (parseInt(fd.get('at2'))||0);
    let scoreP = (parseInt(fd.get('pra1'))||0) + (parseInt(fd.get('pra2'))||0);

    const entry = {
        code: fd.get('code'),
        etude: fd.get('etude'),
        savoir: scoreK >= 4 ? 'Expert' : (scoreK >= 2 ? 'Moyen' : 'Faible'),
        attitude: scoreA >= 3 ? 'Positive' : 'Négative',
        pratique: scoreP >= 3 ? 'Correcte' : 'Incorrecte'
    };

    db.push(entry);
    alert("Fiche enregistrée !");
    updateTable();
    form.reset();
}

function updateTable() {
    const tbody = document.querySelector('#tableDepouillement tbody');
    tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td></tr>`).join('');
}

function updateStats() {
    if(db.length === 0) return;
    document.getElementById('res-n').innerText = db.length;
    const experts = db.filter(d => d.savoir === 'Expert').length;
    document.getElementById('res-k').innerText = Math.round(experts/db.length*100) + "%";
}

window.onload = () => {
    const codeSel = document.getElementById('code-enquete');
    for(let i=1; i<=150; i++) codeSel.options.add(new Option("Fiche ID-"+i, "ID-"+i));
    
    const ageSel = document.getElementById('age-select');
    for(let i=20; i<=70; i++) ageSel.options.add(new Option(i+" ans", i));

    const expSel = document.getElementById('exp-select');
    for(let i=0; i<=40; i++) expSel.options.add(new Option(i+" ans d'expérience", i));
};
</script>
</body>
</html>
