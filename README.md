<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer (FINAL SYNC)</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f4f7f6; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.15); min-height: 800px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.4s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #333; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; color: #b03060; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; background: #fafafa; padding: 15px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 30px; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; box-shadow: 0 4px 10px rgba(176, 48, 96, 0.3); }
        .btn-save:disabled { background: #ccc; cursor: not-allowed; }

        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; font-style: italic; margin-top: 10px; color: #1b5e20; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT GLOBAL</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION DU RÉPONDANT</div>
            <div class="row">
                <div class="field"><label>Code Fiche</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Oncologie</option><option>Urgence</option></select></div>
                <div class="field"><label>Niveau Etude</label><select id="niveau"><option>A2 (Diplômée)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>Cancer = 1ère cause décès ?</label><select id="q1"><option selected>Vrai</option><option>Faux</option></select></div>
                <div class="field"><label>Âge idéal début AES ?</label><select id="q2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option><option>Après 40 ans</option></select></div>
            </div>

            <label style="font-weight:bold; color:#b03060; display:block; margin:10px 0;">Signes d'alerte connus :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="peauorange"> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction mamelon</label>
            </div>

            <div class="section-title">III. ATTITUDES (Échelle 1-5)</div>
            <table>
                <thead><tr><th>Critère</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td>Se sent capable de détecter un nodule</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td>La pudeur freine l'examen</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Fréquence de palpation</label><select id="pratique-freq"><option>Systématique</option><option>Si plainte uniquement</option><option>Rarement</option></select></div>
                <div class="field"><label>Examen effectué ce matin ?</label><select id="pratique-matin"><option>Oui</option><option>Non</option></select></div>
            </div>

            <div class="section-title">V. BARRIÈRES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="cout"> Coût élevé</label>
                <label class="check-item"><input type="checkbox" value="formation"> Manque de formation</label>
                <label class="check-item"><input type="checkbox" value="pudeur"> Pudeur des patientes</label>
                <label class="check-item"><input type="checkbox" value="temps"> Manque de temps</label>
            </div>

            <button type="button" class="btn-save" id="btn-submit" onclick="saveRecord()">💾 ENREGISTRER & ENVOYER AU CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE CODAGE DYNAMIQUE</div>
        <table style="font-size:11px;">
            <thead>
                <tr><th>ID</th><th>Niveau</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Statut Cloud</th></tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE CROISÉE : SAVOIR vs PRATIQUE</div>
        <table id="cross-table">
            <thead><tr><th>Niveau de Connaissance</th><th>N</th><th>Pratique Moyenne</th></tr></thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross" class="interpretation-box"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSIONS GÉNÉRALES</div>
        <div id="final-conclusion" style="padding:20px; border:1px solid #ddd; background:#fff;"></div>
    </div>
</div>

<script>
    let database = [];
    // VOTRE URL MISE À JOUR
    const urlCloud = "https://script.google.com/macros/s/AKfycbz-a9ZgcGRrxTDWXLlbuTnsIzUsdj4ZY5FVgTc7pHAMyyOPdrNQY8lT4HxxXngYGTNy/exec";

    // Setup des codes fiches
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 300; i++) {
        let opt = document.createElement('option');
        opt.value = "F"+i; opt.text = "Fiche N° " + i;
        codeSelect.appendChild(opt);
    }

    async function saveRecord() {
        const btn = document.getElementById('btn-submit');
        btn.disabled = true;
        btn.textContent = "⌛ SYNCHRONISATION EN COURS...";

        const record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            signesCount: document.querySelectorAll('#group-signes input:checked').length,
            p1: document.querySelector('input[name="p1"]:checked').value,
            p2: document.querySelector('input[name="p2"]:checked').value,
            freq: document.getElementById('pratique-freq').value,
            matin: document.getElementById('pratique-matin').value,
            obstacles: Array.from(document.querySelectorAll('#group-obstacles input:checked')).map(cb => cb.value)
        };

        // Calculs automatiques
        let scoreSav = (record.q1 === "Vrai" ? 1 : 0) + (record.q2 === "Dès 20 ans" ? 1 : 0) + record.signesCount;
        record.scoreSavoir = Math.round((scoreSav / 6) * 100); 
        record.scoreAttitude = ((parseInt(record.p1) + parseInt(record.p2)) / 2).toFixed(1);
        record.scorePratique = (record.freq === "Systématique" ? 60 : 20) + (record.matin === "Oui" ? 40 : 0);

        // Sauvegarde locale
        database.push(record);
        document.getElementById('count-badge').textContent = database.length;

        // ENVOI CLOUD (Mode robuste)
        try {
            await fetch(urlCloud, {
                method: "POST",
                mode: "no-cors",
                headers: { "Content-Type": "text/plain" },
                body: JSON.stringify(record)
            });
            alert("✅ Données envoyées à Google Sheets !");
        } catch (e) {
            alert("⚠️ Erreur de connexion au Cloud, mais la fiche est sauvegardée dans le tableau local (onglet 2).");
        } finally {
            btn.disabled = false;
            btn.textContent = "💾 ENREGISTRER & ENVOYER AU CLOUD";
            updateAnalysis();
            // Optionnel : incrémenter le code fiche
            codeSelect.selectedIndex += 1;
        }
    }

    function updateAnalysis() {
        // MAJ Dépouillement
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(r => `<tr><td>${r.id}</td><td>${r.niveau}</td><td>${r.scoreSavoir}%</td><td>${r.scoreAttitude}</td><td>${r.scorePratique}%</td><td style="color:green">☁️ Envoyé</td></tr>`).join('');

        // MAJ Analyse Croisée
        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        
        document.getElementById('cross-body').innerHTML = `
            <tr><td><b>Savoir Élevé (>=70%)</b></td><td>${high.length}</td><td>${avg(high)}%</td></tr>
            <tr><td><b>Savoir Faible (<70%)</b></td><td>${low.length}</td><td>${avg(low)}%</td></tr>
        `;

        document.getElementById('interpretation-cross').innerHTML = `L'analyse des ${database.length} fiches montre que le groupe ayant un savoir élevé présente une pratique moyenne de ${avg(high)}%.`;
        document.getElementById('final-conclusion').innerHTML = `<h3>Synthèse des résultats</h3><p>Le taux global de pratique adéquate est de <b>${avg(database)}%</b> à l'HGRM.</p>`;
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
