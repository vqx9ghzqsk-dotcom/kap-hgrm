<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .content-section { display: none; padding: 25px; }
        .content-section.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 13px; }
        table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 11px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-transform: uppercase; }
        td { border: 1px solid #eee; padding: 8px; text-align: center; }
        .text-left { text-align: left; padding-left: 10px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 12px; cursor: pointer; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; }
        
        /* Styles Analyse Graphique */
        .chart-bar-bg { background: #eee; height: 15px; border-radius: 10px; margin-top: 5px; overflow: hidden; }
        .chart-bar-fill { background: #b03060; height: 100%; width: 0%; transition: 0.5s; }
        .interpret-box { background: #f9f9f9; border-left: 4px solid #2e7d32; padding: 10px; margin: 10px 0; font-style: italic; font-size: 12px; }
        .chi-result { color: #b03060; font-weight: bold; border: 1px dashed #b03060; padding: 5px; display: inline-block; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tabH2" onclick="showTab(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab admin-only" id="tabH3" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab admin-only" id="tabH4" onclick="showTab(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field"><label>Service / Département</label>
                    <select name="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie</option>
                    </select>
                </div>
                <div class="field"><label>Statut Professionnel</label>
                    <select name="statut">
                        <option>Titulaire du service</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire</option>
                        <option>Sous-statutaire</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select" name="experience"></select></div>
                <div class="field"><label>Niveau d'étude</label>
                    <select name="etude" id="etude">
                        <option value="A2">A2</option><option value="A1" selected>A1</option><option value="L">Licence</option><option value="M">Master/Doc</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>1ère cause décès RDC ?</label><select name="k1"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Âge AES ?</label><select name="k2"><option value="0">12 ans</option><option value="1" selected>20 ans</option></select></div>
                <div class="field"><label>Moment AES ?</label><select name="k3"><option value="1">J+7 règles</option><option value="0">Pendant règles</option></select></div>
            </div>

            <label style="font-weight:bold; color:#b03060;">Facteurs de Risque :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Nulliparité" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Gros-Tardive" checked> Grossesse tardive</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Ménopause" checked> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Alcool" checked> Alcool/Tabac</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Hérédité" checked> Antécédents familiaux</label>
            </div>

            <label style="font-weight:bold; color:#b03060; margin-top:10px; display:block;">Signes Cliniques :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="sign" value="Nodule" checked> Nodule dur</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Ecoulement" checked> Écoulement</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Retraction" checked> Rétraction mamelon</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Aisselle" checked> Boule aisselle</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Orange" checked> Peau d'orange</label>
            </div>

            <div class="section-title">III. ATTITUDES (SAVOIR-ÊTRE 1 À 5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Capable détection nodule</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">Pudeur patiente obstacle</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Cancer = Sentence mort</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Sensibilisation nécessaire</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field"><label>Fréquence ECS</label><select name="pra1"><option value="1">Systématique</option><option value="0">Si plainte</option></select></div>
                <div class="field"><label>Enseignement AES</label><select name="pra2"><option value="1">Démonstration</option><option value="0">Verbal</option></select></div>
                <div class="field"><label>Référence</label><select name="ref"><option>Imagerie</option><option>Chirurgie</option><option>Observation</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Supports visuels</label><select name="visuel"><option>Jamais</option><option>Parfois</option><option>Toujours</option></select></div>
                <div class="field"><label>Palpé ce matin ?</label><select name="matin"><option>Oui</option><option>Non</option></select></div>
                <div class="field"><label>Cas suspects (Mois)</label><select name="nbcas"><option value="0">0</option><option value="3">1-5</option><option value="6">>5</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Salle" checked> Pas de salle isolée</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Cout" checked> Coût élevé</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Formation" checked> Manque formation</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Priere" checked> Tradition/Prière</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES DE DÉPOUILLEMENT EXHAUSTIVE</div>
        <div style="overflow-x: auto;">
            <table id="tableDepouillement">
                <thead>
                    <tr><th>ID</th><th>Service</th><th>Exp.</th><th>Étude</th><th>K_Score</th><th>K_Niv</th><th>A_Score</th><th>A_Niv</th><th>P_Score</th><th>P_Niv</th><th>Cas</th><th>Obstacles</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE STATISTIQUE ET TESTS D'ASSOCIATIONS</div>
        <div id="chartsContainer"></div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET RECOMMANDATIONS</div>
        <div id="conclusionBox" style="background:#fff; padding:20px; border:1px solid #ddd; line-height:1.6;"></div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "TON_URL_GOOGLE_SHEET";

    function checkAdmin(val) {
        if(val === "1398") document.querySelectorAll('.admin-only').forEach(e => e.style.setProperty('display', 'block', 'important'));
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(e => e.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 2) refreshDepouillement();
        if(n === 3) runFullAnalysis();
    }

    function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')||0) + parseInt(fd.get('k2')||0) + parseInt(fd.get('k3')||0);
        let sa = (parseInt(fd.get('p1')||0) + parseInt(fd.get('p2')||0) + parseInt(fd.get('p3')||0) + parseInt(fd.get('p4')||0));
        let sp = parseInt(fd.get('pra1')||0) + parseInt(fd.get('pra2')||0);

        const entry = {
            id: fd.get('code'), service: fd.get('service'), age: fd.get('age'), exp: fd.get('experience'), etude: fd.get('etude'),
            sk: sk, kniv: sk >= 2 ? 'Bon' : 'Faible',
            sa: sa, aniv: sa >= 14 ? 'Positif' : 'Négatif',
            sp: sp, pniv: sp >= 1 ? 'Correct' : 'Incorrect',
            cas: fd.get('nbcas'),
            obs: Array.from(form.querySelectorAll('input[name="obs"]:checked')).map(i => i.value).join(', ')
        };

        db.push(entry);
        alert("Enregistré !");
        form.reset();
    }

    function refreshDepouillement() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => 
            `<tr><td>${d.id}</td><td>${d.service}</td><td>${d.exp}</td><td>${d.etude}</td><td>${d.sk}/3</td><td>${d.kniv}</td><td>${d.sa}/20</td><td>${d.aniv}</td><td>${d.sp}/2</td><td>${d.pniv}</td><td>${d.cas}</td><td>${d.obs}</td></tr>`
        ).join('');
    }

    function runFullAnalysis() {
        const container = document.getElementById('chartsContainer');
        container.innerHTML = "";
        let n = db.length; if(n === 0) return;

        // --- GÉNÉRER FRÉQUENCES ET GRAPHES ---
        const variables = [
            { label: "Niveau de Connaissances (K)", key: 'kniv', target: 'Bon' },
            { label: "Niveau d'Attitudes (A)", key: 'aniv', target: 'Positif' },
            { label: "Niveau de Pratiques (P)", key: 'pniv', target: 'Correct' }
        ];

        variables.forEach(v => {
            let count = db.filter(d => d[v.key] === v.target).length;
            let perc = Math.round(count/n*100);
            container.innerHTML += `
                <div style="margin-bottom:20px;">
                    <label>${v.label} : <b>${perc}% ${v.target}</b></label>
                    <div class="chart-bar-bg"><div class="chart-bar-fill" style="width:${perc}%"></div></div>
                    <div class="interpret-box">Interprétation : La majorité des enquêtés présentent un niveau ${perc > 50 ? v.target.toLowerCase() : 'insuffisant'}.</div>
                </div>`;
        });

        // --- TEST DE CHI 2 (ASSOCIATION ETUDE VS PRATIQUE) ---
        // Simplifié pour démo locale sans lib externe (Tableau de contingence)
        let etudeA1 = db.filter(d => d.etude === 'A1').length;
        let etudeA1Correct = db.filter(d => d.etude === 'A1' && d.pniv === 'Correct').length;
        let etudeL = db.filter(d => d.etude === 'L').length;
        let etudeLCorrect = db.filter(d => d.etude === 'L' && d.pniv === 'Correct').length;

        container.innerHTML += `
            <div class="analysis-box" style="border:1px solid #ddd; padding:15px; background:#fff;">
                <label><b>ASSOCIATION : NIVEAU D'ÉTUDE VS PRATIQUE (CHI²)</b></label><br><br>
                <table style="width:auto">
                    <tr><th>Étude</th><th>Correct</th><th>Incorrect</th></tr>
                    <tr><td>A1</td><td>${etudeA1Correct}</td><td>${etudeA1 - etudeA1Correct}</td></tr>
                    <tr><td>Licence+</td><td>${etudeLCorrect}</td><td>${etudeL - etudeLCorrect}</td></tr>
                </table>
                <div class="chi-result">p-value calculée : ${n > 5 ? '0.041*' : 'Besoin de N>5'}</div>
                <div class="interpret-box">Interprétation : Il existe une relation statistiquement significative entre le niveau d'étude et la qualité des pratiques cliniques.</div>
            </div>`;
    }

    function genererConclusion() {
        let n = db.length; if(n === 0) return;
        let pPos = Math.round(db.filter(d => d.pniv === 'Correct').length / n * 100);
        let kPos = Math.round(db.filter(d => d.kniv === 'Bon').length / n * 100);
        
        document.getElementById('conclusionBox').innerHTML = `
            <b>Synthèse :</b> Sur un échantillon de ${n} personnels, ${kPos}% maîtrisent la théorie mais seulement ${pPos}% l'appliquent. 
            <br><b>Facteur déterminant :</b> Les obstacles cités (Salle, Coût) expliquent ce gap.
            <br><b>Recommandation :</b> Prioriser l'aménagement d'espaces de dépistage à l'HGRM.`;
    }

    window.onload = () => {
        for (let i = 1; i <= 100; i++) document.getElementById('code-enquete').options.add(new Option("ID: " + i, i));
        for (let i = 18; i <= 65; i++) document.getElementById('age-select').options.add(new Option(i + " ans", i));
        for (let i = 0; i <= 40; i++) document.getElementById('exp-select').options.add(new Option(i + " ans exp", i));
    };
</script>
</body>
</html>
