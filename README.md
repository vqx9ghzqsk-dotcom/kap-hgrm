<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Système Expert CAP Infirmier - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --success: #059669; --bg: #f1f5f9; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); margin: 0; padding: 15px; }
        .container { max-width: 1300px; margin: auto; background: white; padding: 25px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        
        .top-bar { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; border-bottom: 2px solid #eee; padding-bottom: 15px; position: sticky; top: 0; background: white; z-index: 100; }
        .btn { padding: 10px 16px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; }
        .btn-nav { background: #e2e8f0; color: var(--secondary); margin-right: 5px; }
        .btn-nav.active { background: var(--primary); color: white; }
        .btn-export { background: var(--success); color: white; }

        .page { display: none; }
        .page.active { display: block; }

        h2 { color: var(--primary); font-size: 1em; border-left: 5px solid var(--primary); padding: 8px 12px; margin-top: 20px; background: #fff1f2; text-transform: uppercase; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 15px; }
        .field { border: 1px solid #e2e8f0; padding: 12px; border-radius: 8px; background: #fff; }
        label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 0.85em; color: #475569; }
        input, select, textarea { width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; }
        
        .likert-table { width: 100%; border-collapse: collapse; font-size: 0.85em; margin-top: 10px; }
        .likert-table th, .likert-table td { border: 1px solid #e2e8f0; padding: 8px; text-align: center; }
        .text-left { text-align: left; background: #f8fafc; }

        .btn-submit { background: var(--primary); color: white; width: 100%; margin-top: 30px; padding: 18px; font-size: 1.1em; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body>

<div class="container">
    <div class="top-bar">
        <div class="nav-btns">
            <button class="btn btn-nav active" onclick="show('recolte')">1. COLLECTE INFIRMIÈRE</button>
            <button class="btn btn-nav" onclick="show('data')">2. BASE DE DONNÉES</button>
        </div>
        <button class="btn btn-export" onclick="exportExcel()">⬇️ EXPORT SCIENTIFIQUE (CSV)</button>
    </div>

    <div id="recolte" class="page active">
        <form id="masterForm">
            <h2>I. PROFIL PROFESSIONNEL INFIRMIER</h2>
            <div class="grid">
                <div class="field"><label>Code ID *</label><input type="text" name="id" required></div>
                <div class="field"><label>Service d'affectation *</label><input type="text" name="service" required></div>
                <div class="field"><label>Niveau d'étude *</label>
                    <select name="etude"><option>A2 (Diplômée)</option><option>A1 (Graduée)</option><option>A0 (Licenciée)</option><option>Master+</option></select>
                </div>
                <div class="field"><label>Avez-vous reçu une formation continue sur le cancer du sein ?</label>
                    <select name="form_cont"><option value="0">Non, jamais</option><option value="1">Oui, il y a moins de 2 ans</option><option value="0.5">Oui, il y a longtemps</option></select>
                </div>
            </div>

            <h2>II. CONNAISSANCES CLINIQUES & DÉPISTAGE (Savoir)</h2>
            <div class="grid">
                <div class="field"><label>La parité élevée (>5 enfants) protège-t-elle ?</label>
                    <select name="c1"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>Signe suspect : Une asymétrie brutale des seins ?</label>
                    <select name="c2"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>Âge légal du dépistage mammographique en RDC :</label>
                    <input type="number" name="c3_age" placeholder="ex: 40">
                </div>
                <div class="field"><label>L'allaitement prolongé réduit le risque ?</label>
                    <select name="c4"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>L'examen clinique doit inclure la chaîne ganglionnaire ?</label>
                    <select name="c5"><option value="1">Vrai (Indispensable)</option><option value="0">Faux</option></select>
                </div>
            </div>

            <h2>III. ATTITUDES & POSTURE PROFESSIONNELLE</h2>
            <table class="likert-table">
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Le dépistage est inutile si on n'a pas les moyens de soigner (pessimisme).</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">Je suis à l'aise pour palper les seins d'une patiente.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td class="text-left">Le cancer est une punition divine ou un sort (croyance).</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                </tbody>
            </table>

            <h2>IV. PRATIQUES INFIRMIÈRES & ÉDUCATION DES PATIENTES</h2>
            <div class="grid">
                <div class="field"><label>Démontrez-vous physiquement l'AES aux patientes ?</label>
                    <select name="p1"><option>Souvent</option><option>Rarement</option><option>Jamais</option></select>
                </div>
                <div class="field"><label>Recommandez-vous la mammographie aux femmes de >40 ans ?</label>
                    <select name="p2"><option>Oui</option><option>Non</option></select>
                </div>
                <div class="field"><label>Documentez-vous l'examen des seins dans le dossier infirmier ?</label>
                    <select name="p3"><option>Toujours</option><option>Si anomalie trouvée</option><option>Jamais</option></select>
                </div>
            </div>

            <h2>V. BARRIÈRES À L'HGRM MAKALA</h2>
            <div class="field">
                <label>Quels obstacles rencontrez-vous dans votre pratique ?</label>
                <input type="checkbox" name="bar" value="Outils"> Manque de supports visuels (boîtes à images)<br>
                <input type="checkbox" name="bar" value="Langue"> Difficulté de communication (Langues locales)<br>
                <input type="checkbox" name="bar" value="Pudeur"> Pudeur excessive des patientes<br>
                <input type="checkbox" name="bar" value="Formation"> Manque de mise à jour médicale
            </div>

            <button type="button" class="btn-submit" onclick="saveEntry()">ENREGISTRER LA FICHE INFIRMIÈRE</button>
        </form>
    </div>

    <div id="data" class="page">
        <h2>Base de données des infirmières</h2>
        <div style="overflow-x:auto;">
            <table id="dataTable" style="width:100%; border-collapse: collapse; font-size: 0.85em;">
                <thead style="background:#f1f5f9;">
                    <tr><th>ID</th><th>Service</th><th>Etude</th><th>Score Savoir</th><th>Pratique Educ.</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('cap_infirmier_makala')) || [];

    function show(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.btn-nav').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        if(id === 'data') refreshTable();
    }

    function saveEntry() {
        const form = document.getElementById('masterForm');
        const data = Object.fromEntries(new FormData(form).entries());
        
        let score = 0;
        ['c1','c2','c4','c5'].forEach(q => score += parseFloat(data[q] || 0));
        data.scoreSavoir = score;
        
        db.push(data);
        localStorage.setItem('cap_infirmier_makala', JSON.stringify(db));
        alert("Fiche Infirmier enregistrée !");
        form.reset();
    }

    function refreshTable() {
        const tbody = document.querySelector('#dataTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr style="border-bottom:1px solid #eee;">
                <td>${d.id}</td><td>${d.service}</td><td>${d.etude}</td>
                <td>${d.scoreSavoir}/4</td><td>${d.p1}</td>
            </tr>
        `).join('');
    }

    function exportExcel() {
        if(db.length === 0) return alert("Aucune donnée.");
        let csv = "ID,Service,Etude,FormCont,ScoreSavoir,AttitudeDieu,PratiqueDemo,Barrieres\n";
        db.forEach(d => {
            csv += `${d.id},${d.service},${d.etude},${d.form_cont},${d.scoreSavoir},${d.att3},${d.p1},${d.bar}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a');
        a.href = window.URL.createObjectURL(blob);
        a.download = 'Recherche_CAP_Infirmiers_Makala.csv';
        a.click();
    }
</script>
</body>
</html>
