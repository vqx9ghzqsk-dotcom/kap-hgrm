<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Système Expert CAP Intégral - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --success: #059669; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); margin: 0; padding: 15px; color: var(--secondary); }
        .container { max-width: 1200px; margin: auto; background: white; padding: 25px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        
        /* Navigation */
        .top-bar { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; border-bottom: 2px solid #eee; padding-bottom: 15px; position: sticky; top: 0; background: white; z-index: 100; }
        .nav-btns { display: flex; gap: 8px; flex-wrap: wrap; }
        .btn { padding: 10px 16px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.2s; }
        .btn-nav { background: #e2e8f0; color: var(--secondary); }
        .btn-nav.active { background: var(--primary); color: white; }
        .btn-export { background: var(--success); color: white; }

        .page { display: none; }
        .page.active { display: block; }

        /* Formulaire */
        h2 { color: var(--primary); font-size: 1.1em; border-left: 5px solid var(--primary); padding-left: 12px; margin-top: 25px; background: #fff1f2; padding-block: 8px; text-transform: uppercase; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; }
        .field { border: 1px solid #e2e8f0; padding: 12px; border-radius: 8px; background: #fff; }
        label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 0.85em; }
        input, select, textarea { width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; box-sizing: border-box; }
        
        /* Tableau Likert */
        .likert-table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.9em; }
        .likert-table th, .likert-table td { border: 1px solid #e2e8f0; padding: 10px; text-align: center; }
        .text-left { text-align: left; }

        /* Badges Niveau */
        .badge { padding: 4px 8px; border-radius: 4px; font-size: 0.8em; font-weight: bold; }
        .badge-good { background: #dcfce7; color: #166534; }
        .badge-mid { background: #fef9c3; color: #854d0e; }
        .badge-bad { background: #fee2e2; color: #991b1b; }

        .btn-submit { background: var(--primary); color: white; width: 100%; margin-top: 30px; padding: 20px; font-size: 1.2em; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; }
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
        <button class="btn btn-export" onclick="exportExcel()">⬇️ EXPORT EXCEL (CSV)</button>
    </div>

    <div id="recolte" class="page active">
        <form id="masterForm">
            <h2>I. IDENTIFICATION ET CONSENTEMENT</h2>
            <div class="grid">
                <div class="field"><label>Code de l'enquêtée *</label><input type="text" name="id" required></div>
                <div class="field"><label>Date *</label><input type="date" name="date" required></div>
                <div class="field"><label>Service d'affectation *</label><input type="text" name="service" required></div>
                <div class="field"><label>Enquêteur(trice)</label><input type="text" name="enqueteur"></div>
                <div class="field"><label>Consentement *</label>
                    <select name="consent" required><option value="Oui">J'accepte de participer</option><option value="Non">Je refuse</option></select>
                </div>
            </div>

            <h2>II. DONNÉES SOCIODÉMOGRAPHIQUES (Le Profil)</h2>
            <div class="grid">
                <div class="field"><label>Sexe</label><select name="sexe"><option>Femme</option><option>Homme</option></select></div>
                <div class="field"><label>Âge (ans)</label><input type="number" name="age"></div>
                <div class="field"><label>État civil</label><select name="ecivil"><option>Célibataire</option><option>Mariée</option><option>Veuve</option><option>Autre</option></select></div>
                <div class="field"><label>Niveau d'études</label><select name="niveau"><option value="A2">A2</option><option value="A1">A1</option><option value="A0">A0</option><option value="Master">Master+</option></select></div>
                <div class="field"><label>Expérience (ans)</label><input type="number" name="exp"></div>
                <div class="field"><label>Statut</label><select name="statut"><option>Titulaire</option><option>Contractuelle</option><option>Stagiaire</option><option>Autre</option></select></div>
                <div class="field"><label>Antécédents Familiaux</label><select name="anteced"><option value="0">Non</option><option value="1">Oui</option></select></div>
            </div>

            <h2>III. ÉVALUATION DES CONNAISSANCES (Scoring Scientifique)</h2>
            <div class="grid">
                <div class="field"><label>Risque augmente avec l'âge ?</label><select name="c1"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Obésité/Sédentarité = Risque ?</label><select name="c2"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Allaitement maternel protecteur ?</label><select name="c3"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>L'AES détecte les anomalies ?</label><select name="c4"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Mammographie = Dépistage Secondaire ?</label><select name="c5"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Méthode de référence :</label><select name="c6"><option value="0">---</option><option value="1">Mammographie</option><option value="0">Échographie</option></select></div>
            </div>
            <div class="field" style="margin-top:10px;">
                <label>Signes d'alerte connus (Cochez tout) :</label>
                <input type="checkbox" name="signe" value="masse"> Masse/Nodule | 
                <input type="checkbox" name="signe" value="peau"> Peau d'orange | 
                <input type="checkbox" name="signe" value="sang"> Écoulement sanglant | 
                <input type="checkbox" name="signe" value="retract"> Rétraction mamelon
            </div>

            <h2>IV. ÉVALUATION DES ATTITUDES (Échelle 1 à 5)</h2>
            <table class="likert-table">
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">La prévention est une priorité.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">Le cancer est forcément mortel en RDC.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                </tbody>
            </table>

            <h2>V. ÉVALUATION DES PRATIQUES</h2>
            <div class="grid">
                <div class="field"><label>Pratique personnelle AES ?</label><select name="p1"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="field"><label>Fréquence :</label><select name="p2"><option>Mensuelle</option><option>Occasionnelle</option><option>Rare</option></select></div>
                <div class="field"><label>Examen clinique patientes :</label><select name="p3"><option value="1">Toujours</option><option value="0.5">Parfois</option><option value="0">Jamais</option></select></div>
                <div class="field"><label>Enseignez-vous l'AES ?</label><select name="p4"><option value="1">Oui</option><option value="0">Non</option></select></div>
            </div>

            <h2>VI. OBSTACLES ET RECOMMANDATIONS</h2>
            <div class="field">
                <label>Obstacles à l'HGRM :</label>
                <input type="checkbox" name="obs" value="Formation"> Formation | 
                <input type="checkbox" name="obs" value="Matériel"> Matériel | 
                <input type="checkbox" name="obs" value="Temps"> Temps | 
                <input type="checkbox" name="obs" value="Tabous"> Tabous
            </div>
            <div class="grid" style="margin-top:10px;">
                <div class="field"><label>Type formation souhaitée :</label><select name="type_f"><option>Continue</option><option>Licence</option><option>Master</option></select></div>
                <div class="field"><label>Suggestions libres :</label><textarea name="sugg"></textarea></div>
            </div>

            <button type="button" class="btn-submit" onclick="saveEntry()">ENREGISTRER LA FICHE ET CALCULER LE SCORE</button>
        </form>
    </div>

    <div id="data" class="page">
        <h2>Matrice de Dépouillement (Données Brutes)</h2>
        <div style="overflow-x:auto;">
            <table id="dataTable" style="width:100%; border-collapse: collapse; font-size: 0.85em;">
                <thead style="background:#f1f5f9;">
                    <tr><th>ID</th><th>Service</th><th>Score C.</th><th>Niveau</th><th>Pratique</th><th>Obstacles</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="stats" class="page">
        <h2>Indicateurs CAP Globaux</h2>
        <div class="grid">
            <div style="text-align:center; padding:30px; border: 1px solid #eee;"><h3>Échantillon (N)</h3><div id="sn" style="font-size:3em; color:var(--primary);">0</div></div>
            <div style="text-align:center; padding:30px; border: 1px solid #eee;"><h3>Moyenne Savoir</h3><div id="sc" style="font-size:3em; color:var(--primary);">0%</div></div>
        </div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('cap_makala_expert')) || [];

    function show(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.btn-nav').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        if(id === 'data') refreshTable();
        if(id === 'stats') refreshStats();
    }

    function saveEntry() {
        const form = document.getElementById('masterForm');
        const data = Object.fromEntries(new FormData(form).entries());
        
        // Calcul du score de connaissances (sur 6 questions de C1 à C6)
        let score = 0;
        for(let i=1; i<=6; i++) { score += parseInt(data['c'+i] || 0); }
        data.score = score;
        data.niveau = score >= 5 ? 'Bon' : (score >= 3 ? 'Moyen' : 'Faible');
        
        db.push(data);
        localStorage.setItem('cap_makala_expert', JSON.stringify(db));
        alert("Données enregistrées ! Niveau de cette fiche : " + data.niveau);
        form.reset();
    }

    function refreshTable() {
        const tbody = document.querySelector('#dataTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr style="border-bottom:1px solid #eee;">
                <td>${d.id}</td><td>${d.service}</td><td>${d.score}/6</td>
                <td><span class="badge ${d.niveau==='Bon'?'badge-good':d.niveau==='Moyen'?'badge-mid':'badge-bad'}">${d.niveau}</span></td>
                <td>${d.p3 === '1' ? 'Systématique' : 'Irrégulier'}</td>
                <td>${d.obs || 'N/A'}</td>
            </tr>
        `).join('');
    }

    function refreshStats() {
        const n = db.length;
        if(n === 0) return;
        const totalScore = db.reduce((acc, curr) => acc + parseInt(curr.score), 0);
        document.getElementById('sn').innerText = n;
        document.getElementById('sc').innerText = ((totalScore / (n * 6)) * 100).toFixed(1) + "%";
    }

    function exportExcel() {
        if(db.length === 0) return alert("Base vide.");
        let csv = "ID,Date,Service,Age,NiveauEtude,ScoreConnaissance,NiveauLabel,PratiqueClinique,Obstacles\n";
        db.forEach(d => {
            csv += `${d.id},${d.date},${d.service},${d.age},${d.niveau},${d.score},${d.niveau},${d.p3},${d.obs}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a');
        a.href = window.URL.createObjectURL(blob);
        a.download = 'CAP_HGRM_Makala_Export.csv';
        a.click();
    }
</script>
</body>
</html>
