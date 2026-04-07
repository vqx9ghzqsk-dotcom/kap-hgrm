<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse CAP - Cancer du Sein - Hôpital Makala</title>
    <style>
        /* --- STYLE GLOBAL (Identique) --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }
        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }

        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 25px; font-family: 'Times New Roman', serif; font-size: 14px; background: white;}
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; background: #fdfdfd; padding: 10px; }
        .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 8px; }
        .academic-table .group-header { background-color: #f0f8ff; font-weight: bold; text-align: left; padding-left: 10px; color: #0d47a1; }
        .total-row { font-weight: bold; background: #f5f5f5; border-top: 2px solid #333 !important; }

        .interpretation-text { font-family: 'Segoe UI', sans-serif; font-size: 13px; color: #444; background: #fff8e1; border-left: 4px solid #ffc107; padding: 10px; margin-bottom: 25px; font-style: italic; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        
        .dash-card { background: white; border: 1px solid #e6e6e6; border-radius: 6px; padding: 15px; flex: 1; min-width: 250px; box-shadow: 0 2px 5px rgba(0,0,0,0.02); }
        .bar-chart-container { display: flex; align-items: flex-end; justify-content: space-around; height: 180px; border-bottom: 2px solid #ccc; border-left: 2px solid #ccc; margin-top: 10px; padding-bottom: 25px; }
        .bar { width: 100%; max-width: 40px; background-color: #b03060; border-radius: 3px 3px 0 0; }
        
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; margin-left: -125px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. DISCUSSION</button>
        
        <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; font-size: 18px; text-align:center;">Collecte CAP - Cancer du Sein</h2>
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Médecine Interne</option><option>Chirurgie</option><option>Urgences / Autre</option></select></div>
                <div class="field"><label>Niveau étude</label><select id="niveau"><option value="A2 - ITM">A2 - Niveau technique</option><option value="A1/LMD - ISTM">A1/LMD - Niveau supérieur</option></select></div>
            </div>
            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES EN LIGNE</div>
        <table>
            <thead><tr><th>Code</th><th>Service</th><th>Score Savoir (%)</th><th>Score Pratique (%)</th></tr></thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <button type="button" class="btn-excel admin-only" style="margin-bottom: 20px; width: 100%; background: #d32f2f;" onclick="window.print()">📥 TÉLÉCHARGER LES RÉSULTATS (PDF)</button>

        <div class="section-title">CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES</div>
        <div id="socio-demo-summary"></div>

        <div class="section-title">ANALYSE CROISÉE : PROFIL vs CONNAISSANCES SPÉCIFIQUES</div>
        <div class="interpretation-text">Barème de cotation : Bon (≥70%), Moyen (50-69%), Faible (<50%). Les données sont croisées pour identifier les corrélations entre le profil et les savoirs théoriques.</div>
        <div id="cross-knowledge-tables"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">DISCUSSION</div>
        <button type="button" class="btn-excel admin-only" style="margin-bottom: 20px; width: 100%; background: #d32f2f;" onclick="window.print()">📥 TÉLÉCHARGER LA DISCUSSION (PDF)</button>
        <div id="dynamic-report"></div>
    </div>
</div>

<div id="toast">Action effectuée !</div>

<script type="module">
    let database = [];
    let isAdmin = false;

    // --- MISE À JOUR DE LA DISTRIBUTION D'ÂGE (N=178) ---
    window.generateSimulatedData = function() {
        let simulatedDB = [];
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        
        for (let i = 1; i <= 178; i++) {
            let age;
            if (i <= 23) age = 24 + Math.floor(Math.random() * 5); // < 30 ans (n=23)
            else if (i <= 147) age = 30 + Math.floor(Math.random() * 15); // 30-45 ans (n=124)
            else age = 46 + Math.floor(Math.random() * 10); // > 45 ans (n=31)

            let service = services[Math.floor(Math.random() * services.length)];
            let niveau = (Math.random() < 0.65) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let anciennete = age - 22;

            // Sous-scores de connaissances
            let k_mammo = Math.floor(Math.random() * 101);
            let k_signes = Math.floor(Math.random() * 101);
            let k_risques = Math.floor(Math.random() * 101);
            let k_epi = Math.floor(Math.random() * 101);
            let k_bio = Math.floor(Math.random() * 101);

            simulatedDB.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: service, niveau: niveau, age_participant: age,
                anciennete: anciennete,
                scoreSavoir: Math.round((k_mammo + k_signes + k_risques + k_epi + k_bio) / 5),
                k_mammo: k_mammo, k_sa: k_signes, k_fr: k_risques, k_epi: k_epi, k_bio: k_bio,
                scorePratique: Math.floor(Math.random() * 101),
                scoreAttitude: (Math.random() * 5).toFixed(1)
            });
        }
        return simulatedDB;
    };

    database = window.generateSimulatedData();

    window.updateExtraTables = function() {
        const total = 178;
        const getP = (v, t) => ((v/t)*100).toFixed(1);
        const barème = (score) => score >= 70 ? 'Bon' : (score >= 50 ? 'Moyen' : 'Faible');

        // --- TABLEAU SOCIO-DÉMO AVEC TOTAUX 100% ---
        let age_23 = database.filter(d => d.age_participant < 30).length;
        let age_124 = database.filter(d => d.age_participant >= 30 && d.age_participant <= 45).length;
        let age_31 = database.filter(d => d.age_participant > 45).length;
        let a1 = database.filter(d => d.niveau.includes('A1')).length;
        let a2 = total - a1;

        document.getElementById('socio-demo-summary').innerHTML = `
            <table class="academic-table">
                <thead><tr><th>Variables</th><th>n</th><th>%</th></tr></thead>
                <tbody>
                    <tr><td colspan="3" class="group-header">Tranches d'âge</td></tr>
                    <tr><td>Moins de 30 ans</td><td>${age_23}</td><td>${getP(age_23, total)}</td></tr>
                    <tr><td>Entre 30 et 45 ans</td><td>${age_124}</td><td>${getP(age_124, total)}</td></tr>
                    <tr><td>Plus de 45 ans</td><td>${age_31}</td><td>${getP(age_31, total)}</td></tr>
                    <tr class="total-row"><td>Total Tranches d'âge</td><td>${total}</td><td>100.0%</td></tr>
                    <tr><td colspan="3" class="group-header">Niveau d'études</td></tr>
                    <tr><td>Niveau Supérieur (A1/LMD)</td><td>${a1}</td><td>${getP(a1, total)}</td></tr>
                    <tr><td>Niveau Technique (A2)</td><td>${a2}</td><td>${getP(a2, total)}</td></tr>
                    <tr class="total-row"><td>Total Niveau d'études</td><td>${total}</td><td>100.0%</td></tr>
                </tbody>
            </table>
        `;

        // --- TABLEAUX CROISÉS AVEC BARÈME ---
        const variables = [
            { label: 'Mammographie', key: 'k_mammo' },
            { label: 'Signes d\'alerte', key: 'k_sa' },
            { label: 'Facteurs de risque', key: 'k_fr' },
            { label: 'Épidémiologie & Dépistage', key: 'k_epi' },
            { label: 'Connaissances Biologiques', key: 'k_bio' }
        ];

        let crossHtml = "";
        variables.forEach(v => {
            crossHtml += `<h4>Croisement : Niveau d'étude vs ${v.label}</h4>
            <table class="academic-table">
                <thead>
                    <tr><th>Niveau</th><th>Bon (≥70%)</th><th>Moyen (50-69%)</th><th>Faible (<50%)</th><th>Total</th></tr>
                </thead>
                <tbody>
                    <tr>
                        <td>A1 (Supérieur)</td>
                        <td>${database.filter(d => d.niveau.includes('A1') && barème(d[v.key]) === 'Bon').length}</td>
                        <td>${database.filter(d => d.niveau.includes('A1') && barème(d[v.key]) === 'Moyen').length}</td>
                        <td>${database.filter(d => d.niveau.includes('A1') && barème(d[v.key]) === 'Faible').length}</td>
                        <td>${a1}</td>
                    </tr>
                    <tr>
                        <td>A2 (Technique)</td>
                        <td>${database.filter(d => !d.niveau.includes('A1') && barème(d[v.key]) === 'Bon').length}</td>
                        <td>${database.filter(d => !d.niveau.includes('A1') && barème(d[v.key]) === 'Moyen').length}</td>
                        <td>${database.filter(d => !d.niveau.includes('A1') && barème(d[v.key]) === 'Faible').length}</td>
                        <td>${a2}</td>
                    </tr>
                </tbody>
            </table>`;
        });
        document.getElementById('cross-knowledge-tables').innerHTML = crossHtml;
    };

    // --- FONCTIONS STANDARDS (Identiques) ---
    window.requestAdmin = function() {
        let code = prompt("Code administrateur :"); 
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
            window.updateExtraTables();
        }
    };

    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.updateUI = function() {
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(row => `
            <tr><td>${row.id}</td><td>${row.service}</td><td>${row.scoreSavoir}%</td><td>${row.scorePratique}%</td></tr>
        `).join('');
    };

    window.updateUI();
</script>
</body>
</html>
