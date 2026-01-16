<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE CONSERVÉ DU PREMIER CODE --- */
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
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; text-align: center; }
        .cross-table th { background-color: #333; color: white; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }

        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 10px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 150px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; transition: width 0.5s; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; }

        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; font-style: italic; color: #1b5e20; margin-top: 10px; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 15px; font-style: italic; color: #b71c1c; margin-top: 10px; }
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
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Oncologie</option><option>Médecine Interne</option></select></div>
                <div class="field"><label>Statut</label><select id="statut"><option>Titulaire</option><option>Infirmier(e) de garde</option><option>Stagiaire</option><option>Bénévole</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select"></select></div>
                <div class="field"><label>Niveau Étude</label><select id="niveau"><option>A2 (Diplômée d'État)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option><option>Master / Supérieur</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès ?</label><select id="q1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option><option>Ne sait pas</option></select></div>
                <div class="field"><label>Âge début AES ?</label><select id="q2"><option>Dès 12 ans</option><option selected>Dès 25-30 ans</option><option>Après 50 ans</option></select></div>
                <div class="field"><label>Moment AES ?</label><select id="q3"><option selected>7 jours après les règles</option><option>Pendant les règles</option><option>N'importe quand</option></select></div>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060; display:block;">Facteurs de risque (Cochez si connu) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Avancée en âge</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux / BRCA</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménarche précoce / Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" value="nulliparite"> Nulliparité / Maternité tardive</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité / Sédentarité</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="contraceptif"> Contraceptifs oraux / Hormono</label>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060; display:block;">Signes d'alerte (Cochez si connu) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="forme"> Modification forme/volume</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction mamelon</label>
                <label class="check-item"><input type="checkbox" value="peauorange"> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" value="adenopathie"> Adénopathie axillaire</label>
            </div>

            <div class="section-title">III. ATTITUDES (1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">Le diagnostic en RDC est souvent trop tardif.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4" checked></td><td><input type="radio" name="p2" value="5"></td></tr>
                    <tr><td class="text-left">La douleur est le premier signe (Croyance).</td><td><input type="radio" name="p3" value="1" checked></td><td><input type="radio" name="p3" value="2"></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES</div>
            <div class="row">
                <div class="field"><label>Promotion Allaitement</label><select id="pratique-allaitement"><option>Systématique</option><option>Parfois</option><option>Jamais</option></select></div>
                <div class="field"><label>Enseignement AES</label><select id="pratique-enseigne"><option>Démonstration physique</option><option>Verbalement</option><option>Pas d'enseignement</option></select></div>
                <div class="field"><label>Technique palpation</label><select id="pratique-tech"><option value="complete">Complète (Quadrant+Axillaire)</option><option value="rapide">Rapide/Sommaire</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="formation"> Manque formation</label>
                <label class="check-item"><input type="checkbox" value="materiel"> Manque matériel/Mammographe</label>
                <label class="check-item"><input type="checkbox" value="intimite"> Absence intimité</label>
                <label class="check-item"><input type="checkbox" value="culture"> Croyances/Tabous</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT GÉNÉRALE</div>
        <table style="font-size:11px;">
            <thead><tr><th>Code</th><th>Niveau</th><th>Exp.</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th></tr></thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. STATISTIQUES DESCRIPTIVES</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Savoir</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de la Pratique</div><div id="graph-pratique"></div></div>
        </div>

        <div class="section-title">2. ANALYSE CROISÉE (SAVOIR VS PRATIQUE)</div>
        <table class="cross-table">
            <thead><tr><th class="text-left">Groupe (Selon le Savoir)</th><th>N</th><th>Attitude Moyenne</th><th>Pratique Moyenne (%)</th></tr></thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross"></div>

        <div class="section-title">3. ANALYSE DES BARRIÈRES</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE DE L'ÉTUDE</div>
        <div id="final-conclusion" style="font-size:14px; line-height:1.6;">En attente de données...</div>
    </div>

</div>

<script>
    let database = [];

    // Init Selects originaux
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 200; i++) { let opt = document.createElement('option'); opt.value = "E-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 65; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; ageSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 40; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans d'exp."; expSelect.appendChild(opt); }

    function saveRecord() {
        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            exp: parseInt(document.getElementById('exp-select').value),
            q1: document.getElementById('q1').value, q2: document.getElementById('q2').value, q3: document.getElementById('q3').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            p1: getRadio('p1'), p2: getRadio('p2'), p3: getRadio('p3'),
            allaitement: document.getElementById('pratique-allaitement').value,
            enseigne: document.getElementById('pratique-enseigne').value,
            tech: document.getElementById('pratique-tech').value,
            obstacles: Array.from(document.querySelectorAll('#group-obstacles input:checked')).map(i => i.value)
        };

        // Scoring Savoir
        let ptsSavoir = (record.q1.includes("Vrai")?2:0) + (record.q2.includes("25-30")?2:0) + (record.q3.includes("7 jours")?2:0) + record.risques + record.signes;
        record.scoreSavoir = Math.round((ptsSavoir / 18) * 100);

        // Scoring Attitude (Inversion P3 car c'est une fausse croyance)
        record.scoreAttitude = ((parseInt(record.p1) + parseInt(record.p2) + (6 - parseInt(record.p3))) / 3).toFixed(1);

        // Scoring Pratique
        let ptsPrac = 0;
        if(record.allaitement === "Systématique") ptsPrac += 30;
        if(record.enseigne === "Démonstration physique") ptsPrac += 40;
        if(record.tech === "complete") ptsPrac += 30;
        record.scorePratique = ptsPrac;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        alert("Fiche enregistrée !");
        codeSelect.selectedIndex++;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(!database.length) return;

        // Onglet 2
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(r => `<tr><td>${r.id}</td><td>${r.niveau}</td><td>${r.exp} ans</td><td>${r.scoreSavoir}%</td><td>${r.scoreAttitude}</td><td>${r.scorePratique}%</td></tr>`).join('');

        // Onglet 3
        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        let avgPH = getAvg(high, 'scorePratique');
        let avgPL = getAvg(low, 'scorePratique');

        document.getElementById('cross-body').innerHTML = `
            <tr><td class="text-left"><strong>Haut Savoir (>=70%)</strong></td><td>${high.length}</td><td>${getAvg(high,'scoreAttitude')} / 5</td><td>${avgPH}%</td></tr>
            <tr><td class="text-left"><strong>Faible Savoir (<70%)</strong></td><td>${low.length}</td><td>${getAvg(low,'scoreAttitude')} / 5</td><td>${avgPL}%</td></tr>`;

        // Graphiques barres
        renderBar('graph-savoir', [{l:'Satisfaisant', v:high.length, t:database.length, c:'green'}, {l:'Insuffisant', v:low.length, t:database.length, c:'red'}]);
        renderBar('graph-pratique', [{l:'Moyenne Pratique', v:getAvg(database,'scorePratique'), t:100, c:'#b03060'}]);

        // Interprétation automatique
        let interpret = document.getElementById('interpretation-cross');
        if(avgPH > avgPL + 10) {
            interpret.innerHTML = `<div class="interpretation-box">✅ <strong>Corrélation Positive :</strong> Votre étude montre que les infirmières ayant un meilleur savoir théorique ont une pratique nettement supérieure (${avgPH}% contre ${avgPL}%).</div>`;
        } else {
            interpret.innerHTML = `<div class="alert-box">⚠️ <strong>Disparité Savoir-Agir :</strong> Le niveau de pratique reste faible même chez celles qui ont un bon savoir. Cela indique des obstacles structurels majeurs à l'HGRM.</div>`;
        }

        // Obstacles
        let obsCounts = {};
        database.forEach(r => r.obstacles.forEach(o => obsCounts[o] = (obsCounts[o]||0)+1));
        document.getElementById('graph-obstacles').innerHTML = Object.entries(obsCounts).map(([k, v]) => {
            let pct = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k.toUpperCase()}</div><div class="bar-track"><div class="bar-fill" style="width:${pct}%; background:#b03060;">${pct}%</div></div></div>`;
        }).join('');

        // Conclusion
        document.getElementById('final-conclusion').innerHTML = `<h3>Synthèse des ${database.length} fiches</h3><p>Le taux de connaissances satisfaisantes est de ${((high.length/database.length)*100).toFixed(0)}%. La pratique moyenne globale est de ${getAvg(database,'scorePratique')}%.</p>`;
    }

    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getRadio(n) { return document.querySelector(`input[name="${n}"]:checked`)?.value || 0; }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a, b) => a + parseFloat(b[p]), 0) / arr.length).toFixed(1) : 0; }
    function renderBar(id, data) {
        document.getElementById(id).innerHTML = data.map(d => `<div class="bar-container"><div class="bar-label">${d.l}</div><div class="bar-track"><div class="bar-fill" style="width:${(d.v/d.t)*100}%; background:${d.c};">${d.v}</div></div></div>`).join('');
    }
    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }
    function exportToCSV() {
        let csv = "ID,Savoir,Attitude,Pratique\n" + database.map(r => `${r.id},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let a = document.createElement('a'); a.href = URL.createObjectURL(new Blob([csv], {type:'text/csv'})); a.download = 'KAP_HGRM_Final.csv'; a.click();
    }
</script>
</body>
</html>
