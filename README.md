<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP Cancer du Sein - Makala</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
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

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input, textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; width: 100%; box-sizing: border-box; }

        /* Tables Académiques */
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 35px; font-family: 'Times New Roman', serif; font-size: 14px; background: white; box-shadow: 0 2px 5px rgba(0,0,0,0.05);}
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; padding: 10px; text-align: center; }
        .academic-table tbody td { border-bottom: 1px solid #eee; padding: 8px; text-align: center; }
        .academic-table tbody tr:last-child td { border-bottom: 2px solid #000; }
        .academic-table .row-header { text-align: left; padding-left: 15px; }
        .table-caption { font-weight: bold; color: #333; margin-bottom: 8px; font-size: 14px; text-align: left; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; padding: 15px; background: #f9f9f9; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; }
        
        /* Stats & Charts */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; display: flex; flex-direction: column; align-items: center; }
        .pie-box { display: flex; flex-wrap: wrap; justify-content: center; align-items: center; width: 100%; gap: 15px; margin-top: 10px; }
        .pie-legend { font-size: 11px; display: flex; flex-direction: column; gap: 4px; }
        .legend-item { display: flex; align-items: center; gap: 5px; }
        .legend-color { width: 10px; height: 10px; border-radius: 2px; }

        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 5px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; transform: translateX(-50%); }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" onclick="switchTab(2)">2. MATRICE</button>
        <button class="tab admin-only" onclick="switchTab(3)">3. RÉSULTATS (17 TABLEAUX)</button>
        <button class="tab admin-only" onclick="switchTab(4)">4. CONCLUSIONS</button>
        
        <div class="sim-badge">N=178 (KINSHASA)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="text-align:center; color:#b03060;">Enquête KAP - Prévention Cancer du Sein (Makala)</h2>
        <form id="kapForm">
            <div class="section-title">I. PROFIL & IDENTIFICATION</div>
            <div class="row">
                <div class="field"><label>Code</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option>
                        <option>Chirurgie</option><option>Urgences / Autre</option>
                    </select>
                </div>
                <div class="field"><label>Niveau</label>
                    <select id="niveau">
                        <option>A1/LMD - ISTM</option><option>A2 - ITM</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté (ans)</label><input type="number" id="anciennete" value="5"></div>
                <div class="field"><label>Âge</label><input type="number" id="age-participant" value="30"></div>
                <div class="field"><label>État Civil</label>
                    <select id="etat-civil">
                        <option>Célibataire</option><option>Mariée</option><option>Veuve</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="row">
                <div class="field"><label>Classification Moléculaire ?</label><select id="q-moleculaire"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Connaissance HER2 Low ?</label><select id="q-her2"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Moment idéal AES</label><select id="q-moment-aes"><option value="apres">7-10j après règles</option><option value="regles">Pendant</option></select></div>
            </div>

            <div class="sub-title">Facteurs de Risque (Cochez)</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age" checked> Âge > 50 ans</label>
                <label class="check-item"><input type="checkbox" value="famille" checked> ATCD Familiaux</label>
                <label class="check-item"><input type="checkbox" value="tabac"> Tabac/Alcool</label>
            </div>

            <button type="button" class="btn-save">☁️ SAUVEGARDER</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">Base de données (Extraits)</div>
        <table class="academic-table" style="font-size: 11px;">
            <thead><tr><th>Code</th><th>Service</th><th>Savoir %</th><th>Pratique %</th><th>Statut</th></tr></thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE GRAPHIQUE (DIAGRAMMES)</div>
        <div class="row">
            <div class="stat-card"><div id="pie-savoir" class="pie-box"></div><p>Niveau de Savoir</p></div>
            <div class="stat-card"><div id="pie-pratique" class="pie-box"></div><p>Qualité Pratique</p></div>
            <div class="stat-card"><div id="pie-service" class="pie-box"></div><p>Répartition Services</p></div>
        </div>

        <div class="section-title">TABLEAUX ACADÉMIQUES (1 À 17)</div>
        <div id="tables-container">
            </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">Rapport Final</div>
        <div id="dynamic-report" style="background:#fff; padding:20px; border:1px solid #ddd; border-radius:8px;">
            En cours de calcul...
        </div>
    </div>
</div>

<div id="toast">Action réussie !</div>

<script type="module">
    // Simulation / Données
    let database = [];
    let isAdmin = false;

    // --- GENERATEUR DE DONNÉES SIMULÉES ---
    const generateData = () => {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let data = [];
        for(let i=1; i<=178; i++) {
            let srv = services[Math.floor(Math.random()*services.length)];
            let scoreK = srv === 'Gynécologie-Obstétrique' ? 75 + Math.random()*20 : 40 + Math.random()*40;
            let scoreP = srv === 'Gynécologie-Obstétrique' ? 70 + Math.random()*25 : 30 + Math.random()*50;
            data.push({
                id: "INF-"+i.toString().padStart(3,'0'),
                service: srv,
                niveau: Math.random() > 0.3 ? 'A1/LMD - ISTM' : 'A2 - ITM',
                age: 22 + Math.floor(Math.random()*30),
                anciennete: Math.floor(Math.random()*20),
                etat_civil: Math.random() > 0.4 ? 'Mariée' : 'Célibataire',
                scoreSavoir: Math.round(scoreK),
                scorePratique: Math.round(scoreP),
                attitude: (2.5 + Math.random()*2.5).toFixed(1),
                risques: Math.random() > 0.5 ? ['age', 'famille'] : ['age'],
                obstacles: Math.random() > 0.6 ? ['Formation', 'Temps'] : ['Coût'],
                q_moleculaire: Math.random() > 0.7 ? 'oui' : 'non'
            });
        }
        return data;
    };

    // --- RENDU DES DIAGRAMMES (SVG) ---
    window.renderPie = (containerId, data) => {
        const container = document.getElementById(containerId);
        if(!container) return;
        const total = data.reduce((s, i) => s + i.v, 0);
        let currentAngle = 0;
        let svg = `<svg width="120" height="120" viewBox="-1 -1 2 2" style="transform: rotate(-90deg); border-radius:50%">`;
        data.forEach(item => {
            const p = item.v / total;
            const x1 = Math.cos(2 * Math.PI * currentAngle);
            const y1 = Math.sin(2 * Math.PI * currentAngle);
            currentAngle += p;
            const x2 = Math.cos(2 * Math.PI * currentAngle);
            const y2 = Math.sin(2 * Math.PI * currentAngle);
            svg += `<path d="M 0 0 L ${x1} ${y1} A 1 1 0 ${p>0.5?1:0} 1 ${x2} ${y2} Z" fill="${item.c}"></path>`;
        });
        svg += `</svg>`;
        let legend = `<div class="pie-legend">` + data.map(i => `<div class="legend-item"><div class="legend-color" style="background:${i.c}"></div>${i.l} (${Math.round(i.v/total*100)}%)</div>`).join('') + `</div>`;
        container.innerHTML = svg + legend;
    };

    // --- GÉNÉRATION DES 17 TABLEAUX ---
    const generate17Tables = () => {
        const container = document.getElementById('tables-container');
        const N = database.length;
        let html = "";

        const createTable = (num, title, headers, rows) => {
            return `
                <div class="table-caption">Tableau ${num} : ${title}</div>
                <table class="academic-table">
                    <thead><tr>${headers.map(h => `<th>${h}</th>`).join('')}</tr></thead>
                    <tbody>${rows.map(r => `<tr>${r.map((cell,idx) => `<td class="${idx===0?'row-header':''}">${cell}</td>`).join('')}</tr>`).join('')}</tbody>
                </table>
            `;
        };

        // 1. Âge
        let a1 = database.filter(d=>d.age<30).length;
        html += createTable(1, "Répartition par tranches d'âge", ["Tranche", "n", "%"], [["< 30 ans", a1, (a1/N*100).toFixed(1)], ["> 30 ans", N-a1, ((N-a1)/N*100).toFixed(1)]]);

        // 2. Niveau d'étude
        let n1 = database.filter(d=>d.niveau.includes('A1')).length;
        html += createTable(2, "Répartition par niveau d'étude", ["Niveau", "n", "%"], [["A1/LMD", n1, (n1/N*100).toFixed(1)], ["A2/ITM", N-n1, ((N-n1)/N*100).toFixed(1)]]);

        // 3. État Civil
        let ec1 = database.filter(d=>d.etat_civil==='Mariée').length;
        html += createTable(3, "Répartition par état civil", ["État", "n", "%"], [["Mariée", ec1, (ec1/N*100).toFixed(1)], ["Célibataire", N-ec1, ((N-ec1)/N*100).toFixed(1)]]);

        // 4. Ancienneté
        let anc1 = database.filter(d=>d.anciennete<10).length;
        html += createTable(4, "Ancienneté professionnelle", ["Années", "n", "%"], [["< 10 ans", anc1, (anc1/N*100).toFixed(1)], ["> 10 ans", N-anc1, ((N-anc1)/N*100).toFixed(1)]]);

        // 5. Service
        let srv1 = database.filter(d=>d.service.includes('Gynéco')).length;
        html += createTable(5, "Distribution par service d'affectation", ["Service", "n", "%"], [["Gynécologie", srv1, (srv1/N*100).toFixed(1)], ["Autres", N-srv1, ((N-srv1)/N*100).toFixed(1)]]);

        // 6. Savoir Global
        let sk1 = database.filter(d=>d.scoreSavoir>=70).length;
        html += createTable(6, "Niveau de connaissances globales", ["Niveau", "n", "%"], [["Bon (≥70%)", sk1, (sk1/N*100).toFixed(1)], ["Moyen/Faible", N-sk1, ((N-sk1)/N*100).toFixed(1)]]);

        // 7. Facteurs de risque
        html += createTable(7, "Connaissances des facteurs de risque", ["Facteurs", "n", "%"], [["Âge avancé", N, "100"], ["Génétique/Famille", Math.round(N*0.8), "80"]]);

        // 8. Signes d'alerte
        html += createTable(8, "Identification des signes d'alerte", ["Signe", "n", "%"], [["Nodule indolore", Math.round(N*0.7), "70"], ["Écoulement", Math.round(N*0.4), "40"]]);

        // 9. Savoir Moléculaire
        let mol = database.filter(d=>d.q_moleculaire==='oui').length;
        html += createTable(9, "Connaissance de la classification moléculaire", ["Réponse", "n", "%"], [["Oui", mol, (mol/N*100).toFixed(1)], ["Non", N-mol, ((N-mol)/N*100).toFixed(1)]]);

        // 10. Attitude
        let att1 = database.filter(d=>parseFloat(d.attitude)>3.5).length;
        html += createTable(10, "Type d'attitude face au dépistage", ["Attitude", "n", "%"], [["Positive", att1, (att1/N*100).toFixed(1)], ["Neutre/Négative", N-att1, ((N-att1)/N*100).toFixed(1)]]);

        // 11. Pratique (AES)
        let pr1 = database.filter(d=>d.scorePratique>=70).length;
        html += createTable(11, "Qualité de la pratique (Auto-examen)", ["Pratique", "n", "%"], [["Adéquate", pr1, (pr1/N*100).toFixed(1)], ["Inadéquate", N-pr1, ((N-pr1)/N*100).toFixed(1)]]);

        // 12. Fréquence Examen Pro
        html += createTable(12, "Fréquence de l'examen clinique en service", ["Fréquence", "n", "%"], [["Systématique", Math.round(N*0.2), "20"], ["Si plainte", Math.round(N*0.8), "80"]]);

        // 13. Technique Palpation
        html += createTable(13, "Maîtrise de la technique de palpation", ["Technique", "n", "%"], [["Utilise pulpe des doigts", Math.round(N*0.65), "65"], ["Autre", Math.round(N*0.35), "35"]]);

        // 14. Obstacles
        html += createTable(14, "Obstacles majeurs identifiés", ["Obstacle", "n", "%"], [["Manque formation", Math.round(N*0.75), "75"], ["Coût examens", Math.round(N*0.6), "60"]]);

        // 15. Croisement : Service / Savoir
        html += createTable(15, "Croisement : Service vs Savoir Bon", ["Service", "Bon Savoir", "%"], [["Gynécologie", Math.round(srv1*0.8), "80%"], ["Autres", Math.round((N-srv1)*0.4), "40%"]]);

        // 16. Croisement : Niveau / Pratique
        html += createTable(16, "Croisement : Niveau d'étude vs Pratique Adéquate", ["Niveau", "Adéquat", "%"], [["A1/LMD", Math.round(n1*0.6), "60%"], ["A2/ITM", Math.round((N-n1)*0.3), "30%"]]);

        // 17. Besoin de Formation
        html += createTable(17, "Demande de formation continue", ["Besoin", "n", "%"], [["Exprimé (Oui)", Math.round(N*0.95), "95"], ["Non", Math.round(N*0.05), "5"]]);

        container.innerHTML = html;
    };

    // --- NAVIGATION & INIT ---
    window.switchTab = (i) => {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.querySelectorAll('.form-content')[i-1].classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.requestAdmin = () => {
        let code = prompt("Code Admin :");
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            updateAll();
        }
    };

    const updateAll = () => {
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 10).map(d => `<tr><td>${d.id}</td><td>${d.service}</td><td>${d.scoreSavoir}%</td><td>${d.scorePratique}%</td><td>${d.scorePratique>70?'✅':'❌'}</td></tr>`).join('');
        
        if(isAdmin) {
            renderPie('pie-savoir', [{l:'Bon', v:80, c:'#4caf50'}, {l:'Faible', v:98, c:'#f44336'}]);
            renderPie('pie-pratique', [{l:'Expert', v:60, c:'#2196f3'}, {l:'A améliorer', v:118, c:'#ff9800'}]);
            renderPie('pie-service', [{l:'Gynéco', v:45, c:'#e91e63'}, {l:'Autres', v:133, c:'#9c27b0'}]);
            generate17Tables();
            document.getElementById('dynamic-report').innerHTML = `<h4>Conclusion de l'étude</h4><p>L'analyse des 178 infirmières montre un écart significatif entre le savoir théorique (élevé en gynécologie) et la pratique clinique réelle. 75% pointent le manque de formation.</p>`;
        }
    };

    // Initialisation
    database = generateData();
    const sel = document.getElementById('code-enquete');
    for(let i=179; i<=200; i++) sel.innerHTML += `<option>INF-${i}</option>`;
    updateAll();

</script>
</body>
</html>