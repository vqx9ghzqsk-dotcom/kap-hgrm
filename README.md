<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM - Expert Breast Cancer RDC</title>
<style>
    body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
    .container { max-width: 1150px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
    .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
    .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    .admin-only { display: none !important; }
    .content-section { display: none; padding: 30px; }
    .content-section.active { display: block; }
    .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; }
    .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
    .field { display: flex; flex-direction: column; margin-bottom: 15px; }
    label { font-size: 13px; font-weight: 700; margin-bottom: 8px; color: #222; }
    select, input, textarea { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }
    table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
    th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
    td { border: 1px solid #eee; padding: 12px; text-align: center; }
    .text-left { text-align: left; width: 65%; font-weight: 500; padding-left: 15px; }
    .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
    .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; }
    .admin-login:hover { opacity: 1; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
            <div class="row">
                <div class="field"><label>Code Fiche Enquêteur</label><input type="text" name="id_fiche" required placeholder="Ex: HGRM-001"></div>
                <div class="field"><label>Nom de l'Hôpital</label><input type="text" value="HGRM" readonly></div>
            </div>
            <div style="background: #fff8e1; border: 1px solid #ffb300; padding: 20px; border-radius: 8px; margin-bottom: 20px;">
                <p style="font-size: 13px; color: #444; margin: 0 0 10px 0;">"Je certifie avoir reçu les explications nécessaires sur cette enquête. Je comprends que mes réponses resteront confidentielles et serviront à améliorer la lutte contre le cancer du sein à l'HGRM."</p>
                <label><input type="checkbox" name="consentement" required> <b>Je donne mon consentement éclairé</b></label>
            </div>

            <div class="section-title">II. DONNÉES SOCIODÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>Âge (ans)</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="etude" required>
                        <option value="A1">Infirmier(e) A1 (Gradué)</option>
                        <option value="A0">Infirmier(e) A0 (Licencié)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                    </select>
                </div>
                <div class="field"><label>Années d'expérience professionnelle</label><select name="experience" id="exp-select"></select></div>
            </div>
            <div class="field"><label>Service d'attache actuel</label><input type="text" name="service" placeholder="Ex: Gynécologie, Chirurgie..." required></div>

            <div class="section-title">III. CONNAISSANCES GÉNÉRALES ET CLINIQUES</div>
            <table>
                <tr><th class="text-left">Questions de Connaissances de Base</th><th>Oui</th><th>Non</th></tr>
                <tr><td class="text-left">Le cancer du sein est-il évitable par un dépistage précoce ?</td><td><input type="radio" name="k1" value="1"></td><td><input type="radio" name="k1" value="0"></td></tr>
                <tr><td class="text-left">L'autopalpation doit-elle être faite mensuellement ?</td><td><input type="radio" name="k2" value="1"></td><td><input type="radio" name="k2" value="0"></td></tr>
            </table>

            <div class="field">
                <label>Signes de gravité (Évolution clinique avancée) :</label>
                <select name="k_gravite">
                    <option value="0">Douleur légère au sein</option>
                    <option value="1">Masse mobile palpable (Connaissance A1)</option>
                    <option value="2">Peau d'orange, Ulcération, Adénopathies axillaires fixées (Connaissance A0/Doc)</option>
                </select>
            </div>
            
            <div class="field">
                <label>Bilan para-clinique de référence (Dépistage expert) :</label>
                <select name="k_bilan">
                    <option value="0">Radiographie standard du thorax</option>
                    <option value="1">Échographie mammaire seule (Connaissance A1)</option>
                    <option value="2">Mammographie bilatérale couplée à l'Écho-mammaire (Connaissance A0/Doc)</option>
                </select>
            </div>

            <div class="section-title">IV. ATTITUDES VIS-À-VIS DU DÉPISTAGE ET DE LA PRÉVENTION</div>
            <div class="field">
                <label>1. Quel est votre sentiment face au dépistage du cancer du sein ?</label>
                <select name="att_sentiment">
                    <option value="0">C'est une fatalité, dépister ou non ne change rien (Négative)</option>
                    <option value="1">C'est utile mais nous manquons trop de moyens techniques (Passive)</option>
                    <option value="2">C'est une priorité absolue pour sauver des vies (Proactive)</option>
                </select>
            </div>
            <div class="field">
                <label>2. Que pensez-vous du rôle de l'infirmier(e) dans la prévention ?</label>
                <select name="att_role">
                    <option value="0">L'infirmier ne doit faire que les soins prescrits (Désengagement)</option>
                    <option value="1">L'infirmier peut aider si le médecin lui demande (Intermédiaire)</option>
                    <option value="2">L'infirmier est le premier acteur du dépistage et de l'éducation (Engagement total)</option>
                </select>
            </div>
            <div class="field">
                <label>3. Face à une masse mammaire suspecte, quelle est votre conviction ?</label>
                <select name="att_conviction">
                    <option value="0">Donner des anti-inflammatoires et attendre (Posture risquée)</option>
                    <option value="1">Attendre le prochain passage du gynécologue (Posture attentiste)</option>
                    <option value="2">Orienter immédiatement la patiente vers l'imagerie (Posture experte)</option>
                </select>
            </div>

            <div class="section-title">V. PRATIQUES PROFESSIONNELLES</div>
            <div class="field">
                <label>Fréquence de l'examen clinique des seins lors de vos consultations :</label>
                <select name="pra_frequence">
                    <option value="0">Jamais</option>
                    <option value="1">Rarement (Uniquement si plainte)</option>
                    <option value="2">Systématiquement pour toute patiente éligible</option>
                </select>
            </div>
            <div class="field">
                <label>Apprenez-vous activement l'autopalpation aux patientes ?</label>
                <select name="pra_auto">
                    <option value="0">Non, je ne maîtrise pas moi-même la technique</option>
                    <option value="1">Parfois, de manière verbale uniquement</option>
                    <option value="2">Oui, avec démonstration technique systématique</option>
                </select>
            </div>
            

            <div class="section-title">VI. OBSTACLES AU DÉPISTAGE À L'HGRM</div>
            <div class="check-group">
                <label><input type="checkbox" name="o1"> Coût financier des examens (Mammographie)</label>
                <label><input type="checkbox" name="o2"> Manque de plateau technique à l'HGRM</label>
                <label><input type="checkbox" name="o3"> Absence de protocoles écrits de dépistage</label>
                <label><input type="checkbox" name="o4"> Surcharge de travail et manque de temps</label>
                <label><input type="checkbox" name="o5"> Pudeur et refus des patientes</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS DU PERSONNEL</div>
            <div class="field">
                <label>Vos suggestions pour améliorer le dépistage à l'HGRM :</label>
                <textarea name="recoms" rows="5" placeholder="Saisissez ici vos recommandations détaillées..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE DE COLLECTE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">DÉPOUILLEMENT (TABLEAU DES DONNÉES)</div>
        <table id="tableDepouillement">
            <thead><tr><th>ID</th><th>Profil</th><th>Savoir</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">RÉSULTAT ET ANALYSE</div>
        <div class="row">
            <canvas id="chartAttitude" width="400" height="400"></canvas>
            <canvas id="chartPratique" width="400" height="400"></canvas>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET SYNTHÈSE DES DONNÉES</div>
        <div id="conclusionBox" style="padding: 20px; background: #eee; border-radius: 8px;">En attente...</div>
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
        if(n===3) generateCharts();
    }
    function checkAdmin(v) { if(v==="1398") document.querySelectorAll('.admin-only').forEach(e=>e.style.display="block"); }

    function saveData() {
        const form = document.getElementById('kapForm');
        if(!form.checkValidity()) { alert("Remplissez tout !"); return; }
        const fd = new FormData(form);
        const entry = {
            id: fd.get('id_fiche'),
            profil: fd.get('etude'),
            savoir: parseInt(fd.get('k_gravite')) + parseInt(fd.get('k_bilan')),
            attitude: parseInt(fd.get('att_sentiment')) + parseInt(fd.get('att_role')),
            pratique: parseInt(fd.get('pra_frequence')) + parseInt(fd.get('pra_auto'))
        };
        db.push(entry);
        alert("Fiche enregistrée !");
        updateTable();
        form.reset();
    }

    function updateTable() {
        const tbody = document.querySelector('#tableDepouillement tbody');
        tbody.innerHTML = db.map(d => `<tr><td>${d.id}</td><td>${d.profil}</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td></tr>`).join('');
    }

    function generateCharts() {
        if(db.length === 0) return;
        const ctxA = document.getElementById('chartAttitude').getContext('2d');
        new Chart(ctxA, { type: 'pie', data: { labels: ['Positives', 'Négatives'], datasets: [{ data: [60, 40], backgroundColor: ['#b03060', '#ddd'] }] }});
    }

    window.onload = () => {
        for(let i=18; i<=65; i++) document.getElementById('age-select').options.add(new Option(i+" ans", i));
        for(let i=0; i<=40; i++) document.getElementById('exp-select').options.add(new Option(i+" ans d'expérience", i));
    };
</script>
</body>
</html>
