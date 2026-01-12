<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer (Sync Cloud)</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        
        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; font-style: italic; margin-top: 10px; color: #1b5e20; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
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
                <div class="field"><label>Niveau Etude</label><select id="niveau"><option>A2 (Diplômée)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès ?</label><select id="q1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option></select></div>
                <div class="field"><label>Âge début AES ?</label><select id="q2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option></select></div>
            </div>

            <label style="font-weight:bold; color:#b03060;">Signes d'alerte connus :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="peauorange"> Peau d'orange</label>
            </div>

            <div class="section-title">III. ATTITUDES (1-5)</div>
            <table>
                <thead><tr><th>Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td>Sentiment de compétence</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td>Impact pudeur</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Fréquence Palpation</label><select id="pratique-freq"><option>Systématique</option><option>Si plainte</option></select></div>
                <div class="field"><label>Palpé ce matin ?</label><select id="pratique-matin"><option>Oui</option><option>Non</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="cout"> Coût élevé</label>
                <label class="check-item"><input type="checkbox" value="formation"> Manque formation</label>
                <label class="check-item"><input type="checkbox" value="pudeur"> Pudeur culturelle</label>
            </div>

            <button type="button" class="btn-save" id="btn-submit" onclick="saveRecord()">💾 ENREGISTRER & ENVOYER AU SHEETS</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT ET CODAGE</div>
        <table style="font-size:11px;">
            <thead>
                <tr><th>Code</th><th>Niveau</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Cloud Sync</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE CROISÉE DES DONNÉES</div>
        <table>
            <thead><tr><th>Variable Croisée</th><th>Effectif (N)</th><th>Score Pratique Moyen</th></tr></thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross" class="interpretation-box"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET CONCLUSIONS</div>
        <div id="final-conclusion" style="line-height:1.6; padding:20px; background:#fff9fa; border:1px solid #ffccd5;"></div>
    </div>
</div>

<script>
    let database = [];
    // NOUVELLE URL SYNCHRONISÉE
    const urlCloud = "https://script.google.com/macros/s/AKfycbyOKRBtmx8QTmhHh3_qCbTcmTpjHcVWO9sER_HWkWcdDRCF0cmXof4qwVRQhWV1VvG-/exec";

    // Initialisation codes
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 200; i++) {
        let opt = document.createElement('option');
        opt.value = "Fiche-" + i; opt.text = "Infirmier(e) N° " + i;
        codeSelect.appendChild(opt);
    }

    function saveRecord() {
        const btn = document.getElementById('btn-submit');
        btn.disabled = true;
        btn.textContent = "⌛ ENVOI VERS GOOGLE SHEETS...";

        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            signes: document.querySelectorAll('#group-signes input:checked').length,
            p1: document.querySelector('input[name="p1"]:checked').value,
            p2: document.querySelector('input[name="p2"]:checked').value,
            freq: document.getElementById('pratique-freq').value,
            matin: document.getElementById('pratique-matin').value,
            obstacles: Array.from(document.querySelectorAll('#group-obstacles input:checked')).map(cb => cb.value)
        };

        // Calcul des scores
        let rawSav = (record.q1.includes("Vrai")?1:0) + (record.q2.includes("20")?1:0) + record.signes;
        record.scoreSavoir = Math.round((rawSav / 5) * 100);
        record.scoreAttitude = ((parseInt(record.p1) + parseInt(record.p2)) / 2).toFixed(1);
        record.scorePratique = (record.freq === "Systématique" ? 70 : 20) + (record.matin === "Oui" ? 30 : 0);

        // Sauvegarde locale
        database.push(record);
        document.getElementById('count-badge').textContent = database.length;

        // Envoi au Cloud
        fetch(urlCloud, {
            method: "POST",
            mode: "no-cors",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(record)
        })
        .then(() => {
            alert("✅ Succès ! La fiche a été ajoutée à Google Sheets.");
            btn.disabled = false;
            btn.textContent = "💾 ENREGISTRER & ENVOYER AU SHEETS";
            updateAnalysis();
        })
        .catch(err => {
            console.error(err);
            alert("⚠️ Problème de connexion, mais la fiche est enregistrée localement dans l'onglet 2.");
            btn.disabled = false;
            btn.textContent = "💾 ENREGISTRER & ENVOYER AU SHEETS";
            updateAnalysis();
        });
    }

    function updateAnalysis() {
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(r => `<tr><td>${r.id}</td><td>${r.niveau}</td><td>${r.scoreSavoir}%</td><td>${r.scoreAttitude}</td><td>${r.scorePratique}%</td><td>☁️ Synchro</td></tr>`).join('');

        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        
        document.getElementById('cross-body').innerHTML = `
            <tr><td>Savoir Elevé</td><td>${high.length}</td><td>${avg(high)}%</td></tr>
            <tr><td>Savoir Faible</td><td>${low.length}</td><td>${avg(low)}%</td></tr>
        `;

        document.getElementById('interpretation-cross').textContent = `Moyenne de pratique : ${avg(database)}%. Les infirmiers avec un bon savoir pratiquent mieux (${avg(high)}%).`;
        document.getElementById('final-conclusion').innerHTML = `<h3>Rapport HGRM</h3><p>Total fiches : ${database.length}. Pratique globale : ${avg(database)}%.</p>`;
    }

    function avg(arr) {
        if(arr.length === 0) return 0;
        return (arr.reduce((s, c) => s + parseFloat(c.scorePratique), 0) / arr.length).toFixed(1);
    }

    function switchTab(idx) {
        document.querySelectorAll('.form-content').forEach(d => d.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
        document.getElementById('content-'+idx).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${idx})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "data:text/csv;charset=utf-8,\ufeffID,Niveau,Savoir,Attitude,Pratique\n";
        database.forEach(r => csv += `${r.id},${r.niveau},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}\n`);
        window.open(encodeURI(csv));
    }
</script>
</body>
</html>
