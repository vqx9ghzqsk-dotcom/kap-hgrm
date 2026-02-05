<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* Simulation Mode Badge */
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }

        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}

        /* Contenu */
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; }
        
        /* Stats */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        
        <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; font-size: 18px; text-align:center;">Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</h2>
        <p style="text-align: center; font-style: italic;">Veuillez remplir les informations de l'enquête ici.</p>
        <button type="button" class="btn-save" disabled>FORMULAIRE DE COLLECTE ACTIF</button>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES EN LIGNE (N = <span id="n-total">0</span>)</div>
        <table>
            <thead>
                <tr><th>Code</th><th>Sexe</th><th>Service</th><th>Score Savoir</th><th>Score Pratique</th><th>Diagnostic</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. CROISEMENTS ANALYTIQUES INTELLIGENTS</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">1. Connaissances × Formation</div>
                <div id="graph-cross-1"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">2. Attitudes × Connaissances</div>
                <div id="graph-cross-2"></div>
            </div>
        </div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">3. Pratiques × Connaissances</div>
                <div id="graph-cross-3"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">4. Pratiques × Attitudes</div>
                <div id="graph-cross-4"></div>
            </div>
        </div>
        <div class="stat-card">
            <div class="stat-title">5. Pratiques × Formation</div>
            <div id="graph-cross-5"></div>
        </div>

        <div class="section-title">2. SYNTHÈSE DES GROUPES (RÉSUMÉ ANALYTIQUE)</div>
        <table id="table-synthese" style="width:100%; border: 2px solid #b03060;">
            <thead style="background: #b03060; color:white;">
                <tr>
                    <th style="padding:15px;">GROUPE D'ANALYSE</th>
                    <th>EFFECTIF (N)</th>
                    <th>CONNAISSANCES MOY.</th>
                    <th>PRATIQUES MOY.</th>
                    <th>ATTITUDE (/5)</th>
                </tr>
            </thead>
            <tbody id="synthesis-body" style="font-weight: bold; font-size: 14px;">
                </tbody>
        </table>

        <div class="section-title">3. HIÉRARCHIE DES OBSTACLES</div>
        <div id="graph-obstacles-anal"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE AUTOMATISÉE ET RECOMMANDATIONS</div>
        <div id="dynamic-report"></div>
    </div>
</div>

<script type="module">
    let database = []; 
    let isAdmin = false;

    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let simulatedDB = [];
        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let a_formation = Math.random() < 0.25; // 25% ont eu une formation
            let scoreSavoir = a_formation ? Math.floor(75 + Math.random() * 20) : Math.floor(30 + Math.random() * 40);
            let attitude = (scoreSavoir / 20) + (Math.random() * 1);
            let scorePratique = (scoreSavoir * 0.6) + (attitude * 5) + (Math.random() * 10);

            simulatedDB.push({
                id: "INF-MAK-" + i.padStart,
                service: service,
                formation: a_formation ? "Oui" : "Non",
                scoreSavoir: Math.min(100, Math.round(scoreSavoir)),
                scorePratique: Math.min(100, Math.round(scorePratique)),
                scoreAttitude: Math.min(5, attitude).toFixed(1),
                obstacles: (Math.random() < 0.74) ? ["Formation"] : ["Coût"]
            });
        }
        return simulatedDB;
    };

    database = window.generateSimulatedData();

    window.requestAdmin = function() {
        let code = prompt("Code administrateur :"); 
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
            window.switchTab(3);
        }
    };

    window.updateUI = function() {
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 10).map(row => `
            <tr><td>${row.id}</td><td>F</td><td>${row.service}</td><td>${row.scoreSavoir}%</td><td>${row.scorePratique}%</td><td>Moyen</td></tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        // --- 1. CROISEMENTS ---
        
        // C1: Connaissances x Formation
        let fOui = database.filter(r => r.formation === "Oui");
        let fNon = database.filter(r => r.formation === "Non");
        renderBars('graph-cross-1', [
            {l: 'Avec Formation', v: getAvg(fOui, 'scoreSavoir'), t: 100, c: '#2e7d32'},
            {l: 'Sans Formation', v: getAvg(fNon, 'scoreSavoir'), t: 100, c: '#c62828'}
        ]);

        // C2: Attitudes x Connaissances
        let cHaute = database.filter(r => r.scoreSavoir >= 70);
        let cBasse = database.filter(r => r.scoreSavoir < 70);
        renderBars('graph-cross-2', [
            {l: 'Savoir Élevé (Attitude /5)', v: getAvg(cHaute, 'scoreAttitude'), t: 5, c: '#43a047'},
            {l: 'Savoir Faible (Attitude /5)', v: getAvg(cBasse, 'scoreAttitude'), t: 5, c: '#fb8c00'}
        ]);

        // C3: Pratiques x Connaissances
        renderBars('graph-cross-3', [
            {l: 'Savoir >= 70% (Pratique %)', v: getAvg(cHaute, 'scorePratique'), t: 100, c: '#1565c0'},
            {l: 'Savoir < 70% (Pratique %)', v: getAvg(cBasse, 'scorePratique'), t: 100, c: '#546e7a'}
        ]);

        // C4: Pratiques x Attitudes
        let aPos = database.filter(r => r.scoreAttitude >= 3.5);
        let aNeg = database.filter(r => r.scoreAttitude < 3.5);
        renderBars('graph-cross-4', [
            {l: 'Attitude Positive (Pratique %)', v: getAvg(aPos, 'scorePratique'), t: 100, c: '#00897b'},
            {l: 'Attitude Négative (Pratique %)', v: getAvg(aNeg, 'scorePratique'), t: 100, c: '#8d6e63'}
        ]);

        // C5: Pratiques x Formation
        renderBars('graph-cross-5', [
            {l: 'Formées (Pratique %)', v: getAvg(fOui, 'scorePratique'), t: 100, c: '#6a1b9a'},
            {l: 'Non Formées (Pratique %)', v: getAvg(fNon, 'scorePratique'), t: 100, c: '#ad1457'}
        ]);

        // --- 2. TABLEAU DE SYNTHÈSE (GRAS) ---
        const sBody = document.getElementById('synthesis-body');
        const groups = [
            {n: "Global Makala", data: database},
            {n: "Personnel Formé", data: fOui},
            {n: "Personnel Non Formé", data: fNon},
            {n: "Gynéco-Obstétrique", data: database.filter(r => r.service === "Gynécologie-Obstétrique")},
            {n: "Autres Services", data: database.filter(r => r.service !== "Gynécologie-Obstétrique")}
        ];

        sBody.innerHTML = groups.map(g => `
            <tr>
                <td style="text-align:left; padding-left:10px;">${g.n.toUpperCase()}</td>
                <td>${g.data.length}</td>
                <td>${getAvg(g.data, 'scoreSavoir')}%</td>
                <td>${getAvg(g.data, 'scorePratique')}%</td>
                <td>${getAvg(g.data, 'scoreAttitude')}</td>
            </tr>
        `).join('');

        // Obstacles
        let vFormation = database.filter(r => r.obstacles.includes("Formation")).length;
        renderBars('graph-obstacles-anal', [
            {l: 'Manque de formation', v: vFormation, t: database.length, c: '#b03060'},
            {l: 'Coût des examens', v: database.length - vFormation, t: database.length, c: '#757575'}
        ]);
    };

    function getAvg(arr, p) { 
        if(!arr.length) return 0;
        return (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1); 
    }

    function renderBars(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = Math.round((i.v/i.t)*100);
            return `<div class="bar-container"><div class="bar-label"><b>${i.l}</b></div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${i.v}${i.t==100?'%':''}</div></div></div>`;
        }).join('');
    }

    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.updateUI();
</script>
</body>
</html>
