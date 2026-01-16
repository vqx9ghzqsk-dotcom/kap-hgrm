<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE EXISTANT (Conservé) --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel:hover { background: #1b5e20; }

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
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }

        /* --- STYLES ANALYSE --- */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 10px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 150px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; transition: width 0.5s; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; }

        .cross-table th { background-color: #333; color: white; }
        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; font-style: italic; color: #1b5e20; margin-top: 10px; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 15px; font-style: italic; color: #b71c1c; margin-top: 10px; }

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
        <div style="background: #e3f2fd; padding: 10px; border-radius: 5px; margin-bottom: 15px; color: #0d47a1;">
            <strong>ℹ️ Mode Saisie Mémoire :</strong> Évaluation des Connaissances, Attitudes et Pratiques des infirmières (KAP).
        </div>
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Urgences</option><option>Médecine Interne</option></select></div>
                <div class="field"><label>Niveau Étude</label><select id="niveau"><option>A2 (Diplômée d'État)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option><option>Master/DS</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select"></select></div>
                <div class="field"><label>Ancienneté (Expérience)</label><select id="exp-select"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS THÉORIQUES)</div>
            <div class="row">
                <div class="field"><label>Fréquence du Cancer du Sein ?</label><select id="q1"><option selected>1er cancer chez la femme</option><option>2ème cancer</option><option>Maladie rare</option></select></div>
                <div class="field"><label>Examen de référence dépistage ?</label><select id="q2"><option>Échographie</option><option selected>Mammographie</option><option>Scanner</option></select></div>
                <div class="field"><label>Âge recommandé examen clinique ?</label><select id="q3"><option>Dès 50 ans</option><option selected>Dès 25-30 ans</option><option>Seulement si douleur</option></select></div>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Facteurs de Risque (Cochez les éléments valides) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux (BRCA)</label>
                <label class="check-item"><input type="checkbox" value="menarche"> Ménarche précoce / Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" value="nullipare"> Nulliparité / Maternité tardive</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Consommation d'Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité / Sédentarité</label>
                <label class="check-item"><input type="checkbox" value="hormone"> Contraception / Hormonothérapie prolongée</label>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Signes d'Alerte (Cochez si connu) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="masse"> Masse/Nodule (sein ou aisselle)</label>
                <label class="check-item"><input type="checkbox" value="volume"> Modification forme/volume</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction/Inversion mamelon</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement anormal (sanglant)</label>
                <label class="check-item"><input type="checkbox" value="orange"> Aspect peau d'orange</label>
                <label class="check-item"><input type="checkbox" value="rougeur"> Rougeurs persistantes</label>
            </div>

            <div class="section-title">III. ATTITUDES (ÉCHELLE DE LIKERT 1-5)</div>
            <p style="font-size: 11px; color: #666;">1: Tout à fait d'accord | 5: Pas du tout d'accord</p>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">L'infirmière a un rôle central dans la sensibilisation.</td><td><input type="radio" name="p1" value="1" checked></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4"></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">Le diagnostic tardif est lié au manque d'info des femmes.</td><td><input type="radio" name="p2" value="1" checked></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5"></td></tr>
                    <tr><td class="text-left">La peur du cancer empêche les femmes de consulter.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Je me sens suffisamment formée pour éduquer les patientes.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3" checked></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field"><label>Enseignez-vous l'auto-examen (AES) ?</label><select id="pratique-aes"><option>Systématiquement</option><option>Occasionnellement</option><option>Jamais</option></select></div>
                <div class="field"><label>Fréquence recommandation AES ?</label><select id="pratique-freq-aes"><option selected>1 fois par mois (après règles)</option><option>1 fois par an</option><option>Seulement si nodule</option></select></div>
                <div class="field"><label>Réalisez-vous l'examen clinique ?</label><select id="pratique-examen"><option>Oui, à chaque patiente cible</option><option>Si la patiente le demande</option><option>Rarement/Jamais</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES IDENTIFIÉS</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="formation"> Manque de formation continue</label>
                <label class="check-item"><input type="checkbox" value="temps"> Charge de travail / Manque de temps</label>
                <label class="check-item"><input type="checkbox" value="materiel"> Absence de matériel de démonstration</label>
                <label class="check-item"><input type="checkbox" value="tabou"> Tabous culturels / Pudeur</label>
                <label class="check-item"><input type="checkbox" value="cout"> Coût élevé des examens (Mammographie)</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT AUTOMATISÉE</div>
        <table style="font-size:11px;">
            <thead>
                <tr>
                    <th>Code</th>
                    <th>Service</th>
                    <th>Niveau Savoir (%)</th>
                    <th>Moy. Attitude</th>
                    <th>Score Pratique (%)</th>
                    <th>Statut Global</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">RÉSULTATS ET ANALYSE CROISÉE</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances Théoriques</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Niveau de Pratique Clinique</div>
                <div id="graph-pratique"></div>
            </div>
        </div>

        <table class="cross-table">
            <thead>
                <tr>
                    <th class="text-left">Groupe de Savoir</th>
                    <th>N</th>
                    <th>Attitude Moyenne</th>
                    <th>Pratique Moyenne (%)</th>
                </tr>
            </thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross"></div>

        <div class="section-title">PRÉVALENCE DES OBSTACLES</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
        <div id="final-conclusion" style="font-size:14px; line-height:1.6;">
            En attente de saisies pour générer la conclusion...
        </div>
    </div>
</div>

<script>
    let database = [];

    // Init listes
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 150; i++) { let opt = document.createElement('option'); opt.value = "INF-"+i; opt.text = "Infirmière N° " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 20; i <= 65; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; ageSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 40; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans d'exp."; expSelect.appendChild(opt); }

    function saveRecord() {
        let record = {
            id: document.getElementById('code-enquete').value,
            service: document.getElementById('service').value,
            niveau: document.getElementById('niveau').value,
            // Savoirs
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            // Attitudes
            p1: getRadioValue('p1'), p2: getRadioValue('p2'), p3: getRadioValue('p3'), p4: getRadioValue('p4'),
            // Pratiques
            aes: document.getElementById('pratique-aes').value,
            examen: document.getElementById('pratique-examen').value,
            obstacles: getCheckedValues('group-obstacles')
        };

        // Scoring Savoir (Total 15 pts max)
        let s = 0;
        if(record.q1.includes("1er")) s++;
        if(record.q2.includes("Mammo")) s++;
        if(record.q3.includes("25-30")) s++;
        s += record.risques + record.signes;
        record.scoreSavoir = Math.round((s / 15) * 100);

        // Scoring Attitude
        record.scoreAttitude = ((parseInt(record.p1)+parseInt(record.p2)+parseInt(record.p3)+parseInt(record.p4))/4).toFixed(1);

        // Scoring Pratique
        let p = 0;
        if(record.aes === "Systématiquement") p += 50; else if(record.aes === "Occasionnellement") p += 20;
        if(record.examen.includes("Chaque")) p += 50; else if(record.examen.includes("demande")) p += 20;
        record.scorePratique = p;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        
        // UI Reset
        document.querySelectorAll('input[type="checkbox"]').forEach(i => i.checked = false);
        codeSelect.selectedIndex++;
        
        updateAnalysis();
        alert("Données enregistrées !");
    }

    function updateAnalysis() {
        if(database.length === 0) return;

        // Tableau Matrice
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = '';
        database.forEach(r => {
            tbody.innerHTML += `<tr>
                <td>${r.id}</td><td>${r.service}</td>
                <td style="color:${getColor(r.scoreSavoir)}">${r.scoreSavoir}%</td>
                <td>${r.scoreAttitude}</td>
                <td style="color:${getColor(r.scorePratique)}">${r.scorePratique}%</td>
                <td>${r.scoreSavoir > 70 ? '✅ Adéquat' : '⚠️ Insuffisant'}</td>
            </tr>`;
        });

        // Stats Croisées
        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        
        document.getElementById('cross-body').innerHTML = `
            <tr><td>Savoir Satisfaisant (>=70%)</td><td>${high.length}</td><td>${getAvg(high, 'scoreAttitude')}</td><td>${getAvg(high, 'scorePratique')}%</td></tr>
            <tr><td>Savoir Insuffisant (<70%)</td><td>${low.length}</td><td>${getAvg(low, 'scoreAttitude')}</td><td>${getAvg(low, 'scorePratique')}%</td></tr>
        `;

        // Obstacles Graphe
        let counts = {};
        database.forEach(r => r.obstacles.forEach(o => counts[o] = (counts[o] || 0) + 1));
        let obstHtml = "";
        for (let [k, v] of Object.entries(counts)) {
            let pct = Math.round((v/database.length)*100);
            obstHtml += `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${pct}%; background:#b03060;">${pct}%</div></div></div>`;
        }
        document.getElementById('graph-obstacles').innerHTML = obstHtml;

        // Conclusion
        let avgSavoir = getAvg(database, 'scoreSavoir');
        document.getElementById('final-conclusion').innerHTML = `
            <p>Sur <strong>${database.length}</strong> répondants, le niveau moyen de connaissances est de <strong>${avgSavoir}%</strong>.</p>
            <div class="interpretation-box">L'étude montre que ${avgSavoir < 60 ? "le personnel nécessite une formation urgente sur les protocoles de dépistage." : "les connaissances sont bonnes mais les obstacles structurels limitent la pratique."}</div>
        `;
    }

    // Helpers
    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(c => c.value); }
    function getRadioValue(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e ? e.value : 0; }
    function getColor(s) { return s >= 70 ? 'green' : (s >= 50 ? 'orange' : 'red'); }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a, b) => a + parseFloat(b[p]), 0) / arr.length).toFixed(1) : 0; }
    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "ID,Service,Savoir,Attitude,Pratique\n";
        database.forEach(r => csv += `${r.id},${r.service},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}\n`);
        let link = document.createElement("a");
        link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "Analyse_Memoire_HGRM.csv";
        link.click();
    }
</script>

</body>
</html>
