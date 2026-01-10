<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 28px; font-weight: bold; color: #b03060; }
        .highlight-box { background-color: #e8f5e9; border: 2px solid #2e7d32; padding: 20px; border-radius: 8px; margin-top: 20px; }
        .highlight-text { font-size: 16px; color: #1b5e20; font-style: italic; font-weight: 600; }
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.5s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 60px; border: 1px solid #ccc; font-size: 10px; padding: 4px; border-radius: 4px; }
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
        <form class="form-content" id="kapForm">
            
            <div class="section-title">I. PROFIL SOCIODÉMOGRAPHIQUE</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service</label>
                    <select name="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Chirurgie</option>
                        <option>Médecine Interne</option>
                        <option>Pédiatrie</option>
                        <option>Urgence</option>
                    </select>
                </div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">L (Licenciée)</option>
                        <option value="M">M (Master/Doctorat)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field">
                    <label>Ancienneté</label>
                    <select name="experience">
                        <option value="0-5">0-5 ans</option>
                        <option value="6-10">6-10 ans</option>
                        <option value="11-20">11-20 ans</option>
                        <option value="20+">Plus de 20 ans</option>
                    </select>
                </div>
                <div class="field">
                    <label>Formation continue Cancer ?</label>
                    <select name="formation">
                        <option value="1">Oui, < 2 ans</option>
                        <option value="1">Oui, > 2 ans</option>
                        <option value="0">Jamais</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>1. 1ère cause décès cancer femme RDC ?</label>
                    <select name="k1">
                        <option value="0">Col de l'utérus</option>
                        <option value="1">Sein</option>
                        <option value="0">Poumon</option>
                    </select>
                </div>
                <div class="field">
                    <label>2. Fréquence idéale AES ?</label>
                    <select name="k2">
                        <option value="0">Chaque jour</option>
                        <option value="1">1x / mois (après règles)</option>
                        <option value="0">1x / an</option>
                    </select>
                </div>
                <div class="field">
                    <label>3. Signe d'alerte majeur ?</label>
                    <select name="k3">
                        <option value="0">Douleur règles</option>
                        <option value="1">Nodule dur indolore</option>
                        <option value="0">Volume des deux seins</option>
                    </select>
                </div>
            </div>
            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">4. Facteurs de risque (Cochez si connu) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Heredite"> Hérédité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Nulliparite"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Menopause"> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Alcool"> Alcool / Tabac</label>
            </div>

            <div class="section-title">III. ATTITUDES (LIKERT 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1 (Pas d'accord)</th><th>5 (D'accord)</th></tr></thead>
                <tbody>
                    <tr>
                        <td class="text-left">Le dépistage précoce permet la guérison totale</td>
                        <td colspan="2" style="padding:10px;">
                            <input type="range" name="att1" min="1" max="5" value="3" style="width:100%">
                            <div style="display:flex; justify-content:space-between; font-size:10px;"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span></div>
                        </td>
                    </tr>
                    <tr>
                        <td class="text-left">Je me sens capable de réaliser un ECS efficace</td>
                        <td colspan="2" style="padding:10px;">
                            <input type="range" name="att2" min="1" max="5" value="3" style="width:100%">
                            <div style="display:flex; justify-content:space-between; font-size:10px;"><span>1</span><span>2</span><span>3</span><span>4</span><span>5</span></div>
                        </td>
                    </tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>1. Réalisez-vous l'ECS patientes ?</label>
                    <select name="pra1">
                        <option value="1">Systématiquement</option>
                        <option value="0">Parfois / Rarement</option>
                    </select>
                </div>
                <div class="field">
                    <label>2. Enseignez-vous l'AES (Démonstration) ?</label>
                    <select name="pra2">
                        <option value="1">Oui, physique</option>
                        <option value="0">Verbal uniquement</option>
                        <option value="0">Non</option>
                    </select>
                </div>
                <div class="field">
                    <label>3. Pratiquez-vous l'AES sur vous-même ?</label>
                    <select name="pra3">
                        <option value="1">Oui, mensuellement</option>
                        <option value="0">Irrégulièrement / Jamais</option>
                    </select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES (CONTEXTE)</div>
            <div class="field">
                <label>Quel est le FREIN PRINCIPAL dans votre service ?</label>
                <select name="obs_main">
                    <option value="Local">Manque de local / Intimité</option>
                    <option value="Oubli">Oubli / Surcharge travail</option>
                    <option value="Materiel">Manque matériel (Support visuel)</option>
                    <option value="Croyance">Refus patiente (Prière/Tradition)</option>
                </select>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES DE DÉPOUILLEMENT</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Étude</th><th>Savoir</th><th>Attitude</th><th>Pratique</th><th>Obstacle</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">STATISTIQUES AVANCÉES</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total N</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Bon Savoir</div></div>
            <div class="stat-card"><div class="stat-val" id="res-a">0%</div><div class="stat-label">Bonne Attitude</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Bonne Pratique</div></div>
        </div>

        <div class="highlight-box">
            <label style="color:#2e7d32; font-weight:bold;">ANALYSE CROISÉE AUTOMATIQUE (FOCUS A1) :</label>
            <p id="dynamic-insight" class="highlight-text">En attente de données...</p>
        </div>

        <div class="row" style="margin-top:20px;">
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Répartition par Étude (%)</b></label>
                <div id="study-dist" style="margin-top:10px; font-size:12px;"></div>
            </div>
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Obstacle n°1 Identifié</b></label>
                <p id="top-obstacle" style="color:#b03060; font-weight:bold;">--</p>
            </div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET RECOMMANDATIONS EXPERTES</div>
        <div id="summary" style="line-height:1.8; background:#fff; padding:30px; border:1px solid #ddd; border-radius:8px; font-size:14px;">
            En attente de saisie...
        </div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
            alert("Accès autorisé.");
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        const tabIds = ['','tabH2','tabH3','tabH4'];
        if(n > 1) document.getElementById(tabIds[n-1]).classList.add('active');
        else document.querySelector('.tab').classList.add('active');
        if(n >= 3) calculerAnalyse();
    }

    async function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        // Calcul SCORE SAVOIR (Max 5 points : 3 QCM + risques)
        let riskCount = document.querySelectorAll('input[name="risk"]:checked').length;
        let scoreK = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3')) + (riskCount >= 2 ? 1 : 0);
        let valK = scoreK >= 3 ? 'Bon' : 'Faible';

        // Calcul SCORE ATTITUDE (Moyenne Likert)
        let scoreA = parseInt(fd.get('att1')) + parseInt(fd.get('att2'));
        let valA = scoreA >= 7 ? 'Positive' : 'Negative'; // 7/10 minimum

        // Calcul SCORE PRATIQUE
        let scoreP = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2')) + parseInt(fd.get('pra3'));
        let valP = scoreP >= 2 ? 'Correcte' : 'Incorrecte';

        const entry = {
            code: fd.get('code'),
            service: fd.get('service'),
            etude: fd.get('etude'),
            experience: fd.get('experience'),
            savoir: valK,
            attitude: valA,
            pratique: valP,
            obstacle: fd.get('obs_main')
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            db.push(entry);
            actualiserTableau();
            alert("Fiche " + entry.code + " enregistrée !");
            form.reset();
        } catch (e) { alert("Erreur réseau mais continuez."); }
    }

    function actualiserTableau() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => 
            `<tr><td>${d.code}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td><td>${d.obstacle}</td></tr>`
        ).join('');
    }

    function calculerAnalyse() {
        let n = db.length; if(n === 0) return;
        
        let kHigh = db.filter(d => d.savoir === 'Bon').length;
        let aGood = db.filter(d => d.attitude === 'Positive').length;
        let pGood = db.filter(d => d.pratique === 'Correcte').length;
        
        // Mise à jour des cartes
        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
        document.getElementById('res-a').innerText = Math.round(aGood/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";

        // --- INTELLIGENCE POUR LA PHRASE SPECIFIQUE ---
        // On filtre uniquement les A1
        let a1Data = db.filter(d => d.etude === 'A1');
        let countA1 = a1Data.length;
        
        if (countA1 > 0) {
            let a1Att = a1Data.filter(d => d.attitude === 'Positive').length;
            let a1Pra = a1Data.filter(d => d.pratique === 'Correcte').length;
            
            // Trouver l'obstacle le plus fréquent chez les A1
            let obstaclesA1 = a1Data.map(d => d.obstacle);
            let topObs = obstaclesA1.sort((a,b) => obstaclesA1.filter(v => v===a).length - obstaclesA1.filter(v => v===b).length).pop();
            
            let txtObs = "";
            if(topObs === "Local") txtObs = "du manque de local";
            else if(topObs === "Oubli") txtObs = "de l'oubli/surcharge";
            else if(topObs === "Materiel") txtObs = "du manque de matériel";
            else txtObs = "des croyances";

            let pctAtt = Math.round(a1Att/countA1*100);
            let pctPra = Math.round(a1Pra/countA1*100);

            document.getElementById('dynamic-insight').innerHTML = 
                `"${pctAtt}% des infirmières graduées (A1) ont une bonne attitude, mais seulement ${pctPra}% ont une pratique correcte principalement à cause ${txtObs}."`;
        } else {
            document.getElementById('dynamic-insight').innerText = "Pas encore assez de données 'A1' pour générer l'analyse.";
        }

        // Répartition Études
        let studies = ['A2', 'A1', 'L', 'M'];
        let distHtml = "";
        studies.forEach(s => {
            let count = db.filter(d => d.etude === s).length;
            distHtml += `<b>${s}:</b> ${Math.round(count/n*100)}% | `;
        });
        document.getElementById('study-dist').innerHTML = distHtml;

        // Obstacle Global
        let allObs = db.map(d => d.obstacle);
        let mainObs = allObs.sort((a,b) => allObs.filter(v => v===a).length - allObs.filter(v => v===b).length).pop();
        document.getElementById('top-obstacle').innerText = mainObs || "--";

        // Conclusion Générale
        let conc = `<b>SYNTHÈSE :</b><br>L'étude sur ${n} sujets révèle une dissonance entre le savoir (${Math.round(kHigh/n*100)}%) et la pratique (${Math.round(pGood/n*100)}%).<br>`;
        conc += `Le frein majeur identifié est : <b>${mainObs}</b>. <br>Il est impératif d'améliorer les conditions structurelles.`;
        document.getElementById('summary').innerHTML = conc;
    }

    function exportCSV() {
        let csv = "Code,Service,Etude,Savoir,Attitude,Pratique,Obstacle\n";
        db.forEach(d => { csv += `${d.code},${d.service},${d.etude},${d.savoir},${d.attitude},${d.pratique},${d.obstacle}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'Rapport_KAP_HGRM.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) cs.options.add(new Option("ID: " + i, i));
        const as = document.getElementById('age-select');
        for (let i = 20; i <= 65; i++) as.options.add(new Option(i + " ans", i));
    };
</script>
</body>
</html>
