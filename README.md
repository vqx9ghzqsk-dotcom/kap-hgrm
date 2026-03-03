<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse CAP - HGR Makala</title>
    <style>
        /* --- STYLE GLOBAL (Conservé & Optimisé) --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }
        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; }
        
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 13px; }
        
        /* Tableaux Académiques */
        table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 12px; }
        .academic-table { font-family: 'Times New Roman', serif; font-size: 14px; }
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; padding: 8px; }
        .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 6px; text-align: center; }
        .academic-table .row-header { text-align: left; font-weight: normal; }

        /* --- STYLE GRAPHIQUES CAMEMBERT --- */
        .charts-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-top: 20px; }
        .pie-card { background: #fff; border: 1px solid #eee; border-radius: 8px; padding: 15px; text-align: center; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .pie-container { position: relative; width: 150px; height: 150px; margin: 0 auto 15px; }
        .pie-svg { transform: rotate(-90deg); border-radius: 50%; }
        .pie-legend { font-size: 11px; text-align: left; display: inline-block; width: 100%; margin-top: 10px; }
        .legend-item { display: flex; align-items: center; margin-bottom: 4px; }
        .legend-color { width: 12px; height: 12px; margin-right: 8px; border-radius: 2px; }
        
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; }
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; left: 50%; bottom: 30px; transform: translateX(-50%); }
        #toast.show { visibility: visible; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE 📊</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSIONS</button>
        <div class="sim-badge">HGR MAKALA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <p style="text-align:center;">Formulaire de collecte actif...</p>
        <button type="button" class="btn-save" onclick="window.saveRecord()">ENREGISTRER</button>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">Base de données</div>
        <div id="database-body"></div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">0. ANALYSE DES RÉPARTITIONS GÉNÉRALES (CAMEMBERTS 📊)</div>
        <div class="charts-grid" id="main-pies-container"></div>

        <div class="section-title">1. TABLEAUX CROISÉS & ANALYSE DE LA PRATIQUE (TOTAL LIGNE 100%)</div>
        <div id="detailed-tables-container"></div>

        <div class="section-title">2. CROISEMENTS DES CONNAISSANCES (CAMEMBERTS 📊)</div>
        <div class="charts-grid" id="cross-pies-container"></div>

        <div class="section-title">3. LIEN C.A.P & SYNTHÈSE</div>
        <div id="cap-link-container"></div>
        
        <div class="section-title">4. ANALYSE DES 17 TABLEAUX SUPPLÉMENTAIRES</div>
        <div id="extra-tables-container"></div>
    </div>

    <div id="content-4" class="form-content">
        <div id="dynamic-report"></div>
    </div>
</div>

<div id="toast">Synchronisation...</div>

<script type="module">
    // --- INITIALISATION DONNÉES (Identique à ton code) ---
    let database = [];
    let isAdmin = false;

    // Simulation de données (Logique identique à ton code)
    window.generateSimulatedData = function() {
        let db = [];
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences'];
        for(let i=1; i<=178; i++){
            let s = services[Math.floor(Math.random()*services.length)];
            let n = Math.random() > 0.3 ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let sk = s === 'Gynécologie-Obstétrique' ? 85 : 45 + Math.random()*20;
            let sp = s === 'Gynécologie-Obstétrique' ? 80 : 40 + Math.random()*25;
            db.push({ id: "INF-"+i, service: s, niveau: n, scoreSavoir: Math.round(sk), scorePratique: Math.round(sp), scoreAttitude: (2.5 + Math.random()*2).toFixed(1) });
        }
        return db;
    };
    database = window.generateSimulatedData();

    // --- FONCTION DE GÉNÉRATION DE CAMEMBERT (SVG) ---
    window.renderPie = function(containerId, title, slices) {
        let total = slices.reduce((sum, s) => sum + s.value, 0);
        let currentAngle = 0;
        let svgContent = '';

        slices.forEach(slice => {
            let percent = (slice.value / total) * 100;
            let angle = (slice.value / total) * 360;
            
            // Calcul des coordonnées pour le segment SVG
            const x1 = 50 + 50 * Math.cos(Math.PI * currentAngle / 180);
            const y1 = 50 + 50 * Math.sin(Math.PI * currentAngle / 180);
            currentAngle += angle;
            const x2 = 50 + 50 * Math.cos(Math.PI * currentAngle / 180);
            const y2 = 50 + 50 * Math.sin(Math.PI * currentAngle / 180);
            
            const largeArc = angle > 180 ? 1 : 0;
            svgContent += `<path d="M 50 50 L ${x1} ${y1} A 50 50 0 ${largeArc} 1 ${x2} ${y2} Z" fill="${slice.color}"></path>`;
        });

        let legendHtml = slices.map(s => `
            <div class="legend-item">
                <div class="legend-color" style="background:${s.color}"></div>
                <span><b>${((s.value/total)*100).toFixed(1)}%</b> : ${s.label} (${s.value})</span>
            </div>
        `).join('');

        const html = `
            <div class="pie-card">
                <div style="font-weight:bold; font-size:12px; margin-bottom:10px; height:35px;">${title}</div>
                <div class="pie-container">
                    <svg viewBox="0 0 100 100" class="pie-svg" width="100%" height="100%">${svgContent}</svg>
                </div>
                <div class="pie-legend">${legendHtml}</div>
            </div>
        `;
        document.getElementById(containerId).innerHTML += html;
    };

    // --- MISE À JOUR ANALYTIQUE (Règle 100% + Camemberts) ---
    window.updateAnalytics = function() {
        if(database.length === 0) return;
        const total = database.length;

        // 1. Camemberts Généraux
        const mainCont = document.getElementById('main-pies-container');
        mainCont.innerHTML = '';
        
        let skBon = database.filter(d => d.scoreSavoir >= 70).length;
        renderPie('main-pies-container', "Niveau de Savoir (Connaissances)", [
            { label: "Adéquat (≥70%)", value: skBon, color: "#2e7d32" },
            { label: "Insuffisant (<70%)", value: total - skBon, color: "#c62828" }
        ]);

        let spBon = database.filter(d => d.scorePratique >= 70).length;
        renderPie('main-pies-container', "Qualité de la Pratique", [
            { label: "Conforme", value: spBon, color: "#1565c0" },
            { label: "À améliorer", value: total - spBon, color: "#ff9800" }
        ]);

        let attPos = database.filter(d => parseFloat(d.scoreAttitude) >= 3.5).length;
        renderPie('main-pies-container', "Attitudes", [
            { label: "Positives", value: attPos, color: "#9c27b0" },
            { label: "Neutres/Négatives", value: total - attPos, color: "#e91e63" }
        ]);

        // 2. Tableaux avec Règle 100%
        const tableCont = document.getElementById('detailed-tables-container');
        let services = [...new Set(database.map(d => d.service))];
        
        let htmlTable = `
            <table class="academic-table">
                <thead>
                    <tr>
                        <th class="row-header">Service</th>
                        <th>Pratique Adéquate (n)</th>
                        <th>Pratique Insuffisante (n)</th>
                        <th>Total (N)</th>
                        <th style="background:#f9f9f9;">Total Ligne (%)</th>
                    </tr>
                </thead>
                <tbody>
        `;

        const crossCont = document.getElementById('cross-pies-container');
        crossCont.innerHTML = '';

        services.forEach(s => {
            let sub = database.filter(d => d.service === s);
            let n = sub.length;
            let bon = sub.filter(d => d.scorePratique >= 70).length;
            let mauv = n - bon;
            
            htmlTable += `
                <tr>
                    <td class="row-header"><b>${s}</b></td>
                    <td style="color:green;">${bon} (${((bon/n)*100).toFixed(1)}%)</td>
                    <td style="color:red;">${mauv} (${((mauv/n)*100).toFixed(1)}%)</td>
                    <td><b>${n}</b></td>
                    <td style="background:#f9f9f9;"><b>100.0%</b></td>
                </tr>
            `;

            // Ajout Camembert de croisement pour ce service
            renderPie('cross-pies-container', `Savoir : ${s}`, [
                { label: "Bon", value: sub.filter(d=>d.scoreSavoir>=70).length, color: "#4caf50" },
                { label: "Faible", value: sub.filter(d=>d.scoreSavoir<70).length, color: "#f44336" }
            ]);
        });
        htmlTable += `</tbody></table>`;
        tableCont.innerHTML = htmlTable;

        // 3. Croisement Savoir / Niveau d'étude (Camemberts)
        ['A1/LMD - ISTM', 'A2 - ITM'].forEach(niv => {
            let sub = database.filter(d => d.niveau === niv);
            renderPie('cross-pies-container', `Savoir par Niveau : ${niv.split(' ')[0]}`, [
                { label: "Maîtrise", value: sub.filter(d=>d.scoreSavoir>=70).length, color: "#00bcd4" },
                { label: "Lacunes", value: sub.filter(d=>d.scoreSavoir<70).length, color: "#3f51b5" }
            ]);
        });
    };

    // --- FONCTIONS NAVIGATION (Identiques) ---
    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
        if(i===3) window.updateAnalytics();
    };

    window.requestAdmin = function() {
        let code = prompt("Code :");
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            switchTab(3);
        }
    };

    // Initialisation
    setTimeout(() => { if(isAdmin) updateAnalytics(); }, 500);

</script>
</body>
</html>
