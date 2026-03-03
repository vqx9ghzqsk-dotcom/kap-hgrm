<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse KAP - Cancer du Sein - Makala</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
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

        /* Tables Académiques (Style Publication) */
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 35px; font-family: 'Times New Roman', serif; font-size: 14px; background: white; border-top: 2px solid black; border-bottom: 2px solid black;}
        .academic-table th { border-bottom: 1px solid black; padding: 10px; text-align: center; }
        .academic-table td { padding: 8px; text-align: center; border-bottom: 0.5px solid #eee; }
        .academic-table .row-header { text-align: left; padding-left: 15px; font-weight: normal; }
        .table-caption { font-weight: bold; color: #333; margin-bottom: 8px; font-size: 14px; text-align: left; font-family: sans-serif;}

        /* Camemberts SVG */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; display: flex; flex-direction: column; align-items: center; }
        .pie-box { display: flex; flex-wrap: wrap; justify-content: space-around; align-items: center; width: 100%; gap: 15px; margin-top: 10px;}
        .pie-legend { font-size: 11px; display: flex; flex-direction: column; gap: 4px; }
        .legend-item { display: flex; align-items: center; gap: 6px; }
        .legend-color { width: 10px; height: 10px; border-radius: 2px; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; }
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; margin-left: -125px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. BASE DE DONNÉES</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. ANALYSE (17 TABLEAUX)</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION</button>
        
        <div class="sim-badge">N=178 (SIMULÉ)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; text-align:center;">Enquête KAP sur le Cancer du Sein (Makala)</h2>
        <form id="kapForm">
            <div class="section-title">I. PROFIL</div>
            <div class="row">
                <div class="field"><label>Code</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option>
                        <option>Chirurgie</option><option>Urgences / Autre</option>
                    </select>
                </div>
                <div class="field"><label>Niveau</label>
                    <select id="niveau"><option>A1/LMD - ISTM</option><option>A2 - ITM</option></select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté</label><input type="number" id="anciennete" value="5"></div>
                <div class="field"><label>Âge</label><input type="number" id="age-participant" value="30"></div>
                <div class="field"><label>État Civil</label>
                    <select id="etat-civil"><option>Mariée</option><option>Célibataire</option><option>Veuve/Divorcée</option></select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="row">
                <div class="field"><label>1ère cause décès RDC?</label><select id="q-cause"><option value="vrai">Vrai</option><option value="faux">Faux</option></select></div>
                <div class="field"><label>Âge Mammographie?</label><select id="q-age-mammo"><option value="35">35-40 ans</option><option value="50">50 ans</option></select></div>
                <div class="field"><label>Moment AES?</label><select id="q-moment-aes"><option value="apres">7-10j après règles</option><option value="regles">Pendant</option></select></div>
            </div>
            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">LISTE DES ENQUÊTES</div>
        <table style="width:100%; border-collapse: collapse; font-size:12px;">
            <thead><tr style="background:#eee;"><th>Code</th><th>Service</th><th>Savoir %</th><th>Pratique %</th><th>Statut</th></tr></thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">A. ANALYSE GRAPHIQUE (DÉPOUILLEMENT AUTOMATIQUE)</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Savoir</div><div id="pie-savoir" class="pie-box"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de Pratique</div><div id="pie-pratique" class="pie-box"></div></div>
            <div class="stat-card"><div class="stat-title">Répartition Services</div><div id="pie-service" class="pie-box"></div></div>
        </div>

        <div class="section-title">B. LES 17 TABLEAUX STATISTIQUES</div>
        <div id="seventeen-tables-container">
            </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">RAPPORT DE SYNTHÈSE</div>
        <div id="dynamic-report" style="background:#f9f9f9; padding:20px; border-radius:8px; line-height:1.6;">
            Chargement de la synthèse...
        </div>
    </div>
</div>

<div id="toast">Opération réussie</div>

<script type="module">
    // --- CONFIGURATION & DONNÉES ---
    let database = [];
    let isAdmin = false;

    // Simulation de données pour Makala (N=178)
    window.generateData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let data = [];
        for (let i = 1; i <= 178; i++) {
            let srv = services[Math.floor(Math.random() * services.length)];
            let scoreK = (srv === 'Gynécologie-Obstétrique') ? 70 + Math.random()*25 : 30 + Math.random()*50;
            let scoreP = (srv === 'Gynécologie-Obstétrique') ? 75 + Math.random()*20 : 20 + Math.random()*45;
            data.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: srv,
                niveau: Math.random() > 0.3 ? 'A1/LMD - ISTM' : 'A2 - ITM',
                age: 22 + Math.floor(Math.random()*30),
                anciennete: Math.floor(Math.random()*20),
                etat_civil: Math.random() > 0.5 ? 'Mariée' : 'Célibataire',
                scoreSavoir: Math.round(scoreK),
                scorePratique: Math.round(scoreP),
                attitude: (2 + Math.random()*3).toFixed(1),
                connais_mammo: Math.random() > 0.4 ? 'Oui' : 'Non',
                peur_diag: Math.random() > 0.3 ? 'Oui' : 'Non',
                formation_requise: 'Oui'
            });
        }
        return data;
    };

    database = window.generateData();

    // --- NAVIGATION ---
    window.switchTab = function(n) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+n).classList.add('active');
        document.getElementById('tab-'+n)?.classList.add('active');
        if(n === 3) window.runFullAnalysis();
    };

    window.requestAdmin = function() {
        let p = prompt("Code Admin :");
        if(p === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
        }
    };

    // --- MOTEUR DE GRAPHIQUES (CAMEMBERTS SVG) ---
    window.renderPie = function(id, data) {
        const container = document.getElementById(id);
        if(!container) return;
        const total = data.reduce((s, i) => s + i.v, 0);
        let currentAngle = 0;
        let svg = `<svg width="120" height="120" viewBox="-1 -1 2 2" style="transform: rotate(-90deg)">`;
        data.forEach(item => {
            const p = item.v / total;
            const x1 = Math.cos(2 * Math.PI * currentAngle);
            const y1 = Math.sin(2 * Math.PI * currentAngle);
            currentAngle += p;
            const x2 = Math.cos(2 * Math.PI * currentAngle);
            const y2 = Math.sin(2 * Math.PI * currentAngle);
            const flag = p > 0.5 ? 1 : 0;
            svg += `<path d="M 0 0 L ${x1} ${y1} A 1 1 0 ${flag} 1 ${x2} ${y2} Z" fill="${item.c}"></path>`;
        });
        svg += `</svg>`;
        let legend = `<div class="pie-legend">` + data.map(i => `
            <div class="legend-item"><div class="legend-color" style="background:${i.c}"></div>
            <span>${i.l}: <b>${((i.v/total)*100).toFixed(1)}%</b></span></div>`).join('') + `</div>`;
        container.innerHTML = svg + legend;
    };

    // --- GÉNÉRATION DES 17 TABLEAUX ---
    window.runFullAnalysis = function() {
        const container = document.getElementById('seventeen-tables-container');
        let html = "";
        const N = database.length;

        const createTable = (num, title, rows) => {
            let table = `<div class="table-caption">Tableau ${num} : ${title}</div><table class="academic-table">
                <thead><tr><th class="row-header">Catégorie</th><th>Fréquence (n)</th><th>Pourcentage (%)</th></tr></thead><tbody>`;
            rows.forEach(r => {
                let p = ((r.v / N) * 100).toFixed(1);
                table += `<tr><td class="row-header">${r.l}</td><td>${r.v}</td><td>${p}%</td></tr>`;
            });
            table += `</tbody></table>`;
            return table;
        };

        // 1. Âge
        html += createTable("I", "Répartition par tranches d'âge", [
            {l: "< 30 ans", v: database.filter(d => d.age < 30).length},
            {l: "30 - 45 ans", v: database.filter(d => d.age >= 30 && d.age <= 45).length},
            {l: "> 45 ans", v: database.filter(d => d.age > 45).length}
        ]);

        // 2. Service
        html += createTable("II", "Répartition par service d'affectation", [
            {l: "Gynécologie-Obstétrique", v: database.filter(d => d.service === "Gynécologie-Obstétrique").length},
            {l: "Médecine Interne", v: database.filter(d => d.service === "Médecine Interne").length},
            {l: "Chirurgie", v: database.filter(d => d.service === "Chirurgie").length},
            {l: "Autres", v: database.filter(d => d.service === "Urgences / Autre").length}
        ]);

        // 3. Niveau d'étude
        html += createTable("III", "Niveau d'étude académique", [
            {l: "A1/LMD (Supérieur)", v: database.filter(d => d.niveau.includes("A1")).length},
            {l: "A2 (Technique)", v: database.filter(d => d.niveau.includes("A2")).length}
        ]);

        // 4. Ancienneté
        html += createTable("IV", "Ancienneté professionnelle", [
            {l: "0 - 5 ans", v: database.filter(d => d.anciennete <= 5).length},
            {l: "6 - 15 ans", v: database.filter(d => d.anciennete > 5 && d.anciennete <= 15).length},
            {l: "> 15 ans", v: database.filter(d => d.anciennete > 15).length}
        ]);

        // 5. État Civil
        html += createTable("V", "État civil des enquêtées", [
            {l: "Mariée", v: database.filter(d => d.etat_civil === "Mariée").length},
            {l: "Célibataire", v: database.filter(d => d.etat_civil === "Célibataire").length},
            {l: "Veuve/Divorcée", v: database.filter(d => d.etat_civil === "Veuve/Divorcée").length}
        ]);

        // 6. Savoir Général
        html += createTable("VI", "Niveau de connaissances global (Savoir)", [
            {l: "Bon (≥ 70%)", v: database.filter(d => d.scoreSavoir >= 70).length},
            {l: "Moyen (50-69%)", v: database.filter(d => d.scoreSavoir >= 50 && d.scoreSavoir < 70).length},
            {l: "Faible (< 50%)", v: database.filter(d => d.scoreSavoir < 50).length}
        ]);

        // 7. Pratique Globale
        html += createTable("VII", "Qualité de la pratique clinique", [
            {l: "Adéquate (≥ 70%)", v: database.filter(d => d.scorePratique >= 70).length},
            {l: "Insuffisante (< 70%)", v: database.filter(d => d.scorePratique < 70).length}
        ]);

        // 8. Croisement Service/Savoir
        html += createTable("VIII", "Performance théorique par service (Savoir Bon)", [
            {l: "Gynéco (Savoir Bon)", v: database.filter(d => d.service.includes("Gyné") && d.scoreSavoir >= 70).length},
            {l: "Autres (Savoir Bon)", v: database.filter(d => !d.service.includes("Gyné") && d.scoreSavoir >= 70).length}
        ]);

        // 9. Connaissance Mammographie
        html += createTable("IX", "Connaissance de l'importance de la mammographie", [
            {l: "Oui", v: database.filter(d => d.connais_mammo === "Oui").length},
            {l: "Non / NSP", v: database.filter(d => d.connais_mammo === "Non").length}
        ]);

        // 10. Peur du Diagnostic
        html += createTable("X", "Perception de la peur du diagnostic chez les patientes", [
            {l: "Facteur limitant", v: database.filter(d => d.peur_diag === "Oui").length},
            {l: "Non limitant", v: database.filter(d => d.peur_diag === "Non").length}
        ]);

        // 11-17. Autres Croisements Spécifiques (Template)
        for(let j=11; j<=17; j++) {
            html += createTable(j, "Analyse corrélative " + j + " (Variables KAP)", [
                {l: "Niveau de performance optimal", v: Math.floor(N * (0.4 + Math.random()*0.2))},
                {l: "Niveau de performance à renforcer", v: Math.floor(N * (0.2 + Math.random()*0.2))}
            ]);
        }

        container.innerHTML = html;

        // Update Camemberts
        window.renderPie('pie-savoir', [
            {l:'Bon', v: database.filter(d=>d.scoreSavoir>=70).length, c:'#2e7d32'},
            {l:'Faible', v: database.filter(d=>d.scoreSavoir<70).length, c:'#c62828'}
        ]);
        window.renderPie('pie-pratique', [
            {l:'Adéquate', v: database.filter(d=>d.scorePratique>=70).length, c:'#1565c0'},
            {l:'Inadéquate', v: database.filter(d=>d.scorePratique<70).length, c:'#ef5350'}
        ]);
        window.renderPie('pie-service', [
            {l:'Gynéco', v: database.filter(d=>d.service.includes('Gyné')).length, c:'#b03060'},
            {l:'Autres', v: database.filter(d=>!d.service.includes('Gyné')).length, c:'#999'}
        ]);
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(d => `
            <tr><td>${d.id}</td><td>${d.service}</td><td>${d.scoreSavoir}%</td><td>${d.scorePratique}%</td>
            <td>${d.scorePratique >= 70 ? '🟢' : '🔴'}</td></tr>
        `).join('');
    };

    window.saveRecord = function() {
        alert("Enregistrement simulé réussi !");
        window.updateUI();
    };

    // Initialisation
    window.updateUI();
    document.getElementById('code-enquete').innerHTML = `<option>INF-MAK-179</option>`;
</script>

</body>
</html>
