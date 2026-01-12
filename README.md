<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE CONSERVÉ ET OPTIMISÉ --- */
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
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 15px; transform: scale(1.4); width: auto; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .stat-title { font-weight: bold; color: #555; border-bottom: 2px solid #b03060; display: inline-block; margin-bottom: 10px; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 180px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; transition: width 0.5s; }

        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; color: #1b5e20; margin-top: 10px; font-style: italic; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 15px; color: #b71c1c; margin-top: 10px; font-style: italic; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
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
                <div class="field"><label>Statut</label><select id="statut"><option>Titulaire</option><option>De garde</option><option>Stagiaire</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select"></select></div>
                <div class="field"><label>Niveau Étude</label><select id="niveau"><option>A2</option><option selected>A1</option><option>L0/L1</option><option>Master</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS & TECHNIQUE)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès ?</label><select id="q1"><option>Vrai</option><option>Faux</option></select></div>
                <div class="field"><label>Moment idéal AES ?</label><select id="q2"><option selected>2-3 jours après règles</option><option>Pendant règles</option><option>Avant règles</option></select></div>
                <div class="field"><label>Partie de main ?</label><select id="q3"><option>Paume</option><option selected>Pulpe des 3 doigts</option><option>Pouce</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Position ?</label><select id="q4"><option>Assise</option><option selected>Couchée, bras relevé</option></select></div>
                <div class="field"><label>Mouvement ?</label><select id="q5"><option selected>Cercles (3 pressions)</option><option>Pincement</option></select></div>
            </div>

            <label style="display:block; margin:15px 0 5px 0; font-weight:bold;">Facteurs de Risques (Cochez) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="nulli"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" value="tard"> Grossesse > 30 ans</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
            </div>

            <label style="display:block; margin:15px 0 5px 0; font-weight:bold;">Signes d'Alerte (Cochez) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur</label>
                <label class="check-item"><input type="checkbox" value="orange"> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" value="sang"> Écoulement sanglant</label>
            </div>

            <div class="section-title">III. ATTITUDES (LIKERT 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Le cancer est curable si détecté tôt.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4" checked></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">La palpation doit être systématique.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5" checked></td></tr>
                    <tr><td class="text-left">La pudeur est un frein majeur.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4" checked></td><td><input type="radio" name="att3" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Patient palpées (Mois dernier)</label><select id="prac1"><option>Toutes</option><option selected>> 50%</option><option>< 50%</option><option>Aucune</option></select></div>
                <div class="field"><label>Démonstration faite ?</label><select id="prac2"><option selected>Toujours</option><option>Rarement</option><option>Jamais</option></select></div>
                <div class="field"><label>Auto-Examen (Sur vous)</label><select id="prac3"><option selected>Chaque mois</option><option>Irrégulier</option><option>Jamais</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="Temps"> Manque de Temps</label>
                <label class="check-item"><input type="checkbox" value="Intimité"> Absence Local Privé</label>
                <label class="check-item"><input type="checkbox" value="Formation"> Manque Formation</label>
                <label class="check-item"><input type="checkbox" value="Refus"> Refus Patiente</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT (TOUTES LES FICHES)</div>
        <table>
            <thead>
                <tr>
                    <th>Code</th><th>Niveau</th><th>Exp.</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Statut</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. STATISTIQUES DESCRIPTIVES</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Savoir</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de Pratique</div><div id="graph-pratique"></div></div>
        </div>

        <div class="section-title">2. ANALYSE CROISÉE (ASSOCIATIONS)</div>
        <table class="cross-table">
            <thead>
                <tr><th class="text-left">Groupe (Selon Savoir)</th><th>N</th><th>Attitude Moy.</th><th>Pratique Moy.</th></tr>
            </thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross"></div>

        <div class="section-title">3. ANALYSE DES BARRIÈRES (FRÉQUENCES)</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET CONCLUSION</div>
        <div id="final-conclusion" style="line-height:1.6;"></div>
    </div>
</div>

<script>
    let database = [];

    // Initialisation sélecteurs
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 200; i++) { let opt = document.createElement('option'); opt.value = "E-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 65; i++) { ageSelect.add(new Option(i+" ans", i)); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 40; i++) { expSelect.add(new Option(i+" ans d'exp.", i)); }

    function saveRecord() {
        let record = {
            id: codeSelect.value,
            niveau: document.getElementById('niveau').value,
            exp: document.getElementById('exp-select').value,
            // Savoir
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            q4: document.getElementById('q4').value,
            q5: document.getElementById('q5').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            // Attitude
            att: (parseInt(getRadioValue('att1')) + parseInt(getRadioValue('att2')) + parseInt(getRadioValue('att3'))) / 3,
            // Pratique
            p1: document.getElementById('prac1').value,
            p2: document.getElementById('prac2').value,
            p3: document.getElementById('prac3').value,
            // Obstacles
            obstacles: getCheckedValues('group-obstacles')
        };

        // Calcul Scores
        let s = 0;
        if(record.q1 === "Vrai") s += 20;
        if(record.q2.includes("2-3 jours")) s += 20;
        if(record.q3.includes("Pulpe")) s += 20;
        if(record.q4.includes("Couchée")) s += 10;
        if(record.q5.includes("Cercles")) s += 10;
        s += (record.risques * 10) + (record.signes * 10);
        record.scoreSavoir = Math.min(100, s);
        
        record.scoreAttitude = record.att.toFixed(1);

        let p = 0;
        if(record.p1 === "Toutes") p += 40; else if(record.p1 === "> 50%") p += 20;
        if(record.p2 === "Toujours") p += 30;
        if(record.p3 === "Chaque mois") p += 30;
        record.scorePratique = p;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        alert("Fiche enregistrée avec succès !");
        codeSelect.selectedIndex++;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(database.length === 0) return;

        // 1. Dépouillement
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(r => `
            <tr>
                <td><strong>${r.id}</strong></td><td>${r.niveau}</td><td>${r.exp} ans</td>
                <td style="color:${getColor(r.scoreSavoir)}">${r.scoreSavoir}%</td>
                <td>${r.scoreAttitude}</td>
                <td style="color:${getColor(r.scorePratique)}">${r.scorePratique}%</td>
                <td>${r.scoreSavoir >= 70 && r.scorePratique >= 60 ? '🟢 Performant' : '🔴 À former'}</td>
            </tr>
        `).join('');

        // 2. Croisement
        let highS = database.filter(r => r.scoreSavoir >= 70);
        let lowS = database.filter(r => r.scoreSavoir < 70);
        
        document.getElementById('cross-body').innerHTML = `
            <tr><td class="text-left">Savoir Élevé (>=70%)</td><td>${highS.length}</td><td>${getAvg(highS, 'scoreAttitude')}</td><td>${getAvg(highS, 'scorePratique')}%</td></tr>
            <tr><td class="text-left">Savoir Faible (<70%)</td><td>${lowS.length}</td><td>${getAvg(lowS, 'scoreAttitude')}</td><td>${getAvg(lowS, 'scorePratique')}%</td></tr>
        `;

        // Interpretation
        let inter = document.getElementById('interpretation-cross');
        if(getAvg(highS, 'scorePratique') > getAvg(lowS, 'scorePratique')) {
            inter.innerHTML = `<div class="interpretation-box">✅ Corrélation positive : Le savoir technique améliore la pratique à l'HGRM.</div>`;
        } else {
            inter.innerHTML = `<div class="alert-box">⚠️ Rupture Savoir-Agir : Malgré les connaissances, la pratique reste bloquée.</div>`;
        }

        // 3. Graphiques Barres
        renderBarChart('graph-savoir', [
            {label: 'Bon (>=70%)', val: highS.length, total: database.length, color: '#2e7d32'},
            {label: 'Insuffisant', val: lowS.length, total: database.length, color: '#c62828'}
        ]);

        renderBarChart('graph-pratique', [
            {label: 'Correcte', val: database.filter(r=>r.scorePratique>=60).length, total: database.length, color: '#1565c0'},
            {label: 'Inadéquate', val: database.filter(r=>r.scorePratique<60).length, total: database.length, color: '#f57f17'}
        ]);

        // 4. Obstacles
        let obsCounts = {};
        database.forEach(r => r.obstacles.forEach(o => obsCounts[o] = (obsCounts[o] || 0) + 1));
        document.getElementById('graph-obstacles').innerHTML = Object.entries(obsCounts).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
        }).join('');

        // 5. Conclusion
        document.getElementById('final-conclusion').innerHTML = `
            <h3>Synthèse des ${database.length} fiches</h3>
            <p>L'étude révèle un taux de savoir technique de <strong>${((highS.length/database.length)*100).toFixed(0)}%</strong>. La pratique moyenne globale est de <strong>${getAvg(database, 'scorePratique')}%</strong>.</p>
            <p>Le frein majeur identifié est : <strong>${Object.keys(obsCounts).reduce((a, b) => obsCounts[a] > obsCounts[b] ? a : b, "Aucun")}</strong>.</p>
        `;
    }

    // Helpers
    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(c => c.value); }
    function getRadioValue(name) { return document.querySelector(`input[name="${name}"]:checked`).value; }
    function getColor(s) { return s >= 70 ? 'green' : (s >= 50 ? 'orange' : 'red'); }
    function getAvg(arr, prop) { return arr.length ? (arr.reduce((s, c) => s + parseFloat(c[prop]), 0) / arr.length).toFixed(1) : 0; }
    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }
    function renderBarChart(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.total ? Math.round((i.val/i.total)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.label}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.color};">${p}%</div></div><div class="bar-value">${i.val}</div></div>`;
        }).join('');
    }
    function exportToCSV() {
        let csv = "data:text/csv;charset=utf-8,\ufeffID,Savoir,Attitude,Pratique\n";
        database.forEach(r => csv += `${r.id},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}\n`);
        let link = document.createElement("a"); link.href = encodeURI(csv); link.download = "KAP_HGRM.csv"; link.click();
    }
</script>
</body>
</html>
