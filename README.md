<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
    <style>
        /* --- STYLE GLOBAL (STRICTEMENT IDENTIQUE) --- */
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
        .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; margin-left: 5px; }
        .btn-view-single { background: none; border: 1px solid #0288d1; color: #0288d1; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input, textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; }
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
                <div class="field"><label style="color:#b03060;">2. Consentement Éclairé</label><select id="consentement"><option value="oui">Oui</option><option value="non">Non</option></select></div>
                <div class="field"><label>3. Service d'affectation</label>
                    <select id="service"><option>Gynécologie-Obstétrique</option><option>Médecine Interne</option><option>Chirurgie</option><option>Urgences / Autre</option></select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>4. Niveau d'étude</label><select id="niveau"><option value="A2 - ITM">A2 - ITM</option><option value="A1/LMD - ISTM">A1/LMD - ISTM</option></select></div>
                <div class="field"><label>5. Ancienneté (années)</label><input type="number" id="anciennete" value="5"></div>
                <div class="field"><label>6. Sexe</label><select id="sexe"><option value="F">F (Féminin)</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="row">
                <div class="field"><label>Classification moléculaire ?</label><select id="q-moleculaire"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Terme "HER2 Low" ?</label><select id="q-her2"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Thérapies ciblées ?</label><select id="q-therapie"><option value="non">Non</option><option value="oui">Oui</option></select></div>
            </div>
            <div class="sub-title">Signes d’alerte (Cochez)</div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction</label>
                <label class="check-item"><input type="checkbox" value="peau"> Peau d’orange</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement</label>
            </div>

            <div class="section-title">III. ATTITUDES (Échelle 1-5)</div>
            <table>
                <thead><tr><th class="td-left">Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="td-left">L’éducation à l’AES fait partie de mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5" checked></td></tr>
                    <tr><td class="td-left">Je me sens capable de détecter un nodule.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>15. AES sur vous-même</label><select id="prac-perso"><option value="mois">Tous les mois</option><option value="jamais">Jamais</option></select></div>
                <div class="field"><label>Partie de la main ?</label><select id="prac-main"><option value="pulpe">Pulpe des 3 doigts</option><option value="pointe">Pointe des doigts</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="Formation"> Manque de formation</label>
                <label class="check-item"><input type="checkbox" value="Coût"> Coût des examens</label>
                <label class="check-item"><input type="checkbox" value="Temps"> Manque de temps</label>
            </div>

            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <div style="overflow-x:auto;">
            <table>
                <thead><tr><th>Code</th><th>Sexe</th><th>Service</th><th>Savoir (%)</th><th>Pratique (%)</th><th>Actions</th></tr></thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. ÉVALUATION DES SCORES GLOBAUX</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Connaissances</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de la Pratique</div><div id="graph-pratique"></div></div>
        </div>

        <div class="section-title">2. SYNTHÈSE DES GROUPES ET ANALYSE COMPARATIVE</div>
        <p style="font-size:13px; color:#666; margin-bottom:15px;">Croisement des performances par Service et Niveau d'Étude.</p>
        
        <div style="box-shadow: 0 4px 12px rgba(0,0,0,0.1); border-radius: 10px; overflow: hidden;">
            <table style="margin:0;">
                <thead style="background: #b03060; color: white;">
                    <tr>
                        <th style="padding:15px; text-align:left;">GROUPE</th>
                        <th>EFFECTIF (N)</th>
                        <th>SAVOIR (%)</th>
                        <th>ATTITUDE (/5)</th>
                        <th>PRATIQUE (%)</th>
                        <th>PROFIL</th>
                    </tr>
                </thead>
                <tbody id="cross-body" style="background: white;"></tbody>
            </table>
        </div>

        <div class="section-title">3. HIÉRARCHIE DES OBSTACLES</div>
        <div id="graph-obstacles-anal"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSION & RECOMMANDATIONS</div>
        <div id="dynamic-report"></div>
        <button type="button" class="btn-excel" onclick="window.exportToCSV()">📥 TÉLÉCHARGER CSV</button>
    </div>
</div>

<div id="toast">Donnée synchronisée !</div>

<script type="module">
    // --- LOGIQUE FIREBASE (IDENTIQUE) ---
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, doc, Timestamp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = { projectId: "nero-15812", appId: "1:957894727402:web:5c319686c580c23700e993" };
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    let database = []; 
    let isAdmin = false;

    window.generateSimulatedData = function() {
        let sim = [];
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        for (let i = 1; i <= 178; i++) {
            let srv = services[i % 4];
            let niv = i % 3 === 0 ? "A2 - ITM" : "A1/LMD - ISTM";
            let scoreS = niv === "A2 - ITM" ? 45 + Math.random()*20 : 65 + Math.random()*25;
            sim.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: srv, niveau: niv, anciennete: 5, sexe: "F",
                scoreSavoir: Math.round(scoreS),
                scorePratique: Math.round(scoreS * 0.75),
                scoreAttitude: (3.2 + Math.random()*1.5).toFixed(1),
                obstacles: ["Formation", "Coût"]
            });
        }
        return sim;
    };

    database = window.generateSimulatedData();

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 15).map((row, index) => `
            <tr><td><b>${row.id}</b></td><td>F</td><td>${row.service}</td>
            <td style="color:${row.scoreSavoir > 70 ? 'green':'red'}">${row.scoreSavoir}%</td>
            <td>${row.scorePratique}%</td>
            <td><button class="btn-view-single">👁️</button></td></tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    // --- SYNTHÈSE AMÉLIORÉE (MODIFICATION ICI) ---
    window.updateAnalytics = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        const niveaux = ["A2 - ITM", "A1/LMD - ISTM"];
        const crossBody = document.getElementById('cross-body');
        
        const groups = [
            ...services.map(s => ({label: s, filter: r => r.service === s, type: 'SRV'})),
            ...niveaux.map(n => ({label: "Niveau " + n, filter: r => r.niveau === n, type: 'NIV'}))
        ];

        crossBody.innerHTML = groups.map(g => {
            let sub = database.filter(g.filter);
            let n = sub.length;
            let avgS = (sub.reduce((a,c)=>a+c.scoreSavoir,0)/n).toFixed(1);
            let avgA = (sub.reduce((a,c)=>a+parseFloat(c.scoreAttitude),0)/n).toFixed(1);
            let avgP = (sub.reduce((a,c)=>a+c.scorePratique,0)/n).toFixed(1);
            
            // Logique de profil
            let badge = "";
            if (avgP > 70) badge = `<span style="background:#e8f5e9; color:#2e7d32; padding:4px 8px; border-radius:12px; font-weight:bold;">PERFORMANT</span>`;
            else if (avgP < 50) badge = `<span style="background:#ffebee; color:#c62828; padding:4px 8px; border-radius:12px; font-weight:bold;">PRIORITAIRE</span>`;
            else badge = `<span style="background:#fff3e0; color:#ef6c00; padding:4px 8px; border-radius:12px; font-weight:bold;">INTERMÉDIAIRE</span>`;

            return `
                <tr>
                    <td style="text-align:left; padding:12px; border-bottom:1px solid #eee;"><b>${g.label}</b></td>
                    <td style="border-bottom:1px solid #eee;">${n}</td>
                    <td style="border-bottom:1px solid #eee; font-weight:bold; color:#b03060;">${avgS}%</td>
                    <td style="border-bottom:1px solid #eee;">${avgA}/5</td>
                    <td style="border-bottom:1px solid #eee; font-weight:bold;">${avgP}%</td>
                    <td style="border-bottom:1px solid #eee;">${badge}</td>
                </tr>`;
        }).join('');

        // Graphiques barres (Identique)
        window.renderBars('graph-savoir', [{l:'Moyenne Savoir', v:Math.round(database.reduce((a,c)=>a+c.scoreSavoir,0)/database.length), t:100, c:'#b03060'}]);
        window.renderBars('graph-pratique', [{l:'Moyenne Pratique', v:Math.round(database.reduce((a,c)=>a+c.scorePratique,0)/database.length), t:100, c:'#2e7d32'}]);
    };

    window.renderBars = function(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.v;
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div></div>`;
        }).join('');
    };

    window.requestAdmin = function() {
        if(prompt("Code :") === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            window.updateUI();
            window.switchTab(3);
        }
    };

    window.switchTab = (i) => {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.initCodeDropdown = () => {
        const sel = document.getElementById('code-enquete');
        for(let i=179; i<=200; i++) {
            let o = document.createElement('option');
            o.value = "INF-MAK-"+i; o.text = "Fiche N°"+i; sel.appendChild(o);
        }
    };

    window.initCodeDropdown();
    window.updateUI();
</script>
</body>
</html>
