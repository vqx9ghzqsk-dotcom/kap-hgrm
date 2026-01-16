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
        <div style="background: #e3f2fd; padding: 10px; border-radius: 5px; margin-bottom: 15px; color: #0d47a1;">
            <strong>ℹ️ Mode Saisie :</strong> Remplissez la fiche ci-dessous. En cliquant sur "ENREGISTRER", les données s'ajouteront à la base pour l'analyse globale.
        </div>
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Oncologie</option></select></div>
                <div class="field"><label>Statut</label><select id="statut"><option>Titulaire</option><option>Infirmier(e) de garde</option><option>Stagiaire</option><option>Bénévole</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select"></select></div>
                <div class="field"><label>Niveau Etude</label><select id="niveau"><option>A2 (Diplômée d'État)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option><option>Master</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès ?</label><select id="q1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option><option>Ne sait pas</option></select></div>
                <div class="field"><label>Âge début AES ?</label><select id="q2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option><option>Après 40 ans</option></select></div>
                <div class="field"><label>Moment AES ?</label><select id="q3"><option selected>7 jours après les règles</option><option>Pendant les règles</option><option>N'importe quand</option></select></div>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Facteurs de risque (Cochez si connu) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="nulliparite"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" value="tardive"> 1ère grossesse > 30 ans</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause > 55 ans</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool/Tabac</label>
                <label class="check-item"><input type="checkbox" value="contraceptif"> Contraceptifs oraux</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Signes d'alerte (Cochez si connu) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction mamelon</label>
                <label class="check-item"><input type="checkbox" value="adenopathie"> Adénopathie axillaire</label>
                <label class="check-item"><input type="checkbox" value="peauorange"> Peau d'orange</label>
            </div>

            <div class="section-title">III. ATTITUDES (1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">Pudeur des patientes est un obstacle.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Cancer = Mort inévitable.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Sensibilisation systématique nécessaire.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Fréquence Palpation</label><select id="pratique-freq"><option>Systématique</option><option>Si plainte</option><option>Rarement</option></select></div>
                <div class="field"><label>Enseignement AES</label><select id="pratique-enseigne"><option>Démonstration physique</option><option>Verbalement</option><option>Pas d'enseignement</option></select></div>
                <div class="field"><label>Palpé ce matin ?</label><select id="pratique-matin"><option>Oui</option><option>Non</option></select></div>
                <div class="field"><label>Technique de palpation</label><select id="pratique-technique"><option>Circulaire</option><option>Radiale</option><option>Verticale</option><option>Sommaire</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="intimite"> Absence intimité</label>
                <label class="check-item"><input type="checkbox" value="cout"> Coût élevé</label>
                <label class="check-item"><input type="checkbox" value="formation"> Manque formation</label>
                <label class="check-item"><input type="checkbox" value="culture"> Croyances/Tradition</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE ET CONTINUER</button>
            <p style="text-align:center; color:#777; font-size:12px;">Après avoir enregistré toutes vos fiches, cliquez sur les onglets ci-dessus pour l'analyse.</p>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT (TOUTES LES FICHES)</div>
        <table style="font-size:11px;">
            <thead>
                <tr>
                    <th>Code</th>
                    <th>Niveau</th>
                    <th>Expérience</th>
                    <th>Score Savoir (%)</th>
                    <th>Score Attitude (/5)</th>
                    <th>Score Pratique (%)</th>
                    <th>Statut</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. STATISTIQUES DESCRIPTIVES</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Savoir</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de la Pratique</div><div id="graph-pratique"></div></div>
        </div>
        <div class="section-title">2. ANALYSE CROISÉE</div>
        <table class="cross-table">
            <thead><tr><th class="text-left">Groupe</th><th>Nombre (N)</th><th>Attitude (/5)</th><th>Pratique (%)</th></tr></thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross"></div>
        <div class="section-title">3. ANALYSE DES BARRIÈRES</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE DE L'ÉTUDE</div>
        <div id="final-conclusion">Analyse en attente...</div>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 EXPORT CSV</button>
    </div>

</div>

<script>
    let database = [];
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 200; i++) { let opt = document.createElement('option'); opt.value = "E-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 65; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; ageSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 40; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans d'exp."; expSelect.appendChild(opt); }

    function saveRecord() {
        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            exp: parseInt(document.getElementById('exp-select').value),
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            p1: getRadioValue('p1'), p2: getRadioValue('p2'), p3: getRadioValue('p3'), p4: getRadioValue('p4'),
            freq: document.getElementById('pratique-freq').value,
            enseigne: document.getElementById('pratique-enseigne').value,
            matin: document.getElementById('pratique-matin').value,
            technique: document.getElementById('pratique-technique').value, // Ajouté ici
            obstacles: getCheckedValues('group-obstacles')
        };

        let rawSavoir = 0;
        if(record.q1.includes("Vrai")) rawSavoir++;
        if(record.q2.includes("20 ans")) rawSavoir++;
        if(record.q3.includes("7 jours")) rawSavoir++;
        rawSavoir += record.risques + record.signes;
        record.scoreSavoir = Math.min(100, Math.round((rawSavoir / 14) * 100));

        let sumAtt = parseInt(record.p1) + parseInt(record.p2) + parseInt(record.p3) + parseInt(record.p4);
        record.scoreAttitude = (sumAtt / 4).toFixed(1);

        let rawPrac = 0;
        if(record.freq.includes("Systématique")) rawPrac += 40;
        if(record.enseigne.includes("Démonstration")) rawPrac += 40; else if(record.enseigne.includes("Verbalement")) rawPrac += 10;
        if(record.matin === "Oui") rawPrac += 20;
        record.scorePratique = rawPrac;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        alert(`Fiche enregistrée !`);
        document.querySelectorAll('input[type="checkbox"]').forEach(i => i.checked = false);
        let currIdx = codeSelect.selectedIndex;
        if(currIdx < codeSelect.options.length - 1) codeSelect.selectedIndex = currIdx + 1;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(database.length === 0) return;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = '';
        database.forEach(row => {
            tbody.innerHTML += `<tr><td>${row.id}</td><td>${row.niveau}</td><td>${row.exp}</td><td>${row.scoreSavoir}%</td><td>${row.scoreAttitude}</td><td>${row.scorePratique}%</td><td>${row.scoreSavoir >= 70 ? '🟢' : '🔴'}</td></tr>`;
        });
        // Les fonctions graphiques restent les mêmes pour assurer la stabilité
        let highKnow = database.filter(r => r.scoreSavoir >= 70);
        let lowKnow = database.filter(r => r.scoreSavoir < 70);
        renderBarChart('graph-savoir', [{label: 'Bon', val: highKnow.length, total: database.length, color: '#2e7d32'},{label: 'Insuffisant', val: lowKnow.length, total: database.length, color: '#c62828'}]);
    }

    function getCheckedCount(groupId) { return document.querySelectorAll(`#${groupId} input:checked`).length; }
    function getCheckedValues(groupId) { return Array.from(document.querySelectorAll(`#${groupId} input:checked`)).map(cb => cb.value); }
    function getRadioValue(name) { let el = document.querySelector(`input[name="${name}"]:checked`); return el ? el.value : 0; }
    function renderBarChart(divId, data) {
        let html = '';
        data.forEach(item => {
            let pct = item.total > 0 ? Math.round((item.val / item.total) * 100) : 0;
            html += `<div class="bar-container"><div class="bar-label">${item.label}</div><div class="bar-track"><div class="bar-fill" style="width:${pct}%; background:${item.color};">${pct}%</div></div><div class="bar-value">${item.val}</div></div>`;
        });
        document.getElementById(divId).innerHTML = html;
    }
    function switchTab(idx) {
        document.querySelectorAll('.form-content').forEach(d => d.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
        document.getElementById('content-'+idx).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${idx})`).classList.add('active');
    }
    function exportToCSV() {
        let csv = "ID,Savoir,Attitude,Pratique,Technique\n";
        database.forEach(r => csv += `${r.id},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique},${r.technique}\n`);
        let link = document.createElement("a");
        link.href = encodeURI("data:text/csv;charset=utf-8," + csv);
        link.download = "base.csv";
        link.click();
    }
</script>
</body>
</html>
