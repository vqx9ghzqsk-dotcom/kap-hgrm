<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RECHERCHE CAP - HGRM MAKALA</title>
    <style>
        :root { --pink-dark: #be185d; --slate: #1e293b; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', sans-serif; background: var(--bg); color: #334155; margin: 0; padding: 20px; }
        .container { max-width: 1100px; margin: auto; background: white; padding: 25px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        
        /* Menu de Navigation */
        .nav-menu { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 25px; border-bottom: 3px solid #e2e8f0; padding-bottom: 10px; }
        .nav-link { padding: 12px 20px; border: none; background: #f1f5f9; border-radius: 8px; cursor: pointer; font-weight: bold; color: var(--slate); transition: 0.3s; }
        .nav-link.active { background: var(--pink-dark); color: white; }

        /* Visibilité des Sections */
        .section-page { display: none; animation: fadeIn 0.5s; }
        .section-page.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        h2 { color: var(--pink-dark); border-left: 5px solid var(--pink-dark); padding-left: 15px; background: #fff1f2; padding-top: 5px; padding-bottom: 5px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 20px; }
        .box { padding: 15px; border: 1px solid #e2e8f0; border-radius: 8px; }
        
        /* Tableaux de dépouillement */
        .table-responsive { overflow-x: auto; margin-top: 20px; }
        table { width: 100%; border-collapse: collapse; font-size: 0.9em; }
        th, td { border: 1px solid #cbd5e1; padding: 10px; text-align: left; }
        th { background: #f8fafc; }

        .btn-save { background: var(--pink-dark); color: white; border: none; padding: 20px; width: 100%; border-radius: 10px; font-size: 1.2em; font-weight: bold; cursor: pointer; }
        .card-stat { background: white; border-top: 4px solid var(--pink-dark); padding: 20px; border-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); text-align: center; }
        .big-number { font-size: 2.5em; font-weight: bold; color: var(--pink-dark); }
    </style>
</head>
<body>

<div class="container">
    <div class="nav-menu">
        <button class="nav-link active" onclick="showTab('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="nav-link" onclick="showTab('depouillement')">2. DÉPOUILLEMENT & CODAGE</button>
        <button class="nav-link" onclick="showTab('resultats')">3. RÉSULTATS & ANALYSE</button>
        <button class="nav-link" onclick="showTab('concl_reco')">4. CONCLUSION & RECO</button>
    </div>

    <div id="recolte" class="section-page active">
        <h1>Fiche de Collecte Intégrale</h1>
        <form id="mainForm">
            <h2>I. Identification & Consentement</h2>
            <div class="grid">
                <div class="box"><label>Code :</label><input type="text" name="code" required></div>
                <div class="box"><label>Service :</label><input type="text" name="service"></div>
                <div class="box"><label>Consentement :</label><select name="consent"><option>Oui</option><option>Non</option></select></div>
            </div>

            <h2>II. Données Sociodémographiques</h2>
            <div class="grid">
                <div class="box"><label>Sexe :</label><select name="sexe"><option>Femme</option><option>Homme</option></select></div>
                <div class="box"><label>Âge :</label><input type="number" name="age"></div>
                <div class="box"><label>Niveau :</label><select name="niveau"><option value="1">A2</option><option value="2">A1</option><option value="3">A0</option><option value="4">Master</option></select></div>
                <div class="box"><label>Expérience (Années) :</label><input type="number" name="exp"></div>
                <div class="box"><label>Antécédents :</label><select name="antecedents"><option value="0">Non</option><option value="1">Oui</option></select></div>
            </div>

            <h2>III. Connaissances (Savoir)</h2>
            <div class="grid">
                <div class="box"><label>Risque augmente avec l'âge ?</label><select name="c_age"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="box"><label>Obésité est un facteur ?</label><select name="c_obesite"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="box"><label>Enseignez-vous l'AES ?</label><select name="p_enseigne"><option value="1">Oui</option><option value="0">Non</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="collecter()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="depouillement" class="section-page">
        <h2>Dépouillement et Codage des données</h2>
        <p><i>Cette matrice transforme vos fiches en codes numériques (Saisie & Traitement).</i></p>
        <div class="table-responsive">
            <table id="tableDepouillement">
                <thead>
                    <tr><th>Code</th><th>Âge</th><th>Sexe</th><th>Niveau (Codé)</th><th>C_Age</th><th>C_Obes</th><th>P_Ens</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="resultats" class="section-page">
        <h2>Présentation des Résultats & Analyse</h2>
        <div class="grid">
            <div class="card-stat">
                <h3>Total Fiches</h3>
                <div class="big-number" id="stat_total">0</div>
            </div>
            <div class="card-stat">
                <h3>Niveau Connaissances</h3>
                <div class="big-number" id="stat_con">0%</div>
            </div>
            <div class="card-stat">
                <h3>Niveau Pratiques</h3>
                <div class="big-number" id="stat_prat">0%</div>
            </div>
        </div>
        <div class="box" style="margin-top:20px;">
            <h3>Analyse et Discussion des résultats</h3>
            <p id="analyse_automatique">En attente de données pour générer la discussion comparative...</p>
        </div>
    </div>

    <div id="concl_reco" class="section-page">
        <h2>Conclusion et Recommandations</h2>
        <div class="box">
            <h3>Conclusion</h3>
            <p>Sur la base de l'échantillon prélevé à l'HGRM Makala, nous constatons que...</p>
            <textarea id="synthese_concl" style="width:100%; height:100px;"></textarea>
        </div>
        <div class="box" style="margin-top:20px;">
            <h3>Recommandations</h3>
            <ul id="list_reco">
                <li>Organiser des sessions de formation continue.</li>
                <li>Installer des supports visuels (affiches) dans les services.</li>
            </ul>
        </div>
    </div>
</div>

<script>
    let storage = JSON.parse(localStorage.getItem('db_makala')) || [];

    function showTab(id) {
        document.querySelectorAll('.section-page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        
        if(id === 'depouillement') rafraichirTableau();
        if(id === 'resultats') calculerStats();
    }

    function collecter() {
        const form = document.getElementById('mainForm');
        const data = Object.fromEntries(new FormData(form).entries());
        storage.push(data);
        localStorage.setItem('db_makala', JSON.stringify(storage));
        alert("Fiche enregistrée avec succès !");
        form.reset();
    }

    function rafraichirTableau() {
        const tbody = document.querySelector('#tableDepouillement tbody');
        tbody.innerHTML = storage.map(d => `
            <tr>
                <td>${d.code}</td>
                <td>${d.age}</td>
                <td>${d.sexe}</td>
                <td>${d.niveau}</td>
                <td>${d.c_age}</td>
                <td>${d.c_obesite}</td>
                <td>${d.p_enseigne}</td>
            </tr>
        `).join('');
    }

    function calculerStats() {
        const n = storage.length;
        if(n === 0) return;

        const sumCon = storage.reduce((acc, d) => acc + parseInt(d.c_age), 0);
        const sumPrat = storage.reduce((acc, d) => acc + parseInt(d.p_enseigne), 0);

        document.getElementById('stat_total').innerText = n;
        document.getElementById('stat_con').innerText = ((sumCon/n)*100).toFixed(1) + "%";
        document.getElementById('stat_prat').innerText = ((sumPrat/n)*100).toFixed(1) + "%";
        
        document.getElementById('analyse_texte').innerText = `L'analyse de ${n} fiches à Makala montre un taux de pratique de ${((sumPrat/n)*100).toFixed(1)}%.`;
    }
</script>

</body>
</html>
