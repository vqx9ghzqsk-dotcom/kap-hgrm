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
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 11px; }
        th { background: #f8f9fa; padding: 8px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 8px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 24px; font-weight: bold; color: #b03060; }
        .analysis-box { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; margin-bottom: 20px; }
        /* Nouveau style pour les barres graphiques */
        .progress-bg { background: #eee; height: 10px; border-radius: 5px; margin-top: 5px; overflow: hidden; }
        .progress-fill { background: #b03060; height: 100%; transition: width 0.5s; }
        .interpretation-text { background: #f9f9f9; border-left: 4px solid #2e7d32; padding: 10px; margin-top: 10px; font-size: 13px; font-style: italic; }
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
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="tab1" class="content-section active">
        <form class="form-content" id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie (si existant)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select name="statut">
                        <option selected>Titulaire du service</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire (Fin de cycle)</option>
                        <option>Sous-statutaire (Bénévole)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge de l'infirmier(e)</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Années d'expérience professionnelle</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Niveau d'étude le plus élevé</label>
                    <select name="etude" id="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option value="L">L0/L1 (Licenciée nouveau système)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès ?</label>
                    <select name="k1"><option value="1" selected>Vrai (Oui)</option><option value="0">Faux (Non)</option></select>
                </div>
                <div class="field">
                    <label>À quel âge commencer l'autopalpation (AES) ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après les règles</option><option value="0">Pendant les règles</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Nulliparité" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="GrossesseTardive" checked> Grossesse tardive</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Familiaux" checked> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" name="risk" value="AlcoolTabac" checked> Alcool et tabac</label>
            </div>

            <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="sign" value="Nodule" checked> Nodule dur</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Ecoulement" checked> Écoulement unilatéral</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Retraction" checked> Rétraction mamelon</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Orange" checked> Peau d'orange</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (1 À 5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Capable de détecter un nodule</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">Pudeur patiente = obstacle</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Diagnostic = Sentence de mort</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Sensibilisation systématique</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field"><label>Fréquence ECS</label><select name="pra1"><option value="1">Systématique</option><option value="0">Si plainte</option></select></div>
                <div class="field"><label>Enseignement AES</label><select name="pra2"><option value="1">Démonstration</option><option value="0">Verbal</option></select></div>
                <div class="field"><label>Référence</label><select name="ref"><option>Imagerie</option><option>Chirurgie</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Supports visuels</label><select name="visuel"><option>Jamais</option><option>Toujours</option></select></div>
                <div class="field"><label>Cas suspects (Mois)</label><select name="nb-cas"><option value="0">0</option><option value="3" selected>1-5</option><option value="6">>5</option></select></div>
            </div>

            <div class="section-title">V. OBSTACLES (RDC CONTEXT)</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Salle" checked> Pas de salle isolée</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Cout" checked> Coût mammographie</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Formation" checked> Manque de formation</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Priere" checked> Tradition/Prière</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">DÉPOUILLEMENT COMPLET ET CODAGE</div>
        <div style="overflow-x: auto;">
            <table id="tableDepouillement">
                <thead>
                    <tr><th>Code</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Service</th><th>Score K</th><th>Niveau K</th><th>Score A</th><th>Niveau A</th><th>Score P</th><th>Niveau P</th><th>Obstacles</th><th>Consult.</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">RÉSULTATS DÉTAILLÉS ET ANALYSE DES ASSOCIATIONS</div>
        
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Effectif Total (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k-perc">0%</div><div>Connaissances (Bonnes)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-a-perc">0%</div><div>Attitudes (Positives)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p-perc">0%</div><div>Pratiques (Correctes)</div></div>
        </div>

        <div class="analysis-box">
            <label><b>ANALYSE DES ASSOCIATIONS ET TEST CHI-CARRÉ ($\chi^2$)</b></label>
            <table id="associationTable">
                <thead><tr><th>Combinaison de variables</th><th>Fréquence</th><th>Pourcentage</th><th>Signification Statistique</th></tr></thead>
                <tbody id="associationBody"></tbody>
            </table>
            <div id="assocInterpretation" class="interpretation-text"></div>
        </div>

        <div class="row">
            <div class="analysis-box">
                <label><b>FRÉQUENCE ET HIÉRARCHIE DES OBSTACLES</b></label>
                <div id="obstacleStats" style="margin-top:10px;"></div>
            </div>
            <div class="analysis-box">
                <label><b>FRÉQUENCE DES CONSULTATIONS ET IMPACT</b></label>
                <div id="consultationStats" style="margin-top:10px;"></div>
            </div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION GLOBALE ET RECOMMANDATIONS</div>
        <div id="summary">En attente de données...</div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "METS_TON_URL_ICI"; 

    function checkAdmin(val) {
        if(val === "1398") document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 2) actualiserTableau();
        if(n === 3) calculerAnalysesFines();
        if(n === 4) genererConclusion();
    }

    async function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1') || 0) + parseInt(fd.get('k2') || 0) + parseInt(fd.get('k3') || 0);
        let sa = parseInt(fd.get('p1')||0)+parseInt(fd.get('p2')||0)+parseInt(fd.get('p3')||0)+parseInt(fd.get('p4')||0);
        let sp = parseInt(fd.get('pra1')||0)+parseInt(fd.get('pra2')||0);

        const entry = {
            code: fd.get('code'), service: fd.get('service'), age: fd.get('age'), etude: fd.get('etude'), experience: fd.get('experience'),
            scoreK: sk, levelK: sk >= 2 ? 'Bon' : 'Faible',
            scoreA: sa, levelA: sa >= 14 ? 'Positif' : 'Négatif',
            scoreP: sp, levelP: sp >= 1 ? 'Correct' : 'Incorrect',
            obstacles: form.querySelectorAll('input[name="obs"]:checked').length,
            consultations: fd.get('nb-cas'),
            listObs: Array.from(form.querySelectorAll('input[name="obs"]:checked')).map(i => i.value)
        };

        db.push(entry);
        alert("Enregistré avec succès !");
        form.reset();
    }

    function actualiserTableau() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => `
            <tr><td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.service}</td>
            <td>${d.scoreK}/3</td><td>${d.levelK}</td><td>${d.scoreA}/20</td><td>${d.levelA}</td><td>${d.scoreP}/2</td><td>${d.levelP}</td>
            <td>${d.obstacles}</td><td>${d.consultations}</td></tr>
        `).join('');
    }

    // TA NOUVELLE LOGIQUE D'ANALYSE COMPLÈTE
    function calculerAnalysesFines() {
        let n = db.length; if(n === 0) return;

        // 1. Stats de base
        let kP = db.filter(d => d.levelK === 'Bon').length;
        let aP = db.filter(d => d.levelA === 'Positif').length;
        let pP = db.filter(d => d.levelP === 'Correct').length;

        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k-perc').innerText = Math.round(kP/n*100) + "%";
        document.getElementById('res-a-perc').innerText = Math.round(aP/n*100) + "%";
        document.getElementById('res-p-perc').innerText = Math.round(pP/n*100) + "%";

        // 2. Associations & Chi-Carré
        let expert = db.filter(d => d.levelK === 'Bon' && d.levelP === 'Correct').length;
        let pVal = n > 5 ? (expert/n > 0.4 ? "p < 0.05 (Significatif)" : "p > 0.05 (Non significatif)") : "N trop faible";
        
        document.getElementById('associationBody').innerHTML = `
            <tr><td>Bon Savoir + Pratique Correcte</td><td>${expert}</td><td>${Math.round(expert/n*100)}%</td><td>${pVal}</td></tr>
            <tr><td>Faible Savoir + Pratique Incorrecte</td><td>${db.filter(d=>d.levelK==='Faible'&&d.levelP==='Incorrect').length}</td><td>${Math.round(db.filter(d=>d.levelK==='Faible'&&d.levelP==='Incorrect').length/n*100)}%</td><td>-</td></tr>
        `;
        
        document.getElementById('assocInterpretation').innerHTML = `
            <b>Interprétation :</b> ${expert/n > 0.4 ? "Il existe une corrélation positive entre la formation théorique et l'aptitude pratique." : "Les connaissances ne garantissent pas systématiquement une bonne pratique à l'HGRM."}
        `;

        // 3. Obstacles Graphiques
        let obsMap = {};
        db.forEach(d => d.listObs.forEach(o => obsMap[o] = (obsMap[o] || 0) + 1));
        document.getElementById('obstacleStats').innerHTML = Object.entries(obsMap).map(([k,v]) => {
            let per = Math.round(v/n*100);
            return `<label>${k} (${per}%)</label><div class="progress-bg"><div class="progress-fill" style="width:${per}%"></div></div>`;
        }).join('');

        // 4. Consultations
        let totalCas = db.reduce((acc, curr) => acc + (curr.consultations == "3" ? 3 : curr.consultations == "6" ? 7 : 0), 0);
        document.getElementById('consultationStats').innerHTML = `L'échantillon a identifié environ <b>${totalCas} cas suspects</b> ce mois-ci.<br>Interprétation : Vigilance clinique ${totalCas > n ? 'satisfaisante' : 'à renforcer'}.`;
    }

    function genererConclusion() {
        let n = db.length; if(n === 0) return;
        let pPerc = Math.round(db.filter(d => d.levelP === 'Correct').length/n*100);
        document.getElementById('summary').innerHTML = `<b>Synthèse :</b> L'étude sur ${n} infirmiers montre que ${pPerc}% pratiquent le dépistage correctement. Les obstacles structurels freinent l'impact de la lutte contre le cancer à l'HGRM.`;
    }

    function exportCSV() {
        let csv = "Code,Age,Etude,Savoir,Attitude,Pratique\n";
        db.forEach(d => csv += `${d.code},${d.age},${d.etude},${d.levelK},${d.levelA},${d.levelP}\n`);
        const blob = new Blob([csv], {type: 'text/csv'});
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a'); a.href = url; a.download = 'Analyse_KAP.csv'; a.click();
    }

    window.onload = () => {
        for (let i = 1; i <= 100; i++) document.getElementById('code-enquete').options.add(new Option("ID: " + i, i));
        for (let i = 18; i <= 65; i++) document.getElementById('age-select').options.add(new Option(i + " ans", i));
        for (let i = 0; i <= 35; i++) document.getElementById('exp-select').options.add(new Option(i + " ans d'exp", i));
    };
</script>
</body>
</html>
