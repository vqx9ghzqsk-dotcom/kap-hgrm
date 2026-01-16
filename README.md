<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données & Analyse Expert</title>
    <style>
        /* --- STYLE GLOBAL FUSIONNÉ --- */
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
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }

        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
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
        <button class="tab" onclick="switchTab(3)">3. ANALYSE STATISTIQUE</button>
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
                <div class="field"><label>Niveau Étude</label><select id="niveau"><option>A2 (Diplômée d'État)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option><option>Master / Diplôme Supérieur</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (BASÉES SUR LA REVUE)</div>
            <div class="row">
                <div class="field"><label>1ère cause de décès par cancer chez la femme ?</label><select id="q1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option><option>Ne sait pas</option></select></div>
                <div class="field"><label>Examen clinique recommandé dès quel âge ?</label><select id="q2"><option>Dès 15 ans</option><option selected>Dès 25-30 ans</option><option>Seulement après 50 ans</option></select></div>
                <div class="field"><label>Moment idéal pour l'auto-palpation ?</label><select id="q3"><option selected>Juste après les règles</option><option>Pendant les règles</option><option>N'importe quand</option></select></div>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Facteurs de risque (Cochez si connu) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Avancée en âge</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux / Mutations BRCA</label>
                <label class="check-item"><input type="checkbox" value="menarche"> Ménarche précoce / Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" value="nulliparite"> Nulliparité ou maternité tardive</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité et Sédentarité</label>
                <label class="check-item"><input type="checkbox" value="hormono"> Contraception / Hormonothérapie prolongée</label>
            </div>

            <label style="margin:10px 0; font-weight:bold; color:#b03060;">Signes d'alerte (Cochez si connu) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Masse ou nodule (sein/aisselle)</label>
                <label class="check-item"><input type="checkbox" value="forme"> Modification forme/volume du sein</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction ou inversion mamelon</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="peauorange"> Aspect "Peau d'orange" / Rougeurs</label>
            </div>

            <div class="section-title">III. ATTITUDES (Échelle Likert 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">L'infirmière a un rôle central dans la sensibilisation.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4"></td><td><input type="radio" name="p1" value="5" checked></td></tr>
                    <tr><td class="text-left">La peur du cancer est un frein au dépistage.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4" checked></td><td><input type="radio" name="p2" value="5"></td></tr>
                    <tr><td class="text-left">Le diagnostic en RDC est souvent trop tardif.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2"></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5" checked></td></tr>
                    <tr><td class="text-left">La douleur est le premier signe du cancer (Croyance).</td><td><input type="radio" name="p4" value="1" checked></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES DE PRÉVENTION</div>
            <div class="row">
                <div class="field"><label>Promotion de l'Allaitement ?</label><select id="pratique-allaitement"><option>Systématique</option><option>Parfois</option><option>Jamais</option></select></div>
                <div class="field"><label>Démonstration d'Auto-examen ?</label><select id="pratique-aes"><option>Démonstration physique</option><option>Verbalement uniquement</option><option>Aucun enseignement</option></select></div>
            </div>
            <div class="row">
                <div class="field">
                    <label>Technique de palpation utilisée ?</label>
                    <select id="pratique-technique">
                        <option value="rapide">1. Palpation rapide sans méthode</option>
                        <option value="systematique">2. Quadrant par quadrant</option>
                        <option value="complete" selected>3. Complète (Quadrant + Axillaire + Mamelon)</option>
                    </select>
                </div>
                <div class="field"><label>Orientation vers Mammographie ?</label><select id="pratique-mammo"><option>Régulièrement</option><option>Si suspicion uniquement</option><option>Jamais</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES IDENTIFIÉS (RDC/HGRM)</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="accessibilite"> Accès limité à la mammographie</label>
                <label class="check-item"><input type="checkbox" value="formation"> Manque de formation continue</label>
                <label class="check-item"><input type="checkbox" value="socio_eco"> Obstacles socio-économiques</label>
                <label class="check-item"><input type="checkbox" value="tabou"> Tabous culturels / Représentations</label>
                <label class="check-item"><input type="checkbox" value="intimite"> Absence d'intimité dans les locaux</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE ET ANALYSER</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT GÉNÉRALE</div>
        <table style="font-size:11px;">
            <thead><tr><th>Code</th><th>Niveau</th><th>Exp.</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Statut</th></tr></thead>
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
            <thead><tr><th class="text-left">Groupe</th><th>N</th><th>Attitude Moyenne</th><th>Pratique Moyenne (%)</th></tr></thead>
            <tbody id="cross-body"></tbody>
        </table>
        <div id="interpretation-cross"></div>
        
        <div class="section-title">3. ANALYSE DES BARRIÈRES</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE FINALE DE L'ÉTUDE</div>
        <div id="final-conclusion" style="font-size:14px; line-height:1.6;">En attente de données...</div>
        <br>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 TÉLÉCHARGER LES RÉSULTATS (CSV)</button>
    </div>
</div>

<script>
    let database = [];

    // Init Listes
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 1; i <= 200; i++) { let opt = document.createElement('option'); opt.value = "HGRM-"+i; opt.text = "Fiche N° " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 20; i <= 65; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; ageSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 40; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans d'exp."; expSelect.appendChild(opt); }

    function saveRecord() {
        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            exp: parseInt(document.getElementById('exp-select').value),
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            p1: getRadioValue('p1'), p2: getRadioValue('p2'), p3: getRadioValue('p3'), p4: getRadioValue('p4'),
            allaitement: document.getElementById('pratique-allaitement').value,
            aes: document.getElementById('pratique-aes').value,
            technique: document.getElementById('pratique-technique').value,
            mammo: document.getElementById('pratique-mammo').value,
            obstacles: getCheckedValues('group-obstacles')
        };

        // Calcul Savoir (Poids sur 100%)
        let ptsSavoir = (record.q1.includes("Vrai")?2:0) + (record.q2.includes("25-30")?2:0) + (record.q3.includes("après")?2:0) + record.risques + record.signes;
        record.scoreSavoir = Math.min(100, Math.round((ptsSavoir / 18) * 100));

        // Calcul Attitude (Inversion pour la question P4)
        let sumAtt = parseInt(record.p1) + parseInt(record.p2) + parseInt(record.p3) + (6 - parseInt(record.p4)); 
        record.scoreAttitude = (sumAtt / 4).toFixed(1);

        // Calcul Pratique (Fusion logic)
        let ptsPrac = 0;
        if(record.allaitement === "Systématique") ptsPrac += 20;
        if(record.aes === "Démonstration physique") ptsPrac += 30;
        if(record.mammo !== "Jamais") ptsPrac += 20;
        if(record.technique === "complete") ptsPrac += 30; else if(record.technique === "systematique") ptsPrac += 15;
        record.scorePratique = ptsPrac;

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        alert(`Fiche ${record.id} enregistrée avec succès !`);
        
        // Reset partiel
        document.querySelectorAll('input[type="checkbox"]').forEach(i => i.checked = false);
        codeSelect.selectedIndex++;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(database.length === 0) return;
        
        // Tableau Matrice
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = '';
        database.forEach(row => {
            tbody.innerHTML += `<tr><td>${row.id}</td><td>${row.niveau}</td><td>${row.exp}</td><td>${row.scoreSavoir}%</td><td>${row.scoreAttitude}</td><td>${row.scorePratique}%</td><td>${row.scoreSavoir >= 70 && row.scorePratique >= 60 ? '🟢 OK' : '🔴 À renforcer'}</td></tr>`;
        });

        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);
        
        // Tableau Croisé
        document.getElementById('cross-body').innerHTML = `
            <tr><td>Savoir Satisfaisant (>=70%)</td><td>${high.length}</td><td>${getAvg(high,'scoreAttitude')} / 5</td><td>${getAvg(high,'scorePratique')}%</td></tr>
            <tr><td>Savoir Insuffisant (<70%)</td><td>${low.length}</td><td>${getAvg(low,'scoreAttitude')} / 5</td><td>${getAvg(low,'scorePratique')}%</td></tr>`;

        // Graphiques
        renderBarChart('graph-savoir', [{label:'Satisfaisant', val:high.length, total:database.length, color:'green'}, {label:'Insuffisant', val:low.length, total:database.length, color:'red'}]);
        renderBarChart('graph-pratique', [{label:'Score Moyen', val:getAvg(database,'scorePratique'), total:100, color:'#b03060'}]);

        // Analyse Obstacles
        let obsCounts = {};
        database.forEach(r => r.obstacles.forEach(o => obsCounts[o] = (obsCounts[o] || 0) + 1));
        let obsHtml = "";
        for (const [k, v] of Object.entries(obsCounts)) {
            let pct = Math.round((v/database.length)*100);
            obsHtml += `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${pct}%; background:#b03060;">${pct}%</div></div></div>`;
        }
        document.getElementById('graph-obstacles').innerHTML = obsHtml;

        // Conclusion
        document.getElementById('final-conclusion').innerHTML = `<h3>Analyse HGRM</h3><p>Sur ${database.length} infirmiers, la pratique globale est de ${getAvg(database,'scorePratique')}%. ${getAvg(high,'scorePratique') > getAvg(low,'scorePratique') ? "On note une corrélation directe entre le savoir et l'application clinique." : "Le savoir théorique ne garantit pas une pratique correcte dans ce service."}</p>`;
    }

    // Helpers
    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(c => c.value); }
    function getRadioValue(n) { return document.querySelector(`input[name="${n}"]:checked`)?.value || 0; }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a, b) => a + parseFloat(b[p]), 0) / arr.length).toFixed(1) : 0; }
    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }
    function renderBarChart(id, data) {
        document.getElementById(id).innerHTML = data.map(d => `<div class="bar-container"><div class="bar-label">${d.label}</div><div class="bar-track"><div class="bar-fill" style="width:${(d.val/d.total)*100}%; background:${d.color};">${d.val}</div></div></div>`).join('');
    }
    function exportToCSV() {
        let csv = "ID,Niveau,Exp,Savoir,Attitude,Pratique\n" + database.map(r => `${r.id},${r.niveau},${r.exp},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let a = document.createElement('a');
        a.href = URL.createObjectURL(new Blob([csv], {type: 'text/csv'}));
        a.download = 'KAP_HGRM_Export.csv';
        a.click();
    }
</script>
</body>
</html>