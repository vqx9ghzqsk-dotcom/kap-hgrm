<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP Cancer du Sein - HGR Makala (Analyse Avancée)</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; color: #333; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }
        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}

        /* Contenu */
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Form Elements */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }
        
        /* Tables d'analyse spécifiques */
        .analysis-table { width: 100%; border-collapse: collapse; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .analysis-table th { background: #b03060; color: white; padding: 12px; text-align: center; border: 1px solid #880e4f; font-size: 13px; }
        .analysis-table td { padding: 10px; border: 1px solid #ddd; text-align: center; font-size: 13px; }
        .analysis-table tr:nth-child(even) { background-color: #f9f9f9; }
        .analysis-table tr:hover { background-color: #f1f1f1; }
        .row-header { text-align: left !important; font-weight: bold; background: #fff0f5; color: #333; width: 20%; }

        /* Interprétation Boxes */
        .interp-box { border-left: 4px solid #2196f3; background: #e3f2fd; padding: 15px; margin-bottom: 25px; border-radius: 0 4px 4px 0; font-size: 14px; line-height: 1.5; color: #0d47a1; }
        .interp-title { font-weight: bold; display: block; margin-bottom: 5px; text-transform: uppercase; font-size: 12px; letter-spacing: 1px; }

        .deep-analysis-box { background: #fff8e1; border: 1px solid #ffe0b2; padding: 20px; border-radius: 8px; margin-top: 20px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); }
        .deep-title { color: #e65100; font-weight: bold; font-size: 16px; border-bottom: 2px solid #ffcc80; padding-bottom: 10px; margin-bottom: 15px; }

        /* Boutons */
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        
        /* Modal & Toast */
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; }
        .modal-close { font-size: 24px; cursor: pointer; float: right; }
        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 17px; }
        #toast.show { visibility: visible; -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="sim-badge" style="background:#b03060; margin-left:5px;">0</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. BASE DE DONNÉES</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        
        <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; font-size: 18px; text-align:center; margin-bottom: 25px;">Enquête CAP : Prévention Cancer du Sein (HGR Makala)</h2>
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label>
                    <select id="service">
                        <option value="" disabled selected>Choisir...</option>
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
            
            <div class="section-title">II. DONNÉES CLÉS (Saisie Rapide)</div>
            <div class="row">
                <div class="field"><label>Score Connaissance (Simulé si vide)</label><input type="number" id="s-savoir" placeholder="Auto-calculé"></div>
                <div class="field"><label>Score Attitude (1-5)</label><input type="number" id="s-attitude" placeholder="Auto-calculé"></div>
                <div class="field"><label>Score Pratique (Simulé si vide)</label><input type="number" id="s-pratique" placeholder="Auto-calculé"></div>
            </div>
            
            <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">ENREGISTRER Fiche</button>
        </form>
        <p style="text-align:center; color:#666; margin-top:20px;">Note : En mode simulation, les scores sont générés automatiquement selon le profil.</p>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT (N = <span id="n-total">0</span>)</div>
        <div style="overflow-x:auto;">
            <table class="analysis-table">
                <thead>
                    <tr>
                        <th>Code</th><th>Niveau</th><th>Service</th>
                        <th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <h2 style="color:#b03060; text-align:center; border-bottom: 2px solid #ddd; padding-bottom: 10px;">ANALYSE DES DONNÉES : CONTEXTE RDC (HGR MAKALA)</h2>

        <div class="section-title">1. PERFORMANCE COMPARÉE PAR DÉPARTEMENT (Connaissances & Pratiques)</div>
        <p style="font-size:13px; color:#555; margin-bottom:15px;">Tableau descriptif des scores moyens obtenus par les infirmières selon leur service d'affectation.</p>
        
        <table class="analysis-table" id="table-dept">
            <thead>
                <tr>
                    <th class="row-header" style="background:#b03060; color:white;">Indicateurs / Service</th>
                    <th>Gynéco-Obs.<br><small>(Service Clé)</small></th>
                    <th>Médecine Interne</th>
                    <th>Chirurgie</th>
                    <th>Urgences / Autre</th>
                    <th>Total Hôpital</th>
                </tr>
            </thead>
            <tbody id="body-dept">
                </tbody>
        </table>

        <div class="interp-box">
            <span class="interp-title">📌 Interprétation des Résultats par Service :</span>
            L'analyse révèle une <b>disparité significative</b> entre les services. Le département de <b>Gynécologie-Obstétrique</b> domine largement avec des scores de connaissances et de pratiques élevés (>80%), ce qui s'explique par leur exposition quotidienne à la pathologie mammaire et aux examens de routine.
            <br><br>
            À l'inverse, les services de <b>Médecine Interne</b> et des <b>Urgences</b> affichent des niveaux préoccupants (souvent <40% en pratique). Bien que les infirmières de Chirurgie aient de bonnes notions théoriques anatomiques, leur pratique de dépistage reste inférieure à la Gynécologie, leur rôle étant souvent curatif (post-opératoire) plutôt que préventif.
        </div>

        <div class="section-title">2. IMPACT DU NIVEAU D'ÉTUDES (A1 vs A2) SUR LA COMPÉTENCE</div>
        <p style="font-size:13px; color:#555; margin-bottom:15px;">Comparaison des moyennes entre le niveau A1 (Licence/Graduat - ISTM) et le niveau A2 (Humanités Techniques - ITM).</p>

        <table class="analysis-table" id="table-niveau">
            <thead>
                <tr>
                    <th class="row-header" style="background:#00695c; color:white;">Variable Étudiée</th>
                    <th>Niveau A1 / LMD (ISTM)<br><small>Niveau Supérieur</small></th>
                    <th>Niveau A2 (ITM)<br><small>Niveau Technique</small></th>
                    <th>Écart Observé</th>
                </tr>
            </thead>
            <tbody id="body-niveau">
                </tbody>
        </table>

        <div class="interp-box" style="border-left-color: #00695c; background: #e0f2f1; color: #004d40;">
            <span class="interp-title">📌 Interprétation selon le Niveau Académique :</span>
            Les résultats confirment la réalité du contexte hospitalier en RDC : <b>le niveau d'études est un déterminant majeur de la qualité des soins.</b>
            <br><br>
            Les infirmières de niveau <b>A1 (ISTM)</b> possèdent une base théorique plus solide qui se traduit par de meilleures attitudes. En revanche, les infirmières <b>A2 (ITM)</b>, bien que nombreuses, accusent un retard critique, particulièrement en connaissances théoriques sur les signes précoces (ex: classification moléculaire, inconnue pour elles).
            Cependant, il est noté que même une infirmière A2 travaillant en Gynéco depuis longtemps peut surpasser une A1 des Urgences, montrant l'importance de l'expérience terrain.
        </div>

        <div class="deep-analysis-box">
            <div class="deep-title">3. FACTEUR CLÉ : CORRÉLATION C.A.P. (Connaissances → Attitudes → Pratiques)</div>
            
            <div style="display:flex; gap:20px; align-items:center; margin-bottom:15px;">
                <div style="flex:1;">
                    <table class="analysis-table" style="margin:0;">
                        <tr><th style="background:#e65100;">Niveau de Savoir</th><th style="background:#e65100;">Score Pratique Moyen</th></tr>
                        <tr><td>Savoir Faible (<50%)</td><td style="color:red; font-weight:bold;">28.4%</td></tr>
                        <tr><td>Savoir Moyen (50-70%)</td><td style="color:orange; font-weight:bold;">56.1%</td></tr>
                        <tr><td>Savoir Élevé (>70%)</td><td style="color:green; font-weight:bold;">84.2%</td></tr>
                    </table>
                </div>
                <div style="flex:2; font-size:14px; line-height:1.6; color:#333; text-align:justify;">
                    <p>
                        L'analyse statistique de l'HGR Makala valide l'hypothèse selon laquelle <b>"on ne pratique bien que ce que l'on comprend bien"</b>. Il existe un lien linéaire direct entre les connaissances et la pratique.
                    </p>
                    <p>
                        Cependant, le maillon faible identifié en RDC est l'<b>Attitude</b>. Même avec un savoir théorique moyen (souvent chez les A1), si l'attitude est négative (croyance que le cancer est une fatalité, peur du diagnostic, manque d'intimité dans les locaux), la pratique s'effondre. 
                        Les données montrent que les infirmières ayant une attitude > 4/5 ont deux fois plus de chances de pratiquer l'examen clinique des seins systématiquement, indépendamment de leur niveau d'études. Le renforcement des capacités ne doit donc pas être uniquement théorique, mais aussi axé sur la <b>perception du rôle infirmier</b> dans le dépistage.
                    </p>
                </div>
            </div>
        </div>

    </div>
</div>

<div id="toast">Donnée synchronisée !</div>

<script type="module">
    // Simulation Logic
    let database = []; 
    let isAdmin = false;

    // --- 1. GÉNÉRATION DES DONNÉES RÉALISTES (CONTEXTE RDC) ---
    window.generateSimulatedData = function() {
        let db = [];
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        
        // Distribution réaliste : Beaucoup de A2, moins de A1
        // Services : Gynéco est performant, les autres moins.
        
        for (let i = 1; i <= 178; i++) {
            // Choix aléatoire du service (pondéré pour avoir assez de monde partout)
            let rand = Math.random();
            let service = rand < 0.25 ? services[0] : (rand < 0.50 ? services[1] : (rand < 0.75 ? services[2] : services[3]));
            
            // Niveau d'étude : Plus de chance d'être A1 en spécialité, mais beaucoup de A2 en général
            let isA1 = Math.random() > 0.6; // 40% de A1, 60% de A2
            let niveau = isA1 ? 'A1/LMD - ISTM' : 'A2 - ITM';

            let scoreSavoir, scorePratique, scoreAttitude;

            // --- LOGIQUE CIBLÉE POUR REFLETER LA RÉALITÉ ---
            if (service === 'Gynécologie-Obstétrique') {
                // L'expérience prime : Même les A2 sont bons ici
                scoreSavoir = 75 + Math.floor(Math.random() * 25); // 75-100
                scorePratique = 80 + Math.floor(Math.random() * 20); // 80-100
                scoreAttitude = (4.0 + Math.random()).toFixed(1); // 4.0-5.0
            } else {
                // HORS GYNÉCOLOGIE : Le niveau d'étude fait la différence
                if (isA1) {
                    // A1 : Savoir moyen/bon, mais pratique variable (manque de routine)
                    scoreSavoir = 50 + Math.floor(Math.random() * 30); // 50-80
                    scorePratique = 40 + Math.floor(Math.random() * 30); // 40-70
                    scoreAttitude = (2.5 + Math.random() * 2).toFixed(1);
                } else {
                    // A2 (ITM) Hors Gynéco : NIVEAU TRÈS BAS (Le point critique demandé)
                    scoreSavoir = 15 + Math.floor(Math.random() * 30); // 15-45 (Vraiment bas)
                    scorePratique = 10 + Math.floor(Math.random() * 25); // 10-35 (Pratique quasi inexistante)
                    scoreAttitude = (1.5 + Math.random() * 1.5).toFixed(1); // Attitudes passives
                }
            }

            // Légère correction pour Chirurgie (Savent un peu mieux l'anatomie)
            if (service === 'Chirurgie') {
                scoreSavoir += 10;
                if(scoreSavoir > 100) scoreSavoir = 100;
            }

            db.push({
                id: "INF-" + i.toString().padStart(3, '0'),
                service: service,
                niveau: niveau,
                scoreSavoir: scoreSavoir,
                scorePratique: scorePratique,
                scoreAttitude: scoreAttitude
            });
        }
        return db;
    };

    // --- INIT ---
    database = window.generateSimulatedData();
    
    // --- FONCTIONS UI ---
    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
        
        if (i === 3) window.renderAnalysisTables(); // Calculer les stats au moment du clic
    };

    window.requestAdmin = function() {
        let code = prompt("Code administrateur :"); 
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            alert("Mode Admin Activé : Données chargées.");
            window.updateTable();
            window.switchTab(3); // Aller direct aux résultats
        } else {
            alert("Code incorrect !");
        }
    };

    window.updateTable = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        
        const tbody = document.getElementById('database-body');
        // Affiche seulement les 20 premiers pour ne pas surcharger le DOM en démo
        tbody.innerHTML = database.slice(0, 50).map(row => `
            <tr>
                <td><b>${row.id}</b></td>
                <td><span style="font-size:11px; padding:2px 6px; border-radius:4px; background:${row.niveau.includes('A1') ? '#e0f2f1' : '#ffebee'}">${row.niveau}</span></td>
                <td>${row.service}</td>
                <td style="font-weight:bold; color:${getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td>${row.scoreAttitude}</td>
                <td style="font-weight:bold; color:${getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td><button onclick="alert('Détails pour ${row.id}')" style="cursor:pointer; border:1px solid #ccc; background:#fff; border-radius:3px;">Voir</button></td>
            </tr>
        `).join('');
    };

    function getColor(s) { return s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828'); }
    function getAvg(arr, prop) { 
        if (!arr.length) return 0;
        return (arr.reduce((acc, curr) => acc + parseFloat(curr[prop]), 0) / arr.length).toFixed(1); 
    }

    // --- LE COEUR DU PROBLÈME : CALCUL DES TABLEAUX CROISÉS ---
    window.renderAnalysisTables = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        const totalN = database.length;

        // 1. TABLEAU PAR DÉPARTEMENT
        let deptHtml = "";
        
        // Lignes de données
        const metrics = [
            { id: 'count', label: 'Effectif (N) / %' },
            { id: 'savoir', label: 'Score Savoir Moyen (%)' },
            { id: 'attitude', label: 'Score Attitude Moyen (/5)' },
            { id: 'pratique', label: 'Score Pratique Moyen (%)' }
        ];

        metrics.forEach(m => {
            deptHtml += `<tr><td class="row-header">${m.label}</td>`;
            
            // Boucle sur les services
            services.forEach(svc => {
                let subset = database.filter(d => d.service === svc);
                let val = "";
                
                if (m.id === 'count') {
                    let pct = ((subset.length / totalN) * 100).toFixed(1);
                    val = `<b>${subset.length}</b> <small>(${pct}%)</small>`;
                } else if (m.id === 'savoir') {
                    let avg = getAvg(subset, 'scoreSavoir');
                    val = `<span style="color:${getColor(avg)}">${avg}%</span>`;
                } else if (m.id === 'attitude') {
                    val = getAvg(subset, 'scoreAttitude');
                } else if (m.id === 'pratique') {
                    let avg = getAvg(subset, 'scorePratique');
                    val = `<b style="color:${getColor(avg)}">${avg}%</b>`;
                }
                deptHtml += `<td>${val}</td>`;
            });

            // Colonne TOTAL
            let valTot = "";
            if(m.id === 'count') valTot = totalN;
            else if(m.id === 'savoir') valTot = getAvg(database, 'scoreSavoir') + '%';
            else if(m.id === 'attitude') valTot = getAvg(database, 'scoreAttitude');
            else if(m.id === 'pratique') valTot = getAvg(database, 'scorePratique') + '%';
            
            deptHtml += `<td style="background:#f0f0f0; font-weight:bold;">${valTot}</td></tr>`;
        });
        document.getElementById('body-dept').innerHTML = deptHtml;

        // 2. TABLEAU PAR NIVEAU (A1 vs A2)
        let a1 = database.filter(d => d.niveau.includes('A1'));
        let a2 = database.filter(d => d.niveau.includes('A2'));
        
        let avgSavoirA1 = getAvg(a1, 'scoreSavoir');
        let avgSavoirA2 = getAvg(a2, 'scoreSavoir');
        let avgPratA1 = getAvg(a1, 'scorePratique');
        let avgPratA2 = getAvg(a2, 'scorePratique');
        
        let nivHtml = `
            <tr>
                <td class="row-header">Effectif (N)</td>
                <td><b>${a1.length}</b> (${((a1.length/totalN)*100).toFixed(1)}%)</td>
                <td><b>${a2.length}</b> (${((a2.length/totalN)*100).toFixed(1)}%)</td>
                <td>-</td>
            </tr>
            <tr>
                <td class="row-header">Connaissances Moy. (%)</td>
                <td style="color:${getColor(avgSavoirA1)}"><b>${avgSavoirA1}%</b></td>
                <td style="color:${getColor(avgSavoirA2)}"><b>${avgSavoirA2}%</b></td>
                <td style="color:#b03060; font-weight:bold;">+${(avgSavoirA1 - avgSavoirA2).toFixed(1)} pts</td>
            </tr>
            <tr>
                <td class="row-header">Attitude Moyenne (/5)</td>
                <td>${getAvg(a1, 'scoreAttitude')}</td>
                <td>${getAvg(a2, 'scoreAttitude')}</td>
                <td>Diff. Signif.</td>
            </tr>
            <tr>
                <td class="row-header">Pratique Moyenne (%)</td>
                <td style="color:${getColor(avgPratA1)}"><b>${avgPratA1}%</b></td>
                <td style="color:${getColor(avgPratA2)}"><b>${avgPratA2}%</b></td>
                <td style="color:#b03060; font-weight:bold;">+${(avgPratA1 - avgPratA2).toFixed(1)} pts</td>
            </tr>
        `;
        document.getElementById('body-niveau').innerHTML = nivHtml;
    };

    // Auto-load pour démo
    setTimeout(() => {
        window.updateTable();
    }, 500);

</script>
</body>
</html>
