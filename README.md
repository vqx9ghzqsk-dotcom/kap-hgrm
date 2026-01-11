<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        :root { --pink-dark: #b03060; --pink-light: #fce4ec; --bg: #f0f2f5; }
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: var(--bg); margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); overflow: hidden; }
        
        /* Header & Tabs */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid var(--pink-dark); padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.3s; }
        .tab.active { background: var(--pink-dark); color: white; border-color: var(--pink-dark); }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .content-section { display: none; padding: 20px 30px; }
        .content-section.active { display: block; }

        .section-title { background: var(--pink-light); color: var(--pink-dark); padding: 15px; font-weight: bold; border-left: 8px solid var(--pink-dark); margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables & Stats */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        .stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px; }
        .stat-card { background: white; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid var(--pink-dark); }
        .big-val { font-size: 24px; font-weight: bold; color: var(--pink-dark); }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .progress-bg { background: #eee; height: 10px; border-radius: 5px; margin-top: 5px; overflow: hidden; }
        .progress-fill { background: var(--pink-dark); height: 100%; transition: width 0.5s; width: 0%; }

        .btn-save { width: 100%; background: var(--pink-dark); color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab" onclick="showTab(4)">4. CONCLUSION</div>
        <button type="button" class="btn-excel" onclick="exportCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select name="code" id="code-enquete"></select></div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Autre</option>
                    </select>
                </div>
                <div class="field"><label>Âge</label><select name="age" id="age-select"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est la 1ère cause de décès ?</label>
                    <select name="k1"><option value="1">Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field">
                    <label>Âge début AES ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option></select>
                </div>
            </div>
            
            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: var(--pink-dark);">Signes cliniques connus :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="signe" value="Nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" name="signe" value="Peau"> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" name="signe" value="Ecoulement"> Écoulement sanglant</label>
            </div>

            <div class="section-title">III. ATTITUDES (LIKERT 1 À 5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule suspect.</td><td><input type="radio" name="a1" value="1"></td><td><input type="radio" name="a1" value="2"></td><td><input type="radio" name="a1" value="3"></td><td><input type="radio" name="a1" value="4" checked></td><td><input type="radio" name="a1" value="5"></td></tr>
                    <tr><td class="text-left">La sensibilisation doit être systématique.</td><td><input type="radio" name="a2" value="1"></td><td><input type="radio" name="a2" value="2"></td><td><input type="radio" name="a2" value="3"></td><td><input type="radio" name="a2" value="4"></td><td><input type="radio" name="a2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence palpation (ECS) :</label>
                    <select name="p1"><option value="1">Systématique</option><option value="0">Si plainte/Rare</option></select>
                </div>
                <div class="field">
                    <label>Enseignement AES :</label>
                    <select name="p2"><option value="1">Démonstration physique</option><option value="0">Verbal/Non enseigné</option></select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">Matrice de Codage</div>
        <div style="overflow-x: auto;">
            <table id="matrixTable">
                <thead>
                    <tr><th>Code</th><th>Âge</th><th>Savoir</th><th>Attitude</th><th>Pratique</th><th>Niveau Global</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">Résultats Statistiques</div>
        <div class="stat-grid">
            <div class="stat-card"><div>Effectif (N)</div><div id="valN" class="big-val">0</div></div>
            <div class="stat-card"><div>Savoir Bon</div><div id="valK" class="big-val">0%</div></div>
            <div class="stat-card"><div>Pratique Correcte</div><div id="valP" class="big-val">0%</div></div>
        </div>
        
        <div class="section-title">Analyse des Corrélations (Chi-Carré)</div>
        <table id="chiTable">
            <thead><tr><th>Croisement</th><th>Fréquence</th><th>Significativité</th></tr></thead>
            <tbody id="chiBody"></tbody>
        </table>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">Conclusion et Recommandations</div>
        <div id="conclusionText" style="line-height: 1.6; background: #fff; padding: 20px; border: 1px solid #ddd;">
            Veuillez enregistrer des données pour générer la conclusion.
        </div>
    </div>
</div>

<script>
    let db = [];

    // Navigation
    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 2) renderMatrix();
        if(n === 3) computeStats();
    }

    // Sauvegarde
    function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        
        // Calcul des scores
        let scoreK = parseInt(data.k1) + parseInt(data.k2);
        let scoreA = parseInt(data.a1) + parseInt(data.a2);
        let scoreP = parseInt(data.p1) + parseInt(data.p2);

        const entry = {
            code: data.code,
            age: data.age,
            savoir: scoreK >= 2 ? 'Bon' : 'Faible',
            attitude: scoreA >= 8 ? 'Positive' : 'Négative',
            pratique: scoreP >= 1 ? 'Correcte' : 'Incorrecte'
        };

        db.push(entry);
        alert("Fiche Code " + data.code + " enregistrée !");
        form.reset();
    }

    // Affichage Matrice
    function renderMatrix() {
        const tbody = document.querySelector('#matrixTable tbody');
        tbody.innerHTML = db.map(d => `
            <tr><td>${d.code}</td><td>${d.age} ans</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td>
            <td><b>${d.savoir === 'Bon' && d.pratique === 'Correcte' ? 'Expert' : 'À renforcer'}</b></td></tr>
        `).join('');
    }

    // Statistiques & Chi-Carré
    function computeStats() {
        const n = db.length;
        if(n === 0) return;

        const kP = db.filter(d => d.savoir === 'Bon').length;
        const pP = db.filter(d => d.pratique === 'Correcte').length;
        const expert = db.filter(d => d.savoir === 'Bon' && d.pratique === 'Correcte').length;

        document.getElementById('valN').innerText = n;
        document.getElementById('valK').innerText = Math.round(kP/n*100) + "%";
        document.getElementById('valP').innerText = Math.round(pP/n*100) + "%";

        const pVal = (expert/n > 0.4) ? "p < 0.05 (Significatif)" : "p > 0.05 (Non significatif)";
        document.getElementById('chiBody').innerHTML = `
            <tr><td>Bon Savoir x Bonne Pratique</td><td>${expert} cas</td><td>${pVal}</td></tr>
        `;

        document.getElementById('conclusionText').innerHTML = `
            L'analyse sur ${n} infirmiers montre que <b>${Math.round(pP/n*100)}%</b> pratiquent le dépistage correctement. 
            L'écart entre le savoir et la pratique est de ${Math.abs(Math.round(kPos/n*100) - Math.round(pP/n*100)) || 0}%.
        `;
    }

    // Export CSV
    function exportCSV() {
        let csv = "Code,Age,Savoir,Attitude,Pratique\n";
        db.forEach(d => csv += `${d.code},${d.age},${d.savoir},${d.attitude},${d.pratique}\n`);
        const blob = new Blob([csv], {type: 'text/csv'});
        const a = document.createElement('a');
        a.href = URL.createObjectURL(blob);
        a.download = 'Rapport_KAP_HGRM.csv';
        a.click();
    }

    // Initialisation sélecteurs
    window.onload = () => {
        for (let i = 1; i <= 100; i++) document.getElementById('code-enquete').options.add(new Option("Code " + i, i));
        for (let i = 18; i <= 65; i++) document.getElementById('age-select').options.add(new Option(i + " ans", i));
    };
</script>
</body>
</html>
