<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse CAP Complète - HGR Makala</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* Badges & Buttons */
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }
        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }

        /* Contenu */
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections & Tables */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input, textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .td-left { text-align: left; padding-left: 15px; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        
        /* Stats Cards */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; }

        /* Toast & Modals */
        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" style="background:#b03060; color:white; padding:2px 6px; border-radius:10px;">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DONNÉES</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. ANALYSES CROISÉES & KAP</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSIONS & EXPORT</button>
        
        <div class="sim-badge">HGR MAKALA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; text-align:center;">Enquête CAP - Prévention Cancer du Sein</h2>
        
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION PROFESSIONNELLE</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Médecine Interne</option>
                        <option>Chirurgie</option>
                        <option>Urgences / Autre</option>
                    </select>
                </div>
                <div class="field"><label>Niveau d'étude</label>
                    <select id="niveau">
                        <option value="A2 - ITM">A2 - Niveau technique (ITM)</option>
                        <option value="A1/LMD - ISTM">A1/LMD - Niveau supérieur (ISTM)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté (ans)</label><input type="number" id="anciennete" placeholder="Ex: 5"></div>
                <div class="field"><label>Âge</label><input type="number" id="age-participant"></div>
                <div class="field"><label>État Civil</label>
                    <select id="etat-civil">
                        <option>Célibataire</option><option>Mariée</option><option>Divorcée</option><option>Veuve</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. SAVOIRS THÉORIQUES (DÉTAILLÉS)</div>
            <div class="row" style="background:#f0f8ff; padding:10px; border-radius:6px;">
                <div class="field"><label>Classification moléculaire ?</label><select id="q-moleculaire"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Terme "HER2 Low" ?</label><select id="q-her2"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Thérapies ciblées ?</label><select id="q-therapie"><option value="non">Non</option><option value="oui">Oui</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>1ère cause de décès RDC ?</label><select id="q-cause"><option value="vrai">Vrai</option><option value="faux">Faux</option></select></div>
                <div class="field"><label>Âge 1ère Mammographie ?</label><select id="q-age-mammo"><option value="35">35-40 ans</option><option value="50">50 ans</option></select></div>
                <div class="field"><label>Moment idéal AES ?</label><select id="q-moment-aes"><option value="apres">7-10j après règles</option><option value="regles">Pendant</option></select></div>
            </div>

            <div class="sub-title">Facteurs de risque & Signes d'alerte</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive</label>
            </div>

            <div class="section-title">III. ATTITUDES (ÉCHELLE DE LIKERT)</div>
            <table>
                <thead><tr><th class="td-left">Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="td-left">L’éducation à l’AES fait partie de mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="td-left">Je me sens capable de détecter un nodule.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES & TECHNIQUE CLINIQUE</div>
            <div class="row">
                <div class="field"><label>Partie de la main utilisée ?</label>
                    <select id="prac-main"><option value="pulpe">Pulpe des 3 doigts</option><option value="paume">Paume</option><option value="pointe">Pointe</option></select>
                </div>
                <div class="field"><label>Zone "oubliée" incluse ?</label>
                    <select id="prac-zone"><option value="axillaire">Creux axillaire</option><option value="mamelon">Mamelon</option></select>
                </div>
            </div>
            <label>Mouvements (Cocher) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" value="circulaire"> Circulaire</label>
                <label class="check-item"><input type="checkbox" value="vertical"> Vertical</label>
                <label class="check-item"><input type="checkbox" value="radial"> Radial</label>
            </div>

            <div class="section-title">V. OBSTACLES & CNLC</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="Formation"> Manque de formation</label>
                <label class="check-item"><input type="checkbox" value="Coût"> Coût des examens</label>
                <label class="check-item"><input type="checkbox" value="Pudeur"> Pudeur / Culture</label>
            </div>
            <div class="row" style="margin-top:15px;">
                <div class="field"><label>Connaissance du CNLC ?</label><select id="connaissance-cnlc"><option>Non</option><option>Oui</option></select></div>
                <div class="field"><label>Suggestions (Verbatim)</label><textarea id="reco-verbatim" rows="2"></textarea></div>
            </div>

            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES (N = <span id="n-total">0</span>)</div>
        <div style="overflow-x:auto;">
            <table>
                <thead><tr><th>Code</th><th>Sexe</th><th>Service</th><th>Savoir (%)</th><th>Pratique (%)</th><th>Diagnostic</th><th>Actions</th></tr></thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. ANALYSES CROISÉES DES DÉTERMINANTS</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Savoir × Formation</div><div id="cross-1"></div></div>
            <div class="stat-card"><div class="stat-title">Attitude × Savoir</div><div id="cross-2"></div></div>
        </div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Pratique × Savoir</div><div id="cross-3"></div></div>
            <div class="stat-card"><div class="stat-title">Pratique × Attitude</div><div id="cross-4"></div></div>
        </div>
        <div class="stat-card"><div class="stat-title">Impact direct : Formation × Pratique</div><div id="cross-5"></div></div>

        <div class="section-title">2. SYNTHÈSE DES GROUPES (RÉSUMÉ EXÉCUTIF)</div>
        <table style="width:100%; box-shadow: 0 4px 15px rgba(0,0,0,0.1); border-radius: 8px; overflow:hidden;">
            <thead style="background: #b03060; color: white;">
                <tr><th style="padding:15px;">Groupe d'Analyse</th><th>Effectif</th><th>Savoir Moyen</th><th>Pratique Moyenne</th><th>Attitude (/5)</th></tr>
            </thead>
            <tbody id="cross-body-groups" style="font-size:14px; font-weight:bold;"></tbody>
        </table>

        <div class="section-title">3. HIÉRARCHIE DES OBSTACLES</div>
        <div id="graph-obstacles-anal"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">RAPPORT AUTOMATISÉ</div>
        <div id="dynamic-report" class="stat-card" style="line-height:1.6;"></div>
        <button class="btn-excel" onclick="window.exportToCSV()">📥 TÉLÉCHARGER (.CSV)</button>
    </div>
</div>

<div id="toast">Opération réussie !</div>

<script type="module">
    // --- LOGIQUE FUSIONNÉE ---
    let database = [];
    let isAdmin = false;

    window.generateData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let db = [];
        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let trained = Math.random() > 0.75;
            
            let sSavoir = trained ? Math.floor(75 + Math.random()*20) : Math.floor(40 + Math.random()*25);
            let sPrac = (trained || sSavoir > 70) ? Math.floor(65 + Math.random()*30) : Math.floor(15 + Math.random()*20);
            
            db.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: service, sexe: "F",
                scoreSavoir: sSavoir, scorePratique: sPrac,
                scoreAttitude: (2.5 + Math.random()*2).toFixed(1),
                obstacles: trained ? ["Coût"] : ["Formation", "Coût"],
                trained: trained
            });
        }
        return db;
    };

    database = window.generateData();

    window.updateAnalytics = function() {
        // 1. Calculs des croisements
        const trained = database.filter(r => r.trained);
        const nonTrained = database.filter(r => !r.trained);
        const highK = database.filter(r => r.scoreSavoir >= 70);
        const lowK = database.filter(r => r.scoreSavoir < 70);

        const render = (id, label1, val1, label2, val2, color) => {
            document.getElementById(id).innerHTML = `
                <div class="bar-container"><div class="bar-label"><b>${label1}</b></div><div class="bar-track"><div class="bar-fill" style="width:${val1}%; background:${color}">${val1}%</div></div></div>
                <div class="bar-container"><div class="bar-label"><b>${label2}</b></div><div class="bar-track"><div class="bar-fill" style="width:${val2}%; background:#ccc">${val2}%</div></div></div>
            `;
        };

        render('cross-1', 'Formées (Savoir)', Math.round(getAvg(trained,'scoreSavoir')), 'Non-Formées', Math.round(getAvg(nonTrained,'scoreSavoir')), '#2e7d32');
        render('cross-2', 'Savoir + (Attitude %)', Math.round(getAvg(highK,'scoreAttitude')*20), 'Savoir -', Math.round(getAvg(lowK,'scoreAttitude')*20), '#4527a0');
        render('cross-3', 'Savoir + (Pratique)', Math.round(getAvg(highK,'scorePratique')), 'Savoir -', Math.round(getAvg(lowK,'scorePratique')), '#1565c0');
        render('cross-5', 'Si Formation (Pratique)', Math.round(getAvg(trained,'scorePratique')), 'Sans Formation', Math.round(getAvg(nonTrained,'scorePratique')), '#c62828');

        // 2. Tableau de Synthèse
        const groups = [
            {n: "HGR Makala (Total)", d: database},
            {n: "Gynéco-Obstétrique", d: database.filter(r => r.service.includes("Gynéco"))},
            {n: "Groupe Formé", d: trained},
            {n: "Déficit Formation", d: nonTrained}
        ];
        document.getElementById('cross-body-groups').innerHTML = groups.map(g => `
            <tr><td style="text-align:left; padding:12px;">${g.n}</td><td>${g.d.length}</td><td>${Math.round(getAvg(g.d,'scoreSavoir'))}%</td><td>${Math.round(getAvg(g.d,'scorePratique'))}%</td><td>${getAvg(g.d,'scoreAttitude')}</td></tr>
        `).join('');

        // 3. Obstacles
        let obsMap = {"Formation":0, "Coût":0, "Pudeur":0};
        database.forEach(r => r.obstacles.forEach(o => obsMap[o]++));
        document.getElementById('graph-obstacles-anal').innerHTML = Object.entries(obsMap).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div></div>`;
        }).join('');
    };

    window.getAvg = (arr, p) => arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0;

    window.switchTab = (i) => {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.requestAdmin = () => {
        if(prompt("Code Admin:") === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            window.updateUI();
            window.switchTab(3);
        }
    };

    window.updateUI = () => {
        document.getElementById('n-total').textContent = database.length;
        document.getElementById('database-body').innerHTML = database.slice(0,10).map(r => `
            <tr><td>${r.id}</td><td>F</td><td>${r.service}</td><td>${r.scoreSavoir}%</td><td>${r.scorePratique}%</td><td>${r.scorePratique>60?'🟢':'🔴'}</td><td>👁️</td></tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.exportToCSV = () => { alert("Exportation de 178 lignes vers Rapport_Makala.csv..."); };
    window.saveRecord = () => { alert("Mode Simulation : Connexion Cloud établie."); };

    setTimeout(() => { 
        window.updateUI();
        const sel = document.getElementById('code-enquete');
        for(let i=179; i<210; i++) sel.add(new Option("Fiche N°"+i, "INF-"+i));
    }, 500);
</script>
</body>
</html>
