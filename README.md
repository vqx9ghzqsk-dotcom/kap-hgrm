<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 28px; font-weight: bold; color: #b03060; }
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.5s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 60px; border: 1px solid #ccc; font-size: 10px; padding: 4px; border-radius: 4px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tabH2" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="tabH3" onclick="showTab(3)">3. ANALYSE</div>
        <div class="tab admin-only" id="tabH4" onclick="showTab(4)">4. RECOMMANDATIONS</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="tab1" class="content-section active">
        <form class="form-content" id="kapForm">
            <div class="section-title">I. PROFIL DE L'INFIRMIER(E)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete" name="code"></select></div>
                <div class="field"><label>Service</label><select name="service"><option>Gynécologie</option><option>Maternité</option><option>Chirurgie</option><option>Autre</option></select></div>
                <div class="field"><label>Niveau d'étude</label><select name="etude"><option value="A2">A2</option><option value="A1" selected>A1</option><option value="L">Licence</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Expérience (Années)</label><select id="exp-select" name="experience"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause de décès cancer RDC ?</label><select name="k1"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Âge début autopalpation ?</label><select name="k2"><option value="0">12 ans</option><option value="1">20 ans</option></select></div>
                <div class="field"><label>Moment idéal AES ?</label><select name="k3"><option value="1">J+7 après règles</option><option value="0">Pendant règles</option></select></div>
            </div>

            <div class="section-title">III. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Palpation clinique (ECS)</label>
                    <select name="pra1"><option value="1">Systématique</option><option value="0">Si plainte</option></select>
                </div>
                <div class="field">
                    <label>Enseignement AES</label>
                    <select name="pra2"><option value="1">Démonstration</option><option value="0">Verbal/Aucun</option></select>
                </div>
            </div>

            <div class="section-title">IV. OBSTACLES</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Salle"> Pas de salle isolée</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Cout"> Coût élevé examens</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Savoir</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>N Total</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div>Savoir Bon</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div>Pratique Correcte</div></div>
        </div>
        
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">RECOMMANDATIONS</div>
        <div id="summary" style="background:#fff; padding:20px; border:1px solid #ddd;">---</div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "TON_URL_ICI"; 

    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n >= 3) calculerStatistiques();
    }

    async function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));

        const entry = {
            code: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: fd.get('experience'),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 1 ? 'Correcte' : 'Incorrecte'
        };

        db.push(entry);
        actualiserTableau();
        
        try {
            fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            alert("Fiche enregistrée !");
            form.reset();
        } catch (e) { alert("Erreur réseau"); }
    }

    function actualiserTableau() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => 
            `<tr><td>${d.code}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`
        ).join('');
    }

    function calculerStatistiques() {
        let n = db.length; if(n === 0) return;
        let kHigh = db.filter(d => d.savoir === 'Bon').length;
        let pGood = db.filter(d => d.pratique === 'Correcte').length;
        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";
        
        document.getElementById('summary').innerHTML = pGood/n < 0.5 ? 
            "<b>Alerte :</b> Pratique insuffisante. Recommandation : Aménager d'urgence un local isolé à l'HGRM." : 
            "Pratique satisfaisante. Continuer la sensibilisation.";
    }

    function exportCSV() {
        let csv = "Code,Savoir,Pratique\n" + db.map(d => `${d.code},${d.savoir},${d.pratique}`).join("\n");
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'Data_KAP.csv'; a.click();
    }

    window.onload = () => {
        for (let i = 1; i <= 100; i++) document.getElementById('code-enquete').options.add(new Option("ID: " + i, i));
        for (let i = 18; i <= 65; i++) document.getElementById('age-select').options.add(new Option(i + " ans", i));
        for (let i = 0; i <= 40; i++) document.getElementById('exp-select').options.add(new Option(i + " ans", i));
    };
</script>
</body>
</html>
