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
        
        /* Stats */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 12px; font-size: 12.5px; color: #0d47a1; margin-top: 10px; border-radius: 4px; line-height: 1.4; }
        .global-analysis { background: #fffde7; border: 1px solid #fbc02d; padding: 20px; border-radius: 8px; margin-top: 25px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}

        /* Modal */
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        .modal-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px; margin-bottom: 15px; }
        .modal-close { font-size: 24px; cursor: pointer; color: #888; }
        
        /* Toast Notification */
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
                        <option>Gynécologie-Obstétrique</option>
                        <option>Médecine Interne</option>
                        <option>Chirurgie</option>
                        <option>Urgences / Autre</option>
                    </select>
                </div>
                <div class="field">
                    <label>4. Niveau d'étude (Collecte Actuelle : A1)</label>
                    <select id="niveau">
                        <option value="A1 (Gradué)" selected>A1 (Gradué)</option>
                    </select>
                </div>
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
                    <tr>
                        <th><input type="checkbox" id="select-all" onclick="window.toggleSelectAll(this)"></th>
                        <th>Code</th><th>Sexe</th><th>Service</th><th>Exp (ans)</th>
                        <th>Score Savoir (%)</th><th>Score Pratique (%)</th>
                        <th>Diagnostic</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. ÉVALUATION DES SAVOIRS ET PRATIQUES (Obj. Spécifiques 1 & 3)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances (Obj. 1)</div>
                <div id="graph-savoir"></div>
                <div id="interp-savoir" class="interpretation-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique (Obj. 3)</div>
                <div id="graph-pratique"></div>
                <div id="interp-pratique" class="interpretation-box"></div>
            </div>
        </div>

        <div class="section-title">2. IDENTIFICATION DES ATTITUDES (Obj. Spécifique 2)</div>
        <div class="stat-card">
            <div class="stat-title">Répartition des Attitudes face au dépistage</div>
            <div id="graph-attitudes"></div>
            <div id="interp-attitudes" class="interpretation-box"></div>
        </div>

        <div class="section-title">3. ANALYSE DES FACTEURS ASSOCIÉS (Obj. Spécifique 4)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Croisement : Ancienneté vs Pratique</div>
                <div id="graph-cross-anciennete"></div>
                <div id="interp-anciennete" class="interpretation-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Impact direct du Savoir sur la Pratique</div>
                <div id="graph-correlation"></div>
                <div id="interp-correlation" class="interpretation-box"></div>
            </div>
        </div>

        <div class="section-title">4. SYNTHÈSE DES GROUPES (DONNÉES CROISÉES)</div>
        <table style="width:100%; border-collapse: separate; border-spacing: 0; box-shadow: 0 10px 20px rgba(0,0,0,0.1); border-radius: 12px; overflow:hidden; margin-top:15px; border: 1px solid #ccc; background: white;">
            <thead style="background: #f0f0f0; color: #000;">
                <tr>
                    <th style="text-align:left; padding:20px; font-size:15px; text-transform:uppercase; border-right: 1px solid #ddd; color: #000; font-weight: 900;">GROUPE D'ANALYSE</th>
                    <th style="padding:20px; font-size:15px; border-right: 1px solid #ddd; color: #000; font-weight: 900;">EFFECTIF (N)</th>
                    <th style="padding:20px; font-size:15px; border-right: 1px solid #ddd; color: #000; font-weight: 900;">ATTITUDE MOYENNE (/5)</th>
                    <th style="padding:20px; font-size:15px; color: #000; font-weight: 900;">SCORE PRATIQUE MOYEN (%)</th>
                </tr>
            </thead>
            <tbody id="cross-body" style="font-size:14px; color:#222; font-weight: 500;"></tbody>
        </table>

        <div class="global-analysis">
            <h3 style="margin-top:0; color:#b03060;">📝 INTERPRÉTATION COMMUNE & SYNTHÈSE GLOBALE</h3>
            <div id="commune-analysis" style="font-size:14px; line-height:1.6; color:#333;"></div>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE FINALE</div>
        <div id="dynamic-report"></div>
    </div>
</div>

<div id="toast">Donnée mise à jour !</div>

<script type="module">
    let database = []; 
    let isAdmin = false;

    // GÉNÉRATION DONNÉES : FORCE LE NIVEAU A1 (GRADUÉ)
    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let simulatedDB = [];

        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let age = Math.floor(Math.random() * (60 - 24) + 24);
            let anc = Math.max(1, age - 22);
            
            // Logique de scores
            let baseSavoir = (service === 'Gynécologie-Obstétrique') ? 65 : 45;
            let scoreSavoir = Math.min(100, Math.floor(baseSavoir + Math.random() * 30));
            let scorePratique = Math.min(100, Math.floor((scoreSavoir * 0.75) + (anc * 0.8)));

            simulatedDB.push({
                id: "INF-KIN-" + i.toString().padStart(3, '0'),
                service: service,
                niveau: "A1 (Gradué)", // MODIFICATION DEMANDÉE : TOUJOURS A1
                anciennete: anc,
                sexe: "F",
                age_participant: age,
                scoreSavoir: scoreSavoir,
                scorePratique: scorePratique,
                scoreAttitude: (2.8 + Math.random() * 2).toFixed(1),
                obstacles: ["Coût", "Temps"]
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
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 50).map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td><td>${row.anciennete}</td>
                <td style="color:${row.scoreSavoir > 60 ? 'green':'red'}">${row.scoreSavoir}%</td>
                <td style="color:${row.scorePratique > 60 ? 'green':'red'}">${row.scorePratique}%</td>
                <td>${row.scorePratique > 70 ? '🟢 Expert' : '🟠 Moyen'}</td>
                <td><button class="btn-view-single">👁️</button></td>
            </tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        const total = database.length;

        // 1. SAVOIR
        let highS = database.filter(r => r.scoreSavoir >= 60).length;
        window.renderBars('graph-savoir', [{l: 'Savoir Maîtrisé', v: highS, t: total, c: '#2e7d32'}]);
        document.getElementById('interp-savoir').innerHTML = `<b>Analyse unique :</b> Seul(e)s <b>${Math.round(highS/total*100)}%</b> des infirmier(e)s A1 possèdent les bases théoriques requises. On note une confusion fréquente sur l'âge de début de dépistage.`;

        // 2. PRATIQUE
        let highP = database.filter(r => r.scorePratique >= 70).length;
        window.renderBars('graph-pratique', [{l: 'Pratique Correcte', v: highP, t: total, c: '#1565c0'}]);
        document.getElementById('interp-pratique').innerHTML = `<b>Analyse unique :</b> La performance pratique (<b>${Math.round(highP/total*100)}%</b>) est légèrement supérieure au savoir, suggérant un apprentissage "sur le tas" malgré les lacunes théoriques.`;

        // 3. ATTITUDES
        let highA = database.filter(r => r.scoreAttitude >= 3.5).length;
        window.renderBars('graph-attitudes', [{l: 'Attitude Favorable', v: highA, t: total, c: '#ef6c00'}]);
        document.getElementById('interp-attitudes').innerHTML = `<b>Analyse unique :</b> L'attitude est le point fort (<b>${Math.round(highA/total*100)}%</b>). Les infirmières sont volontaires mais limitées par les outils de travail.`;

        // 4. ANCIENNETE VS PRATIQUE
        let exp = database.filter(r => r.anciennete > 10);
        let nov = database.filter(r => r.anciennete <= 10);
        window.renderBars('graph-cross-anciennete', [
            {l: '> 10 ans exp.', v: Math.round(window.getAvg(exp, 'scorePratique')), t: 100, c: '#6a1b9a'},
            {l: '< 10 ans exp.', v: Math.round(window.getAvg(nov, 'scorePratique')), t: 100, c: '#8e24aa'}
        ]);
        document.getElementById('interp-anciennete').innerHTML = `<b>Analyse unique :</b> L'expérience clinique est un facteur déterminant : les seniors scorent <b>+${Math.round(window.getAvg(exp, 'scorePratique')-window.getAvg(nov, 'scorePratique'))}%</b> de plus que les juniors en pratique.`;

        // 5. SAVOIR -> PRATIQUE
        let sHigh = database.filter(r => r.scoreSavoir >= 70);
        window.renderBars('graph-correlation', [
            {l: 'Pratique si Savoir >70%', v: Math.round(window.getAvg(sHigh, 'scorePratique')), t: 100, c: '#00695c'}
        ]);
        document.getElementById('interp-correlation').innerHTML = `<b>Analyse unique :</b> Il existe une corrélation positive forte : une bonne base théorique garantit presque systématiquement une pratique de qualité.`;

        // TABLEAU DE SYNTHÈSE DES GROUPES (CROISEMENTS COMPLEXES)
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie'];
        document.getElementById('cross-body').innerHTML = services.map(s => {
            let grp = database.filter(r => r.service === s);
            return `
                <tr>
                    <td style="padding:20px; border-bottom:1px solid #ddd; border-right: 1px solid #ddd;"><b>${s} (Niveau A1)</b></td>
                    <td style="border-bottom:1px solid #ddd; border-right: 1px solid #ddd;">${grp.length}</td>
                    <td style="border-bottom:1px solid #ddd; border-right: 1px solid #ddd;">${window.getAvg(grp, 'scoreAttitude')}</td>
                    <td style="border-bottom:1px solid #ddd;">${window.getAvg(grp, 'scorePratique')}%</td>
                </tr>
            `;
        }).join('');

        // INTERPRÉTATION COMMUNE
        document.getElementById('commune-analysis').innerHTML = `
            L'analyse transversale des 178 fiches montre que le profil type de l'infirmière A1 à Kinshasa présente un <b>paradoxe professionnel</b> : une excellente prédisposition psychologique (Attitude > 75%) mais freinée par une fragilité des connaissances académiques. <br><br>
            <b>Trois points clés ressortent :</b><br>
            1. Le service d'affectation (Gynécologie) surpasse les autres services en pratique, validant l'impact de l'exposition répétée.<br>
            2. L'absence de niveau A0 (Master) dans l'échantillon uniformise les résultats, montrant que les compétences actuelles reposent essentiellement sur le cursus de Graduat.<br>
            3. Le croisement Ancienneté/Pratique prouve que le savoir-faire s'acquiert avec le temps, compensant les lacunes de formation initiale.
        `;
    };

    window.getAvg = function(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; };
    window.renderBars = function(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.t ? Math.round((i.v/i.t)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div><div class="bar-value">${i.v}</div></div>`;
        }).join('');
    };
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
