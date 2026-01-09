<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Système Expert CAP Complet - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --success: #059669; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); margin: 0; padding: 15px; color: var(--secondary); }
        .container { max-width: 1250px; margin: auto; background: white; padding: 25px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        
        .top-bar { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; border-bottom: 2px solid #eee; padding-bottom: 15px; position: sticky; top: 0; background: white; z-index: 100; }
        .nav-btns { display: flex; gap: 8px; flex-wrap: wrap; }
        .btn { padding: 10px 16px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.2s; }
        .btn-nav { background: #e2e8f0; color: var(--secondary); }
        .btn-nav.active { background: var(--primary); color: white; }
        .btn-export { background: var(--success); color: white; }

        .page { display: none; }
        .page.active { display: block; }

        h2 { color: var(--primary); font-size: 1.1em; border-left: 5px solid var(--primary); padding-left: 12px; margin-top: 25px; background: #fff1f2; padding-block: 8px; text-transform: uppercase; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; }
        .field { border: 1px solid #e2e8f0; padding: 12px; border-radius: 8px; background: #fff; }
        label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 0.85em; }
        input, select, textarea { width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; box-sizing: border-box; }
        
        .likert-table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.85em; }
        .likert-table th, .likert-table td { border: 1px solid #e2e8f0; padding: 8px; text-align: center; }
        .text-left { text-align: left; background: #f8fafc; font-weight: bold; }

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
            <h2>I. IDENTIFICATION & CONTEXTE PROFESSIONNEL</h2>
            <div class="grid">
                <div class="field"><label>ID Enquêtée *</label><input type="text" name="id" required></div>
                <div class="field"><label>Service (ex: Maternité, Chirurgie) *</label><input type="text" name="service" required></div>
                <div class="field"><label>Niveau d'études *</label>
                    <select name="etude"><option>A2</option><option>A1/Graduée</option><option>A0/Licenciée</option><option>Master/DS</option></select>
                </div>
                <div class="field"><label>Ancienneté Pro (ans)</label><input type="number" name="exp"></div>
                <div class="field"><label>Avez-vous déjà soigné une patiente cancéreuse ?</label>
                    <select name="soin_connais"><option value="Oui">Oui</option><option value="Non">Non</option></select>
                </div>
            </div>

            <h2>II. CONNAISSANCES APPROFONDIES (SAVOIRS)</h2>
            <div class="grid">
                <div class="field"><label>La nulliparité (ne pas avoir d'enfant) est un risque ?</label>
                    <select name="c1"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>La ménopause tardive augmente le risque ?</label>
                    <select name="c2"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>L'AES doit se faire 7 jours après les règles ?</label>
                    <select name="c3"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>Le cancer du sein est-il contagieux ? (Mythe)</label>
                    <select name="c4"><option value="1">Faux</option><option value="0">Vrai</option></select>
                </div>
                <div class="field"><label>L'échographie est-elle utile chez la femme de <35 ans ?</label>
                    <select name="c5"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field"><label>Une plaie qui ne guérit pas au sein est un signe ?</label>
                    <select name="c6"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
            </div>

            <h2>III. ATTITUDES & PERCEPTIONS (LIKERT 1-5)</h2>
            <table class="likert-table">
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je pense que la médecine traditionnelle peut guérir le cancer.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">J'ai peur de découvrir un nodule lors d'un examen.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td class="text-left">Le dépistage précoce coûte trop cher pour mes patientes.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                    <tr><td class="text-left">La mastectomie (ablation) est une mutilation inacceptable.</td><td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td></tr>
                </tbody>
            </table>

            <h2>IV. PRATIQUES PROFESSIONNELLES</h2>
            <div class="grid">
                <div class="field"><label>Demandez-vous l'histoire familiale de cancer ?</label>
                    <select name="p1"><option>Systématiquement</option><option>Parfois</option><option>Jamais</option></select>
                </div>
                <div class="field"><label>Inspectez-vous les aisselles (creux axillaires) ?</label>
                    <select name="p2"><option>Oui</option><option>Non</option></select>
                </div>
                <div class="field"><label>Remettez-vous des dépliants sur le cancer ?</label>
                    <select name="p3"><option>Oui</option><option>Non (Manque de supports)</option></select>
                </div>
                <div class="field"><label>Nombre moyen de palpations faites ce mois :</label>
                    <input type="number" name="p4" placeholder="0">
                </div>
            </div>

            <h2>V. BARRIÈRES SYSTÉMIQUES (RDC)</h2>
            <div class="field">
                <label>Qu'est-ce qui vous empêche d'agir plus ? (Plusieurs choix)</label>
                <input type="checkbox" name="bar" value="Formation"> Absence de protocoles écrits<br>
                <input type="checkbox" name="bar" value="Religion"> Influence religieuse des patientes<br>
                <input type="checkbox" name="bar" value="Materiel"> Manque de salle d'examen isolée<br>
                <input type="checkbox" name="bar" value="Honte"> Pudeur/Honte de la patiente
            </div>

            <button type="button" class="btn-submit" onclick="saveEntry()">ENREGISTRER LA FICHE COMPLÈTE</button>
        </form>
    </div>

    <div id="data" class="page">
        <h2>Matrice de Dépouillement avec Variables Croisées</h2>
        <div style="overflow-x:auto;">
            <table id="dataTable" style="width:100%; border-collapse: collapse; font-size: 0.8em;">
                <thead style="background:#f1f5f9;">
                    <tr><th>ID</th><th>Sexe</th><th>Etude</th><th>Score Savoir</th><th>Attitude (Moy)</th><th>Pratique</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="stats" class="page">
        <h2>Statistiques de Recherche</h2>
        <div class="grid">
            <div class="field" style="text-align:center;"><h3>N Total</h3><div id="sn" style="font-size:2em; font-weight:bold;">0</div></div>
            <div class="field" style="text-align:center;"><h3>Niveau de Savoir Moyen</h3><div id="sc" style="font-size:2em; font-weight:bold;">0%</div></div>
        </div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('cap_makala_expert_final')) || [];

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
        
        // Calcul du score de savoir sur 6 questions
        let score = 0;
        for(let i=1; i<=6; i++) { score += parseInt(data['c'+i] || 0); }
        data.scoreSavoir = score;
        
        db.push(data);
        localStorage.setItem('cap_makala_expert_final', JSON.stringify(db));
        alert("Fiche ajoutée avec succès !");
        form.reset();
    }

    function refreshTable() {
        const tbody = document.querySelector('#dataTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr style="border-bottom:1px solid #eee;">
                <td>${d.id}</td><td>${d.sexe || 'F'}</td><td>${d.etude}</td>
                <td>${d.scoreSavoir}/6</td>
                <td>${d.att1 || 0}/5</td>
                <td>${d.p1}</td>
            </tr>
        `).join('');
    }

    function refreshStats() {
        const n = db.length;
        if(n === 0) return;
        const total = db.reduce((acc, curr) => acc + parseInt(curr.scoreSavoir), 0);
        document.getElementById('sn').innerText = n;
        document.getElementById('sc').innerText = ((total / (n * 6)) * 100).toFixed(1) + "%";
    }

    function exportExcel() {
        if(db.length === 0) return alert("Base vide.");
        let csv = "ID,Service,Etude,Exp,ScoreSavoir,Attitude1,Pratique1,Barriere\n";
        db.forEach(d => {
            csv += `${d.id},${d.service},${d.etude},${d.exp},${d.scoreSavoir},${d.att1},${d.p1},${d.bar}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a');
        a.href = window.URL.createObjectURL(blob);
        a.download = 'CAP_CancerSein_RDC.csv';
        a.click();
    }
</script>
</body>
</html>
