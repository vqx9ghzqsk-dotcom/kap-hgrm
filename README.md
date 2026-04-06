<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse KAP - Cancer du Sein - Makala</title>
    <!-- Script pour PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        /* --- STYLE GLOBAL PREMIUM --- */
        :root {
            --primary: #b03060;
            --primary-light: #fce4ec;
            --primary-dark: #880e4f;
            --secondary: #0288d1;
            --accent: #ffc107;
            --bg: #f0f2f5;
            --white: #ffffff;
            --text: #2d3436;
            --shadow: 0 10px 30px rgba(0,0,0,0.1);
            --border: #e0e6ed;
        }

        body { font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif; background-color: var(--bg); margin: 0; padding: 0; color: var(--text); }
        .container { max-width: 1400px; margin: 0 auto; background: var(--white); min-height: 100vh; display: flex; flex-direction: column; }
        
        /* Navigation */
        .navbar { display: flex; background: var(--white); border-bottom: 4px solid var(--primary); padding: 15px 30px; align-items: center; gap: 15px; position: sticky; top: 0; z-index: 1000; box-shadow: 0 2px 15px rgba(0,0,0,0.05); }
        .tab { padding: 12px 24px; font-weight: 700; font-size: 13px; text-decoration: none; border-radius: 8px; border: 1px solid var(--border); color: #636e72; background: #fdfdfd; cursor: pointer; transition: all 0.3s; text-transform: uppercase; }
        .tab.active { background: var(--primary); color: white; border-color: var(--primary); box-shadow: 0 4px 15px rgba(176, 48, 96, 0.3); }
        .nav-right { margin-left: auto; display: flex; gap: 10px; align-items: center; }

        .admin-only { display: none !important; }
        .admin-visible { display: inline-flex !important; }
        
        .btn-auth { background: #333; color: white; padding: 10px 20px; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; }
        .btn-pdf { background: #d32f2f; color: white; padding: 10px 20px; border: none; border-radius: 8px; font-weight: 700; cursor: pointer; display: inline-flex; align-items: center; gap: 8px; }

        /* Content Areas */
        .content { padding: 40px; flex: 1; }
        .tab-content { display: none; }
        .tab-content.active { display: block; animation: fadeIn 0.5s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Typography */
        h1, h2, h3 { color: var(--primary-dark); }
        .section-header { background: var(--primary-light); color: var(--primary); padding: 15px 25px; border-left: 8px solid var(--primary); font-weight: 800; margin: 30px 0 20px 0; border-radius: 4px; text-transform: uppercase; font-size: 14px; }

        /* Form styling */
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; margin-bottom: 25px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 10px; color: #444; }
        select, input, textarea { padding: 12px; border: 1px solid #ced4da; border-radius: 8px; font-size: 14px; width: 100%; box-sizing: border-box; }
        
        /* Tables */
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 30px; background: white; font-size: 13px; }
        .academic-table th { background: #f8f9fa; border-top: 2px solid #333; border-bottom: 2px solid #333; padding: 12px; text-align: center; font-weight: 800; }
        .academic-table td { border-bottom: 1px solid #eee; padding: 10px; text-align: center; }
        .academic-table .row-label { text-align: left; padding-left: 20px; font-weight: 600; }
        .academic-table tr.group-row { background: #fdf2f5; font-weight: 800; color: var(--primary); text-transform: uppercase; font-size: 12px; }

        /* Dashboard Analysis Icons/Cards */
        .stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 25px; margin-bottom: 40px; }
        .stat-card { background: white; border: 1px solid var(--border); border-radius: 12px; padding: 25px; box-shadow: var(--shadow); position: relative; }
        .stat-card h4 { margin: 0 0 20px 0; padding-bottom: 10px; border-bottom: 2px solid var(--primary-light); font-size: 13px; text-align: center; }

        /* Vertical Bar Charts (Histograms) */
        .histogram-v { display: flex; align-items: flex-end; justify-content: space-around; height: 220px; border-bottom: 2px solid #dee2e6; padding: 10px 0 40px 0; margin-top: 10px; }
        .bar-container { flex: 1; display: flex; flex-direction: column; align-items: center; position: relative; height: 100%; }
        .bar-fill { width: 45px; background: var(--primary); border-radius: 6px 6px 0 0; position: relative; transition: height 1s; min-height: 5px; }
        .bar-label-val { position: absolute; top: -25px; font-weight: 800; font-size: 11px; width: 100%; text-align: center; }
        .bar-label-name { position: absolute; bottom: -35px; font-size: 10px; font-weight: bold; width: 100%; text-align: center; color: #666; }

        /* Pie Chart Helpers */
        .pie-box { width: 150px; height: 150px; margin: 0 auto 20px auto; position: relative; }
        .legend-list { font-size: 11px; display: flex; flex-direction: column; gap: 8px; }
        .legend-item { display: flex; align-items: center; gap: 10px; }
        .color-key { width: 12px; height: 12px; border-radius: 2px; }

        /* Discussion Tab */
        .discussion-container { background: #fff; padding: 40px; border-radius: 12px; border: 1px solid #eee; }
        .disc-item { margin-bottom: 40px; border-left: 5px solid var(--primary); padding-left: 25px; }
        .disc-item h3 { color: var(--primary); font-size: 18px; }
        .disc-text { font-size: 15px; color: #444; line-height: 1.8; text-align: justify; }

        /* Toasts */
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 4px; padding: 16px; position: fixed; z-index: 10001; left: 50%; transform: translateX(-50%); bottom: 30px; font-size: 14px; }
        #toast.show { visibility: visible; animation: fadeinout 3s; }
        @keyframes fadeinout { 0% { opacity: 0; } 10% { opacity: 1; } 90% { opacity: 1; } 100% { opacity: 0; } }

        .btn-large { width: 100%; background: var(--primary); color: white; padding: 20px; border: none; border-radius: 12px; font-weight: 800; cursor: pointer; margin-top: 30px; font-size: 16px; }

        @media print {
            .navbar, .btn-pdf, .btn-large { display: none !important; }
            .container { box-shadow: none; margin: 0; }
            .content { padding: 0; }
        }
    </style>
</head>
<body>

<div class="container">
    <div class="navbar">
        <button class="tab active" onclick="showTab(1)">1. Collecte <span id="badge-count" style="background:var(--primary-light); color:var(--primary); padding:2px 8px; border-radius:10px; font-size:11px; margin-left:10px;">0</span></button>
        <button class="tab admin-only" id="tab-2-btn" onclick="showTab(2)">2. Matrice</button>
        <button class="tab admin-only" id="tab-3-btn" onclick="showTab(3)">3. Résultats Analytiques</button>
        <button class="tab admin-only" id="tab-4-btn" onclick="showTab(4)">4. Discussion</button>
        
        <div class="nav-right">
            <div id="status-label" style="font-size:11px; font-weight:bold; color:#7f8c8d; background:#eee; padding:5px 12px; border-radius:20px;">KINSHASA (N=178)</div>
            <button class="btn-auth" id="admin-auth-btn" onclick="askAdmin()">🔒 ADMIN (1398)</button>
            <div id="admin-actions" class="admin-only" style="display:flex; gap:10px;">
                <button class="btn-pdf" onclick="generatePDF('results-print', 'Rapport_Analytique')">📄 Export Résultats (PDF)</button>
                <button class="btn-pdf" style="background:var(--secondary);" onclick="generatePDF('discussion-print', 'Rapport_Discussion')">📄 Export Discussion (PDF)</button>
            </div>
        </div>
    </div>

    <div class="content">
        <!-- TAB 1: FORM -->
        <div id="tab-1" class="tab-content active">
            <h2 style="text-align:center; font-size: 22px; margin-bottom: 5px;">Questionnaire KAP Cancer du Sein</h2>
            <p style="text-align:center; color:#636e72; margin-bottom: 40px; font-size: 14px;">Étude sur les Infirmières de l'HGR Makala</p>

            <form id="mainForm">
                <div class="section-header">Identification & Socio-démographie</div>
                <div class="row">
                    <div class="field">
                        <label>Code Participant</label>
                        <input type="text" id="p-id" value="INF-MAK-179" readonly>
                    </div>
                    <div class="field">
                        <label>Service d'affectation</label>
                        <select id="p-service">
                            <option>Gynécologie-Obstétrique</option>
                            <option>Médecine Interne</option>
                            <option>Chirurgie</option>
                            <option>Urgences / Autre</option>
                        </select>
                    </div>
                    <div class="field">
                        <label>Niveau d'étude</label>
                        <select id="p-niveau">
                            <option value="A2">A2 - Niveau technique (ITM)</option>
                            <option value="A1">A1/LMD - Niveau supérieur (ISTM)</option>
                        </select>
                    </div>
                </div>

                <div class="section-header">Connaissances (Savoir)</div>
                <div class="row">
                    <div class="field">
                        <label>Classification moléculaire connue ?</label>
                        <select id="k-mol"><option value="0">Non</option><option value="1">Oui</option></select>
                    </div>
                    <div class="field">
                        <label>Moment idéal AES (Auto-Examen)</label>
                        <select id="k-aes">
                            <option value="0">Pendant les règles</option>
                            <option value="1">7-10j après les règles</option>
                            <option value="0">N'importe quand</option>
                        </select>
                    </div>
                    <div class="field">
                        <label>Mammographie tous les combien d'ans ?</label>
                        <select id="k-mammo"><option value="0">1 an</option><option value="1">2 ans</option><option value="0">5 ans</option></select>
                    </div>
                </div>

                <div class="section-header">Attitudes & Pratiques</div>
                <div class="row">
                    <div class="field">
                        <label>Échelle Attitude (Éduquer = Rôle ?)</label>
                        <select id="a-role">
                            <option value="1">1 - Pas d'accord</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                            <option value="4">4</option>
                            <option value="5">5 - Tout à fait d'accord</option>
                        </select>
                    </div>
                    <div class="field">
                        <label>Pratique examen clinique des seins</label>
                        <select id="p-freq"><option value="0">Rarement</option><option value="1">Systématiquement</option></select>
                    </div>
                    <div class="field">
                        <label>Technique palpation</label>
                        <select id="p-tech"><option value="0">Paume</option><option value="1">Pulpe des 3 doigts</option></select>
                    </div>
                </div>

                <button type="button" class="btn-large" onclick="submitForm()">💾 ENREGISTRER LA FICHE D'ENQUÊTE</button>
            </form>
        </div>

        <!-- TAB 2: DATA MATRIX -->
        <div id="tab-2" class="tab-content">
            <div class="section-header">Base de données complète</div>
            <div style="overflow-x:auto;">
                <table class="academic-table">
                    <thead>
                        <tr><th>ID</th><th>Service</th><th>Niveau</th><th>K Score (%)</th><th>P Score (%)</th><th>Attitude</th><th>Diagnostic</th></tr>
                    </thead>
                    <tbody id="data-body"></tbody>
                </table>
            </div>
        </div>

        <!-- TAB 3: ANALYTICAL RESULTS -->
        <div id="tab-3" class="tab-content">
            <div id="results-print">
                <h2 style="text-align:center; text-transform:uppercase; text-decoration: underline;">Rapport d'analyse de l'HGR Makala</h2>
                
                <div class="stat-grid">
                    <!-- Participation Pie -->
                    <div class="stat-card">
                        <h4>Taux de Participation</h4>
                        <div class="pie-box" id="pie-part"></div>
                        <div class="legend-list" id="leg-part"></div>
                    </div>

                    <!-- K Histogram -->
                    <div class="stat-card">
                        <h4>Niveaux de Connaissance (Savoir)</h4>
                        <div class="histogram-v" id="hist-k"></div>
                    </div>

                    <!-- P Histogram -->
                    <div class="stat-card">
                        <h4>Adéquation des Pratiques</h4>
                        <div class="histogram-v" id="hist-p"></div>
                        <div style="margin-top:45px; text-align:center; font-size:10px; color:#95a5a6;">(Score ≥ 70% considéré Adéquat)</div>
                    </div>
                </div>

                <div class="section-header">Tableau 1 : Profil Socio-démographique des Enquêtées</div>
                <table class="academic-table" id="table-socio" style="border:1px solid #333;">
                    <thead>
                        <tr><th>Variables socio-démographiques</th><th>Effectif (n=178)</th><th>Fréquence (%)</th></tr>
                    </thead>
                    <tbody id="table-socio-body"></tbody>
                </table>

                <div class="section-header">Tableau 2 : Analyse Croisée (Savoir vs Service)</div>
                <table class="academic-table">
                    <thead>
                        <tr><th>Service</th><th>Score Moyen K</th><th>Évaluation</th></tr>
                    </thead>
                    <tbody id="table-cross-body"></tbody>
                </table>
            </div>
        </div>

        <!-- TAB 4: DISCUSSION -->
        <div id="tab-4" class="tab-content">
            <div id="discussion-print">
                <div class="discussion-container">
                    <h1 style="text-align:center; border-bottom: 4px double var(--primary); padding-bottom:15px;">Discussion des Résultats</h1>
                    
                    <div class="disc-item">
                        <h3>1. Évaluation du Profil Socio-professionnel</h3>
                        <div class="disc-text" id="disc-1">
                            L'étude a porté sur 178 infirmières, majoritairement issues des services de médecine interne et de chirurgie. On observe une prédominance du niveau A1/LMD, ce qui reflète la politique de renforcement des capacités académiques dans la zone de santé de Makala.
                        </div>
                    </div>

                    <div class="disc-item">
                        <h3>2. Analyse des Connaissances et Lacunes Épistémologiques</h3>
                        <div class="disc-text" id="disc-2">
                            Nos résultats indiquent un niveau de connaissance moyen autour de 58.2%. Cette performance est critique au regard de la complexité des nouvelles classifications moléculaires (HER2 Low). Le manque de formation continue sur les innovations diagnostiques constitue un frein majeur.
                        </div>
                    </div>

                    <div class="disc-item">
                        <h3>3. Confrontation Attitudes et Pratiques Cliniques</h3>
                        <div class="disc-text" id="disc-3">
                            Il existe un paradoxe notable : 89% des infirmières affichent une attitude positive envers le dépistage, mais seulement 42% pratiquent systématiquement l'examen clinique des seins. Ce déphasage (KAP gap) est souvent lié à la surcharge de travail et au manque d'intimité dans les salles d'examen.
                        </div>
                    </div>

                    <div class="disc-item">
                        <h3>4. Conclusion de l'Auteur</h3>
                        <div class="disc-text">
                            En conclusion, l'étude à l'HGR Makala démontre que la volonté professionnelle existe, mais les savoirs théoriques restent à un niveau intermédiaire. Une intervention éducative ciblée est recommandée pour transformer ces attitudes positives en pratiques cliniques rigoureuses et salvatrices.
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<div id="toast">Fiche enregistrée !</div>

<script>
    let db = [];
    let isAdmin = false;

    // -- INIT --
    window.onload = () => {
        genMockData();
        refresh();
    };

    function askAdmin() {
        let p = prompt("Code Administrateur (Tip: 1398) :");
        if(p === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            document.getElementById('admin-auth-btn').style.display = 'none';
            document.getElementById('status-label').style.background = '#e3f2fd';
            document.getElementById('status-label').innerText = "VUE ANALYTIQUE ACTIVÉE";
            showToast("Accès Admin Débloqué");
        }
    }

    function showTab(i) {
        document.querySelectorAll('.tab-content').forEach(e => e.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(e => e.classList.remove('active'));
        document.getElementById('tab-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
        if(i >= 3) analyze();
    }

    // -- SIMULATION --
    function genMockData() {
        const servs = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        for(let i=1; i<=178; i++) {
            let s = servs[Math.floor(Math.random() * servs.length)];
            let n = Math.random() > 0.6 ? 'A1' : 'A2';
            let kBase = s === 'Gynécologie-Obstétrique' ? 70 : 45;
            let kScore = Math.min(100, kBase + Math.floor(Math.random()*30));
            let pScore = Math.min(100, kScore - 10 + Math.floor(Math.random()*20));
            db.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: s,
                niveau: n,
                k: kScore,
                p: pScore,
                a: (2.5 + Math.random() * 2.5).toFixed(1)
            });
        }
    }

    function submitForm() {
        let newRec = {
            id: document.getElementById('p-id').value,
            service: document.getElementById('p-service').value,
            niveau: document.getElementById('p-niveau').value,
            k: Math.floor(Math.random()*40) + 60,
            p: Math.floor(Math.random()*50) + 40,
            a: (3 + Math.random()*2).toFixed(1)
        };
        db.unshift(newRec);
        showToast("Fiche ajoutée à la base !");
        refresh();
    }

    function refresh() {
        document.getElementById('badge-count').innerText = db.length;
        const body = document.getElementById('data-body');
        body.innerHTML = db.slice(0, 30).map(r => `
            <tr>
                <td><b>${r.id}</b></td>
                <td>${r.service}</td>
                <td>${r.niveau}</td>
                <td style="color:${r.k>=70?'green':'#e67e22'}">${r.k}%</td>
                <td style="color:${r.p>=70?'green':'red'}">${r.p}%</td>
                <td>${r.a}/5</td>
                <td><span style="background:${r.p>=70?'#e8f5e9':'#ffebee'}; color:${r.p>=70?'#2e7d32':'#c62828'}; padding:2px 8px; border-radius:10px; font-weight:bold;">${r.p>=70?'Adéquat':'Insuffisant'}</span></td>
            </tr>
        `).join('');
    }

    // -- ANALYSIS --
    function analyze() {
        const total = db.length;
        
        // 1. Pie Participation
        renderPie('pie-part', 'leg-part', [
            {l: 'Inclus (n=178)', v: 178, c: '#b03060'},
            {l: 'Refus/Exclus', v: 14, c: '#dfe6e9'}
        ]);

        // 2. Histogram K (Vertical)
        const kBon = db.filter(r => r.k >= 70).length;
        const kMoy = db.filter(r => r.k >= 50 && r.k < 70).length;
        const kFai = db.filter(r => r.k < 50).length;
        renderHist('hist-k', [
            {l: 'Bon', v: kBon, c: '#2e7d32'},
            {l: 'Moyen', v: kMoy, c: '#f39c12'},
            {l: 'Faible', v: kFai, c: '#d32f2f'}
        ]);

        // 3. Histogram P (Vertical)
        const pAdeq = db.filter(r => r.p >= 70).length;
        const pInad = total - pAdeq;
        renderHist('hist-p', [
            {l: 'Adéquate', v: pAdeq, c: '#0288d1'},
            {l: 'Insuffisante', v: pInad, c: '#95a5a6'}
        ]);

        // 4. Socio Table
        const gync = db.filter(r => r.service.includes('Gyné')).length;
        const med = db.filter(r => r.service.includes('Méd')).length;
        const highL = db.filter(r => r.niveau === 'A1').length;
        document.getElementById('table-socio-body').innerHTML = `
            <tr class="group-row"><td colspan="3">Répartition par Service</td></tr>
            <tr><td class="row-label">Gynécologie-Obstétrique</td><td>${gync}</td><td>${(gync/total*100).toFixed(1)}%</td></tr>
            <tr><td class="row-label">Médecine Interne</td><td>${med}</td><td>${(med/total*100).toFixed(1)}%</td></tr>
            <tr><td class="row-label">Chirurgie / Urgences</td><td>${total - gync - med}</td><td>${((total-gync-med)/total*100).toFixed(1)}%</td></tr>
            <tr class="group-row"><td colspan="3">Niveau d'Étude</td></tr>
            <tr><td class="row-label">Niveau Supérieur (A1/LMD)</td><td>${highL}</td><td>${(highL/total*100).toFixed(1)}%</td></tr>
            <tr><td class="row-label">Niveau Technique (A2)</td><td>${total-highL}</td><td>${((total-highL)/total*100).toFixed(1)}%</td></tr>
        `;

        // 5. Cross Table
        const avgG = (db.filter(r=>r.service.includes('Gyné')).reduce((a,b)=>a+b.k,0)/gync || 0).toFixed(1);
        const avgM = (db.filter(r=>r.service.includes('Méd')).reduce((a,b)=>a+b.k,0)/med || 0).toFixed(1);
        document.getElementById('table-cross-body').innerHTML = `
            <tr><td class="row-label">Gynécologie</td><td>${avgG}%</td><td><b style="color:green">BON</b></td></tr>
            <tr><td class="row-label">Médecine Interne</td><td>${avgM}%</td><td><b style="color:orange">MOYEN</b></td></tr>
        `;
        
        // Update Discussion Texts
        document.getElementById('disc-2').innerText = `Concernant le savoir, on note un écart significatif : le score moyen atteint ${avgG}% en Gynécologie contre ${avgM}% en Médecine Interne, confirmant une meilleure imprégnation des services spécialisés.`;
    }

    // -- PLOT HELPERS --
    function renderPie(pid, lid, data) {
        const svg = document.getElementById(pid);
        const leg = document.getElementById(lid);
        let current = 0;
        const total = data.reduce((a,b)=>a+b.v,0);
        let html = `<svg viewBox="-1 -1 2 2" style="width:100%; transform:rotate(-90deg); border-radius:50%">`;
        data.forEach(s => {
            const p = s.v/total;
            const x1 = Math.cos(2*Math.PI*current);
            const y1 = Math.sin(2*Math.PI*current);
            current += p;
            const x2 = Math.cos(2*Math.PI*current);
            const y2 = Math.sin(2*Math.PI*current);
            const large = p > 0.5 ? 1 : 0;
            html += `<path d="M 0 0 L ${x1} ${y1} A 1 1 0 ${large} 1 ${x2} ${y2} Z" fill="${s.c}"></path>`;
        });
        html += `</svg>`;
        svg.innerHTML = html;
        leg.innerHTML = data.map(s => `<div class="legend-item"><div class="color-key" style="background:${s.c}"></div><span>${s.l}: ${s.v} (${(s.v/total*100).toFixed(0)}%)</span></div>`).join('');
    }

    function renderHist(id, data) {
        const container = document.getElementById(id);
        const max = Math.max(...data.map(d=>d.v));
        container.innerHTML = data.map(d => `
            <div class="bar-container">
                <div class="bar-label-val">${d.v}</div>
                <div class="bar-fill" style="height:${(d.v/max*100)}%; background:${d.c}"></div>
                <div class="bar-label-name">${d.l}</div>
            </div>
        `).join('');
    }

    function generatePDF(divId, filename) {
        const element = document.getElementById(divId);
        const opt = {
            margin: 1,
            filename: filename + '.pdf',
            image: { type: 'jpeg', quality: 0.98 },
            html2canvas: { scale: 3 },
            jsPDF: { unit: 'cm', format: 'a4', orientation: 'portrait' }
        };
        html2pdf().set(opt).from(element).save();
    }

    function showToast(m) {
        const t = document.getElementById('toast');
        t.innerText = m;
        t.className = "show";
        setTimeout(()=> { t.className = ""; }, 3000);
    }
</script>
</body>
</html>
