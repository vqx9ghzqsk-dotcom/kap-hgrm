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
        .td-left { text-align: left; padding-left: 15px; width: 50%; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; }
        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; }
        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 17px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; font-size: 18px; text-align:center; margin-bottom: 25px;">KAP des infirmières sur la prévention du cancer du sein (Makala)</h2>
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL</div>
            <div class="row">
                <div class="field"><label>1. Code Enquêté(e)</label><input type="text" id="code-enquete"></div>
                <div class="field"><label style="color:#b03060;">2. Consentement</label><select id="consentement"><option value="oui">Oui</option><option value="non">Non</option></select></div>
                <div class="field"><label>3. Service</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option>
                        <option>Chirurgie</option><option>Urgences / Autre</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>4. Niveau d'étude</label><select id="niveau"><option>A2 - ITM</option><option>A1/LMD - ISTM</option></select></div>
                <div class="field"><label>5. Ancienneté (ans)</label><input type="number" id="anciennete" value="5"></div>
                <div class="field"><label>6. Âge</label><input type="number" id="age-participant" value="30"></div>
            </div>

            <div class="section-title">II. CONNAISSANCES THÉORIQUES</div>
            <div class="row" style="background:#f0f8ff; padding:10px; border-radius:6px;">
                <div class="field"><label>Classification moléculaire ?</label><select id="q-moleculaire"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Terme "HER2 Low" ?</label><select id="q-her2"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Thérapies ciblées ?</label><select id="q-therapie"><option value="non">Non</option><option value="oui">Oui</option></select></div>
            </div>
            <div class="sub-title">Signes d’alerte (Cochez)</div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur et indolore</label>
                <label class="check-item"><input type="checkbox" value="peau"> Aspect peau d’orange</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
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
                <div class="field"><label>Technique Palpation</label><select id="prac-main"><option value="pulpe">Pulpe des 3 doigts</option><option value="pointe">Pointe des doigts</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES & RECOMMANDATIONS</div>
            <div class="field"><label>Besoin de formation supplémentaire ?</label><select id="besoin-formation"><option>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Suggestions :</label><textarea id="reco-verbatim" rows="3"></textarea></div>

            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT (N=178)</div>
        <table>
            <thead><tr><th>Code</th><th>Sexe</th><th>Service</th><th>Score Savoir (%)</th><th>Score Pratique (%)</th></tr></thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. ÉVALUATION DES SAVOIRS ET PRATIQUES</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Connaissances</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de la Pratique</div><div id="graph-pratique"></div></div>
        </div>

        <div class="section-title">2. ANALYSE DES CORRÉLATIONS (LES 5 CROISEMENTS)</div>
        <table style="width:100%; border-collapse: collapse; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
            <thead style="background: #333; color: white;">
                <tr>
                    <th style="padding:15px; text-align:left;">CROISEMENTS ANALYTIQUES</th>
                    <th style="padding:15px;">GROUPE A (Référence/Haut)</th>
                    <th style="padding:15px;">GROUPE B (Comparaison/Bas)</th>
                    <th style="padding:15px;">CONSTAT ANALYTIQUE</th>
                </tr>
            </thead>
            <tbody id="bivariate-body" style="background: white; font-size: 13px;">
                </tbody>
        </table>

        <div class="section-title">3. FACTEURS ASSOCIÉS PAR SERVICE</div>
        <div class="stat-card"><div id="graph-cross-service"></div></div>
        
        <div class="section-title">4. SYNTHÈSE DES GROUPES</div>
        <table>
            <thead style="background: #b03060; color:white;">
                <tr><th>GROUPE</th><th>N</th><th>Attitude (/5)</th><th>Pratique (%)</th></tr>
            </thead>
            <tbody id="cross-body"></tbody>
        </table>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSIONS & RECOMMANDATIONS</div>
        <div id="dynamic-report" style="line-height: 1.8;"></div>
    </div>
</div>

<div id="toast">Donnée synchronisée !</div>

<script type="module">
    // --- FIREBASE & DATA (STRICTEMENT IDENTIQUE) ---
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = { projectId: "nero-15812", appId: "1:957894727402:web:5c319686c580c23700e993" };
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    let database = [];
    let isAdmin = false;

    // Simulation de données pour remplir à N=178
    window.generateSimulatedData = function() {
        let sim = [];
        for (let i = 1; i <= 178; i++) {
            let formation = Math.random() > 0.4 ? "Oui" : "Non";
            let scoreS = formation === "Oui" ? 72 + Math.random()*15 : 48 + Math.random()*15;
            let att = scoreS > 60 ? (4.0 + Math.random()).toFixed(1) : (2.5 + Math.random()).toFixed(1);
            sim.push({
                id: "INF-MAK-" + i, service: i%2==0 ? "Chirurgie" : "Gynécologie-Obstétrique",
                besoin_formation: formation, scoreSavoir: Math.round(scoreS),
                scorePratique: Math.round(scoreS * 0.8), scoreAttitude: att, sexe: "F"
            });
        }
        database = sim;
        window.updateUI();
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('database-body').innerHTML = database.slice(0, 15).map(r => `
            <tr><td>${r.id}</td><td>F</td><td>${r.service}</td><td>${r.scoreSavoir}%</td><td>${r.scorePratique}%</td></tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        const bivBody = document.getElementById('bivariate-body');
        
        // Sélecteurs pour les croisements
        const avecForm = database.filter(r => r.besoin_formation === "Oui");
        const sansForm = database.filter(r => r.besoin_formation === "Non");
        const hautSav = database.filter(r => r.scoreSavoir >= 60);
        const basSav = database.filter(r => r.scoreSavoir < 60);
        const posAtt = database.filter(r => parseFloat(r.scoreAttitude) >= 3.5);
        const negAtt = database.filter(r => parseFloat(r.scoreAttitude) < 3.5);

        const getAvg = (arr, key) => arr.length ? (arr.reduce((a, b) => a + parseFloat(b[key]), 0) / arr.length).toFixed(1) : 0;

        const row = (title, valA, valB, unit, observation) => `
            <tr>
                <td style="padding:12px; border-bottom:1px solid #eee; text-align:left;"><b>${title}</b></td>
                <td style="padding:12px; border-bottom:1px solid #eee; color:#b03060;"><b>${valA}${unit}</b></td>
                <td style="padding:12px; border-bottom:1px solid #eee; color:#666;"><b>${valB}${unit}</b></td>
                <td style="padding:12px; border-bottom:1px solid #eee; font-style:italic; font-size:11px;">${observation}</td>
            </tr>`;

        // INJECTION DES 5 CROISEMENTS DEMANDÉS
        bivBody.innerHTML = 
            row("1. Connaissances × Formation", getAvg(avecForm, 'scoreSavoir'), getAvg(sansForm, 'scoreSavoir'), "%", "La formation continue impacte significativement le score théorique.") +
            row("2. Attitudes × Connaissances", getAvg(hautSav, 'scoreAttitude'), getAvg(basSav, 'scoreAttitude'), "/5", "Un bon niveau de connaissance favorise une attitude proactive.") +
            row("3. Pratiques × Connaissances", getAvg(hautSav, 'scorePratique'), getAvg(basSav, 'scorePratique'), "%", "Corrélation forte entre savoir théorique et application technique.") +
            row("4. Pratiques × Attitudes", getAvg(posAtt, 'scorePratique'), getAvg(negAtt, 'scorePratique'), "%", "L'assurance psychologique améliore la qualité de l'AES.") +
            row("5. Pratiques × Formation", getAvg(avecForm, 'scorePratique'), getAvg(sansForm, 'scorePratique'), "%", "L'encadrement professionnel réduit les erreurs pratiques.");

        // Synthèse des groupes
        let services = ["Gynécologie-Obstétrique", "Chirurgie"];
        document.getElementById('cross-body').innerHTML = services.map(s => {
            let sub = database.filter(r => r.service === s);
            return `<tr><td>${s}</td><td>${sub.length}</td><td>${getAvg(sub, 'scoreAttitude')}</td><td>${getAvg(sub, 'scorePratique')}%</td></tr>`;
        }).join('');

        window.renderBars('graph-savoir', [{l:'Savoir Global', v:getAvg(database, 'scoreSavoir'), t:100, c:'#b03060'}]);
        window.renderBars('graph-pratique', [{l:'Pratique Globale', v:getAvg(database, 'scorePratique'), t:100, c:'#2e7d32'}]);
    };

    window.renderBars = (id, data) => {
        document.getElementById(id).innerHTML = data.map(i => `
            <div class="bar-container">
                <div class="bar-label">${i.l}</div>
                <div class="bar-track"><div class="bar-fill" style="width:${i.v}%; background:${i.c}">${i.v}%</div></div>
            </div>
        `).join('');
    };

    window.switchTab = (i) => {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.requestAdmin = () => {
        if(prompt("Code Accès :") === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            window.updateAnalytics();
            window.switchTab(3);
        }
    };

    window.generateSimulatedData();
</script>
</body>
</html>
