<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        :root { --primary: #b03060; --secondary: #fce4ec; --dark: #2c3e50; --success: #27ae60; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.15); overflow: hidden; }
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid var(--primary); padding: 12px; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 12px 18px; font-weight: bold; font-size: 13px; border-radius: 6px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.3s; }
        .tab.active { background: var(--primary); color: white; border-color: var(--primary); }
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: var(--success); color: white; border: none; padding: 10px 20px; border-radius: 6px; font-weight: bold; cursor: pointer; }

        .content-section { display: none; padding: 25px; }
        .content-section.active { display: block; }

        /* Formulaire */
        .section-title { background: var(--secondary); color: var(--primary); padding: 15px; font-weight: bold; border-left: 8px solid var(--primary); margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: var(--dark); }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; }

        /* Tableaux */
        table { width: 100%; border-collapse: collapse; margin-top: 10px; background: white; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; font-size: 12px; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; font-size: 13px; }
        .text-left { text-align: left; padding-left: 15px; }

        /* Dashboard & Stats */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin-bottom: 30px; }
        .stat-card { background: white; padding: 25px; border-radius: 10px; text-align: center; border: 1px solid #eee; border-bottom: 5px solid var(--primary); box-shadow: 0 4px 6px rgba(0,0,0,0.05); }
        .stat-val { font-size: 35px; font-weight: bold; color: var(--primary); display: block; }
        .stat-label { font-size: 12px; color: #777; font-weight: bold; text-transform: uppercase; margin-top: 5px; }

        .analysis-box { background: #f9f9f9; padding: 20px; border-radius: 8px; border: 1px solid #ddd; line-height: 1.6; }
        .btn-save { width: 100%; background: var(--primary); color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; box-shadow: 0 5px 15px rgba(176, 48, 96, 0.3); }

        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.05; transition: 0.5s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 50px; padding: 5px; font-size: 10px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE DES DONNÉES</div>
        <div class="tab admin-only" id="t2" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="t3" onclick="showTab(3)">3. ANALYSE STATISTIQUE</div>
        <div class="tab admin-only" id="t4" onclick="showTab(4)">4. CONCLUSION</div>
        <button type="button" class="btn-excel admin-only" id="exBtn" onclick="exportCSV()">📊 EXPORTER CSV</button>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            <div class="section-title">I. Profil de l'intervenant</div>
            <div class="row">
                <div class="field"><label>ID Enquêté</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service</label>
                    <select name="service">
                        <option>Gynécologie</option><option>Chirurgie</option><option>Maternité</option><option>Urgences</option>
                    </select>
                </div>
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude" id="etude">
                        <option value="A2">A2 (Diplômé d'Etat)</option>
                        <option value="A1">A1 (Gradué)</option>
                        <option value="L2">L2 (Licencié)</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. Connaissances (Savoir)</div>
            <div class="row">
                <div class="field"><label>Cancer du sein = 1ère cause décès RDC ?</label><select name="k1"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Âge début Autopalpation</label><select name="k2"><option value="0">12 ans</option><option value="1">20 ans</option></select></div>
                <div class="field"><label>Moment idéal AES</label><select name="k3"><option value="1">7j après règles</option><option value="0">Pendant règles</option></select></div>
            </div>

            <div class="section-title">III. Pratiques (Savoir-Faire)</div>
            <div class="row">
                <div class="field"><label>Palpation clinique (ECS)</label><select name="pra1"><option value="1">Systématique</option><option value="0">Rarement</option></select></div>
                <div class="field"><label>Enseignement AES aux patientes</label><select name="pra2"><option value="1">Démonstration</option><option value="0">Verbal/Jamais</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">Base de données en temps réel</div>
        <div style="overflow-x:auto;">
            <table id="tableDepouillement">
                <thead><tr><th>Code</th><th>Service</th><th>Âge</th><th>Étude</th><th>Savoir (Score)</th><th>Pratique (Score)</th><th>Statut Savoir</th></tr></thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">Indicateurs de Performance</div>
        <div class="stats-grid">
            <div class="stat-card"><span class="stat-val" id="res-n">0</span><span class="stat-label">Échantillon (N)</span></div>
            <div class="stat-card"><span class="stat-val" id="res-k">0%</span><span class="stat-label">Savoir Satisfaisant</span></div>
            <div class="stat-card"><span class="stat-val" id="res-p">0%</span><span class="stat-label">Pratique Correcte</span></div>
        </div>
        <div class="analysis-box" id="stat-interpretation">
            En attente de données pour l'analyse croisée...
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">Synthèse et Recommandations</div>
        <div id="final-summary" class="analysis-box" style="background: white; border: 2px solid var(--primary);">
            Veuillez collecter des données pour générer le rapport.
        </div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
            alert("Accès Expert Déverrouillé");
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 3) runAnalysis();
        if(n === 4) generateConclusion();
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
            scoreK: sk,
            scoreP: sp,
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 1 ? 'Correcte' : 'Incorrecte'
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            db.push(entry);
            updateTable();
            alert("Fiche enregistrée avec succès !");
            form.reset();
        } catch (e) { alert("Erreur d'envoi"); }
    }

    function updateTable() {
        const tbody = document.querySelector('#tableDepouillement tbody');
        tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.service}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.scoreK}/3</td><td>${d.scoreP}/2</td><td>${d.savoir}</td></tr>`).join('');
    }

    function runAnalysis() {
        let n = db.length; if(n === 0) return;
        let kGood = db.filter(d => d.savoir === 'Bon').length;
        let pGood = db.filter(d => d.pratique === 'Correcte').length;
        
        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(kGood/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";

        let text = `Sur un échantillon de ${n} infirmiers, le niveau de connaissance global est de ${Math.round(kGood/n*100)}%. `;
        if (kGood/n < 0.5) text += "On observe une carence théorique majeure qui nécessite une intervention urgente.";
        else text += "La base théorique est satisfaisante.";
        
        document.getElementById('stat-interpretation').innerHTML = `<strong>Analyse automatique :</strong><br>${text}`;
    }

    function generateConclusion() {
        let n = db.length; if(n < 1) return;
        let kP = Math.round(db.filter(d => d.savoir === 'Bon').length / n * 100);
        let pP = Math.round(db.filter(d => d.pratique === 'Correcte').length / n * 100);

        let conclusion = `<h4>CONCLUSION GÉNÉRALE</h4>`;
        conclusion += `<p>L'étude montre un décalage entre le savoir (${kP}%) et la pratique effective (${pP}%). </p>`;
        conclusion += `<h4>RECOMMANDATIONS</h4>`;
        conclusion += `<ul>
            <li>Organiser des séances de recyclage pratique sur l'examen clinique des seins.</li>
            <li>Intégrer systématiquement la sensibilisation au cancer dans les consultations prénatales et gynécologiques.</li>
            <li>Améliorer le plateau technique de l'HGRM pour faciliter les références.</li>
        </ul>`;
        document.getElementById('final-summary').innerHTML = conclusion;
    }

    function exportCSV() {
        let csv = "Code,Service,Age,Etude,Savoir,Pratique\n";
        db.forEach(d => { csv += `${d.code},${d.service},${d.age},${d.etude},${d.savoir},${d.pratique}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'Rapport_KAP.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete'); for (let i = 1; i <= 200; i++) cs.options.add(new Option("ID: " + i, i));
        const as = document.getElementById('age-select'); for (let i = 18; i <= 65; i++) as.options.add(new Option(i + " ans", i));
    };
</script>
</body>
</html>
