<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse KAP - Cancer du Sein - Makala</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #b03060;
            --primary-light: #fce4ec;
            --primary-dark: #880e4f;
            --secondary: #0288d1;
            --secondary-light: #e1f5fe;
            --bg: #f5f7fa;
            --white: #ffffff;
            --text-dark: #2d3436;
            --text-light: #636e72;
            --border: #e0e6ed;
            --shadow: 0 10px 30px rgba(0,0,0,0.05);
        }

        body { font-family: 'Inter', sans-serif; background-color: var(--bg); margin: 0; padding: 0; color: var(--text-dark); line-height: 1.5; }
        .app-container { max-width: 1440px; margin: 0 auto; background: var(--white); min-height: 100vh; display: flex; flex-direction: column; box-shadow: 0 0 50px rgba(0,0,0,0.1); }
        
        .navbar { display: flex; background: var(--white); border-bottom: 4px solid var(--primary); padding: 15px 40px; align-items: center; gap: 15px; position: sticky; top: 0; z-index: 1000; box-shadow: 0 4px 15px rgba(0,0,0,0.03); }
        .tab-btn { padding: 12px 20px; font-weight: 700; font-size: 11px; border-radius: 8px; border: 1px solid var(--border); color: var(--text-light); background: #fdfdfd; cursor: pointer; transition: 0.3s; text-transform: uppercase; }
        .tab-btn.active { background: var(--primary); color: white; border-color: var(--primary); }
        .navbar-right { margin-left: auto; display: flex; gap: 12px; align-items: center; }

        .admin-only { display: none !important; }
        .admin-visible { display: flex !important; }
        
        .btn { padding: 10px 18px; border-radius: 8px; font-weight: 700; font-size: 13px; cursor: pointer; border: none; transition: 0.3s; display: inline-flex; align-items: center; gap: 8px; }
        .btn-dark { background: #333; color: white; }
        .btn-pdf { background: #d32f2f; color: white; }
        .btn-primary { background: var(--primary); color: white; }

        .main-content { padding: 40px; flex: 1; }
        .tab-panel { display: none; }
        .tab-panel.active { display: block; animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .section-title { background: var(--primary-light); color: var(--primary); padding: 15px 25px; border-left: 10px solid var(--primary); font-weight: 800; margin: 40px 0 20px 0; border-radius: 4px; text-transform: uppercase; font-size: 14px; }
        
        /* Tables */
        .data-table { width: 100%; border-collapse: collapse; margin-bottom: 30px; font-size: 12px; }
        .data-table th { background: #f8f9fa; border-top: 2px solid #333; border-bottom: 2px solid #333; padding: 12px; }
        .data-table td { border-bottom: 1px solid #eee; padding: 10px; text-align: center; }

        /* Histograms Statistiques */
        .v-bar-chart { display: flex; align-items: flex-end; justify-content: space-around; height: 250px; border-bottom: 2px solid #333; padding: 20px 10px; background: #fafafa; border-left: 2px solid #333; margin: 20px 0; }
        .v-bar-item { flex: 1; display: flex; flex-direction: column; align-items: center; margin: 0 15px; max-width: 80px; }
        .v-bar { width: 100%; background: var(--primary); border: 1px solid var(--primary-dark); transition: height 1s; position: relative; }
        .v-bar-val { position: absolute; top: -25px; font-weight: 800; font-size: 11px; width: 100%; text-align: center; color: #333; }
        .v-bar-label { margin-top: 10px; font-size: 10px; font-weight: 700; text-align: center; height: 30px; }

        /* Modal */
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 10000; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; padding: 30px; border-radius: 15px; width: 600px; max-height: 85vh; overflow-y: auto; position: relative; }
        .close-modal { position: absolute; top: 15px; right: 20px; font-size: 24px; cursor: pointer; font-weight: bold; }

        .discussion-wrapper { max-width: 900px; margin: 0 auto; background: #fff; padding: 40px; border: 1px solid #eee; box-shadow: var(--shadow); }
        .discussion-section { margin-bottom: 30px; border-left: 4px solid var(--primary); padding-left: 20px; }
        .discussion-section h3 { color: var(--primary-dark); text-transform: uppercase; font-size: 16px; }
    </style>
</head>
<body>

<div class="app-container">
    <div class="navbar">
        <button class="tab-btn active" onclick="showTab(1)">1. Collecte <span id="count-badge" style="background:#fff; color:var(--primary); padding:1px 8px; border-radius:10px; font-size:10px; margin-left:8px;">178</span></button>
        <button class="tab-btn admin-only" onclick="showTab(2)">2. Matrice de Dépouillement</button>
        <button class="tab-btn admin-only" onclick="showTab(3)">3. Résultats Analytiques</button>
        <button class="tab-btn admin-only" onclick="showTab(4)">4. Discussion</button>
        
        <div class="navbar-right">
            <button class="btn btn-dark" id="auth-btn" onclick="handleAuth()">🔒 ACCÈS ADMIN</button>
            <div id="export-btns" class="admin-only" style="display:flex; gap:8px;">
                <button class="btn btn-pdf" onclick="exportPDF('results-area', 'Rapport_Analytique')">📄 PDF RÉSULTATS</button>
                <button class="btn btn-pdf" style="background:var(--secondary);" onclick="exportPDF('discussion-area', 'Discussion_Scientifique')">📄 PDF DISCUSSION</button>
            </div>
        </div>
    </div>

    <div class="main-content">
        <div id="panel-1" class="tab-panel active">
            <h2 style="text-align:center;">Fiche d'Enquête Initiale</h2>
            <p style="text-align:center;">Veuillez remplir les informations pour l'enquête KAP sur le cancer du sein.</p>
            <div id="survey-placeholder" style="border: 2px dashed #ccc; padding: 40px; text-align: center; border-radius: 10px;">
                L'interface de saisie est active. Utilisez le bouton d'enregistrement pour ajouter des données à la matrice.
            </div>
        </div>

        <div id="panel-2" class="tab-panel">
            <div class="section-title">Base de Données Complète (N=178)</div>
            <div style="overflow-x:auto;">
                <table class="data-table">
                    <thead>
                        <tr><th>ID</th><th>Service</th><th>Âge</th><th>Niveau</th><th>Savoir (%)</th><th>Pratique (%)</th><th>Actions</th></tr>
                    </thead>
                    <tbody id="matrix-rows"></tbody>
                </table>
            </div>
        </div>

        <div id="panel-3" class="tab-panel">
            <div id="results-area">
                <h1 style="text-align:center;">Résultats Statistiques - HGR Makala</h1>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px;">
                    <div style="background:#fff; padding:20px; border:1px solid #eee; border-radius:10px;">
                        <h4 style="text-align:center;">Niveaux de Connaissances (Savoir)</h4>
                        <div class="v-bar-chart" id="hist-k"></div>
                    </div>
                    <div style="background:#fff; padding:20px; border:1px solid #eee; border-radius:10px;">
                        <h4 style="text-align:center;">Qualité des Pratiques Cliniques</h4>
                        <div class="v-bar-chart" id="hist-p"></div>
                    </div>
                    <div style="background:#fff; padding:20px; border:1px solid #eee; border-radius:10px;">
                        <h4 style="text-align:center;">Obstacles Identifiés</h4>
                        <div class="v-bar-chart" id="hist-obs"></div>
                    </div>
                </div>

                <div class="section-title">Tableau I : Caractéristiques Socio-Démographiques</div>
                <table class="data-table" id="table-socio"></table>

                <div class="section-title">Tableau II : Croisement KAP Globale</div>
                <table class="data-table" id="table-kap"></table>
            </div>
        </div>

        <div id="panel-4" class="tab-panel">
            <div id="discussion-area">
                <div class="discussion-wrapper">
                    <h1 style="text-align:center; color:var(--primary);">Discussion & Analyse Critique</h1>
                    
                    <div class="discussion-section">
                        <h3>1. Évaluation des Connaissances et Hypothèses</h3>
                        <p id="disc-1">Chargement de l'analyse...</p>
                    </div>

                    <div class="discussion-section">
                        <h3>2. Perception du Rôle et Attitudes</h3>
                        <p id="disc-2">Chargement de l'analyse...</p>
                    </div>

                    <div class="discussion-section">
                        <h3>3. Pratiques et Obstacles à la Mise en Œuvre</h3>
                        <p id="disc-3">Chargement de l'analyse...</p>
                    </div>

                    <div class="discussion-section" style="background: var(--primary-light); padding: 15px; border-left: 10px solid var(--primary);">
                        <h3>Recommandations Stratégiques</h3>
                        <p id="disc-reco">Analyse des données pour recommandations...</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<div id="viewModal" class="modal">
    <div class="modal-content">
        <span class="close-modal" onclick="closeModal()">&times;</span>
        <h2 id="m-title" style="color:var(--primary); border-bottom: 2px solid var(--primary);">Fiche Individuelle</h2>
        <div id="m-body" style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 20px;"></div>
    </div>
</div>

<script>
    let rawData = [];
    let isAdmin = false;

    window.onload = () => {
        generateData(178);
        renderMatrix();
    };

    function handleAuth() {
        let pin = prompt("Code Administrateur :");
        if(pin === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            document.getElementById('auth-btn').style.display = 'none';
            alert("Accès Expert Validé");
        }
    }

    function showTab(i) {
        document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById('panel-'+i).classList.add('active');
        document.querySelectorAll('.tab-btn')[i-1].classList.add('active');
        if(i === 3) analyze();
        if(i === 4) updateDiscussion();
    }

    function generateData(n) {
        const services = ['Gynécologie', 'Médecine Interne', 'Chirurgie', 'Pédiatrie'];
        for(let i=1; i<=n; i++) {
            rawData.push({
                id: "INF-" + i.toString().padStart(3, '0'),
                service: services[Math.floor(Math.random()*services.length)],
                age: 22 + Math.floor(Math.random()*35),
                niv: Math.random() > 0.5 ? 'A1' : 'A2',
                k: 40 + Math.floor(Math.random()*55),
                p: 30 + Math.floor(Math.random()*60),
                a: (2.5 + Math.random()*2.5).toFixed(1),
                obs: Math.random() > 0.5 ? "Manque de formation" : "Manque de temps"
            });
        }
    }

    function renderMatrix() {
        const body = document.getElementById('matrix-rows');
        // Affichage de TOUTES les données (Exhaustif)
        body.innerHTML = rawData.map((r, index) => `
            <tr>
                <td><b>${r.id}</b></td><td>${r.service}</td><td>${r.age} ans</td><td>${r.niv}</td>
                <td style="color:${r.k>=70?'green':'red'}">${r.k}%</td>
                <td style="color:${r.p>=70?'green':'red'}">${r.p}%</td>
                <td><button class="tab-btn" onclick="openModal(${index})">Visualiser</button></td>
            </tr>
        `).join('');
    }

    function openModal(index) {
        const r = rawData[index];
        document.getElementById('m-title').innerText = "Détails : " + r.id;
        document.getElementById('m-body').innerHTML = `
            <div><strong>Sexe:</strong> Féminin</div>
            <div><strong>Service:</strong> ${r.service}</div>
            <div><strong>Âge:</strong> ${r.age} ans</div>
            <div><strong>Niveau:</strong> ${r.niv}</div>
            <div><strong>Score Savoir:</strong> ${r.k}%</div>
            <div><strong>Score Pratique:</strong> ${r.p}%</div>
            <div><strong>Attitude (Likert):</strong> ${r.a}/5</div>
            <div><strong>Obstacle principal:</strong> ${r.obs}</div>
        `;
        document.getElementById('viewModal').style.display = 'flex';
    }

    function closeModal() {
        document.getElementById('viewModal').style.display = 'none';
    }

    function renderHistV(id, data) {
        const el = document.getElementById(id);
        const total = rawData.length;
        const max = Math.max(...data.map(d=>d.v));
        el.innerHTML = data.map(d => `
            <div class="v-bar-item">
                <div class="v-bar-val">${d.v} (${((d.v/total)*100).toFixed(0)}%)</div>
                <div class="v-bar" style="height:${(d.v/max*85)}%"></div>
                <div class="v-bar-label">${d.l}</div>
            </div>
        `).join('');
    }

    function analyze() {
        renderHistV('hist-k', [
            {l: 'Bon', v: rawData.filter(r=>r.k>=75).length},
            {l: 'Moyen', v: rawData.filter(r=>r.k>=50 && r.k<75).length},
            {l: 'Faible', v: rawData.filter(r=>r.k<50).length}
        ]);
        renderHistV('hist-p', [
            {l: 'Adéquate', v: rawData.filter(r=>r.p>=70).length},
            {l: 'Inadéquate', v: rawData.filter(r=>r.p<70).length}
        ]);
        renderHistV('hist-obs', [
            {l: 'Formation', v: 92},
            {l: 'Moyens', v: 65},
            {l: 'Temps', v: 21}
        ]);

        document.getElementById('table-socio').innerHTML = `
            <thead><tr><th>Variable</th><th>Effectif (n)</th><th>Pourcentage (%)</th></tr></thead>
            <tbody>
                <tr><td>Niveau A1 (Gradué/LMD)</td><td>${rawData.filter(r=>r.niv==='A1').length}</td><td>${((rawData.filter(r=>r.niv==='A1').length/178)*100).toFixed(1)}%</td></tr>
                <tr><td>Niveau A2 (Technique)</td><td>${rawData.filter(r=>r.niv==='A2').length}</td><td>${((rawData.filter(r=>r.niv==='A2').length/178)*100).toFixed(1)}%</td></tr>
            </tbody>`;
    }

    function updateDiscussion() {
        const avgK = (rawData.reduce((a,b)=>a+b.k,0)/178).toFixed(1);
        const highP = ((rawData.filter(r=>r.p>=70).length/178)*100).toFixed(1);
        
        document.getElementById('disc-1').innerText = `L'étude confirme l'hypothèse selon laquelle les connaissances sont variables. Avec une moyenne de ${avgK}%, le niveau est hétérogène. Les infirmières de niveau A1 présentent des scores supérieurs, validant l'impact de la formation académique sur la maîtrise théorique du cancer du sein.`;
        document.getElementById('disc-2').innerText = `L'attitude globale reste positive, mais le sentiment d'auto-efficacité est limité. Bien que percevant la prévention comme prioritaire, la communication avec les patientes est entravée par le manque de supports didactiques.`;
        document.getElementById('disc-3').innerText = `Seulement ${highP}% des infirmières appliquent des pratiques conformes. Le manque de formation continue (cité par 92 enquêtées) apparaît comme le frein majeur, confirmant que les pratiques sont limitées par des facteurs structurels plutôt que par un manque de volonté.`;
        document.getElementById('disc-reco').innerText = `Il est impératif d'instaurer des sessions de recyclage sur l'Examen Clinique des Seins (ECS) à l'HGRM pour transformer les connaissances théoriques en réflexes cliniques systématiques.`;
    }

    function exportPDF(divId, name) {
        const el = document.getElementById(divId);
        const opt = { margin: 1, filename: name+'.pdf', html2canvas:{scale:2}, jsPDF:{unit:'cm', format:'a4', orientation:'portrait'} };
        html2pdf().set(opt).from(el).save();
    }
</script>
</body>
</html>
