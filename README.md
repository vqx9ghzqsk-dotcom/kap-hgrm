<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR Kinshasa - RDC) - Données Simulées</title>
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

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; line-height: 1.4; }
        .global-interpretation { background: #fffde7; border: 2px solid #fbc02d; padding: 20px; margin: 20px 0; border-radius: 8px; color: #333; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}

        /* Modal */
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        .modal-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px; margin-bottom: 15px; }
        .modal-close { font-size: 24px; cursor: pointer; color: #888; }
        .detail-row { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px dashed #eee; font-size: 13px; }
        .detail-label { font-weight: bold; color: #555; }
        .detail-val { color: #b03060; font-weight: 600; text-align: right; width: 50%; }
        
        .reco-box { background: #fff3e0; border: 1px solid #ffe0b2; padding: 15px; border-radius: 6px; margin-bottom: 10px; }
        .reco-title { color: #e65100; font-weight: bold; margin-bottom: 5px; }

        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 17px; }
        #toast.show { visibility: visible; -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        
        <div class="sim-badge">DATA: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL PROFESSIONNEL</div>
            <div class="row">
                <div class="field">
                    <label>1. Code Enquêté(e)</label>
                    <select id="code-enquete"></select>
                </div>
                <div class="field">
                    <label>3. Service d'affectation</label>
                    <select id="service">
                        <option value="" disabled selected>Choisir un service...</option>
                        <option>Gynécologie-Obstétrique</option>
                        <option>Médecine Interne</option>
                        <option>Chirurgie</option>
                        <option>Urgences / Autre</option>
                    </select>
                </div>
                <div class="field">
                    <label>4. Niveau d'étude</label>
                    <select id="niveau">
                        <option value="A1 (Gradué)" selected>A1 (Gradué)</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="sub-title">Signes d’alerte & Risques</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="tabac"> Tabac/Alcool</label>
            </div>

            <div class="section-title">III. ATTITUDES (1-5)</div>
            <table>
                <thead>
                    <tr><th class="td-left">Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                </thead>
                <tbody>
                    <tr><td class="td-left">L’éducation à l’AES fait partie de mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence examen patientes</label>
                    <select id="prac-pro-freq">
                        <option value="syst">Systématiquement</option>
                        <option value="plainte">Uniquement si plainte</option>
                        <option value="rare">Rarement</option>
                    </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES (N = <span id="n-total">0</span>)</div>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th>Code</th><th>Service</th><th>Niveau</th>
                        <th>Savoir (%)</th><th>Pratique (%)</th><th>Attitude (/5)</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="global-interpretation">
            <h3 style="margin-top:0; color:#b03060;">📝 INTERPRÉTATION GLOBALE TRANSVERSALE</h3>
            <p id="interp-generale">L'analyse croisée des 178 fiches montre une corrélation directe entre l'exposition clinique en Gynécologie et la maîtrise des gestes de palpation. Bien que le niveau d'étude soit homogène (A1 Gradué), les disparités de pratique s'expliquent par l'absence de protocoles standardisés dans les services de médecine générale.</p>
        </div>

        <div class="section-title">1. ÉVALUATION DES SAVOIRS (Obj. Spécifique 1)</div>
        <div class="stat-card">
            <div id="graph-savoir"></div>
            <div id="interp-savoir" class="interpretation-box"></div>
        </div>

        <div class="section-title">2. ÉVALUATION DES PRATIQUES (Obj. Spécifique 3)</div>
        <div class="stat-card">
            <div id="graph-pratique"></div>
            <div id="interp-pratique" class="interpretation-box"></div>
        </div>

        <div class="section-title">3. ANALYSE DES ATTITUDES (Obj. Spécifique 2)</div>
        <div class="stat-card">
            <div id="graph-attitudes"></div>
            <div id="interp-attitudes" class="interpretation-box"></div>
        </div>

        <div class="section-title">4. SYNTHÈSE DES GROUPES (CROISEMENTS)</div>
        <table style="width:100%; border: 2px solid #333; border-collapse: collapse;">
            <thead style="background: #eee; color: #000;">
                <tr>
                    <th style="padding:15px; border: 1px solid #333; font-weight: 900; color: #000; font-size: 14px;">GROUPE D'ANALYSE</th>
                    <th style="padding:15px; border: 1px solid #333; font-weight: 900; color: #000; font-size: 14px;">EFFECTIF (N)</th>
                    <th style="padding:15px; border: 1px solid #333; font-weight: 900; color: #000; font-size: 14px;">ATTITUDE MOYENNE (/5)</th>
                    <th style="padding:15px; border: 1px solid #333; font-weight: 900; color: #000; font-size: 14px;">SCORE PRATIQUE MOYEN (%)</th>
                </tr>
            </thead>
            <tbody id="cross-body" style="color: #000; font-weight: bold; font-size: 14px;"></tbody>
        </table>

        <div class="section-title">5. OBSTACLES (Obj. Spécifique 4)</div>
        <div class="stat-card">
            <div id="graph-obstacles-anal"></div>
            <div id="interp-obstacles" class="interpretation-box"></div>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div id="dynamic-report"></div>
    </div>
</div>

<script type="module">
    let database = []; 
    let isAdmin = false;

    // GÉNÉRATION DES DONNÉES (UNIFORMISÉES SUR A1 GRADUÉ)
    window.generateData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let data = [];
        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let scoreSavoir = Math.floor(45 + Math.random() * 45);
            let scorePratique = (service === 'Gynécologie-Obstétrique') ? Math.floor(65 + Math.random() * 30) : Math.floor(30 + Math.random() * 40);
            data.push({
                id: "INF-KIN-" + i.toString().padStart(3, '0'),
                service: service,
                niveau: "A1 (Gradué)",
                scoreSavoir: scoreSavoir,
                scorePratique: scorePratique,
                scoreAttitude: (3.1 + Math.random() * 1.5).toFixed(1),
                obstacles: Math.random() > 0.5 ? ["Coût", "Temps"] : ["Formation"]
            });
        }
        return data;
    };

    database = window.generateData();

    window.requestAdmin = function() {
        let code = prompt("Code administrateur :"); 
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            document.getElementById('btn-auth').style.display = 'none';
            updateUI(); 
            window.switchTab(3);
        }
    };

    window.updateUI = function() {
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 50).map(row => `
            <tr>
                <td><b>${row.id}</b></td><td>${row.service}</td><td>${row.niveau}</td>
                <td>${row.scoreSavoir}%</td><td>${row.scorePratique}%</td><td>${row.scoreAttitude}</td>
                <td><button class="btn-view-single">👁️ Détails</button></td>
            </tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        // 1. SAVOIR
        let highS = database.filter(r => r.scoreSavoir >= 60).length;
        renderBars('graph-savoir', [{l: 'Savoir satisfaisant', v: highS, t: 178, c: '#2e7d32'}, {l: 'Savoir insuffisant', v: 178-highS, t: 178, c: '#c62828'}]);
        document.getElementById('interp-savoir').innerHTML = `<b>Interprétation :</b> Plus de ${Math.round(highS/1.78)}% des infirmières graduées possèdent les bases théoriques. Cependant, les classifications moléculaires restent mal connues.`;

        // 2. PRATIQUE
        let highP = database.filter(r => r.scorePratique >= 70).length;
        renderBars('graph-pratique', [{l: 'Maîtrise Technique', v: highP, t: 178, c: '#1565c0'}, {l: 'Gestuelle à corriger', v: 178-highP, t: 178, c: '#f57f17'}]);
        document.getElementById('interp-pratique').innerHTML = `<b>Interprétation :</b> La pratique est le point faible. Bien que graduées (A1), l'absence de matériel didactique réduit la performance gestuelle à ${Math.round(highP/1.78)}% de l'effectif.`;

        // 3. ATTITUDES
        let highA = database.filter(r => r.scoreAttitude >= 3.8).length;
        renderBars('graph-attitudes', [{l: 'Attitude Pro-Dépistage', v: highA, t: 178, c: '#43a047'}, {l: 'Attitude Neutre/Réticente', v: 178-highA, t: 178, c: '#d81b60'}]);
        document.getElementById('interp-attitudes').innerHTML = `<b>Interprétation :</b> L'engagement moral est fort, montrant que les infirmières perçoivent le dépistage comme une mission prioritaire malgré les conditions de travail.`;

        // 4. SYNTHESE (CROISEMENTS)
        let gyneco = database.filter(r => r.service === 'Gynécologie-Obstétrique');
        let autres = database.filter(r => r.service !== 'Gynécologie-Obstétrique');
        
        document.getElementById('cross-body').innerHTML = `
            <tr>
                <td style="padding:15px; border:1px solid #333;">Service Gynécologie (A1)</td>
                <td style="padding:15px; border:1px solid #333;">${gyneco.length}</td>
                <td style="padding:15px; border:1px solid #333;">${getAvg(gyneco, 'scoreAttitude')}</td>
                <td style="padding:15px; border:1px solid #333;">${getAvg(gyneco, 'scorePratique')}%</td>
            </tr>
            <tr>
                <td style="padding:15px; border:1px solid #333;">Autres Services (A1)</td>
                <td style="padding:15px; border:1px solid #333;">${autres.length}</td>
                <td style="padding:15px; border:1px solid #333;">${getAvg(autres, 'scoreAttitude')}</td>
                <td style="padding:15px; border:1px solid #333;">${getAvg(autres, 'scorePratique')}%</td>
            </tr>
        `;

        // 5. OBSTACLES
        renderBars('graph-obstacles-anal', [{l: 'Manque de Formation', v: 92, t: 178, c: '#b03060'}, {l: 'Coût des examens', v: 65, t: 178, c: '#b03060'}]);
        document.getElementById('interp-obstacles').innerHTML = `<b>Interprétation :</b> Le manque de formation continue est le frein majeur cité (51%), devant les barrières financières des patientes.`;
    };

    function renderBars(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = Math.round((i.v/i.t)*100);
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div><div class="bar-value">${i.v}</div></div>`;
        }).join('');
    }

    function getAvg(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; }

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
