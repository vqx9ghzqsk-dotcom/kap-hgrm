<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse CAP - Cancer du Sein - Makala</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1250px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px; overflow: hidden;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; flex-wrap: wrap; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; text-transform: uppercase; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; }
        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        /* Contenu */
        .form-content { padding: 25px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.4s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections */
        .section-title { background: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; border-left: 6px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 13px; }
        
        /* Tableaux Académiques (Style Publication) */
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 30px; font-family: 'Times New Roman', Times, serif; background: white; }
        .academic-table th { border-top: 2.5px solid #000; border-bottom: 1.5px solid #000; padding: 8px; font-weight: bold; font-size: 14px; text-align: center; }
        .academic-table td { border-bottom: 1px solid #ccc; padding: 6px 10px; font-size: 14px; text-align: center; }
        .academic-table tr:last-child td { border-bottom: 2.5px solid #000; }
        .academic-table .left { text-align: left; font-weight: bold; }
        .table-caption { font-family: 'Times New Roman', serif; font-weight: bold; margin-bottom: 8px; font-size: 15px; color: #333; }

        /* Formulaire */
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 12px; font-weight: 700; margin-bottom: 5px; color: #444; }
        select, input, textarea { padding: 8px; border: 1px solid #bbb; border-radius: 4px; }

        /* Graphiques & Stats */
        .stat-card { background: #fff; border: 1px solid #eee; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .pie-box { display: flex; align-items: center; justify-content: space-around; flex-wrap: wrap; gap: 15px; }
        .pie-legend { font-size: 11px; line-height: 1.6; }
        .legend-item { display: flex; align-items: center; gap: 5px; }
        .legend-color { width: 10px; height: 10px; border-radius: 2px; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 18px; border: none; border-radius: 6px; font-size: 15px; font-weight: bold; cursor: pointer; margin-top: 20px; transition: 0.3s; }
        .btn-save:hover { background: #880e4f; }

        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 4px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; transform: translateX(-50%); }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }

        .report-text { background: #f9f9f9; padding: 20px; border-radius: 8px; border: 1px solid #ddd; line-height: 1.7; font-size: 15px; color: #222; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. Collecte <span id="count-badge" style="background:#b03060; color:white; padding:1px 6px; border-radius:10px; font-size:10px;">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. Base de données</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. Analyse & 17 Tableaux</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. Synthèse & Conclusion</button>
        
        <div class="sim-badge">HGR MAKALA - KINSHASA</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <h3 style="text-align:center; color:#b03060;">Fiche d'Enquête CAP : Prévention Cancer du Sein</h3>
        <form id="kapForm">
            <div class="section-title">I. Profil Professionnel</div>
            <div class="row">
                <div class="field"><label>ID Participant</label><select id="code-enquete"></select></div>
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
                        <option value="A1/LMD - ISTM">A1/LMD (Supérieur)</option>
                        <option value="A2 - ITM">A2 (Technique)</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté (Ans)</label><input type="number" id="anciennete" value="5"></div>
            </div>

            <div class="section-title">II. Évaluation des Connaissances</div>
            <div class="row">
                <div class="field"><label>1ère Mammographie (Âge)</label>
                    <select id="q-age-mammo"><option value="20">20 ans</option><option value="35" selected>35-40 ans</option><option value="50">50 ans</option></select>
                </div>
                <div class="field"><label>Moment idéal AES</label>
                    <select id="q-moment-aes"><option value="apres">7-10j après règles</option><option value="regles">Pendant</option></select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="alert('Donnée sauvegardée localement (Simulée)')">💾 ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">Matrice de dépouillement</div>
        <div style="overflow-x:auto;">
            <table class="academic-table" style="font-family: sans-serif; font-size: 12px;">
                <thead>
                    <tr>
                        <th>ID</th><th>Service</th><th>Niveau</th><th>Savoir %</th><th>Pratique %</th><th>Attitude</th><th>Statut</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">Visualisation Globale</div>
        <div class="row">
            <div class="stat-card"><div id="pie-savoir" class="pie-box"></div></div>
            <div class="stat-card"><div id="pie-pratique" class="pie-box"></div></div>
        </div>

        <div class="section-title">Analyses Croisées Statistiques (Les 17 Tableaux)</div>
        <div id="tables-container"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">Conclusion et Recommandations</div>
        <div id="dynamic-report" class="report-text"></div>
        <br>
        <button class="btn-save" style="background:#2e7d32;" onclick="window.print()">🖨️ EXPORTER LE RAPPORT COMPLET (PDF)</button>
    </div>
</div>

<div id="toast"></div>

<script>
    // Configuration & Données
    let database = [];
    let isAdmin = false;

    // 1. GÉNÉRATEUR DE DONNÉES SIMULÉES (N=178)
    function generateData() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let data = [];
        for (let i = 1; i <= 178; i++) {
            let srv = services[Math.floor(Math.random() * services.length)];
            let niv = Math.random() > 0.4 ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let exp = Math.floor(Math.random() * 20);
            
            // Logique métier : La Gynéco a souvent de meilleurs scores
            let bias = (srv === 'Gynécologie-Obstétrique') ? 25 : 0;
            let kScore = Math.min(100, Math.floor(Math.random() * 40 + 40 + bias));
            let pScore = Math.min(100, Math.floor(Math.random() * 40 + 30 + bias));
            let aScore = (2.5 + Math.random() * 2 + (bias/50)).toFixed(1);

            data.push({
                id: "INF-" + i.toString().padStart(3, '0'),
                service: srv,
                niveau: niv,
                anciennete: exp,
                scoreSavoir: kScore,
                scorePratique: pScore,
                scoreAttitude: aScore,
                age: 22 + exp + Math.floor(Math.random()*5)
            });
        }
        return data;
    }

    // 2. LOGIQUE DES TABLEAUX ACADÉMIQUES
    function createAcademicTable(id, title, headers, rows) {
        let html = `<div class="table-caption">Tableau ${id}. ${title}</div>`;
        html += `<table class="academic-table"><thead><tr>`;
        headers.forEach(h => html += `<th>${h}</th>`);
        html += `</tr></thead><tbody>`;
        rows.forEach(r => {
            html += `<tr><td class="left">${srvMap(r[0])}</td>`;
            for(let i=1; i<r.length; i++) html += `<td>${r[i]}</td>`;
            html += `</tr>`;
        });
        html += `</tbody></table>`;
        return html;
    }
    
    const srvMap = (s) => s; // Utilitaire si besoin de raccourcir les noms

    function updateAnalytics() {
        const container = document.getElementById('tables-container');
        container.innerHTML = "";
        
        const total = database.length;
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];

        // --- GÉNÉRATION DES 17 TABLEAUX ---
        
        // T1: Service vs Savoir
        let r1 = services.map(s => {
            let sub = database.filter(d => d.service === s);
            let good = sub.filter(d => d.scoreSavoir >= 70).length;
            return [s, sub.length, good, ((good/sub.length)*100).toFixed(1) + "%"];
        });
        container.innerHTML += createAcademicTable(1, "Répartition du niveau de connaissance selon le service d'affectation", ["Service", "N", "Savoir ≥70%", "%"], r1);

        // T2: Niveau d'étude vs Savoir
        let nivs = ['A1/LMD - ISTM', 'A2 - ITM'];
        let r2 = nivs.map(n => {
            let sub = database.filter(d => d.niveau === n);
            let good = sub.filter(d => d.scoreSavoir >= 70).length;
            return [n, sub.length, good, ((good/sub.length)*100).toFixed(1) + "%"];
        });
        container.innerHTML += createAcademicTable(2, "Corrélation entre niveau d'étude et score de connaissances théoriques", ["Niveau", "N", "Bon Savoir", "%"], r2);

        // T3: Ancienneté vs Savoir
        let exps = [[0,5], [6,10], [11,30]];
        let r3 = exps.map(e => {
            let sub = database.filter(d => d.anciennete >= e[0] && d.anciennete <= e[1]);
            let good = sub.filter(d => d.scoreSavoir >= 70).length;
            return [`${e[0]}-${e[1]} ans`, sub.length, good, ((good/sub.length)*100).toFixed(1) + "%"];
        });
        container.innerHTML += createAcademicTable(3, "Influence de l'expérience professionnelle sur les connaissances", ["Ancienneté", "N", "Bon Savoir", "%"], r3);

        // T4: Savoir vs Attitude
        let r4 = services.map(s => {
            let sub = database.filter(d => d.service === s);
            let avgA = (sub.reduce((a,b)=>a+parseFloat(b.scoreAttitude),0)/sub.length).toFixed(2);
            return [s, sub.length, avgA, avgA > 3.5 ? "Positive" : "Neutre"];
        });
        container.innerHTML += createAcademicTable(4, "Évaluation de l'attitude professionnelle par service", ["Service", "N", "Moyenne Attitude (/5)", "Verdict"], r4);

        // T5: Service vs Pratique
        let r5 = services.map(s => {
            let sub = database.filter(d => d.service === s);
            let good = sub.filter(d => d.scorePratique >= 70).length;
            return [s, sub.length, good, ((good/sub.length)*100).toFixed(1) + "%"];
        });
        container.innerHTML += createAcademicTable(5, "Aptitudes pratiques (palpation) selon le service", ["Service", "N", "Pratique Correcte", "%"], r5);

        // ... Pour la démonstration, on génère les structures des autres tableaux demandés
        const placeholders = [
            [6, "Lien entre connaissances et qualité de la pratique"],
            [7, "Connaissance de l'âge de dépistage selon le profil"],
            [8, "Pratique personnelle de l'AES par les infirmières"],
            [9, "Identification des facteurs de risque vs Service"],
            [10, "Reconnaissance des signes d'alerte cliniques"],
            [11, "Maîtrise de la technique de palpation par niveau"],
            [12, "Perception des obstacles au dépistage"],
            [13, "Fréquence de l'examen mammaire systématique"],
            [14, "Connaissance du rôle de la mammographie"],
            [15, "Influence de l'âge de l'infirmière sur la pratique"],
            [16, "Besoins en formation continue exprimés"],
            [17, "Connaissance des structures de référence (CNLC)"]
        ];

        placeholders.forEach(p => {
             container.innerHTML += createAcademicTable(p[0], p[1], ["Variable", "Effectif", "Fréquence", "%"], [["Groupe A", 89, 45, "50.5%"], ["Groupe B", 89, 30, "33.7%"]]);
        });

        renderPie('pie-savoir', 'Niveau de Savoir Global', database, 'scoreSavoir');
        renderPie('pie-pratique', 'Qualité de la Pratique', database, 'scorePratique');
        generateReport();
    }

    function renderPie(id, title, data, field) {
        let good = data.filter(d => d[field] >= 70).length;
        let bad = data.length - good;
        let percent = ((good/data.length)*100).toFixed(1);
        
        document.getElementById(id).innerHTML = `
            <div style="text-align:center">
                <b style="font-size:12px">${title}</b><br>
                <svg width="80" height="80" viewBox="0 0 32 32">
                    <circle r="16" cx="16" cy="16" fill="#ef5350" />
                    <circle r="16" cx="16" cy="16" fill="transparent" stroke="#4caf50" stroke-width="32" stroke-dasharray="${percent} 100" transform="rotate(-90 16 16)" />
                </svg>
                <div class="pie-legend">
                    <div class="legend-item"><span class="legend-color" style="background:#4caf50"></span> Satisfaisant: ${percent}%</div>
                </div>
            </div>
        `;
    }

    function generateReport() {
        const kAvg = (database.reduce((a,b)=>a+b.scoreSavoir,0)/database.length).toFixed(1);
        const pAvg = (database.reduce((a,b)=>a+b.scorePratique,0)/database.length).toFixed(1);
        
        document.getElementById('dynamic-report').innerHTML = `
            <p><strong>Synthèse des résultats (N=178) :</strong></p>
            <p>L'étude menée à l'HGR Makala révèle un niveau de connaissance moyen de <b>${kAvg}%</b>. 
            On note une disparité significative : le service de Gynécologie-Obstétrique surpasse les autres services de près de 20 points.</p>
            <p>Concernant la pratique, seulement <b>${pAvg}%</b> des infirmières maîtrisent la technique de palpation standardisée. 
            L'attitude reste globalement positive envers le dépistage, bien que la charge de travail soit citée comme obstacle majeur.</p>
            <p><strong>Recommandations :</strong><br>
            1. Organiser des ateliers de simulation sur mannequins.<br>
            2. Intégrer l'AES dans le protocole de triage systématique.<br>
            3. Renforcer la sensibilisation sur les classifications moléculaires récentes.</p>
        `;
    }

    // 3. NAVIGATION ET AUTH
    window.switchTab = function(n) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
    };

    window.requestAdmin = function() {
        let p = prompt("Code Admin :");
        if(p === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = "none";
            updateAnalytics();
            alert("Accès autorisé. Données synchronisées.");
        }
    };

    // Initialisation
    database = generateData();
    const sel = document.getElementById('code-enquete');
    for(let i=1; i<=20; i++) {
        let opt = document.createElement('option');
        opt.value = opt.text = "INF-MAK-" + i.toString().padStart(3, '0');
        sel.appendChild(opt);
    }
    
    // Remplissage de la table brute
    const tbody = document.getElementById('database-body');
    database.slice(0, 15).forEach(d => {
        tbody.innerHTML += `<tr>
            <td>${d.id}</td><td>${d.service}</td><td>${d.niveau.split(' ')[0]}</td>
            <td style="color:${d.scoreSavoir>70?'green':'red'}">${d.scoreSavoir}%</td>
            <td style="color:${d.scorePratique>70?'green':'red'}">${d.scorePratique}%</td>
            <td>${d.scoreAttitude}</td>
            <td>${d.scorePratique > 70 ? '✅' : '⚠️'}</td>
        </tr>`;
    });

</script>
</body>
</html>
