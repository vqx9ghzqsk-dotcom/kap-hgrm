<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Expert CAP - HGRM Makala (Version Finale)</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', sans-serif; background: var(--bg); margin: 0; padding: 10px; }
        .container { max-width: 1100px; margin: auto; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 5px 25px rgba(0,0,0,0.1); }
        
        /* Menu */
        .header { display: flex; justify-content: space-between; border-bottom: 2px solid #eee; margin-bottom: 20px; padding-bottom: 10px; position: sticky; top: 0; background: white; z-index: 100; }
        .btn { padding: 10px 15px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; }
        .btn-tab { background: #e2e8f0; margin-right: 5px; }
        .btn-tab.active { background: var(--primary); color: white; }
        .btn-export { background: #059669; color: white; }

        .page { display: none; }
        .page.active { display: block; }

        /* Formulaire */
        h2 { color: var(--primary); font-size: 1em; border-left: 5px solid var(--primary); padding: 8px; margin-top: 25px; background: #fff1f2; text-transform: uppercase; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; }
        .box { border: 1px solid #e2e8f0; padding: 12px; border-radius: 8px; background: #fff; }
        label { display: block; margin-bottom: 6px; font-weight: 600; font-size: 0.85em; color: #334155; }
        select, input { width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; }

        /* Tableau Likert */
        table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.85em; }
        th, td { border: 1px solid #e2e8f0; padding: 8px; text-align: center; }
        .text-left { text-align: left; background: #f8fafc; font-weight: 500; }

        .save-bar { background: var(--primary); color: white; width: 100%; margin-top: 30px; padding: 15px; border: none; border-radius: 8px; font-size: 1.1em; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <div>
            <button class="btn btn-tab active" onclick="nav('saisie')">NOUVELLE FICHE</button>
            <button class="btn btn-tab" onclick="nav('view')">BASE DE DONNÉES</button>
        </div>
        <button class="btn btn-export" onclick="exportExcel()">EXPORTER VERS EXCEL</button>
    </div>

    <div id="saisie" class="page active">
        <form id="capForm">
            <h2>I. Profil de l'Infirmier(ère)</h2>
            <div class="grid">
                <div class="box"><label>ID / Code *</label><input type="text" name="id" required></div>
                <div class="box"><label>Service (ex: Chirurgie)</label><input type="text" name="service"></div>
                <div class="box"><label>Niveau d'études</label><select name="etude"><option>A2</option><option>A1</option><option>A0</option><option>Master</option></select></div>
                <div class="box"><label>Expérience (Années)</label><input type="number" name="exp"></div>
            </div>

            <h2>II. Connaissances (Vrai/Faux/NSP)</h2>
            <div class="grid">
                <div class="box"><label>Le risque augmente avec l'âge ?</label><select name="c1"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="box"><label>La nulliparité est un risque ?</label><select name="c2"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="box"><label>L'allaitement est protecteur ?</label><select name="c3"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="box"><label>L'examen clinique doit inclure l'aisselle ?</label><select name="c4"><option value="0">---</option><option value="1">Vrai</option><option value="0">Faux</option></select></div>
            </div>

            <h2>III. Attitudes (Échelle de 1 à 5)</h2>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Le cancer est une fatalité en RDC.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">Je me sens capable de dépister une masse.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                </tbody>
            </table>

            <h2>IV. Pratiques Professionnelles</h2>
            <div class="grid">
                <div class="box"><label>Palpation systématique ?</label><select name="p1"><option>Toujours</option><option>Si plainte</option><option>Jamais</option></select></div>
                <div class="box"><label>Démonstration de l'AES ?</label><select name="p2"><option>Oui</option><option>Non</option></select></div>
                <div class="box"><label>Référence mammographie ?</label><select name="p3"><option>Souvent</option><option>Rarement</option></select></div>
            </div>

            <button type="button" class="save-bar" onclick="enregistrer()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="view" class="page">
        <h2>Données collectées (Total: <span id="compteur">0</span>)</h2>
        <div style="overflow-x:auto;">
            <table id="tableMain">
                <thead><tr style="background:#f1f5f9;"><th>ID</th><th>Service</th><th>Score</th><th>Niveau</th><th>Action</th></tr></thead>
                <tbody></tbody>
            </table>
        </div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('makala_db_expert')) || [];

    function nav(p) {
        document.querySelectorAll('.page').forEach(pg => pg.classList.remove('active'));
        document.querySelectorAll('.btn-tab').forEach(b => b.classList.remove('active'));
        document.getElementById(p).classList.add('active');
        event.target.classList.add('active');
        if(p === 'view') rafraichir();
    }

    function enregistrer() {
        const f = document.getElementById('capForm');
        const d = Object.fromEntries(new FormData(f).entries());
        
        let score = (parseInt(d.c1)||0) + (parseInt(d.c2)||0) + (parseInt(d.c3)||0) + (parseInt(d.c4)||0);
        d.score = score;
        d.niveau = score >= 3 ? 'Bon' : (score == 2 ? 'Moyen' : 'Faible');

        db.push(d);
        localStorage.setItem('makala_db_expert', JSON.stringify(db));
        alert("Fiche " + d.id + " enregistrée avec succès !");
        f.reset();
    }

    function rafraichir() {
        document.getElementById('compteur').innerText = db.length;
        const body = document.querySelector('#tableMain tbody');
        body.innerHTML = db.map((d, index) => `
            <tr>
                <td>${d.id}</td><td>${d.service}</td><td>${d.score}/4</td>
                <td style="font-weight:bold; color:${d.niveau==='Bon'?'green':'red'}">${d.niveau}</td>
                <td><button onclick="supprimer(${index})" style="color:red; border:none; background:none; cursor:pointer;">Supprimer</button></td>
            </tr>
        `).join('');
    }

    function supprimer(i) {
        if(confirm("Supprimer cette fiche ?")) {
            db.splice(i, 1);
            localStorage.setItem('makala_db_expert', JSON.stringify(db));
            rafraichir();
        }
    }

    function exportExcel() {
        if(db.length === 0) return alert("Base vide !");
        let csv = "ID,Service,Etude,Exp,Score,Niveau,Pratique,DemontreAES\n";
        db.forEach(d => { csv += `${d.id},${d.service},${d.etude},${d.exp},${d.score},${d.niveau},${d.p1},${d.p2}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url; a.download = 'Resultats_CAP_Makala.csv'; a.click();
    }
</script>
</body>
</html>
