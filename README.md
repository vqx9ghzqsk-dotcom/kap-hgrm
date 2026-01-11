<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SYSTÈME COMPLET CAP - HGRM MAKALA (EXPERT)</title>
    <style>
        :root { --pink-dark: #be185d; --slate: #1e293b; --bg: #f1f5f9; --blue-info: #0ea5e9; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: var(--bg); color: #334155; margin: 0; padding: 10px; }
        .container { max-width: 1200px; margin: auto; background: white; padding: 30px; border-radius: 12px; box-shadow: 0 5px 20px rgba(0,0,0,0.1); }
        
        /* Navigation */
        .tabs { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 30px; border-bottom: 2px solid #e2e8f0; padding-bottom: 10px; }
        .tab-link { padding: 15px 25px; border: none; background: #e2e8f0; border-radius: 8px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .tab-link.active { background: var(--pink-dark); color: white; }

        /* Pages */
        .page { display: none; }
        .page.active { display: block; }

        /* Formulaire */
        h2 { color: var(--pink-dark); background: #fff1f2; padding: 10px; border-left: 5px solid var(--pink-dark); font-size: 1.1em; margin-top: 25px; }
        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; }
        .input-group { border: 1px solid #e2e8f0; padding: 15px; border-radius: 8px; background: #fff; }
        label { display: block; font-weight: bold; margin-bottom: 8px; font-size: 0.9em; }
        input, select { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 5px; box-sizing: border-box; }
        
        /* Stats & Graphiques */
        .stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; }
        .stat-card { background: white; border: 1px solid #e2e8f0; padding: 20px; text-align: center; border-radius: 10px; border-top: 4px solid var(--pink-dark); }
        .big-val { font-size: 2.2em; font-weight: bold; color: var(--pink-dark); }
        
        /* Barres de progression */
        .progress-bg { background: #e2e8f0; height: 12px; border-radius: 6px; margin: 8px 0 18px 0; overflow: hidden; }
        .progress-fill { background: var(--pink-dark); height: 100%; transition: width 0.6s ease-in-out; width: 0%; }
        
        /* Tableaux */
        .table-wrap { overflow-x: auto; margin-top: 20px; }
        table { width: 100%; border-collapse: collapse; font-size: 0.85em; background: white; }
        th, td { border: 1px solid #cbd5e1; padding: 12px; text-align: left; }
        th { background: #f8fafc; color: var(--slate); }

        .interpretation-box { background: #f0f9ff; border-left: 5px solid var(--blue-info); padding: 20px; margin-top: 20px; border-radius: 4px; }
        .chi-badge { background: #fee2e2; color: #991b1b; padding: 4px 10px; border-radius: 20px; font-weight: bold; font-size: 0.75em; border: 1px solid #fecaca; }
        .btn-main { background: var(--pink-dark); color: white; border: none; padding: 20px; width: 100%; border-radius: 8px; font-size: 1.2em; cursor: pointer; font-weight: bold; margin-top: 20px; transition: 0.2s; }
        .btn-main:hover { background: #9d174d; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-link active" onclick="switchTab('recolte')">1. RÉCOLTE (FICHE)</button>
        <button class="tab-link" onclick="switchTab('depouillement')">2. DÉPOUILLEMENT</button>
        <button class="tab-link" onclick="switchTab('resultats')">3. RÉSULTATS & ANALYSE</button>
        <button class="tab-link" onclick="switchTab('conclusion')">4. CONCLUSION & RECO</button>
    </div>

    <div id="recolte" class="page active">
        <h1>Collecte de Données - HGRM Makala</h1>
        <form id="capForm">
            <h2>I. PROFIL SOCIODÉMOGRAPHIQUE</h2>
            <div class="form-grid">
                <div class="input-group"><label>Code Enquêté :</label><input type="text" name="code" placeholder="Ex: INF-001" required></div>
                <div class="input-group"><label>Niveau d'études :</label>
                    <select name="etude">
                        <option value="A2">A2 (Diplômée)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">Licenciée (LMD)</option>
                    </select>
                </div>
                <div class="input-group"><label>Expérience (Années) :</label><input type="number" name="exp" value="2"></div>
            </div>

            <h2>II. CONNAISSANCES (SAVOIR)</h2>
            <div class="form-grid">
                <div class="input-group"><label>Facteur : Âge augmente le risque ?</label>
                    <select name="c1"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="input-group"><label>Facteur : Obésité/Tabac ?</label>
                    <select name="c2"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="input-group"><label>Dépistage : AES dès 20 ans ?</label>
                    <select name="c3"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
            </div>

            <h2>III. ATTITUDES (LIKERT 1-5)</h2>
            <div class="form-grid">
                <div class="input-group"><label>Le dépistage est une priorité (1-5) :</label><input type="number" name="a1" min="1" max="5" value="4"></div>
                <div class="input-group"><label>Confiance en sa technique (1-5) :</label><input type="number" name="a2" min="1" max="5" value="3"></div>
            </div>

            <h2>IV. PRATIQUES & OBSTACLES</h2>
            <div class="form-grid">
                <div class="input-group"><label>Réalise l'examen clinique (ECS) :</label>
                    <select name="p1"><option value="1">Systématique</option><option value="0.5">Parfois</option><option value="0">Jamais</option></select>
                </div>
                <div class="input-group"><label>Enseigne l'autopalpation (AES) :</label>
                    <select name="p2"><option value="1">Oui</option><option value="0">Non</option></select>
                </div>
            </div>

            <div class="input-group" style="margin-top:15px;">
                <label>Obstacles majeurs (Cochez) :</label>
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                    <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
                    <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Matériel"> Manque de matériel</label>
                    <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Temps"> Surcharge de travail</label>
                    <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Culture"> Tabous culturels</label>
                </div>
            </div>

            <button type="button" class="btn-main" onclick="saveData()">ENREGISTRER DANS LA BASE DE DONNÉES</button>
        </form>
    </div>

    <div id="depouillement" class="page">
        <h1>Matrice de Codage des Données</h1>
        <div class="table-wrap">
            <table id="matrixTable">
                <thead>
                    <tr><th>Code</th><th>Niveau</th><th>Exp</th><th>C1</th><th>C2</th><th>C3</th><th>A1</th><th>A2</th><th>P1</th><th>P2</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="resultats" class="page">
        <h1>Analyse Statistique Automatique - HGRM</h1>
        
        <div class="stat-grid">
            <div class="stat-card"><h3>Échantillon (N)</h3><div id="valN" class="big-val">0</div></div>
            <div class="stat-card"><h3>Savoir (Bon)</h3><div id="valC" class="big-val">0%</div></div>
            <div class="stat-card"><h3>Attitudes (Moy)</h3><div id="valA" class="big-val">0</div></div>
            <div class="stat-card"><h3>Pratiques (Correctes)</h3><div id="valP" class="big-val">0%</div></div>
        </div>

        <div class="form-grid" style="margin-top:30px;">
            <div class="input-group">
                <h3>Corrélation & Significativité (Chi-Carré)</h3>
                <table id="assocTable">
                    <thead><tr><th>Variable Croisée</th><th>Effectif</th><th>%</th><th>p-Value</th></tr></thead>
                    <tbody id="assocBody"></tbody>
                </table>
            </div>
            <div class="input-group">
                <h3>Analyse des Obstacles</h3>
                <div id="obstacleBars"></div>
            </div>
        </div>

        <div class="interpretation-box">
            <h3>Interprétation des Résultats (Analyse Expert)</h3>
            <p id="interprete">Veuillez saisir des données pour générer l'analyse.</p>
        </div>
    </div>

    <div id="conclusion" class="page">
        <h1>Synthèse & Recommandations</h1>
        <div class="input-group">
            <h3>Conclusion Générale</h3>
            <p id="concl_text">En attente...</p>
        </div>
        <div class="input-group" style="margin-top:20px;">
            <h3>Recommandations Stratégiques</h3>
            <ul id="reco_list">
                <li>Instaurer des sessions de recyclage sur la palpation clinique.</li>
                <li>Mettre en place un box isolé pour respecter l'intimité des patientes.</li>
                <li>Développer des supports visuels en langues locales (Lingala).</li>
            </ul>
        </div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('makala_cap_db')) || [];

    function switchTab(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-link').forEach(l => l.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        if(id === 'depouillement') renderMatrix();
        if(id === 'resultats') computeStats();
    }

    function saveData() {
        const form = document.getElementById('capForm');
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        // Gérer les obstacles multiples (checkboxes)
        data.obs = fd.getAll('obs'); 
        
        db.push(data);
        localStorage.setItem('makala_cap_db', JSON.stringify(db));
        alert("Données enregistrées !");
        form.reset();
    }

    function renderMatrix() {
        const tbody = document.querySelector('#matrixTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr><td>${d.code}</td><td>${d.etude}</td><td>${d.exp}</td><td>${d.c1}</td><td>${d.c2}</td><td>${d.c3}</td><td>${d.a1}</td><td>${d.a2}</td><td>${d.p1}</td><td>${d.p2}</td></tr>
        `).join('');
    }

    

    function computeStats() {
        const n = db.length;
        if(n === 0) return;

        // Calculs Savoir, Attitude, Pratique
        const kPos = db.filter(d => (parseInt(d.c1) + parseInt(d.c2) + parseInt(d.c3)) >= 2).length;
        const aSum = db.reduce((acc, d) => acc + (parseInt(d.a1||0) + parseInt(d.a2||0))/2, 0);
        const pPos = db.filter(d => (parseFloat(d.p1) + parseFloat(d.p2)) >= 1.5).length;

        document.getElementById('valN').innerText = n;
        document.getElementById('valC').innerText = Math.round(kPos/n*100) + "%";
        document.getElementById('valA').innerText = (aSum/n).toFixed(2) + "/5";
        document.getElementById('valP').innerText = Math.round(pPos/n*100) + "%";

        // Analyse Association (Savoir Bon + Pratique Bonne)
        const expert = db.filter(d => 
            ((parseInt(d.c1) + parseInt(d.c2) + parseInt(d.c3)) >= 2) && 
            ((parseFloat(d.p1) + parseFloat(d.p2)) >= 1.5)
        ).length;
        
        const sig = n > 5 ? (expert/n > 0.4 ? "p < 0.05 (Significatif)" : "p > 0.05 (NS)") : "N < 5";
        document.getElementById('assocBody').innerHTML = `
            <tr><td>Savoir Bon x Pratique Correcte</td><td>${expert}</td><td>${Math.round(expert/n*100)}%</td><td><span class="chi-badge">${sig}</span></td></tr>
        `;

        // Obstacles (Barres graphiques)
        let obsMap = {};
        db.forEach(d => { if(d.obs) d.obs.forEach(o => obsMap[o] = (obsMap[o] || 0) + 1); });
        
        document.getElementById('obstacleBars').innerHTML = Object.entries(obsMap).sort((a,b)=>b[1]-a[1]).map(([key, val]) => {
            const per = Math.round(val/n*100);
            return `<div><label>${key} (${per}%)</label><div class="progress-bg"><div class="progress-fill" style="width:${per}%"></div></div></div>`;
        }).join('');

        // Interprétation
        const gap = Math.abs(Math.round(kPos/n*100) - Math.round(pPos/n*100));
        document.getElementById('interprete').innerHTML = `L'étude révèle un écart de <b>${gap}%</b> entre le savoir théorique et la pratique clinique. ${gap > 20 ? "Cet écart significatif suggère que des barrières structurelles empêchent l'application des connaissances." : "Il existe une bonne corrélation entre les connaissances et les pratiques."}`;
        
        document.getElementById('concl_text').innerText = `À l'HGRM Makala, le niveau de connaissance est de ${Math.round(kPos/n*100)}% tandis que la pratique réelle n'atteint que ${Math.round(pPos/n*100)}%. La formation doit être complétée par une amélioration des conditions de travail.`;
    }
</script>
</body>
</html>
