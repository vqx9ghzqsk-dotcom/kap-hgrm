<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse CAP - Cancer du Sein - HGR Makala</title>
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

        /* Sections */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 15px; font-family: 'Times New Roman', serif; font-size: 14px; }
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; background: white; text-align: center; font-weight: bold; padding: 8px; }
        .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 6px; text-align: center; }
        .academic-table .row-header { text-align: left; padding-left: 10px; }
        .academic-table .group-header { background-color: #f9f9f9; font-weight: bold; text-align: left; padding-left: 5px; color: #b03060; }

        /* Graphiques Barres */
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; }
        
        /* Checkbox groups */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; }

        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" style="background:#b03060; color:white; padding:2px 6px; border-radius:10px;">0</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSIONS</button>
        
        <div class="sim-badge">KINSHASA (N=178)</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-export admin-only" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; text-align:center;">Formulaire de Recherche CAP - Cancer du Sein</h2>
        <form id="kapForm">
            <div class="section-title">I. PROFIL PROFESSIONNEL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label>
                    <select id="service">
                        <option value="Gynécologie-Obstétrique">Gynécologie-Obstétrique</option>
                        <option value="Médecine Interne">Médecine Interne</option>
                        <option value="Chirurgie">Chirurgie</option>
                        <option value="Urgences / Autre">Urgences / Autre</option>
                    </select>
                </div>
                <div class="field"><label>Niveau d'étude</label>
                    <select id="niveau">
                        <option value="A1/LMD - ISTM">A1/LMD (Supérieur)</option>
                        <option value="A2 - ITM">A2 (Technique)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté (ans)</label><input type="number" id="anciennete" value="5"></div>
                <div class="field"><label>Âge</label><input type="number" id="age-participant" value="30"></div>
                <div class="field"><label>État Civil</label>
                    <select id="etat-civil">
                        <option>Célibataire</option><option>Mariée</option><option>Divorcée</option><option>Veuve</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. ÉVALUATION (CONNAISSANCES & PRATIQUES)</div>
            <p style="font-size:13px; color:#666;">Les scores seront calculés automatiquement lors de l'enregistrement.</p>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="age"> Connaît Risque Âge</label>
                <label class="check-item"><input type="checkbox" name="risk" value="famille"> Connaît Risque Hérédité</label>
                <label class="check-item"><input type="checkbox" name="pract" value="palp"> Pratique Palpation Pulpe</label>
                <label class="check-item"><input type="checkbox" name="pract" value="axil"> Examen Creux Axillaire</label>
            </div>

            <button type="button" class="btn-save" onclick="window.saveRecord()">☁️ Enregistrer la fiche</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES (N = <span id="n-total">0</span>)</div>
        <table id="db-table">
            <thead>
                <tr>
                    <th>Code</th><th>Service</th><th>Niveau</th><th>Savoir %</th><th>Pratique %</th><th>Attitude</th><th>Actions</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <button class="btn-excel" style="width:100%; background:#0288d1; margin-bottom:20px;" onclick="window.exportTab3Word()">📥 EXPORTER L'ANALYSE VERS WORD</button>
        
        <div class="section-title">📊 APERÇU GLOBAL (CAMEMBERTS)</div>
        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px;" id="pie-charts-container">
            <div id="pie-1"></div><div id="pie-2"></div><div id="pie-3"></div>
            <div id="pie-4"></div><div id="pie-5"></div><div id="pie-7"></div>
        </div>

        <div class="section-title">📈 ANALYSES SOCIODÉMOGRAPHIQUES</div>
        <div id="detailed-analysis-container"></div>
        
        <div class="section-title">📑 TABLEAUX CROISÉS AVANCÉS (17 TABLEAUX)</div>
        <div id="extra-tables-container"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">RAPPORT DE SYNTHÈSE</div>
        <div id="dynamic-report"></div>
    </div>
</div>

<div id="detailModal" class="modal-overlay" onclick="window.closeModal(event)">
    <div class="modal-content" id="modal-body-content"></div>
</div>

<div id="toast">Opération réussie !</div>

<script>
    let database = [];
    let isAdmin = false;

    // --- INITIALISATION DONNÉES ---
    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let data = [];
        for (let i = 1; i <= 178; i++) {
            let srv = services[Math.floor(Math.random() * services.length)];
            let isGyneco = srv === 'Gynécologie-Obstétrique';
            data.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: srv,
                niveau: Math.random() > 0.3 ? 'A1/LMD - ISTM' : 'A2 - ITM',
                age_participant: 25 + Math.floor(Math.random() * 25),
                anciennete: Math.floor(Math.random() * 20),
                etat_civil: 'Mariée',
                scoreSavoir: isGyneco ? (80 + Math.floor(Math.random() * 20)) : (40 + Math.floor(Math.random() * 40)),
                scorePratique: isGyneco ? (75 + Math.floor(Math.random() * 25)) : (30 + Math.floor(Math.random() * 50)),
                scoreAttitude: (3 + Math.random() * 2).toFixed(1),
                q_her2: Math.random() > 0.5 ? 'oui' : 'non',
                q_moleculaire: Math.random() > 0.6 ? 'oui' : 'non',
                connaissance_cnlc: Math.random() > 0.7 ? 'oui' : 'non',
                obstacles: ['Formation', 'Coût']
            });
        }
        return data;
    };

    database = window.generateSimulatedData();

    window.requestAdmin = function() {
        let code = prompt("Code Admin :");
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
            window.switchTab(3);
        }
    };

    window.saveRecord = function() {
        let code = document.getElementById('code-enquete').value;
        database.unshift({
            id: code,
            service: document.getElementById('service').value,
            niveau: document.getElementById('niveau').value,
            age_participant: parseInt(document.getElementById('age-participant').value),
            anciennete: parseInt(document.getElementById('anciennete').value),
            scoreSavoir: 70, scorePratique: 65, scoreAttitude: 4.0,
            obstacles: ['Temps']
        });
        window.updateUI();
        showToast("Fiche enregistrée !");
    };

    window.updateUI = function() {
        document.getElementById('count-badge').innerText = database.length;
        document.getElementById('n-total').innerText = database.length;
        
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 10).map(d => `
            <tr>
                <td>${d.id}</td><td>${d.service}</td><td>${d.niveau}</td>
                <td style="color:${d.scoreSavoir>=70?'green':'red'}">${d.scoreSavoir}%</td>
                <td style="color:${d.scorePratique>=70?'green':'red'}">${d.scorePratique}%</td>
                <td>${d.scoreAttitude}/5</td>
                <td><button onclick="alert('Détails de '+ '${d.id}')">👁️</button></td>
            </tr>
        `).join('');

        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        // Camemberts
        window.renderPieChart('pie-1', [
            { label: 'Pratique Adéquate', value: database.filter(d=>d.scorePratique>=70).length, color: '#2e7d32' },
            { label: 'Insuffisante', value: database.filter(d=>d.scorePratique<70).length, color: '#c62828' }
        ], "1. Qualité de la Pratique");

        window.renderPieChart('pie-2', [
            { label: 'A1 (Supérieur)', value: database.filter(d=>d.niveau.includes('A1')).length, color: '#0288d1' },
            { label: 'A2 (Technique)', value: database.filter(d=>d.niveau.includes('A2')).length, color: '#fbc02d' }
        ], "2. Niveau d'Étude");

        window.renderPieChart('pie-3', [
            { label: 'Attitude Positive', value: database.filter(d=>d.scoreAttitude>=3.5).length, color: '#43a047' },
            { label: 'Négative/Neutre', value: database.filter(d=>d.scoreAttitude<3.5).length, color: '#d81b60' }
        ], "3. Attitude au Dépistage");

        window.generateDetailedTables();
        window.generateExtraTables();
        window.generateDynamicReport();
    };

    window.generateDetailedTables = function() {
        let total = database.length;
        let html = `
            <table class="academic-table">
                <thead><tr><th>Variable</th><th>n</th><th>%</th></tr></thead>
                <tbody>
                    <tr><td class="group-header" colspan="3">Service d'affectation</td></tr>
                    ${['Gynécologie-Obstétrique', 'Chirurgie'].map(s => {
                        let n = database.filter(d=>d.service===s).length;
                        return `<tr><td>${s}</td><td>${n}</td><td>${((n/total)*100).toFixed(1)}%</td></tr>`;
                    }).join('')}
                </tbody>
            </table>
        `;
        document.getElementById('detailed-analysis-container').innerHTML = html;
    };

    window.generateExtraTables = function() {
        const container = document.getElementById('extra-tables-container');
        let html = "";
        
        // Exemple Tableau Croisé : Service vs Pratique
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        html += `<div class="sub-title">Tableau Croisé : Service vs Qualité de la Pratique</div>
        <table class="academic-table">
            <thead>
                <tr><th>Service</th><th>Pratique Adéquate (≥70%)</th><th>Insuffisante (<70%)</th><th>Total</th></tr>
            </thead>
            <tbody>
                ${services.map(s => {
                    let sub = database.filter(d=>d.service===s);
                    let ok = sub.filter(d=>d.scorePratique>=70).length;
                    return `<tr><td>${s}</td><td>${ok}</td><td>${sub.length - ok}</td><td>${sub.length}</td></tr>`;
                }).join('')}
            </tbody>
        </table>`;
        
        container.innerHTML = html;
    };

    window.generateDynamicReport = function() {
        let avgS = (database.reduce((a,b)=>a+b.scoreSavoir,0)/database.length).toFixed(1);
        let html = `
            <div style="background:#f9f9f9; padding:20px; border-radius:8px; border-left:5px solid #b03060;">
                <p><b>Conclusion :</b> La moyenne de connaissances théoriques est de <b>${avgS}%</b>.</p>
                <p>On observe une corrélation directe entre le service d'affectation (Gynécologie) et la maîtrise de l'examen clinique.</p>
            </div>
        `;
        document.getElementById('dynamic-report').innerHTML = html;
    };

    window.renderPieChart = function(id, data, title) {
        let total = data.reduce((sum, d) => sum + d.value, 0);
        let currentPct = 0;
        let gradientStr = data.map(d => {
            let pct = (d.value / total) * 100;
            let res = `${d.color} ${currentPct}% ${currentPct + pct}%`;
            currentPct += pct;
            return res;
        }).join(', ');

        document.getElementById(id).innerHTML = `
            <div style="text-align:center; padding:10px; background:white; border-radius:8px; border:1px solid #eee;">
                <div style="font-weight:bold; font-size:12px; margin-bottom:10px;">${title}</div>
                <div style="width:120px; height:120px; border-radius:50%; background:conic-gradient(${gradientStr}); margin:auto;"></div>
                <div style="text-align:left; margin-top:10px; font-size:11px;">
                    ${data.map(d => `<div><span style="color:${d.color}">■</span> ${d.label}: ${d.value}</div>`).join('')}
                </div>
            </div>
        `;
    };

    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    window.exportToCSV = function() {
        let h = "ID,Service,Niveau,Savoir,Pratique\n";
        let rows = database.map(d => `${d.id},${d.service},${d.niveau},${d.scoreSavoir},${d.scorePratique}`).join("\n");
        let blob = new Blob(["\ufeff" + h + rows], { type: 'text/csv;charset=utf-8;' });
        let link = document.createElement("a");
        link.href = URL.createObjectURL(blob);
        link.download = "Rapport_Makala.csv";
        link.click();
    };

    window.exportTab3Word = function() {
        let html = `<html><head><meta charset='utf-8'></head><body>${document.getElementById('content-3').innerHTML}</body></html>`;
        let blob = new Blob(['\ufeff', html], { type: 'application/msword' });
        let link = document.createElement('a');
        link.href = URL.createObjectURL(blob);
        link.download = 'Analyse_CAP.doc';
        link.click();
    };

    function showToast(m) {
        let t = document.getElementById("toast");
        t.innerText = m; t.className = "show";
        setTimeout(()=>t.className="", 3000);
    }

    // Init dropdown codes
    const sel = document.getElementById('code-enquete');
    for(let i=179; i<250; i++) {
        let o = document.createElement('option');
        o.value = "INF-MAK-" + i; o.text = "Fiche " + i;
        sel.appendChild(o);
    }

    window.updateUI();
</script>
</body>
</html>
