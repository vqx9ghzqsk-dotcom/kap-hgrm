<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert System</title>
    <style>
        /* --- STYLE & DESIGN --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px; overflow: hidden;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; flex-wrap: wrap;}
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.3s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* Cacher les onglets admin par défaut */
        .admin-only { display: none; }
        .btn-lock { background: #333; color: white; margin-left: auto; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.4s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.3); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 30px; text-transform: uppercase; }
        
        /* GRAPHICS */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 180px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 9px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; transition: width 0.8s ease-out; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; }
        
        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 20px; font-style: italic; color: #1b5e20; margin-top: 20px; border-radius: 4px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        
        <button class="tab admin-only" id="tab2" onclick="switchTab(2)">2. DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab3" onclick="switchTab(3)">3. ANALYSE EXPERTE</button>
        <button class="tab admin-only" id="tab4" onclick="switchTab(4)">4. CONCLUSION</button>
        
        <button class="tab btn-lock" id="btnAdmin" onclick="toggleAdmin()">🔑 MODE ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION DU RÉPONDANT</div>
            <div class="row">
                <div class="field"><label>Code Fiche (Auto)</label><input type="text" id="code-enquete" readonly></div>
                <div class="field"><label>Sexe</label><select id="sexe"><option>Féminin</option><option>Masculin</option></select></div>
                <div class="field"><label>Service</label><select id="service">
                    <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option>
                    <option>Chirurgie</option><option>Urgences / Autre</option>
                </select></div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté</label><select id="exp-select"></select></div>
                <div class="field"><label>Niveau d'étude</label><select id="niveau">
                    <option>A2 (Diplômée d'État)</option><option selected>A1 (Graduée)</option><option>A0 (Licenciée/Master)</option>
                </select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès femme RDC ?</label><select id="q1"><option>Vrai</option><option>Faux</option><option>Je ne sais pas</option></select></div>
                <div class="field"><label>Âge 1ère Mammographie ?</label><select id="q2"><option>Dès 20 ans</option><option selected>Vers 35-40 ans</option><option>Vers 50 ans</option></select></div>
                <div class="field"><label>Moment idéal AES ?</label><select id="q3"><option>Pendant les règles</option><option selected>7 à 10 jours après les règles</option><option>N'importe quand</option></select></div>
            </div>

            <label style="margin:10px 0; display:block; font-weight:bold; color:#b03060;">Facteurs de risque connus :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge (> 50 ans)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="nulli"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" value="obese"> Obésité</label>
            </div>

            <div class="section-title">III. ATTITUDES</div>
            <table>
                <thead><tr><th style="text-align:left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td style="text-align:left">Le dépistage précoce permet la guérison.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4"></td><td><input type="radio" name="p1" value="5" checked></td></tr>
                    <tr><td style="text-align:left">Je me sens capable de réaliser l'examen.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4" checked></td><td><input type="radio" name="p2" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES TECHNIQUES</div>
            <div class="row">
                <div class="field"><label>Partie de la main utilisée</label><select id="prac-main"><option>Bout des doigts</option><option selected>Pulpe des 3 doigts</option><option>Paume</option></select></div>
                <div class="field"><label>Zone "Oubliée" à inclure</label><select id="prac-zone"><option>Mamelon</option><option selected>Prolongement axillaire</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER MA FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT COMPLÈTE</div>
        <table>
            <thead><tr><th>Code</th><th>Niveau</th><th>Exp</th><th>Savoir %</th><th>Attitude /5</th><th>Pratique %</th></tr></thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE STATISTIQUE DES DONNÉES</div>
        <div class="row">
            <div class="stat-card"><b>Niveau de Savoir</b><div id="graph-savoir"></div></div>
            <div class="stat-card"><b>Qualité Pratique</b><div id="graph-pratique"></div></div>
        </div>
        <div id="interpretation-cross"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE FINALE</div>
        <div id="final-conclusion"></div>
        <br>
        <button class="btn-save" style="background:#2e7d32" onclick="exportToCSV()">📥 EXPORTER LA BASE EN CSV</button>
        <button class="btn-save" style="background:#c62828" onclick="clearData()">⚠️ EFFACER TOUTE LA BASE (RESET)</button>
    </div>
</div>

<script>
    let database = [];
    let isAdmin = false;
    let adminCode = "2024"; // <-- VOTRE CODE ICI

    // Init au démarrage
    window.onload = function() {
        // Charger la mémoire locale
        const saved = localStorage.getItem('kap_hgr_db');
        if(saved) {
            database = JSON.parse(saved);
            updateUI();
        }
        
        // Init Listes
        const expSel = document.getElementById('exp-select');
        for(let i=0; i<=40; i++) { let o=document.createElement('option'); o.value=i; o.text=i+" ans d'exp."; expSel.appendChild(o); }
        
        generateCode();
    };

    function generateCode() {
        document.getElementById('code-enquete').value = "E-" + (database.length + 1);
    }

    function toggleAdmin() {
        if(!isAdmin) {
            let pass = prompt("Saisissez le code administrateur pour voir les résultats :");
            if(pass === adminCode) {
                isAdmin = true;
                document.querySelectorAll('.admin-only').forEach(el => el.style.display = "block");
                document.getElementById('btnAdmin').textContent = "🔓 ADMIN ACTIF";
                document.getElementById('btnAdmin').style.background = "#2e7d32";
                alert("Accès autorisé. Les onglets d'analyse sont maintenant visibles.");
            } else {
                alert("Code erroné.");
            }
        } else {
            isAdmin = false;
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = "none");
            document.getElementById('btnAdmin').textContent = "🔑 MODE ADMIN";
            document.getElementById('btnAdmin').style.background = "#333";
            switchTab(1);
        }
    }

    function saveRecord() {
        let r = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            exp: document.getElementById('exp-select').value,
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            risques: document.querySelectorAll('#group-risques input:checked').length,
            p1: getRadio('p1'), p2: getRadio('p2'),
            main: document.getElementById('prac-main').value,
            zone: document.getElementById('prac-zone').value
        };

        // Scores rapides
        let s = 0;
        if(r.q1 === "Vrai") s += 30;
        if(r.q2.includes("35-40")) s += 30;
        if(r.q3.includes("7 à 10")) s += 40;
        r.scoreSavoir = s;

        let p = 0;
        if(r.main.includes("Pulpe")) p += 50;
        if(r.zone.includes("axillaire")) p += 50;
        r.scorePratique = p;

        r.scoreAttitude = ((parseInt(r.p1)+parseInt(r.p2))/2).toFixed(1);

        database.push(r);
        localStorage.setItem('kap_hgr_db', JSON.stringify(database));
        
        alert("Fiche enregistrée avec succès dans la base !");
        document.getElementById('kapForm').reset();
        updateUI();
        generateCode();
    }

    function updateUI() {
        document.getElementById('count-badge').textContent = database.length;
        
        // Table
        document.getElementById('database-body').innerHTML = database.map(row => `
            <tr>
                <td><b>${row.id}</b></td><td>${row.niveau}</td><td>${row.exp} ans</td>
                <td>${row.scoreSavoir}%</td><td>${row.scoreAttitude}</td><td>${row.scorePratique}%</td>
            </tr>
        `).join('');

        // Graphes (Simple)
        let highS = database.filter(x => x.scoreSavoir >= 60).length;
        renderBar('graph-savoir', "Correct", highS, database.length, "green");
        
        let highP = database.filter(x => x.scorePratique >= 100).length;
        renderBar('graph-pratique', "Maîtrisé", highP, database.length, "blue");

        document.getElementById('final-conclusion').innerHTML = `<h3>Total: ${database.length} répondants</h3><p>Le système a compilé les données. Exportez le CSV pour votre analyse finale dans Excel.</p>`;
    }

    function renderBar(id, label, val, total, col) {
        let p = total > 0 ? Math.round((val/total)*100) : 0;
        document.getElementById(id).innerHTML = `<div class="bar-container">
            <div class="bar-label">${label}</div>
            <div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${col}">${p}%</div></div>
        </div>`;
    }

    function getRadio(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e?e.value:0; }

    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "ID,Niveau,Exp,Savoir,Attitude,Pratique\n" + database.map(r => `${r.id},${r.niveau},${r.exp},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let link = document.createElement("a");
        link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "Rapport_Memoire_HGRM.csv";
        link.click();
    }

    function clearData() {
        if(confirm("Voulez-vous vraiment TOUT effacer ? Cette action est irréversible.")) {
            localStorage.removeItem('kap_hgr_db');
            database = [];
            updateUI();
            alert("Base de données vidée.");
        }
    }
</script>
</body>
</html>
