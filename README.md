<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR RDC)</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* Boutons Actions */
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-delete-all { background: #c62828; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 11px; }
        .btn-delete-row { background: #ffebee; color: #c62828; border: 1px solid #c62828; padding: 4px 8px; border-radius: 4px; cursor: pointer; font-size: 10px; font-weight: bold; }
        .btn-delete-row:hover { background: #c62828; color: white; }

        /* Contenu */
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections Formulaire */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"] { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        /* Tableaux */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        /* Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        /* Bouton Enregistrer */
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        
        /* Analyse */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 20px; font-style: italic; color: #1b5e20; margin-top: 20px; border-radius: 0 8px 8px 0; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 20px; font-style: italic; color: #b71c1c; margin-top: 20px; border-radius: 0 8px 8px 0; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE CROISÉE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION & SYNTHÈSE</button>
        <button type="button" class="btn-delete-all" onclick="clearFullDatabase()">🗑️ VIDER LA BASE</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL PROFESSIONNEL</div>
            <div class="row">
                <div class="field"><label>1. Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>2. Service d'affectation</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Médecine Interne</option>
                        <option>Chirurgie</option>
                        <option>Urgences / Autre</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>3. Niveau d'étude</label><select id="niveau"><option>A2</option><option selected>A1</option><option>A0</option></select></div>
                <div class="field"><label>4. Ancienneté</label><input type="number" id="anciennete" value="5"></div>
                <div class="field"><label>5. Sexe</label><select id="sexe"><option>F</option><option>M</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="row">
                <div class="field"><label>1ère cause décès cancer RDC ?</label><select id="q-cause"><option value="vrai">Vrai</option><option value="faux">Faux</option></select></div>
                <div class="field"><label>Âge 1ère Mammographie ?</label><select id="q-age-mammo"><option value="20">20 ans</option><option value="50">50 ans</option></select></div>
            </div>

            <div class="sub-title">Facteurs de risque</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Famille</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool/Tabac</label>
            </div>

            <div class="section-title">III. ATTITUDES (1-5)</div>
            <table>
                <tr><td class="td-left">L'éducation à l'AES est mon rôle.</td><td>1<input type="radio" name="att1" value="1"></td><td>2<input type="radio" name="att1" value="2"></td><td>3<input type="radio" name="att1" value="3"></td><td>4<input type="radio" name="att1" value="4"></td><td>5<input type="radio" name="att1" value="5" checked></td></tr>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Technique palpation ?</label><select id="prac-main"><option value="pulpe">Pulpe des doigts</option><option value="pointe">Pointe</option></select></div>
                <div class="field"><label>Zone axillaire incluse ?</label><select id="prac-zone"><option value="axillaire">Oui</option><option value="non">Non</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="Temps"> Temps</label>
                <label class="check-item"><input type="checkbox" value="Formation"> Formation</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT (N = <span id="n-total">0</span>)</div>
        <table>
            <thead>
                <tr><th>Code</th><th>Sexe</th><th>Savoir %</th><th>Pratique %</th><th>Statut</th><th>Action</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">RÉSULTATS ANALYTIQUES</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau Savoir</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Niveau Pratique</div><div id="graph-pratique"></div></div>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE</div>
        <div id="final-conclusion">En attente de données...</div>
    </div>
</div>

<script>
    let database = JSON.parse(localStorage.getItem('survey_database')) || [];

    window.onload = function() {
        const sel = document.getElementById('code-enquete');
        for(let i=1; i<=200; i++) { 
            let o=document.createElement('option'); 
            o.value="INF-"+i.toString().padStart(3,'0'); 
            o.text="Fiche N° "+i; sel.appendChild(o); 
        }
        updateUI();
    };

    function saveRecord() {
        let r = {
            id: document.getElementById('code-enquete').value,
            sexe: document.getElementById('sexe').value,
            service: document.getElementById('service').value,
            q_cause: document.getElementById('q-cause').value,
            q_age: document.getElementById('q-age-mammo').value,
            risques: Array.from(document.querySelectorAll('#group-risques input:checked')).map(i => i.value),
            att1: parseInt(document.querySelector('input[name="att1"]:checked').value),
            prac_main: document.getElementById('prac-main').value,
            prac_zone: document.getElementById('prac-zone').value,
            obstacles: Array.from(document.querySelectorAll('#group-obstacles input:checked')).map(i => i.value)
        };

        // Scores simplifiés
        r.scoreSavoir = (r.q_cause === "vrai" ? 50 : 0) + (r.risques.length * 10);
        r.scorePratique = (r.prac_main === "pulpe" ? 50 : 0) + (r.prac_zone === "axillaire" ? 50 : 0);

        database.push(r);
        localStorage.setItem('survey_database', JSON.stringify(database));
        alert("Fiche enregistrée !");
        updateUI();
    }

    function updateUI() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;

        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td><b>${row.id}</b></td><td>${row.sexe}</td>
                <td>${row.scoreSavoir}%</td><td>${row.scorePratique}%</td>
                <td>${row.scoreSavoir >= 60 ? '🟢' : '🔴'}</td>
                <td><button class="btn-delete-row" onclick="deleteSingleRecord(${index})">Supprimer</button></td>
            </tr>
        `).join('');

        updateCharts();
    }

    // NOUVELLE FONCTION : Supprimer une seule fiche
    function deleteSingleRecord(index) {
        if(confirm("Supprimer cette fiche définitivement ?")) {
            database.splice(index, 1);
            localStorage.setItem('survey_database', JSON.stringify(database));
            updateUI();
        }
    }

    // NOUVELLE FONCTION : Vider toute la base
    function clearFullDatabase() {
        if(confirm("ATTENTION : Voulez-vous vraiment supprimer TOUTES les fiches enregistrées ? Cette action est irréversible.")) {
            database = [];
            localStorage.removeItem('survey_database');
            updateUI();
            alert("Base de données vidée.");
        }
    }

    function updateCharts() {
        if(database.length === 0) return;
        let highS = database.filter(r => r.scoreSavoir >= 60).length;
        renderBar('graph-savoir', highS, database.length, '#2e7d32', 'Conformes');
        let highP = database.filter(r => r.scorePratique >= 60).length;
        renderBar('graph-pratique', highP, database.length, '#1565c0', 'Maîtrisées');
    }

    function renderBar(id, val, total, color, label) {
        let p = Math.round((val/total)*100);
        document.getElementById(id).innerHTML = `
            <div class="bar-container"><div class="bar-label">${label}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${color}">${p}%</div></div></div>
        `;
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }

    function exportToCSV() {
        let csv = "ID,Sexe,Savoir,Pratique\n" + database.map(r => `${r.id},${r.sexe},${r.scoreSavoir},${r.scorePratique}`).join("\n");
        let link = document.createElement("a");
        link.href = "data:text/csv;charset=utf-8," + encodeURI("\ufeff"+csv);
        link.download = "export_cap.csv"; link.click();
    }
</script>
</body>
</html>
