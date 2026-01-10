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
        <div class="tab admin-only" id="tabH2" onclick="showTab(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab admin-only" id="tabH3" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab admin-only" id="tabH4" onclick="showTab(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="tab1" class="content-section active">
        <form class="form-content" id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie (si existant)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select name="statut">
                        <option selected>Titulaire du service</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire (Fin de cycle)</option>
                        <option>Sous-statutaire (Bénévole)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge de l'infirmier(e)</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Années d'expérience professionnelle</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Niveau d'étude le plus élevé</label>
                    <select name="etude" id="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option value="L">L0/L1 (Licenciée nouveau système)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="k1"><option value="1" selected>Vrai (Oui)</option><option value="0">Faux (Non)</option><option value="0">Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>À quel âge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option><option value="0">Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après les règles</option><option value="0">Pendant les règles</option><option value="0">N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Nullipare" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="GrosseTardive" checked> 1ère grossesse > 30 ans</label>
                <label class="check-item"><input type="checkbox" name="risk" value="MenopauseTardive" checked> Ménopause > 55 ans</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Alcool" checked> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Heredite" checked> Antécédents familiaux</label>
            </div>

            <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="sign" value="Nodule" checked> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Ecoulement" checked> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Retraction" checked> Rétraction mamelon</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Adenopathie" checked> Boule sous l'aisselle</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Orange" checked> Peau d'orange</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (LIKERT 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Capacité de détection nodule suspect</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">Influence culturelle (pudeur)</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence palpation clinique (ECS) :</label>
                    <select name="pra1"><option value="1">Systématique</option><option value="0" selected>Si plainte / Rarement</option></select>
                </div>
                <div class="field">
                    <label>Enseignement AES :</label>
                    <select name="pra2"><option value="1">Démonstration physique</option><option value="0" selected>Verbal / Pas d'enseignement</option></select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES (RDC CONTEXT)</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Salle"> Pas de salle isolée</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Cout"> Coût Mammographie</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Croyance"> Prière / Tradition</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES DE DÉPOUILLEMENT</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Service</th><th>Étude</th><th>Exp.</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">STATISTIQUES AVANCÉES</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total N</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Savoir Elevé</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Pratique Correcte</div></div>
            <div class="stat-card"><div class="stat-val" id="res-obs">--</div><div class="stat-label">Obstacle Majeur</div></div>
        </div>
        <div class="row">
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Répartition par Étude (%)</b></label>
                <div id="study-dist" style="margin-top:10px; font-size:12px;"></div>
            </div>
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Test Chi-Carré Automatique</b></label>
                <p id="chi-output" style="color:#b03060; font-size:12px;">Besoin de 5 fiches...</p>
            </div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET RECOMMANDATIONS EXPERTES</div>
        <div id="summary" style="line-height:1.8; background:#fff; padding:30px; border:1px solid #ddd; border-radius:8px; font-size:14px;">
            En attente de saisie...
        </div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
            alert("Accès autorisé.");
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        const tabIds = ['','tabH2','tabH3','tabH4'];
        if(n > 1) document.getElementById(tabIds[n-1]).classList.add('active');
        else document.querySelector('.tab').classList.add('active');
        if(n >= 3) calculerAnalyse();
    }

    async function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));
        let obstacles = Array.from(document.querySelectorAll('input[name="obs"]:checked')).map(e => e.value);

        const entry = {
            code: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: parseInt(fd.get('experience')),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 2 ? 'Correcte' : 'Incorrecte',
            obstacles: obstacles
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            db.push(entry);
            actualiserTableau();
            alert("Fiche " + entry.code + " enregistrée avec succès !");
            form.reset();
        } catch (e) { alert("Erreur de réseau."); }
    }

    function actualiserTableau() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => 
            `<tr><td>${d.code}</td><td>${d.service}</td><td>${d.etude}</td><td>${d.experience}ans</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`
        ).join('');
    }

    function calculerAnalyse() {
        let n = db.length; if(n === 0) return;
        let kHigh = db.filter(d => d.savoir === 'Bon').length;
        let pGood = db.filter(d => d.pratique === 'Correcte').length;
        
        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";

        // Répartition Études
        let studies = ['A2', 'A1', 'L', 'M'];
        let distHtml = "";
        studies.forEach(s => {
            let count = db.filter(d => d.etude === s).length;
            distHtml += `<b>${s}:</b> ${Math.round(count/n*100)}% | `;
        });
        document.getElementById('study-dist').innerHTML = distHtml;

        // Conclusion Automatique
        let conc = `<b>ANALYSE SYNTHÉTIQUE :</b><br>Sur un échantillon de ${n} infirmiers, `;
        if(kHigh/n > 0.7) conc += "les connaissances théoriques sont satisfaisantes. ";
        else conc += "on observe une lacune importante des connaissances de base. ";
        
        if(pGood/n < 0.4) conc += "Cependant, la pratique clinique est alarmante car moins de la moitié applique les gestes de dépistage.<br><br>";
        
        conc += "<b>RECOMMANDATIONS :</b><br>1. Organiser des ateliers de démonstration pratique (AES).<br>2. ";
        conc += (pGood < kHigh) ? "Lever les barrières logistiques (salles isolées) car le savoir ne se transforme pas en pratique." : "Renforcer la formation initiale.";
        
        document.getElementById('summary').innerHTML = conc;
    }

    function exportCSV() {
        let csv = "Code,Service,Etude,Experience,Savoir,Pratique\n";
        db.forEach(d => { csv += `${d.code},${d.service},${d.etude},${d.experience},${d.savoir},${d.pratique}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'Rapport_KAP_HGRM.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) cs.options.add(new Option("ID: " + i, i));
        const as = document.getElementById('age-select');
        for (let i = 18; i <= 65; i++) as.options.add(new Option(i + " ans", i));
        const es = document.getElementById('exp-select');
        for (let i = 0; i <= 35; i++) es.options.add(new Option(i + " ans d'exp", i));
    };
</script>
</body>
</html>
