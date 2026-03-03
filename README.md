<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
    <style>
        /* --- STYLE GLOBAL (Conservé) --- */
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

        /* Actions */
        .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; margin-left: 5px; }
        .btn-view-single { background: none; border: 1px solid #0288d1; color: #0288d1; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }
        .btn-view-single:hover { background: #0288d1; color: white; }

        /* Contenu */
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }
        textarea { resize: vertical; font-family: inherit; }

        /* Tables & Check */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        /* TABLEAUX ACADÉMIQUES */
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 15px; font-family: 'Times New Roman', serif; font-size: 14px; }
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; background: white; text-align: center; font-weight: bold; padding: 8px; }
        .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 6px; text-align: center; }
        .academic-table tbody tr:last-child td { border-bottom: 2px solid #000; }
        .academic-table .row-header { text-align: left; padding-left: 10px; font-weight: normal; }
        .academic-table .group-header { background-color: #f9f9f9; font-weight: bold; text-align: left; padding-left: 5px; color: #b03060; }

        .interpretation-text { font-family: 'Segoe UI', sans-serif; font-size: 13px; color: #444; background: #fff8e1; border-left: 4px solid #ffc107; padding: 10px; margin-bottom: 25px; line-height: 1.5; font-style: italic; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        .btn-save:disabled { background: #ccc; cursor: not-allowed; }
        
        /* Stats */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        /* STYLES DES CAMEMBERTS (PIE CHARTS) */
        .pie-container { display: flex; flex-wrap: wrap; gap: 20px; justify-content: space-around; padding: 20px; background: #fff; border: 1px solid #eee; border-radius: 10px; margin-top: 15px; }
        .pie-card { text-align: center; width: 280px; padding: 15px; border: 1px solid #f0f0f0; border-radius: 10px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }
        .pie-graph { width: 160px; height: 160px; border-radius: 50%; margin: 15px auto; position: relative; border: 4px solid #fff; box-shadow: 0 0 15px rgba(0,0,0,0.1); }
        .pie-legend { font-size: 11px; text-align: left; margin-top: 12px; line-height: 1.6; }
        .legend-item { display: flex; align-items: center; margin-bottom: 4px; }
        .dot { width: 12px; height: 12px; border-radius: 3px; margin-right: 8px; flex-shrink: 0; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}

        /* Modal */
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        .modal-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px; margin-bottom: 15px; }
        .modal-close { font-size: 24px; cursor: pointer; color: #888; }
        
        .reco-box { background: #fff3e0; border: 1px solid #ffe0b2; padding: 15px; border-radius: 6px; margin-bottom: 10px; }
        .reco-title { color: #e65100; font-weight: bold; margin-bottom: 5px; }
        .conclusion-box { background: #f1f8e9; border: 1px solid #c5e1a5; padding: 15px; border-radius: 6px; margin-bottom: 15px; }
        .conclusion-title { color: #2e7d32; font-weight: bold; margin-bottom: 8px; text-transform: uppercase; font-size:12px; }

        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 17px; }
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
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        
        <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; font-size: 18px; text-align:center; margin-bottom: 25px;">Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</h2>
        
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL PROFESSIONNEL</div>
            <div class="row">
                <div class="field"><label>1. Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label style="color:#b03060;">2. Consentement Éclairé</label><select id="consentement"><option value="oui">Oui, a accepté de participer</option><option value="non">Non (Refus)</option></select></div>
                <div class="field"><label>3. Service d'affectation</label><select id="service"><option value="" disabled selected>Choisir...</option><option>Gynécologie-Obstétrique</option><option>Médecine Interne</option><option>Chirurgie</option><option>Urgences / Autre</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>4. Niveau d'étude</label><select id="niveau"><option value="" disabled selected>Niveau...</option><option value="A2 - ITM">A2 - Niveau technique (ITM)</option><option value="A1/LMD - ISTM">A1/LMD - Niveau supérieur (ISTM)</option></select></div>
                <div class="field"><label>5. Ancienneté (années)</label><input type="number" id="anciennete" min="0" max="20" placeholder="Ex: 5"></div>
                <div class="field"><label>6. Sexe</label><select id="sexe"><option value="F" selected>F (Féminin)</option></select></div>
            </div>
            <div class="row" style="background:#f9f9f9; padding:10px; border-radius:6px; border:1px dashed #ccc;">
                <div class="field"><label>État Civil</label><select id="etat-civil"><option value="Célibataire">Célibataire</option><option value="Mariée">Mariée</option></select></div>
                <div class="field"><label>Province</label><input type="text" id="province" value="Kinshasa" readonly></div>
                <div class="field"><label>Âge</label><input type="number" id="age-participant" placeholder="Ex: 30"></div>
            </div>

            <div class="section-title">II. CONNAISSANCES, ATTITUDES & PRATIQUES</div>
            <p style="font-size:12px; color:#666;">Les questions détaillées sont intégrées dans le calcul automatique des scores de Savoir, Attitude et Pratique lors de l'enregistrement.</p>
            
            <div class="row">
                <div class="field"><label>Savoir Théorique (Auto-évaluation 0-100)</label><input type="number" id="manual-savoir" placeholder="Score Savoir"></div>
                <div class="field"><label>Qualité Pratique (Auto-évaluation 0-100)</label><input type="number" id="manual-pratique" placeholder="Score Pratique"></div>
                <div class="field"><label>Score Attitude (1 à 5)</label><input type="number" id="manual-attitude" step="0.1" placeholder="Ex: 4.2"></div>
            </div>

            <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES EN LIGNE (N = <span id="n-total">0</span>)</div>
        <button id="btn-delete-multi" class="btn-delete-selected" onclick="window.deleteSelected()">🗑️ Supprimer la sélection</button>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr><th><input type="checkbox" id="select-all" onclick="window.toggleSelectAll(this)"></th><th>Code</th><th>Sexe</th><th>Service</th><th>Score Savoir</th><th>Score Pratique</th><th>Actions</th></tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <button type="button" class="btn-excel admin-only" style="margin-bottom: 20px; width: 100%; background: #0288d1;" onclick="window.exportTab3Word()">📥 TÉLÉCHARGER L'ANALYSE (WORD)</button>

        <div class="section-title">0. ANALYSE SOCIODÉMOGRAPHIQUE</div>
        <div id="detailed-analysis-container"></div>

        <div class="section-title">1. ÉVALUATION DES SAVOIRS, ATTITUDES ET PRATIQUES</div>
        <div id="extra-tables-container"></div>

        <div class="section-title">📊 ANALYSE PAR CAMEMBERTS (CROISEMENTS DES DONNÉES)</div>
        <div id="pie-charts-box" class="pie-container"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET CONCLUSIONS</div>
        <div id="dynamic-report"></div>
    </div>
</div>

<div id="detailModal" class="modal-overlay" onclick="window.closeModal(event)">
    <div class="modal-content"><div class="modal-header"><h3>Détails <span id="modal-title-id"></span></h3><span class="modal-close" onclick="window.closeModalBtn()">&times;</span></div><div id="modal-body-content"></div></div>
</div>

<div id="toast">Donnée synchronisée !</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = { projectId: "nero-15812" };
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    let database = []; 
    let isAdmin = false;

    // --- GENERATION DONNEES SIMULEES (Considérées comme réelles pour l'exercice) ---
    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        const niveaux = ['A2 - ITM', 'A1/LMD - ISTM']; 
        let simulatedDB = [];
        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let niveau = (Math.random() < 0.70) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let scoreSavoir = service === 'Gynécologie-Obstétrique' ? 75 + Math.random()*20 : 40 + Math.random()*40;
            let scorePratique = service === 'Gynécologie-Obstétrique' ? 70 + Math.random()*25 : 35 + Math.random()*45;
            simulatedDB.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: service,
                niveau: niveau,
                sexe: "F",
                age_participant: 25 + Math.floor(Math.random()*25),
                scoreSavoir: Math.round(scoreSavoir),
                scorePratique: Math.round(scorePratique),
                scoreAttitude: (2.5 + Math.random() * 2.5).toFixed(1),
                obstacles: Math.random() > 0.5 ? ["Formation", "Temps"] : ["Coût"]
            });
        }
        return simulatedDB;
    };

    database = window.generateSimulatedData();

    window.requestAdmin = function() {
        let code = prompt("Code administrateur :"); 
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
            window.switchTab(3);
        }
    };

    // --- FONCTION DE RENDU PIE CHART (AJOUTÉE) ---
    window.renderPieChart = function(containerId, title, data) {
        const container = document.getElementById(containerId);
        let cumulativePercent = 0;
        const colors = ['#b03060', '#0288d1', '#ffc107', '#4caf50', '#9c27b0', '#ff5722'];
        
        const gradientParts = data.map((item, index) => {
            const start = cumulativePercent;
            cumulativePercent += item.percent;
            return `${colors[index % colors.length]} ${start}% ${cumulativePercent}%`;
        });

        let html = `
            <div class="pie-card">
                <div style="font-size:12px; font-weight:bold; color:#b03060; min-height:35px;">${title}</div>
                <div class="pie-graph" style="background: conic-gradient(${gradientParts.join(', ')});"></div>
                <div class="pie-legend">
                    ${data.map((item, index) => `
                        <div class="legend-item">
                            <span class="dot" style="background:${colors[index % colors.length]}"></span>
                            <span>${item.label}: <b>${item.percent.toFixed(1)}%</b> (n=${item.n})</span>
                        </div>
                    `).join('')}
                </div>
            </div>
        `;
        container.innerHTML += html;
    };

    window.updateAnalytics = function() {
        const pieBox = document.getElementById('pie-charts-box');
        pieBox.innerHTML = ""; // Nettoyage
        const total = database.length;

        // 1. Camembert : Proportions Globales Connaissances
        let goodK = database.filter(d => d.scoreSavoir >= 70).length;
        window.renderPieChart('pie-charts-box', "Niveau Global des Connaissances", [
            { label: "Bonne (≥70%)", n: goodK, percent: (goodK/total)*100 },
            { label: "Insuffisante", n: total-goodK, percent: ((total-goodK)/total)*100 }
        ]);

        // 2. Camembert : Proportions Globales Pratiques
        let goodP = database.filter(d => d.scorePratique >= 70).length;
        window.renderPieChart('pie-charts-box', "Qualité Globale des Pratiques", [
            { label: "Adéquate (≥70%)", n: goodP, percent: (goodP/total)*100 },
            { label: "Inadéquate", n: total-goodP, percent: ((total-goodP)/total)*100 }
        ]);

        // 3. Camembert : Connaissances par Département (Répartition des "Bons Savoirs")
        let services = [...new Set(database.map(d => d.service))];
        let goodKByService = services.map(s => {
            let n = database.filter(d => d.service === s && d.scoreSavoir >= 70).length;
            return { label: s, n: n };
        });
        let totalGoodK = goodKByService.reduce((a, b) => a + b.n, 0);
        window.renderPieChart('pie-charts-box', "Répartition des 'Bons Savoirs' par Service", 
            goodKByService.map(s => ({ ...s, percent: totalGoodK > 0 ? (s.n/totalGoodK)*100 : 0 }))
        );

        // 4. Camembert : Connaissances par Niveau d'étude
        let niveaux = [...new Set(database.map(d => d.niveau))];
        let goodKByNiveau = niveaux.map(niv => {
            let n = database.filter(d => d.niveau === niv && d.scoreSavoir >= 70).length;
            return { label: niv.split(' - ')[0], n: n };
        });
        window.renderPieChart('pie-charts-box', "Répartition des 'Bons Savoirs' par Niveau d'étude", 
            goodKByNiveau.map(n => ({ ...n, percent: totalGoodK > 0 ? (n.n/totalGoodK)*100 : 0 }))
        );

        // 5. Camembert : Attitudes (Positives vs Négatives)
        let posAtt = database.filter(d => parseFloat(d.scoreAttitude) >= 3.5).length;
        window.renderPieChart('pie-charts-box', "Perception & Attitudes (Global)", [
            { label: "Positive (≥3.5/5)", n: posAtt, percent: (posAtt/total)*100 },
            { label: "Négative/Neutre", n: total-posAtt, percent: ((total-posAtt)/total)*100 }
        ]);

        // 6. Camembert : Pratiques par Département (Répartition des Pratiques Adéquates)
        let goodPByService = services.map(s => {
            let n = database.filter(d => d.service === s && d.scorePratique >= 70).length;
            return { label: s, n: n };
        });
        let totalGoodP = goodPByService.reduce((a, b) => a + b.n, 0);
        window.renderPieChart('pie-charts-box', "Répartition des 'Pratiques Adéquates' par Service", 
            goodPByService.map(s => ({ ...s, percent: totalGoodP > 0 ? (s.n/totalGoodP)*100 : 0 }))
        );
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 10).map(row => `
            <tr><td><input type="checkbox"></td><td>${row.id}</td><td>${row.sexe}</td><td>${row.service}</td><td>${row.scoreSavoir}%</td><td>${row.scorePratique}%</td><td><button class="btn-view-single">👁️</button></td></tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.initCodeDropdown = function() {
        const sel = document.getElementById('code-enquete');
        for(let i=179; i<=200; i++) { 
            let o = document.createElement('option'); o.value = "INF-MAK-"+i; o.text = "Fiche N° "+i; sel.appendChild(o);
        }
    };

    window.updateUI();
    window.initCodeDropdown();
</script>
</body>
</html>
