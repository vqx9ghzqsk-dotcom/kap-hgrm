<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE CONSERVÉ --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; width: 100%; box-sizing: border-box; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 10px; transform: scale(1.2); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 30px; }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 150px; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; color: white; text-align: center; font-size: 10px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; margin-top: 10px; font-style: italic; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 15px; margin-top: 10px; font-style: italic; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT GLOBAL</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTAT ET ANALYSE CROISÉE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL PROFESSIONNEL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Sexe</label><select id="sexe"><option>Féminin</option><option>Masculin</option></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Médecine Interne</option><option>Chirurgie</option><option>Urgences / Autre</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté (Années)</label><select id="exp-select"></select></div>
                <div class="field"><label>Niveau d'étude</label><select id="niveau"><option>A2 (Secondaire)</option><option selected>A1 (Gradué)</option><option>A0 (Licencié/Master)</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS THÉORIQUES)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès femme RDC ?</label><select id="q1"><option>Vrai</option><option>Faux</option><option>Je ne sais pas</option></select></div>
                <div class="field"><label>Âge 1ère Mammographie ?</label><select id="q2"><option>Dès 20 ans</option><option>Vers 35-40 ans</option><option>Vers 50 ans</option></select></div>
                <div class="field"><label>Moment idéal AES ?</label><select id="q3"><option>Pendant les règles</option><option>7 à 10 jours après les règles</option><option>N’importe quand</option></select></div>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Facteurs de risque (Cochez si connu) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé (> 50 ans)</label>
                <label class="check-item"><input type="checkbox" value="heredite"> Hérédité (Antécédents)</label>
                <label class="check-item"><input type="checkbox" value="nulliparite"> Nulliparité / 1ère gross. tardive</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive (> 55 ans)</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité / Sédentarité</label>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Signes d'alerte (Cochez si connu) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule (boule) dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                <label class="check-item"><input type="checkbox" value="peau"> Peau d'orange / Rougeur</label>
                <label class="check-item"><input type="checkbox" value="adenopathie"> Adénopathie (boule) axillaire</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
            </div>

            <div class="section-title">III. ATTITUDES (Echelle de 1 à 5)</div>
            <p style="font-size:12px; color:#666;">1: Pas du tout d'accord | 5: Tout à fait d'accord</p>
            <table>
                <thead><tr><th style="text-align:left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td style="text-align:left">Le dépistage précoce permet de guérir le cancer.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4"></td><td><input type="radio" name="p1" value="5" checked></td></tr>
                    <tr><td style="text-align:left">Je me sens capable d'enseigner l'AES.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4" checked></td><td><input type="radio" name="p2" value="5"></td></tr>
                    <tr><td style="text-align:left">La pudeur est un frein à l'examen clinique.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2"></td><td><input type="radio" name="p3" value="3" checked></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td style="text-align:left">Tout nodule suspect doit être orienté vers un médecin.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (TECHNIQUE D'EXAMEN)</div>
            <div class="row">
                <div class="field"><label>Fréquence examen patientes</label><select id="pratique-freq"><option>Systématiquement</option><option>Si plainte</option><option>Rarement / Jamais</option></select></div>
                <div class="field"><label>Partie de la main utilisée</label><select id="prac-main"><option>Pointe des doigts</option><option selected>Pulpe des 3 doigts du milieu</option><option>Paume de la main</option><option>Pincement (pouce/index)</option></select></div>
                <div class="field"><label>Zone souvent oubliée</label><select id="prac-zone"><option>Mamelon</option><option>Partie supérieure</option><option selected>Prolongement axillaire</option></select></div>
            </div>
            
            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Mouvements de palpation utilisés (Cochez) :</label>
            <div class="check-group" id="group-mouvements">
                <label class="check-item"><input type="checkbox" value="circ"> Circulaire (Spirale)</label>
                <label class="check-item"><input type="checkbox" value="vert"> Vertical (Bandelettes)</label>
                <label class="check-item"><input type="checkbox" value="rad"> Radial (Étoile)</label>
            </div>

            <div class="section-title">V. OBSTACLES RENCONTRÉS</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="formation"> Manque de formation</label>
                <label class="check-item"><input type="checkbox" value="temps"> Manque de temps</label>
                <label class="check-item"><input type="checkbox" value="outil"> Absence de matériel/mannequin</label>
                <label class="check-item"><input type="checkbox" value="culture"> Refus des patientes (Culture)</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <table>
            <thead>
                <tr><th>Code</th><th>Niveau</th><th>Exp</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Statut</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. STATISTIQUES DESCRIPTIVES</div>
        <div class="row"><div class="stat-card"><b>Niveau de Savoir</b><div id="graph-savoir"></div></div><div class="stat-card"><b>Qualité Pratique</b><div id="graph-pratique"></div></div></div>
        <div class="section-title">2. ANALYSE CROISÉE</div>
        <table style="background:#333; color:white;">
            <thead><tr><th>Groupe</th><th>N</th><th>Attitude Moy.</th><th>Pratique Moy.</th></tr></thead>
            <tbody id="cross-body" style="background:white; color:black;"></tbody>
        </table>
        <div id="interpretation-cross"></div>
        <div class="section-title">3. ANALYSE DES BARRIÈRES</div>
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
    for (let i = 1; i <= 200; i++) { let opt = document.createElement('option'); opt.value = "E-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 40; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; expSelect.appendChild(opt); }

    function saveRecord() {
        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            exp: parseInt(expSelect.value),
            sexe: document.getElementById('sexe').value,
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            p1: getRadioValue('p1'), p2: getRadioValue('p2'), p3: getRadioValue('p3'), p4: getRadioValue('p4'),
            freq: document.getElementById('pratique-freq').value,
            main: document.getElementById('prac-main').value,
            zone: document.getElementById('prac-zone').value,
            mouvements: getCheckedCount('group-mouvements'),
            obstacles: getCheckedValues('group-obstacles')
        };

        // SCORING BASÉ SUR VOTRE FICHE
        let rawSavoir = 0;
        if(record.q1 === "Vrai") rawSavoir += 2;
        if(record.q2 === "Vers 35-40 ans") rawSavoir += 2;
        if(record.q3.includes("7 à 10 jours")) rawSavoir += 2;
        rawSavoir += record.risques + record.signes;
        record.scoreSavoir = Math.round((rawSavoir / 16) * 100); // Sur 16 points

        let sumAtt = parseInt(record.p1) + parseInt(record.p2) + parseInt(record.p3) + parseInt(record.p4);
        record.scoreAttitude = (sumAtt / 4).toFixed(1);

        let rawPrac = 0;
        if(record.freq === "Systématiquement") rawPrac += 30;
        if(record.main.includes("Pulpe")) rawPrac += 25;
        if(record.zone.includes("axillaire")) rawPrac += 25;
        if(record.mouvements >= 2) rawPrac += 20;
        record.scorePratique = rawPrac;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        alert(`Fiche ${record.id} enregistrée !`);
        
        // Auto-incrément ID
        codeSelect.selectedIndex++;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(database.length === 0) return;
        
        // 1. Dépouillement
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(row => `<tr>
            <td><b>${row.id}</b></td><td>${row.niveau}</td><td>${row.exp} ans</td>
            <td style="color:${row.scoreSavoir>=70?'green':'red'}">${row.scoreSavoir}%</td>
            <td>${row.scoreAttitude}</td>
            <td style="color:${row.scorePratique>=70?'green':'red'}">${row.scorePratique}%</td>
            <td>${row.scoreSavoir>=70 && row.scorePratique>=60 ? '🟢 Adéquat' : '🔴 À renforcer'}</td>
        </tr>`).join('');

        // 2. Analyse Croisée
        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        
        let avgAttHigh = getAvg(high, 'scoreAttitude'), avgPracHigh = getAvg(high, 'scorePratique');
        let avgAttLow = getAvg(low, 'scoreAttitude'), avgPracLow = getAvg(low, 'scorePratique');

        document.getElementById('cross-body').innerHTML = `
            <tr><td><b>Savoir Élevé (>=70%)</b></td><td>${high.length}</td><td>${avgAttHigh}/5</td><td>${avgPracHigh}%</td></tr>
            <tr><td><b>Savoir Faible (<70%)</b></td><td>${low.length}</td><td>${avgAttLow}/5</td><td>${avgPracLow}%</td></tr>`;

        // Graphes et Interprétation
        renderBarChart('graph-savoir', [{label:'Bon', val:high.length, total:database.length, color:'green'}, {label:'Insuffisant', val:low.length, total:database.length, color:'red'}]);
        
        let obsCount = {}; database.forEach(r => r.obstacles.forEach(o => obsCount[o] = (obsCount[o]||0)+1));
        document.getElementById('graph-obstacles').innerHTML = Object.entries(obsCount).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div></div>`;
        }).join('');

        document.getElementById('final-conclusion').innerHTML = `<h3>Analyse de ${database.length} fiches</h3>
        <p>Le niveau de connaissance moyen est de <b>${getAvg(database, 'scoreSavoir')}%</b>. 
        L'obstacle majeur identifié est le <b>${Object.keys(obsCount)[0] || 'N/A'}</b>.</p>`;
    }

    // Helpers
    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); }
    function getRadioValue(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e ? e.value : 0; }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; }
    function renderBarChart(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.total ? Math.round((i.val/i.total)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.label}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.color}">${p}%</div></div></div>`;
        }).join('');
    }
    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }
    function exportToCSV() {
        let csv = "ID,Sexe,Niveau,Exp,Savoir,Attitude,Pratique\n" + database.map(r => `${r.id},${r.sexe},${r.niveau},${r.exp},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let link = document.createElement("a"); link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "Analyse_KAP_HGRM.csv"; link.click();
    }
</script>
</body>
</html>