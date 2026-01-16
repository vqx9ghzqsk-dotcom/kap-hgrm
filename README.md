<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Analyse Expert Cancer du Sein</title>
    <style>
        /* --- STYLE GLOBAL EXPERT --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 10px; background: #fdfdfd; padding: 20px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.3); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        
        /* --- STYLES ANALYSE (ONGLET 3) --- */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 180px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; position: relative; }
        .bar-fill { height: 100%; transition: width 0.8s ease-out; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; }
        .bar-value { width: 50px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 20px; font-style: italic; color: #1b5e20; margin-top: 20px; line-height: 1.5; border-radius: 0 8px 8px 0; }
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
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT COMPLET (CSV)</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION DU PERSONNEL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label>Sexe</label><select id="sexe"><option>Féminin</option><option>Masculin</option></select></div>
                <div class="field"><label>Service</label><select id="service">
                    <option>Gynécologie-Obstétrique</option>
                    <option>Médecine Interne</option>
                    <option>Chirurgie</option>
                    <option>Urgences / Autre</option>
                </select></div>
            </div>
            <div class="row">
                <div class="field"><label>Ancienneté</label><select id="exp-select"></select></div>
                <div class="field"><label>Niveau d'étude</label><select id="niveau">
                    <option>A2 (Diplômée d'État)</option>
                    <option selected>A1 (Graduée)</option>
                    <option>A0 (Licenciée/Master)</option>
                </select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès femme RDC ?</label><select id="q1"><option>Vrai</option><option>Faux</option><option>Je ne sais pas</option></select></div>
                <div class="field"><label>Âge 1ère Mammographie ?</label><select id="q2"><option>Dès 20 ans</option><option>Vers 35-40 ans</option><option>Vers 50 ans</option></select></div>
                <div class="field"><label>Moment idéal AES ?</label><select id="q3"><option>Pendant les règles</option><option selected>7 à 10 jours après les règles</option><option>N'importe quand</option></select></div>
            </div>

            <label style="margin:10px 0; display:block; font-weight:bold; color:#b03060;">Facteurs de risque connus :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge (> 50 ans)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="nulli"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" value="meno"> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" value="obese"> Obésité / Sédentarité</label>
            </div>

            <label style="margin:20px 0 10px 0; display:block; font-weight:bold; color:#b03060;">Signes d'alerte identifiés :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur/fixe</label>
                <label class="check-item"><input type="checkbox" value="sang"> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" value="peau"> Peau d'orange / Rougeur</label>
                <label class="check-item"><input type="checkbox" value="ganglion"> Adénopathie axillaire</label>
                <label class="check-item"><input type="checkbox" value="mamelon"> Rétraction mamelonnaire</label>
            </div>

            <div class="section-title">III. ATTITUDES (SCORING LIKERT 1-5)</div>
            <table>
                <thead><tr><th style="text-align:left">Énoncés de perception</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td style="text-align:left">Le dépistage précoce garantit la guérison.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4"></td><td><input type="radio" name="p1" value="5" checked></td></tr>
                    <tr><td style="text-align:left">Je suis capable de réaliser une palpation technique.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4" checked></td><td><input type="radio" name="p2" value="5"></td></tr>
                    <tr><td style="text-align:left">La pudeur des patientes est un obstacle majeur.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2"></td><td><input type="radio" name="p3" value="3" checked></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td style="text-align:left">La sensibilisation est une priorité de mon service.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (MAÎTRISE TECHNIQUE)</div>
            <div class="row">
                <div class="field"><label>Fréquence d'examen</label><select id="pratique-freq"><option>Systématique</option><option>Si plainte</option><option>Rarement</option></select></div>
                <div class="field"><label>Partie de la main utilisée</label><select id="prac-main"><option>Pointe des doigts</option><option selected>Pulpe des 3 doigts</option><option>Paume</option></select></div>
                <div class="field"><label>Zone souvent oubliée</label><select id="prac-zone"><option>Mamelon</option><option>Partie haute</option><option selected>Prolongement axillaire</option></select></div>
            </div>
            
            <label style="margin:10px 0; display:block; font-weight:bold; color:#b03060;">Mouvements de palpation maîtrisés :</label>
            <div class="check-group" id="group-mouv">
                <label class="check-item"><input type="checkbox" value="circ"> Circulaire (Spirale)</label>
                <label class="check-item"><input type="checkbox" value="vert"> Vertical (Bandelettes)</label>
                <label class="check-item"><input type="checkbox" value="rad"> Radial (Étoile)</label>
            </div>

            <div class="section-title">V. OBSTACLES STRUCTURELS</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="formation"> Manque de formation spécifique</label>
                <label class="check-item"><input type="checkbox" value="temps"> Surcharge de travail / Pas de temps</label>
                <label class="check-item"><input type="checkbox" value="materiel"> Absence de matériel (Mannequins)</label>
                <label class="check-item"><input type="checkbox" value="pudeur"> Refus / Pudeur culturelle</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE DANS LA BASE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES BRUTE (N = <span id="n-total">0</span>)</div>
        <table>
            <thead>
                <tr>
                    <th>Code</th><th>Sexe</th><th>Niveau</th><th>Exp</th>
                    <th>Score Savoir (%)</th><th>Score Attitude (/5)</th><th>Score Pratique (%)</th>
                    <th>Diagnostic</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. RÉPARTITION DES NIVEAUX (FRÉQUENCES)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances (Savoir)</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique Clinique</div>
                <div id="graph-pratique"></div>
            </div>
        </div>

        <div class="section-title">2. ANALYSE CROISÉE : IMPACT DU SAVOIR SUR L'ACTION</div>
        <table style="background:#444; color:white; border-radius:8px; overflow:hidden;">
            <thead>
                <tr>
                    <th style="text-align:left; padding:15px;">Groupe d'analyse</th>
                    <th>Effectif (N)</th>
                    <th>Attitude Moyenne (/5)</th>
                    <th>Score Pratique Moyen (%)</th>
                </tr>
            </thead>
            <tbody id="cross-body" style="background:white; color:#333;"></tbody>
        </table>

        <div id="interpretation-cross"></div>

        <div class="section-title">3. ANALYSE DES BARRIÈRES À LA PRÉVENTION</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS POUR L'HGRM</div>
        <div id="final-conclusion" style="font-size:15px; line-height:1.8; color:#333;"></div>
        <br><hr><br>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 TÉLÉCHARGER LA BASE DE DONNÉES COMPLÈTE (.CSV)</button>
    </div>
</div>

<script>
    let database = [];

    // Initialisation des listes
    const codeSel = document.getElementById('code-enquete');
    for(let i=1; i<=200; i++) { let o=document.createElement('option'); o.value="E-"+i; o.text="Enquêté(e) "+i; codeSel.appendChild(o); }
    const expSel = document.getElementById('exp-select');
    for(let i=0; i<=40; i++) { let o=document.createElement('option'); o.value=i; o.text=i+" ans d'expérience"; expSel.appendChild(o); }

    function saveRecord() {
        // Collecte
        let r = {
            id: document.getElementById('code-enquete').value,
            sexe: document.getElementById('sexe').value,
            service: document.getElementById('service').value,
            exp: parseInt(expSel.value),
            niveau: document.getElementById('niveau').value,
            q1: document.getElementById('q1').value,
            q2: document.getElementById('q2').value,
            q3: document.getElementById('q3').value,
            risques: getCheckedCount('group-risques'),
            signes: getCheckedCount('group-signes'),
            p1: getRadioValue('p1'), p2: getRadioValue('p2'), p3: getRadioValue('p3'), p4: getRadioValue('p4'),
            freq: document.getElementById('pratique-freq').value,
            main: document.getElementById('prac-main').value,
            zone: document.getElementById('prac-zone').value,
            mouv: getCheckedCount('group-mouv'),
            obstacles: getCheckedValues('group-obstacles')
        };

        // --- SCORING DÉTAILLÉ ---
        let ptsSavoir = 0;
        if(r.q1 === "Vrai") ptsSavoir += 2;
        if(r.q2 === "Vers 35-40 ans") ptsSavoir += 2;
        if(r.q3.includes("7 à 10 jours")) ptsSavoir += 2;
        ptsSavoir += r.risques + r.signes; 
        r.scoreSavoir = Math.round((ptsSavoir / 16) * 100); // Max 16 pts

        let sumAtt = parseInt(r.p1) + parseInt(r.p2) + parseInt(r.p3) + parseInt(r.p4);
        r.scoreAttitude = (sumAtt / 4).toFixed(1);

        let ptsPrac = 0;
        if(r.freq === "Systématique") ptsPrac += 30;
        if(r.main === "Pulpe des 3 doigts") ptsPrac += 25;
        if(r.zone === "Prolongement axillaire") ptsPrac += 25;
        if(r.mouv >= 2) ptsPrac += 20;
        r.scorePratique = ptsPrac;

        database.push(r);
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        
        alert(`Fiche ${r.id} enregistrée.\nScore Savoir: ${r.scoreSavoir}%\nScore Pratique: ${r.scorePratique}%`);
        
        codeSel.selectedIndex++;
        updateAnalysis();
    }

    function updateAnalysis() {
        if(database.length === 0) return;

        // 1. Matrice (Onglet 2)
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(row => `
            <tr>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.niveau}</td><td>${row.exp} ans</td>
                <td style="color:${getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td>${row.scoreAttitude}</td>
                <td style="color:${getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td>${row.scoreSavoir >= 70 && row.scorePratique >= 70 ? '🟢 Performant' : '🔴 À former'}</td>
            </tr>
        `).join('');

        // 2. Croisement (Onglet 3)
        let high = database.filter(r => r.scoreSavoir >= 70);
        let low = database.filter(r => r.scoreSavoir < 70);

        let avgAttH = getAvg(high, 'scoreAttitude'), avgPracH = getAvg(high, 'scorePratique');
        let avgAttL = getAvg(low, 'scoreAttitude'), avgPracL = getAvg(low, 'scorePratique');

        document.getElementById('cross-body').innerHTML = `
            <tr><td style="padding:15px;"><b>Savoir Élevé (>=70%)</b></td><td>${high.length}</td><td>${avgAttH}/5</td><td style="font-weight:bold">${avgPracH}%</td></tr>
            <tr><td style="padding:15px;"><b>Savoir Faible (<70%)</b></td><td>${low.length}</td><td>${avgAttL}/5</td><td style="font-weight:bold">${avgPracL}%</td></tr>
        `;

        // Graphiques
        renderBarChart('graph-savoir', [
            {label: 'Connaissances Satisfaisantes', val: high.length, total: database.length, color: '#2e7d32'},
            {label: 'Connaissances Insuffisantes', val: low.length, total: database.length, color: '#c62828'}
        ]);
        
        let goodPrac = database.filter(r => r.scorePratique >= 75).length;
        renderBarChart('graph-pratique', [
            {label: 'Pratique Technique Correcte', val: goodPrac, total: database.length, color: '#1565c0'},
            {label: 'Pratique Incomplète', val: database.length - goodPrac, total: database.length, color: '#f57f17'}
        ]);

        // Interprétation
        let interp = document.getElementById('interpretation-cross');
        let txt = `<div class="${avgPracH > avgPracL + 15 ? 'interpretation-box' : 'alert-box'}">`;
        txt += `<b>Interprétation statistique :</b> Sur ${database.length} infirmiers, `;
        if(avgPracH > avgPracL + 15) {
            txt += `on observe que les connaissances théoriques influencent directement la qualité technique. Former les agents sur la théorie augmente la précision du geste clinique de ${Math.round(avgPracH-avgPracL)} points.`;
        } else {
            txt += `il existe une disparité entre le savoir et l'agir. Même les agents "savants" ont une pratique faible (${avgPracH}%). Cela indique que l'obstacle est lié aux conditions de travail ou au manque d'outils, et non à l'intelligence.`;
        }
        txt += `</div>`;
        interp.innerHTML = txt;

        // Obstacles
        let obsCounts = {};
        database.forEach(r => r.obstacles.forEach(o => obsCounts[o] = (obsCounts[o]||0)+1));
        document.getElementById('graph-obstacles').innerHTML = Object.entries(obsCounts).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k.toUpperCase()}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
        }).join('');

        // Onglet 4
        document.getElementById('final-conclusion').innerHTML = `
            <h3>Synthèse Globale de l'Étude (HGRM)</h3>
            <p>L'analyse automatisée de <b>${database.length}</b> fiches d'enquête permet de conclure :</p>
            <ul>
                <li><b>Savoir :</b> Seuls ${Math.round((high.length/database.length)*100)}% des enquêtés maîtrisent les fondements du dépistage précoce.</li>
                <li><b>Pratique :</b> La zone axillaire reste un angle mort pour beaucoup, et la technique de la pulpe n'est pas généralisée.</li>
                <li><b>Barrière majeure :</b> L'analyse des obstacles désigne le <b>${Object.keys(obsCounts).sort((a,b)=>obsCounts[b]-obsCounts[a])[0] || '...'}</b> comme frein principal.</li>
            </ul>
        `;
    }

    // --- HELPERS ---
    function getCheckedCount(id) { return document.querySelectorAll(`#${id} input:checked`).length; }
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); }
    function getRadioValue(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e ? e.value : 0; }
    function getColor(s) { return s >= 70 ? 'green' : (s >= 50 ? 'orange' : 'red'); }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; }
    function renderBarChart(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.total ? Math.round((i.val/i.total)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.label}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.color}">${p}%</div></div><div class="bar-value">${i.val}</div></div>`;
        }).join('');
    }
    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }
    function exportToCSV() {
        let csv = "\ufeffID,Sexe,Service,Niveau,Exp,Savoir,Attitude,Pratique\n" + database.map(r => `${r.id},${r.sexe},${r.service},${r.niveau},${r.exp},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let link = document.createElement("a"); link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "Rapport_KAP_CancerSein.csv"; link.click();
    }
</script>
</body>
</html>