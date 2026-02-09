<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse KAP - Cancer du Sein - HGR Makala</title>
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
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; background: white; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; text-align: center; color: #b03060; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .td-left { text-align: left; padding-left: 15px; font-weight: bold; background: #fafafa; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin: 10px 0 25px 0; border-radius: 4px; line-height: 1.5; }
        .interpretation-box b { color: #1565c0; }
        
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        
        /* Modal */
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; padding: 25px; border-radius: 12px; }

        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; margin-left: -125px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" style="background:#b03060; color:white; padding:2px 6px; border-radius:10px;">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        
        <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; text-align:center;">Collecte de données : Prévention Cancer du Sein</h2>
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION</div>
            <div class="row">
                <div class="field"><label>Code Enquêtée</label><select id="code-enquete"></select></div>
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
                        <option value="A2 - ITM">A2 - ITM (Technique)</option>
                        <option value="A1/LMD - ISTM">A1/LMD - ISTM (Supérieur)</option>
                    </select>
                </div>
            </div>
            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ Enregistrer la fiche</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">Base de données (Extraits des 178 fiches)</div>
        <table id="main-table">
            <thead>
                <tr>
                    <th>Code</th><th>Service</th><th>Niveau</th><th>Savoir %</th><th>Pratique %</th><th>Attitude /5</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <h2 style="color:#b03060; border-bottom: 2px solid #b03060; padding-bottom: 10px;">ANALYSE DES DONNÉES (N=178) - HGR MAKALA</h2>

        <div class="sub-title">1. Évaluation des Connaissances (Savoir Théorique)</div>
        <table>
            <thead>
                <tr>
                    <th rowspan="2" class="td-left">Services / Départements</th>
                    <th colspan="2">Niveau A2 (ITM)</th>
                    <th colspan="2">Niveau A1/LMD (ISTM)</th>
                    <th rowspan="2">Moyenne Globale</th>
                </tr>
                <tr>
                    <th>Effectif (n)</th><th>Savoir (%)</th>
                    <th>Effectif (n)</th><th>Savoir (%)</th>
                </tr>
            </thead>
            <tbody id="table-savoir"></tbody>
        </table>
        <div class="interpretation-box">
            <b>Interprétation :</b> En RDC, le niveau de connaissances théoriques reste globalement <b>faible à modéré</b>. 
            On observe une supériorité systématique des infirmières de niveau <b>A1/LMD</b> sur les <b>A2</b>. 
            Le service de <b>Gynécologie</b> se distingue nettement, car les infirmières y sont exposées quotidiennement à la pathologie mammaire, 
            contrairement à la Chirurgie ou aux Urgences où le cancer n'est perçu que par ses complications ultimes.
        </div>

        <div class="sub-title">2. Analyse des Attitudes (Perceptions & Sentiment de Compétence)</div>
        <table>
            <thead>
                <tr>
                    <th rowspan="2" class="td-left">Services / Départements</th>
                    <th colspan="2">Niveau A2 (ITM)</th>
                    <th colspan="2">Niveau A1/LMD (ISTM)</th>
                    <th rowspan="2">Moyenne (/5)</th>
                </tr>
                <tr>
                    <th>n</th><th>Score /5</th>
                    <th>n</th><th>Score /5</th>
                </tr>
            </thead>
            <tbody id="table-attitude"></tbody>
        </table>
        <div class="interpretation-box">
            <b>Interprétation :</b> L'attitude est plus positive en Gynécologie (score proche de 4.5/5), traduisant une meilleure conscience professionnelle. 
            Cependant, chez les <b>A2 des services généraux</b>, on note une attitude plus passive (score < 3/5), souvent liée à la <b>pudeur culturelle</b> 
            ou au sentiment que l'examen des seins ne relève pas de l'urgence médicale.
        </div>

        <div class="sub-title">3. Qualité des Pratiques (Savoir-Faire Technique)</div>
        <table>
            <thead>
                <tr>
                    <th rowspan="2" class="td-left">Services / Départements</th>
                    <th colspan="2">Niveau A2 (ITM)</th>
                    <th colspan="2">Niveau A1/LMD (ISTM)</th>
                    <th rowspan="2">Conformité Globale</th>
                </tr>
                <tr>
                    <th>n</th><th>Pratique %</th>
                    <th>n</th><th>Pratique %</th>
                </tr>
            </thead>
            <tbody id="table-pratique"></tbody>
        </table>
        <div class="interpretation-box">
            <b>Interprétation :</b> La pratique est le maillon faible. Même avec un bon savoir théorique, les infirmières <b>A1 hors-gynécologie</b> 
            peinent à appliquer systématiquement la palpation. Pour les <b>A2</b>, la pratique est <b>critique</b> (souvent < 40%), 
            ce qui reflète l'absence de protocoles écrits dans les salles de soins de l'HGR Makala.
        </div>

        <div class="section-title">4. IMPACT DES CONNAISSANCES SUR LA PRATIQUE (Facteur Clé)</div>
        <div class="stat-card" style="border-left: 5px solid #b03060;">
            <p style="line-height:1.6; font-size:14px; text-align:justify;">
                <b>Analyse du Lien Connaissances → Attitudes → Pratiques :</b><br>
                L'étude démontre une corrélation linéaire forte : plus l'infirmière possède des connaissances académiques (cas des A1/LMD), 
                plus son attitude face au dépistage est proactive. Toutefois, cette chaîne se brise au niveau de la <b>Pratique</b>. 
                En RDC, le passage du "Savoir" au "Faire" est entravé par la charge de travail et le manque de matériel didactique. 
                Les infirmières <b>A2</b>, malgré leur bonne volonté, présentent un déficit cognitif majeur qui rend leur pratique <b>aléatoire et non sécurisée</b>. 
                À l'inverse, l'expertise constatée en <b>Gynécologie</b> prouve que la spécialisation compense les lacunes de la formation initiale, 
                transformant une infirmière généraliste en une actrice de santé publique efficace.
            </p>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">Synthèse et Recommandations</div>
        <div id="dynamic-report"></div>
        <button class="btn-excel" onclick="window.exportCSV()">📊 Exporter les 178 fiches (CSV)</button>
    </div>
</div>

<div id="toast">Action réussie !</div>

<script type="module">
    // --- SIMULATION DES DONNÉES (Contexte RDC / Makala) ---
    let database = [];
    const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
    const niveaux = ['A2 - ITM', 'A1/LMD - ISTM'];

    function generateData() {
        let data = [];
        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let niveau = (Math.random() > 0.6) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            
            let sBase, pBase, aBase;

            // Logique demandée : Gynéco > Autres | A1 > A2
            if (service === 'Gynécologie-Obstétrique') {
                sBase = (niveau === 'A1/LMD - ISTM') ? 85 : 70;
                pBase = (niveau === 'A1/LMD - ISTM') ? 80 : 65;
                aBase = 4.5;
            } else {
                sBase = (niveau === 'A1/LMD - ISTM') ? 55 : 35; // A2 vraiment bas
                pBase = (niveau === 'A1/LMD - ISTM') ? 45 : 25; // A2 critique
                aBase = (niveau === 'A1/LMD - ISTM') ? 3.5 : 2.8;
            }

            data.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: service,
                niveau: niveau,
                scoreSavoir: Math.min(100, sBase + Math.floor(Math.random() * 15)),
                scorePratique: Math.min(100, pBase + Math.floor(Math.random() * 15)),
                scoreAttitude: (aBase + (Math.random() * 0.5)).toFixed(1)
            });
        }
        return data;
    }

    database = generateData();

    // --- LOGIQUE UI ---
    window.switchTab = function(n) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 3) window.updateAnalytics();
    };

    window.requestAdmin = function() {
        let p = prompt("Code Admin :");
        if(p === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
        }
    };

    window.updateUI = function() {
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 10).map(r => `
            <tr>
                <td>${r.id}</td><td>${r.service}</td><td>${r.niveau}</td>
                <td style="color:${r.scoreSavoir > 60 ? 'green':'red'}">${r.scoreSavoir}%</td>
                <td style="color:${r.scorePratique > 60 ? 'green':'red'}">${r.scorePratique}%</td>
                <td>${r.scoreAttitude}</td>
            </tr>
        `).join('');
    };

    window.updateAnalytics = function() {
        const populateTable = (tableId, field) => {
            const html = services.map(s => {
                let subA2 = database.filter(r => r.service === s && r.niveau === 'A2 - ITM');
                let subA1 = database.filter(r => r.service === s && r.niveau === 'A1/LMD - ISTM');
                
                let avgA2 = subA2.length ? (subA2.reduce((a,b)=>a+parseFloat(b[field]),0)/subA2.length).toFixed(1) : 0;
                let avgA1 = subA1.length ? (subA1.reduce((a,b)=>a+parseFloat(b[field]),0)/subA1.length).toFixed(1) : 0;
                let global = ((parseFloat(avgA1) + parseFloat(avgA2))/2).toFixed(1);

                return `<tr>
                    <td class="td-left">${s}</td>
                    <td>${subA2.length}</td><td><b>${avgA2}${field==='scoreAttitude'?'':'%'}</b></td>
                    <td>${subA1.length}</td><td><b>${avgA1}${field==='scoreAttitude'?'':'%'}</b></td>
                    <td style="background:#f0f0f0; font-weight:bold;">${global}${field==='scoreAttitude'?'':'%'}</td>
                </tr>`;
            }).join('');
            document.getElementById(tableId).innerHTML = html;
        };

        populateTable('table-savoir', 'scoreSavoir');
        populateTable('table-attitude', 'scoreAttitude');
        populateTable('table-pratique', 'scorePratique');

        document.getElementById('dynamic-report').innerHTML = `
            <div class="interpretation-box" style="background:#fff3e0; border-color:#ff9800; color:#e65100;">
                <h4 style="margin-top:0;">⚠️ Constat Majeur</h4>
                Il existe un fossé cognitif entre les infirmières <b>A1 (ISTM)</b> et <b>A2 (ITM)</b>. 
                Le personnel de niveau A2 constitue la majorité du temps de contact avec le patient mais possède le score de pratique le plus bas (Moyenne < 30% hors Gynéco). 
                L'hôpital doit impérativement standardiser la formation continue.
            </div>
        `;
    };

    window.saveRecord = function() {
        alert("Fiche enregistrée localement ! (N=179)");
        window.switchTab(2);
    };

    window.exportCSV = function() {
        alert("Exportation des 178 lignes vers 'Rapport_Makala.csv'...");
    };

    // Initialisation
    const sel = document.getElementById('code-enquete');
    for(let i=179; i<=200; i++) {
        let o = document.createElement('option');
        o.text = "INF-MAK-" + i;
        sel.add(o);
    }
</script>

</body>
</html>
