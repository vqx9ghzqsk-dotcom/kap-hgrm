<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Système Expert CAP - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --success: #059669; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); margin: 0; padding: 20px; }
        .container { max-width: 1200px; margin: auto; background: white; padding: 30px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        
        /* Navigation & Actions */
        .top-bar { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; border-bottom: 2px solid #eee; padding-bottom: 15px; }
        .nav-btns { display: flex; gap: 10px; }
        .btn { padding: 10px 18px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.2s; }
        .btn-nav { background: #e2e8f0; color: var(--secondary); }
        .btn-nav.active { background: var(--primary); color: white; }
        .btn-export { background: var(--success); color: white; }

        .page { display: none; }
        .page.active { display: block; }

        /* Formulaire Expert */
        h2 { color: var(--primary); font-size: 1.2em; border-left: 5px solid var(--primary); padding-left: 12px; margin-top: 25px; background: #fff1f2; padding-block: 8px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; }
        .field { border: 1px solid #e2e8f0; padding: 15px; border-radius: 8px; transition: 0.3s; }
        .field:focus-within { border-color: var(--primary); box-shadow: 0 0 0 3px #fff1f2; }
        label { display: block; margin-bottom: 8px; font-weight: 600; color: var(--secondary); font-size: 0.9em; }
        input, select, textarea { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 6px; box-sizing: border-box; }
        
        /* Stats & Badges */
        .badge { padding: 4px 8px; border-radius: 4px; font-size: 0.8em; font-weight: bold; }
        .badge-good { background: #dcfce7; color: #166534; }
        .badge-mid { background: #fef9c3; color: #854d0e; }
        .badge-bad { background: #fee2e2; color: #991b1b; }

        .stat-card { background: white; border: 1px solid #e2e8f0; padding: 20px; border-radius: 12px; text-align: center; }
        .stat-num { font-size: 2.5em; font-weight: bold; color: var(--primary); }
    </style>
</head>
<body>

<div class="container">
    <div class="top-bar">
        <div class="nav-btns">
            <button class="btn btn-nav active" onclick="show('recolte')">1. COLLECTE</button>
            <button class="btn btn-nav" onclick="show('data')">2. BASE DE DONNÉES</button>
            <button class="btn btn-nav" onclick="show('stats')">3. ANALYSE CAP</button>
        </div>
        <button class="btn btn-export" onclick="exportExcel()">⬇️ EXPORTER VERS EXCEL (CSV)</button>
    </div>

    <div id="recolte" class="page active">
        <form id="masterForm">
            <h2>I. IDENTIFICATION (SÉCURISÉE)</h2>
            <div class="grid">
                <div class="field"><label>Code Anonyme (ex: INF001) *</label><input type="text" name="id" required></div>
                <div class="field"><label>Service *</label><input type="text" name="service" required></div>
                <div class="field"><label>Ancienneté (ans) *</label><input type="number" name="exp" required></div>
            </div>

            <h2>II. ÉVALUATION DES CONNAISSANCES (SCORING)</h2>
            <div class="grid">
                <div class="field"><label>Le risque augmente avec l'âge ?</label>
                    <select name="c1"><option value="0">--- Choisir ---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>L'allaitement est protecteur ?</label>
                    <select name="c2"><option value="0">--- Choisir ---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>Méthode de référence dépistage :</label>
                    <select name="c3"><option value="0">--- Choisir ---</option><option value="1">Mammographie</option><option value="0">Échographie</option></select>
                </div>
            </div>

            <h2>III. PRATIQUES & OBSTACLES</h2>
            <div class="grid">
                <div class="field"><label>Réalisez-vous l'examen clinique ?</label>
                    <select name="p1"><option>Toujours</option><option>Parfois</option><option>Jamais</option></select>
                </div>
                <div class="field"><label>Obstacle Majeur :</label>
                    <select name="obs"><option>Manque de formation</option><option>Manque de temps</option><option>Coût des examens</option><option>Tabous</option></select>
                </div>
            </div>

            <button type="button" class="btn" style="background:var(--primary); color:white; width:100%; margin-top:20px; padding:20px;" onclick="saveEntry()">ENREGISTRER & CALCULER LE SCORE</button>
        </form>
    </div>

    <div id="data" class="page">
        <h2>Matrice de Dépouillement avec Scoring</h2>
        <div style="overflow-x:auto;">
            <table id="dataTable" style="width:100%; border-collapse: collapse;">
                <thead style="background:#f1f5f9;">
                    <tr><th>ID</th><th>Service</th><th>Exp</th><th>Score Connais.</th><th>Niveau</th><th>Pratique</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="stats" class="page">
        <h2>Résultats Scientifiques Automatisés</h2>
        <div class="grid">
            <div class="stat-card"><h3>Échantillon (N)</h3><div id="sn" class="stat-num">0</div></div>
            <div class="stat-card"><h3>Moyenne Connaissances</h3><div id="sc" class="stat-num">0%</div></div>
        </div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('makala_pro_db')) || [];

    function show(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.btn-nav').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        if(id === 'data') refreshTable();
        if(id === 'stats') refreshStats();
    }

    function saveEntry() {
        const f = document.getElementById('masterForm');
        const d = Object.fromEntries(new FormData(f).entries());
        
        // Calcul du score de connaissance (Sur 3 points ici)
        let score = parseInt(d.c1) + parseInt(d.c2) + parseInt(d.c3);
        d.score = score;
        d.niveau = score >= 2 ? 'Bon' : (score === 1 ? 'Moyen' : 'Faible');
        
        db.push(d);
        localStorage.setItem('makala_pro_db', JSON.stringify(db));
        alert("Fiche INF-OK ! Niveau calculé : " + d.niveau);
        f.reset();
    }

    function refreshTable() {
        const tbody = document.querySelector('#dataTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr style="border-bottom:1px solid #eee;">
                <td>${d.id}</td><td>${d.service}</td><td>${d.exp} ans</td>
                <td>${d.score}/3</td>
                <td><span class="badge ${d.niveau==='Bon'?'badge-good':d.niveau==='Moyen'?'badge-mid':'badge-bad'}">${d.niveau}</span></td>
                <td>${d.p1}</td>
            </tr>
        `).join('');
    }

    function refreshStats() {
        const n = db.length;
        if(n === 0) return;
        const avg = (db.reduce((acc, curr) => acc + parseInt(curr.score), 0) / (n * 3)) * 100;
        document.getElementById('sn').innerText = n;
        document.getElementById('sc').innerText = avg.toFixed(1) + "%";
    }

    function exportExcel() {
        if(db.length === 0) return alert("Aucune donnée à exporter.");
        let csv = "ID,Service,Experience,Score,Niveau,Pratique,Obstacle\n";
        db.forEach(d => {
            csv += `${d.id},${d.service},${d.exp},${d.score},${d.niveau},${d.p1},${d.obs}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.setAttribute('href', url);
        a.setAttribute('download', 'Donnees_HGRM_Makala.csv');
        a.click();
    }
</script>
</body>
</html>
