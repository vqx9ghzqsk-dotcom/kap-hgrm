<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE EXISTANT (Conservé) --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel:hover { background: #1b5e20; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input[type="text"], input[type="number"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; text-align: center; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }

        /* --- STYLES ANALYSE --- */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 10px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 150px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; transition: width 0.5s; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; }

        .cross-table th { background-color: #333; color: white; }
        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; font-style: italic; color: #1b5e20; margin-top: 10px; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 15px; font-style: italic; color: #b71c1c; margin-top: 10px; }

        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT GLOBAL</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTAT ET ANALYSE CROISÉE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT TOTAL (CSV)</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Oncologie</option></select></div>
                <div class="field"><label>Niveau Etude</label><select id="niveau"><option>A2 (Diplômée)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option><option>Master</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select"></select></div>
                <div class="field"><label>Statut</label><select id="statut"><option>Titulaire</option><option>De garde</option><option>Stagiaire</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS THÉORIQUES & TECHNIQUES)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès ?</label><select id="q1"><option>Vrai</option><option>Faux</option><option>Ne sait pas</option></select></div>
                <div class="field"><label>Âge début AES ?</label><select id="q2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option><option>Après 40 ans</option></select></div>
                <div class="field"><label>Moment idéal (Cycle) ?</label><select id="q3"><option selected>2-3 jours après les règles</option><option>Pendant les règles</option><option>Avant les règles</option></select></div>
            </div>
            
            <div class="row" style="margin-top:15px;">
                <div class="field"><label>Partie de la main utilisée ?</label><select id="tech-main"><option>La paume</option><option selected>Pulpe des 3 doigts du milieu</option><option>Le pouce</option></select></div>
                <div class="field"><label>Position idéale ?</label><select id="tech-pos"><option>Assise</option><option selected>Couchée, bras relevé</option><option>Debout, bras ballants</option></select></div>
                <div class="field"><label>Mouvement ?</label><select id="tech-mouv"><option selected>Petits cercles (3 pressions)</option><option>Balayage vertical</option><option>Pincement</option></select></div>
            </div>

            <label style="margin:20px 0 10px 0; font-weight:bold; color:#b03060; display:block;">Facteurs de risque connus :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="nulliparite"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" value="tardive"> 1ère grossesse > 30 ans</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause > 55 ans</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
            </div>

            <label style="margin:20px 0 10px 0; font-weight:bold; color:#b03060; display:block;">Signes d'alerte connus :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="peauorange"> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction mamelon</label>
            </div>

            <div class="section-title">III. ATTITUDES (Échelle 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Un cancer détecté tôt est curable à l'HGRM.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4" checked></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">Le cancer est une "maladie de la honte".</td><td><input type="radio" name="att2" value="1" checked></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td class="text-left">La palpation doit être systématique pour TOUTES.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5" checked></td></tr>
                    <tr><td class="text-left">J'ai peur de me tromper dans mon examen.</td><td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4" checked></td><td><input type="radio" name="att4" value="5"></td></tr>
                    <tr><td class="text-left">Dénuder une patiente me met mal à l'aise.</td><td><input type="radio" name="att5" value="1" checked></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (CLINIQUE & PERSONNELLE)</div>
            <div class="row">
                <div class="field"><label>Patient palpées (Mois dernier)</label><select id="prac-nb"><option>Toutes</option><option selected>> 50%</option><option>< 50%</option><option>Aucune</option></select></div>
                <div class="field"><label>Démonstration technique faite ?</label><select id="prac-demo"><option selected>Toujours</option><option>Souvent (Verbal)</option><option>Rarement</option><option>Jamais</option></select></div>
                <div class="field"><label>Conduite si masse ?</label><select id="prac-ref"><option selected>Référence immédiate</option><option>Demande écho</option><option>Surveillance</option></select></div>
            </div>
            <div class="row" style="margin-top:15px;">
                <div class="field"><label>Fréquence sur VOUS-MÊME</label><select id="prac-self"><option selected>Chaque mois</option><option>Tous les 3-6 mois</option><option>Si douleur</option><option>Jamais</option></select></div>
                <div class="field"><label>Votre technique perso</label><select id="prac-tech-self"><option selected>Miroir + Palpation</option><option>Sous la douche</option><option>Visuelle simple</option><option>Aucune</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES MAJEURS</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="temps"> Manque de temps / Charge</label>
                <label class="check-item"><input type="checkbox" value="intimite"> Pas de local intime</label>
                <label class="check-item"><input type="checkbox" value="oubli"> Oubli systématique</label>
                <label class="check-item"><input type="checkbox" value="refus"> Refus des patientes</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE ET CONTINUER</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <table style="font-size:11px;">
            <thead>
                <tr><th>Code</th><th>Niveau</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Statut</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE DES FRÉQUENCES</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Savoir</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de Pratique</div><div id="graph-pratique"></div></div>
        </div>
        <div class="section-title">ANALYSE CROISÉE (SAVOIR vs PRATIQUE)</div>
        <table class="cross-table">
            <thead><tr><th>Groupe</th><th>N</th><th>Attitude (/5)</th><th>Pratique Moy. (%)</th></tr></thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross"></div>
        <div class="section-title">ANALYSE DES BARRIÈRES</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE DE L'ÉTUDE</div>
        <div id="final-conclusion">Analyse en attente...</div>
    </div>
</div>

<script>
    let database = [];

    // Init listes
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 300; i++) { let opt = document.createElement('option'); opt.value = "F-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 65; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; ageSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 45; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans d'exp."; expSelect.appendChild(opt); }

    function saveRecord() {
        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            // Savoirs
            q1: document.getElementById('q1').value, 
            q3: document.getElementById('q3').value,
            t1: document.getElementById('tech-main').value,
            t2: document.getElementById('tech-pos').value,
            t3: document.getElementById('tech-mouv').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            // Attitudes (Inversion de score pour les questions négatives att2 et att5)
            attScore: (parseInt(getRadioValue('att1')) + (6-parseInt(getRadioValue('att2'))) + parseInt(getRadioValue('att3')) + (6-parseInt(getRadioValue('att4'))) + (6-parseInt(getRadioValue('att5')))) / 5,
            // Pratiques
            p1: document.getElementById('prac-nb').value,
            p2: document.getElementById('prac-demo').value,
            p3: document.getElementById('prac-self').value,
            obstacles: getCheckedValues('group-obstacles')
        };

        // Calcul Scores
        let s = 0;
        if(record.q1 === "Vrai") s += 2;
        if(record.q3.includes("2-3 jours")) s += 2;
        if(record.t1.includes("Pulpe")) s += 2;
        if(record.t2.includes("Couchée")) s += 2;
        if(record.t3.includes("cercles")) s += 2;
        s += record.risques + record.signes;
        record.scoreSavoir = Math.round((s / 18) * 100); 

        record.scoreAttitude = record.attScore.toFixed(1);

        let p = 0;
        if(record.p1 === "Toutes") p += 40; else if(record.p1 === "> 50%") p += 20;
        if(record.p2 === "Toujours") p += 30;
        if(record.p3 === "Chaque mois") p += 30; else if(record.p3.includes("3-6 mois")) p += 10;
        record.scorePratique = p;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        
        alert("Fiche enregistrée !");
        codeSelect.selectedIndex++;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(database.length === 0) return;
        
        // Table Déroulante
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(r => `<tr><td>${r.id}</td><td>${r.niveau}</td><td style="color:${getColor(r.scoreSavoir)}">${r.scoreSavoir}%</td><td>${r.scoreAttitude}</td><td style="color:${getColor(r.scorePratique)}">${r.scorePratique}%</td><td>${r.scorePratique >= 60 ? '🟢':'🔴'}</td></tr>`).join('');

        // Croisement
        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        
        document.getElementById('cross-body').innerHTML = `
            <tr><td class="text-left">Savoir Élevé (>=70%)</td><td>${high.length}</td><td>${getAvg(high,'scoreAttitude')}</td><td>${getAvg(high,'scorePratique')}%</td></tr>
            <tr><td class="text-left">Savoir Faible (<70%)</td><td>${low.length}</td><td>${getAvg(low,'scoreAttitude')}</td><td>${getAvg(low,'scorePratique')}%</td></tr>
        `;

        // Barres
        renderBarChart('graph-savoir', [{label:'Bon', val:high.length, total:database.length, color:'green'}, {label:'Insuffisant', val:low.length, total:database.length, color:'red'}]);
        
        // Conclusion
        document.getElementById('final-conclusion').innerHTML = `<h3>Analyse de l'HGRM</h3><p>Sur ${database.length} répondants, la pratique moyenne est de ${getAvg(database, 'scorePratique')}%. ${getAvg(high, 'scorePratique') > getAvg(low, 'scorePratique') ? "Le savoir influence positivement l'acte." : "La connaissance ne suffit pas à changer la pratique."}</p>`;
    }

    // Helpers
    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(c => c.value); }
    function getRadioValue(name) { return document.querySelector(`input[name="${name}"]:checked`).value; }
    function getColor(s) { return s >= 70 ? 'green' : (s >= 50 ? 'orange' : 'red'); }
    function getAvg(arr, prop) { return arr.length ? (arr.reduce((s, c) => s + parseFloat(c[prop]), 0) / arr.length).toFixed(1) : 0; }
    
    function renderBarChart(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.total ? Math.round((i.val/i.total)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.label}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.color};">${p}%</div></div></div>`;
        }).join('');
    }

    function switchTab(idx) {
        document.querySelectorAll('.form-content').forEach(d => d.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
        document.getElementById('content-'+idx).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${idx})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "data:text/csv;charset=utf-8,\ufeffID,Niveau,Savoir,Attitude,Pratique\n";
        database.forEach(r => csv += `${r.id},${r.niveau},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}\n`);
        window.open(encodeURI(csv));
    }
</script>
</body>
</html>
