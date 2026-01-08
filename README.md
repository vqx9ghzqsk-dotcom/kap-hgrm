<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SYSTÈME COMPLET CAP - HGRM MAKALA</title>
    <style>
        :root { --pink-dark: #be185d; --slate: #1e293b; --bg: #f1f5f9; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: var(--bg); color: #334155; margin: 0; padding: 10px; }
        .container { max-width: 1200px; margin: auto; background: white; padding: 30px; border-radius: 12px; box-shadow: 0 5px 20px rgba(0,0,0,0.1); }
        
        /* Navigation */
        .tabs { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 30px; border-bottom: 2px solid #e2e8f0; padding-bottom: 10px; }
        .tab-link { padding: 15px 25px; border: none; background: #e2e8f0; border-radius: 8px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .tab-link.active { background: var(--pink-dark); color: white; }

        /* Pages */
        .page { display: none; }
        .page.active { display: block; }

        /* Formulaire Riche */
        h2 { color: var(--pink-dark); background: #fff1f2; padding: 10px; border-left: 5px solid var(--pink-dark); font-size: 1.2em; margin-top: 30px; }
        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; }
        .input-group { border: 1px solid #e2e8f0; padding: 15px; border-radius: 8px; }
        label { display: block; font-weight: bold; margin-bottom: 8px; }
        input, select, textarea { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 5px; }
        .check-group { display: flex; flex-direction: column; gap: 8px; }
        
        /* Tableaux & Stats */
        .table-wrap { overflow-x: auto; margin-top: 20px; }
        table { width: 100%; border-collapse: collapse; font-size: 0.85em; }
        th, td { border: 1px solid #cbd5e1; padding: 10px; text-align: left; }
        th { background: #f8fafc; }
        .stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; }
        .stat-card { background: white; border: 1px solid #e2e8f0; padding: 20px; text-align: center; border-radius: 10px; border-top: 4px solid var(--pink-dark); }
        .big-val { font-size: 2em; font-weight: bold; color: var(--pink-dark); }

        .btn-main { background: var(--pink-dark); color: white; border: none; padding: 20px; width: 100%; border-radius: 8px; font-size: 1.3em; cursor: pointer; font-weight: bold; margin-top: 20px; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-link active" onclick="switchTab('recolte')">1. RÉCOLTE DES DONNÉES (FICHE RICHE)</button>
        <button class="tab-link" onclick="switchTab('depouillement')">2. DÉPOUILLEMENT & CODAGE</button>
        <button class="tab-link" onclick="switchTab('resultats')">3. RÉSULTATS & ANALYSE</button>
        <button class="tab-link" onclick="switchTab('conclusion')">4. CONCLUSION & RECO</button>
    </div>

    <div id="recolte" class="page active">
        <h1>Collecte de Données Exhaustive - HGRM</h1>
        <form id="capForm">
            <h2>I. IDENTIFICATION & CONSENTEMENT</h2>
            <div class="form-grid">
                <div class="input-group"><label>Code :</label><input type="text" name="code" required></div>
                <div class="input-group"><label>Date :</label><input type="date" name="date"></div>
                <div class="input-group"><label>Service d'affectation :</label><input type="text" name="service"></div>
                <div class="input-group"><label>Enquêteur :</label><input type="text" name="enqueteur"></div>
                <div class="input-group"><label>Consentement :</label>
                    <select name="consent"><option value="1">Accepté</option><option value="0">Refusé</option></select>
                </div>
            </div>

            <h2>II. DONNÉES SOCIODÉMOGRAPHIQUES (LE PROFIL)</h2>
            <div class="form-grid">
                <div class="input-group"><label>Sexe :</label><select name="sexe"><option>Femme</option><option>Homme</option></select></div>
                <div class="input-group"><label>Âge :</label><input type="number" name="age"></div>
                <div class="input-group"><label>État Civil :</label>
                    <select name="etat_civil"><option>Célibataire</option><option>Mariée</option><option>Veuve</option><option>Autre</option></select>
                </div>
                <div class="input-group"><label>Niveau d'études :</label>
                    <select name="etude"><option value="1">A2 (Diplômée)</option><option value="2">A1 (Graduée)</option><option value="3">A0 (Licenciée)</option><option value="4">Master</option></select>
                </div>
                <div class="input-group"><label>Années d'expérience :</label><input type="number" name="exp"></div>
                <div class="input-group"><label>Statut :</label>
                    <select name="statut"><option>Titulaire</option><option>Contractuelle</option><option>Stagiaire</option><option>Autre</option></select>
                </div>
                <div class="input-group"><label>Antécédents Familiaux :</label>
                    <select name="antecedents"><option value="0">Non</option><option value="1">Oui</option></select>
                </div>
            </div>

            <h2>III. CONNAISSANCES (LE SAVOIR)</h2>
            <div class="form-grid">
                <div class="input-group"><label>L'âge augmente le risque ?</label>
                    <select name="c1"><option value="1">Vrai</option><option value="0">Faux</option><option value="0">NSP</option></select>
                </div>
                <div class="input-group"><label>L'obésité est un facteur ?</label>
                    <select name="c2"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="input-group"><label>L'allaitement est protecteur ?</label>
                    <select name="c3"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="input-group"><label>L'AES détecte les anomalies ?</label>
                    <select name="c4"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="input-group"><label>Méthode de référence :</label>
                    <select name="c_ref"><option>Mammographie</option><option>Échographie</option><option>Radio</option></select>
                </div>
            </div>
            
            <div class="input-group" style="margin-top:10px;">
                <label>Signes d'alerte connus :</label>
                <div class="check-group">
                    <label><input type="checkbox" name="signe" value="masse"> Masse/Nodule</label>
                    <label><input type="checkbox" name="signe" value="peau"> Peau d'orange</label>
                    <label><input type="checkbox" name="signe" value="ecoul"> Écoulement sanglant</label>
                    <label><input type="checkbox" name="signe" value="retract"> Rétraction mamelon</label>
                </div>
            </div>

            <h2>IV. ATTITUDES (LIKERT 1-5)</h2>
            <div class="form-grid">
                <div class="input-group"><label>Prévention = Priorité ?</label><input type="number" name="a1" min="1" max="5"></div>
                <div class="input-group"><label>Capable d'enseigner ?</label><input type="number" name="a2" min="1" max="5"></div>
                <div class="input-group"><label>Coût = Obstacle ?</label><input type="number" name="a3" min="1" max="5"></div>
            </div>

            <h2>V. PRATIQUES & OBSTACLES</h2>
            <div class="form-grid">
                <div class="input-group"><label>Pratique personnelle AES ?</label><select name="p1"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="input-group"><label>Fréquence :</label><select name="p1_f"><option>Mensuelle</option><option>Rare</option><option>Jamais</option></select></div>
                <div class="input-group"><label>Examen clinique patiente ?</label><select name="p2"><option value="1">Toujours</option><option value="0.5">Parfois</option><option value="0">Jamais</option></select></div>
                <div class="input-group"><label>Enseigne AES aux patientes ?</label><select name="p3"><option value="1">Oui</option><option value="0">Non</option></select></div>
            </div>

            <div class="input-group" style="margin-top:15px;">
                <label>Obstacles rencontrés :</label>
                <div class="check-group">
                    <label><input type="checkbox" name="obs" value="form"> Manque de formation</label>
                    <label><input type="checkbox" name="obs" value="mat"> Manque de matériel</label>
                    <label><input type="checkbox" name="obs" value="temps"> Manque de temps</label>
                    <label><input type="checkbox" name="obs" value="tabou"> Tabous culturels</label>
                </div>
            </div>

            <button type="button" class="btn-main" onclick="saveData()">ENREGISTRER TOUTES LES DONNÉES</button>
        </form>
    </div>

    <div id="depouillement" class="page">
        <h1>Dépouillement & Matrice de Codage</h1>
        <div class="table-wrap">
            <table id="matrixTable">
                <thead>
                    <tr>
                        <th>Code</th><th>Âge</th><th>Niv</th><th>Exp</th><th>C1</th><th>C2</th><th>C3</th><th>A1</th><th>A2</th><th>P1</th><th>P2</th><th>P3</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="resultats" class="page">
        <h1>Analyse Statistique Automatique</h1>
        <div class="stat-grid">
            <div class="stat-card"><h3>Échantillon (N)</h3><div id="valN" class="big-val">0</div></div>
            <div class="stat-card"><h3>Connaissances</h3><div id="valC" class="big-val">0%</div></div>
            <div class="stat-card"><h3>Attitudes (Moy)</h3><div id="valA" class="big-val">0</div></div>
            <div class="stat-card"><h3>Pratiques</h3><div id="valP" class="big-val">0%</div></div>
        </div>
        <div class="input-group" style="margin-top:30px;">
            <h3>Interprétation des résultats</h3>
            <p id="interprete">Aucune donnée pour l'instant.</p>
        </div>
    </div>

    <div id="conclusion" class="page">
        <h1>Synthèse, Conclusion & Recommandations</h1>
        <div class="input-group">
            <h3>Conclusion</h3>
            <p id="concl_text">En attente de traitement...</p>
        </div>
        <div class="input-group" style="margin-top:20px;">
            <h3>Recommandations proposées pour l'HGRM</h3>
            <ul id="reco_list">
                <li>Formation continue obligatoire sur les techniques de palpation.</li>
                <li>Affichage systématique des signes d'alerte dans les salles d'attente.</li>
            </ul>
        </div>
    </div>
</div>



<script>
    let db = JSON.parse(localStorage.getItem('full_cap_db')) || [];

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
        db.push(data);
        localStorage.setItem('full_cap_db', JSON.stringify(db));
        alert("Fiche complète enregistrée !");
        form.reset();
    }

    function renderMatrix() {
        const tbody = document.querySelector('#matrixTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr>
                <td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.exp}</td>
                <td>${d.c1}</td><td>${d.c2}</td><td>${d.c3}</td>
                <td>${d.a1}</td><td>${d.a2}</td>
                <td>${d.p1}</td><td>${d.p2}</td><td>${d.p3}</td>
            </tr>
        `).join('');
    }

    function computeStats() {
        const n = db.length;
        if(n === 0) return;

        const sumC = db.reduce((acc, d) => acc + (parseInt(d.c1)+parseInt(d.c2)+parseInt(d.c3))/3, 0);
        const sumA = db.reduce((acc, d) => acc + (parseInt(d.a1||0)+parseInt(d.a2||0))/2, 0);
        const sumP = db.reduce((acc, d) => acc + (parseFloat(d.p1)+parseFloat(d.p2)+parseFloat(d.p3))/3, 0);

        document.getElementById('valN').innerText = n;
        document.getElementById('valC').innerText = ((sumC/n)*100).toFixed(1) + "%";
        document.getElementById('valA').innerText = (sumA/n).toFixed(2) + "/5";
        document.getElementById('valP').innerText = ((sumP/n)*100).toFixed(1) + "%";

        document.getElementById('interprete').innerText = `L'analyse montre que pour ${n} infirmières à Makala, le niveau de pratique est de ${((sumP/n)*100).toFixed(1)}%, ce qui nécessite une intervention.`;
        document.getElementById('concl_text').innerText = `Il existe un écart de ${((sumC/n)*100 - (sumP/n)*100).toFixed(1)}% entre ce que les infirmières savent et ce qu'elles pratiquent réellement sur le terrain.`;
    }
</script>

</body>
</html>
