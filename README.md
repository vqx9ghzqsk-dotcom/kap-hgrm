<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE EXISTANT --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input[type="text"], input[type="number"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; text-align: center; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }

        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 10px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 150px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; transition: width 0.5s; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT GLOBAL</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTAT ET ANALYSE CROISÉE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT TOTAL (CSV)</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Oncologie</option></select></div>
                <div class="field"><label>Statut</label><select id="statut"><option>Titulaire</option><option>Infirmier(e) de garde</option><option>Stagiaire</option><option>Bénévole</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES</div>
            <div class="row">
                <div class="field"><label>1ère cause décès ?</label><select id="q1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option></select></div>
                <div class="field"><label>Âge début AES ?</label><select id="q2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option></select></div>
            </div>

            <div class="section-title">III. ATTITUDES</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Sensibilisation systématique nécessaire.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES & TECHNIQUES</div>
            <div class="row">
                <div class="field">
                    <label>Technique de palpation utilisée</label>
                    <select id="pratique-technique">
                        <option value="complete">Circulaire (complète avec creux axillaire)</option>
                        <option value="radiale">Radiale (du mamelon vers extérieur)</option>
                        <option value="sommaire">Palpation sommaire/rapide</option>
                        <option value="aucune">Aucune technique précise</option>
                    </select>
                </div>
                <div class="field">
                    <label>Position de l'examen</label>
                    <select id="pratique-position">
                        <option value="assise_couchee">Assise et couchée (Idéal)</option>
                        <option value="assise">Assise uniquement</option>
                        <option value="couchee">Couchée uniquement</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Fréquence Palpation</label><select id="pratique-freq"><option>Systématique</option><option>Si plainte</option><option>Rarement</option></select></div>
                <div class="field"><label>Démonstration à la patiente</label><select id="pratique-enseigne"><option>Oui, démonstration physique</option><option>Verbalement uniquement</option><option>Non</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <table><thead><tr><th>Code</th><th>Savoir %</th><th>Technique</th><th>Pratique %</th></tr></thead><tbody id="database-body"></tbody></table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE DES TECHNIQUES UTILISÉES</div>
        <div id="graph-techniques" class="stat-card"></div>
    </div>
</div>

<script>
    let database = [];

    // Init codes
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 200; i++) { let opt = document.createElement('option'); opt.value = "E-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }

    function saveRecord() {
        let tech = document.getElementById('pratique-technique').value;
        let record = {
            id: document.getElementById('code-enquete').value,
            technique: tech,
            freq: document.getElementById('pratique-freq').value,
            // Calcul du score pratique incluant la technique (40% technique, 40% fréquence, 20% enseignement)
            scorePratique: (tech === 'complete' ? 40 : (tech === 'radiale' ? 25 : 10)) + 
                           (document.getElementById('pratique-freq').value === 'Systématique' ? 40 : 10) +
                           (document.getElementById('pratique-enseigne').value.includes('physique') ? 20 : 5)
        };

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        alert("Fiche enregistrée avec succès !");
        updateAnalysis();
    }

    function updateAnalysis() {
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = '';
        database.forEach(r => {
            tbody.innerHTML += `<tr><td>${r.id}</td><td>80%</td><td>${r.technique}</td><td>${r.scorePratique}%</td></tr>`;
        });

        // Mise à jour du graphique des techniques
        let counts = { complete: 0, radiale: 0, sommaire: 0, aucune: 0 };
        database.forEach(r => counts[r.technique]++);
        
        let html = "";
        for (let t in counts) {
            let pct = Math.round((counts[t] / database.length) * 100);
            html += `<div class="bar-container"><div class="bar-label">${t.toUpperCase()}</div><div class="bar-track"><div class="bar-fill" style="width:${pct}%; background:#b03060;">${pct}%</div></div><div class="bar-value">${counts[t]}</div></div>`;
        }
        document.getElementById('graph-techniques').innerHTML = html;
    }

    function switchTab(idx) {
        document.querySelectorAll('.form-content').forEach(d => d.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
        document.getElementById('content-'+idx).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${idx})`).classList.add('active');
    }
</script>
</body>
</html>
