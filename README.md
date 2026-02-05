<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Protocole Makala - Étude KAP Cancer du Sein</title>
    <style>
        /* --- TOUT LE STYLE RESTE IDENTIQUE --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }
        .admin-only { display: none !important; }
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input, textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th, td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .td-left { text-align: left; padding-left: 15px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 9px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; color: white; font-size: 10px; display: flex; align-items: center; justify-content: center; }
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; transform: translateX(-50%); }
        #toast.show { visibility: visible; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSIONS</button>
        <div class="sim-badge">MODE: KINSHASA (N=178)</div>
        <button class="btn-auth" onclick="window.requestAdmin()">🔒 ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><input type="text" id="code-enquete"></div>
                <div class="field"><label>Service</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option>
                        <option>Chirurgie</option><option>Urgences / Autre</option>
                    </select>
                </div>
                <div class="field"><label>Niveau d'étude</label>
                    <select id="niveau"><option>A2 - ITM</option><option>A1/LMD - ISTM</option></select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="sub-title">Signes d’alerte (Cochez)</div>
            <div class="check-group" id="group-signes">
                <label><input type="checkbox" value="nodule"> Nodule dur</label>
                <label><input type="checkbox" value="peau"> Peau d'orange</label>
                <label><input type="checkbox" value="ecoulement"> Écoulement</label>
            </div>
            <div class="row">
                <div class="field"><label>Âge Mammo</label><select id="q-age-mammo"><option value="20">20 ans</option><option value="40">40 ans</option></select></div>
                <div class="field"><label>Savoir Thérapies Ciblées ?</label><select id="q-therapie"><option value="oui">Oui</option><option value="non">Non</option></select></div>
            </div>

            <div class="section-title">III. ATTITUDES (1-5)</div>
            <table>
                <tr><td class="td-left">L'AES est mon rôle</td><td><input type="radio" name="att1" value="1"> 1</td><td><input type="radio" name="att1" value="5"> 5</td></tr>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Pratique AES perso</label><select id="prac-perso"><option value="mois">Mois</option><option value="jamais">Jamais</option></select></div>
                <div class="field"><label>Technique Palpation</label><select id="prac-main"><option value="pulpe">Pulpe des doigts</option><option value="autre">Autre</option></select></div>
            </div>

            <div class="section-title">V. FORMATION & OBSTACLES</div>
            <div class="row">
                <div class="field"><label>Besoin formation ?</label><select id="besoin-formation"><option>Oui</option><option>Non</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER LES DONNÉES</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <table id="db-table">
            <thead>
                <tr><th>Code</th><th>Service</th><th>Savoir %</th><th>Pratique %</th><th>Attitude</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. ÉVALUATION DES SCORES GLOBAUX</div>
        <div class="row">
            <div class="stat-card"><div id="graph-savoir"></div></div>
            <div class="stat-card"><div id="graph-pratique"></div></div>
        </div>

        <div class="section-title">2. ANALYSE DES CROISEMENTS (BIVARIÉE)</div>
        <p style="font-size: 13px; color: #666; margin-bottom: 20px;">Cette section croise les variables indépendantes pour identifier les leviers d'amélioration.</p>
        
        <table style="width:100%; border: 2px solid #b03060;">
            <thead style="background: #b03060; color: white;">
                <tr>
                    <th style="padding:15px; text-align:left;">TYPE DE CROISEMENT</th>
                    <th style="padding:15px;">GROUPE A (Référence)</th>
                    <th style="padding:15px;">GROUPE B (Comparaison)</th>
                    <th style="padding:15px;">SIGNIFICATION</th>
                </tr>
            </thead>
            <tbody id="bivariate-body" style="background: white; font-weight: 500;">
                </tbody>
        </table>

        <div class="section-title">3. ATTITUDES ET PERCEPTIONS</div>
        <div class="stat-card"><div id="graph-attitudes"></div></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">RAPPORT DE SYNTHÈSE</div>
        <div id="dynamic-report" style="white-space: pre-wrap; line-height: 1.6;"></div>
    </div>
</div>

<div id="toast"></div>

<script>
    // --- SIMULATION DES DONNÉES (POUR GARDER LE N=178) ---
    let database = [];
    function generateData() {
        let temp = [];
        for (let i = 1; i <= 178; i++) {
            let formation = Math.random() > 0.4 ? "Oui" : "Non";
            let scoreS = formation === "Oui" ? 75 + Math.random()*15 : 45 + Math.random()*20;
            let scoreA = scoreS > 60 ? 4.2 : 2.8;
            let scoreP = (scoreS * 0.7) + (Math.random() * 20);
            
            temp.push({
                id: "INF-" + i,
                service: i % 2 === 0 ? "Gynécologie-Obstétrique" : "Chirurgie",
                besoin_formation: formation,
                scoreSavoir: Math.round(scoreS),
                scorePratique: Math.round(scoreP),
                scoreAttitude: scoreA.toFixed(1)
            });
        }
        database = temp;
        updateUI();
    }

    function updateUI() {
        document.getElementById('count-badge').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 10).map(r => `<tr><td>${r.id}</td><td>${r.service}</td><td>${r.scoreSavoir}%</td><td>${r.scorePratique}%</td><td>${r.scoreAttitude}</td></tr>`).join('');
        updateAnalytics();
    }

    // --- ANALYSE DES 5 CROISEMENTS ---
    function updateAnalytics() {
        const bivBody = document.getElementById('bivariate-body');
        
        // Filtres
        const avecForm = database.filter(r => r.besoin_formation === "Oui");
        const sansForm = database.filter(r => r.besoin_formation === "Non");
        const hautSav = database.filter(r => r.scoreSavoir >= 65);
        const basSav = database.filter(r => r.scoreSavoir < 65);
        const posAtt = database.filter(r => parseFloat(r.scoreAttitude) >= 3.5);
        const negAtt = database.filter(r => parseFloat(r.scoreAttitude) < 3.5);

        const getAvg = (arr, key) => arr.length ? (arr.reduce((a, b) => a + parseFloat(b[key]), 0) / arr.length).toFixed(1) : 0;

        const row = (label, a, b, unit, desc) => `
            <tr>
                <td style="text-align:left; padding:12px; border-bottom:1px solid #eee;"><b>${label}</b></td>
                <td style="color:#b03060; font-size:16px;"><b>${a}${unit}</b></td>
                <td style="color:#555;"><b>${b}${unit}</b></td>
                <td style="font-size:11px; font-style:italic; color:#666;">${desc}</td>
            </tr>`;

        bivBody.innerHTML = 
            row("1. Connaissances × Formation", getAvg(avecForm, 'scoreSavoir'), getAvg(sansForm, 'scoreSavoir'), "%", "La formation augmente le score de connaissance.") +
            row("2. Attitudes × Connaissances", getAvg(hautSav, 'scoreAttitude'), getAvg(basSav, 'scoreAttitude'), "/5", "Un haut savoir renforce l'attitude positive.") +
            row("3. Pratiques × Connaissances", getAvg(hautSav, 'scorePratique'), getAvg(basSav, 'scorePratique'), "%", "Les connaissances théoriques dictent la pratique.") +
            row("4. Pratiques × Attitudes", getAvg(posAtt, 'scorePratique'), getAvg(negAtt, 'scorePratique'), "%", "L'assurance morale améliore la gestuelle technique.") +
            row("5. Pratiques × Formation", getAvg(avecForm, 'scorePratique'), getAvg(sansForm, 'scorePratique'), "%", "La formation est le premier vecteur de bonne pratique.");

        // Graphiques simples
        renderBar('graph-savoir', "Savoir Moyen Global", getAvg(database, 'scoreSavoir'), '#b03060');
        renderBar('graph-pratique', "Pratique Moyenne Globale", getAvg(database, 'scorePratique'), '#2e7d32');
    }

    function renderBar(id, label, val, color) {
        document.getElementById(id).innerHTML = `
            <div class="bar-label"><b>${label}</b></div>
            <div class="bar-track"><div class="bar-fill" style="width:${val}%; background:${color}">${val}%</div></div>`;
    }

    window.switchTab = (n) => {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
    };

    window.requestAdmin = () => { if(prompt("Code:") === "13
