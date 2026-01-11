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
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="k1"><option value="1" selected>Vrai (Oui)</option><option value="0">Faux (Non)</option><option value="0">Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>À quel âge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option><option value="0">Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après les règles</option><option value="0">Pendant les règles</option><option value="0">N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus (Cochez les propositions valides) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Nulliparité" checked> Nulliparité (n'avoir jamais accouché)</label>
                <label class="check-item"><input type="checkbox" name="risk" value="GrossesseTardive" checked> Première grossesse tardive (> 30 ans)</label>
                <label class="check-item"><input type="checkbox" name="risk" value="MenopauseTardive" checked> Ménopause tardive (> 55 ans)</label>
                <label class="check-item"><input type="checkbox" name="risk" value="AlcoolTabac" checked> Consommation d'alcool et tabac</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Contraceptifs"> Usage prolongé de contraceptifs oraux</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Familiaux" checked> Antécédents familiaux (Mère, Sœur)</label>
            </div>

            <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte (Signes à rechercher) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="sign" value="Nodule" checked> Nodule dur, fixe et indolore</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Ecoulement" checked> Écoulement séro-sanguinolent unilatéral</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Retraction" checked> Rétraction ou ombilication du mamelon</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Adenopathie" checked> Adénopathie axillaire (boule sous l'aisselle)</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Orange" checked> Aspect de "peau d'orange" sur le tégument</label>
                <label class="check-item"><input type="checkbox" name="sign" value="Douleur"> Douleur mammaire isolée (Mastodynie)</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (SAVOIR-ÊTRE : 1 À 5)</div>
            <table>
                <thead>
                    <tr><th class="text-left">Énoncés (Perception de l'infirmier/e)</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                </thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule suspect lors d'une palpation.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">L'influence culturelle (pudeur) empêche mes patientes de se déshabiller.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Le diagnostic de cancer est une sentence de mort en RDC.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Je pense que chaque femme en consultation doit être sensibilisée au cancer.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence de la palpation clinique des seins (ECS) :</label>
                    <select name="pra1" id="pra1">
                        <option value="1" selected>Systématique pour chaque patiente</option>
                        <option value="0">Uniquement si la patiente se plaint</option>
                        <option value="0">Rarement par manque de temps</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignement de la technique d'autopalpation (AES) :</label>
                    <select name="pra2">
                        <option value="1" selected>Je démontre la technique physiquement</option>
                        <option value="0">J'explique verbalement seulement</option>
                        <option value="0">Je ne l'enseigne pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Référence des cas suspects :</label>
                    <select name="ref">
                        <option selected>Vers l'imagerie (Mammographie/Echo)</option>
                        <option>Vers la Chirurgie directement</option>
                        <option>Observation (Attendre le prochain RDV)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field">
                    <label>Utilisation de supports visuels (Affiches, Boites à images) :</label>
                    <select name="visuel"><option selected>Jamais (Pas de matériel disponible)</option><option>Parfois</option><option>Toujours</option></select>
                </div>
                <div class="field">
                    <label>Avez-vous déjà palpé un sein ce matin ?</label>
                    <select name="ce-matin"><option selected>Oui</option><option>Non</option></select>
                </div>
                <div class="field">
                    <label>Nombre de cas de cancer suspectés ce mois-ci :</label>
                    <select name="nb-cas"><option value="0">0</option><option value="3" selected>1 à 5 cas</option><option value="6">Plus de 5 cas</option></select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES ET SOLUTIONS (RDC CONTEXT)</div>
            <label style="margin-bottom: 10px; display:block; font-weight: bold;">Quelles sont les barrières à l'HGRM ? :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Salle" checked> Absence de salle isolée respectant l'intimité</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Cout" checked> Coût exorbitant de la mammographie (> 50$)</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Formation" checked> Manque de formation continue sur le cancer</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Priere" checked> Préférence des patientes pour la prière/tradition</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Surcharge"> Surcharge de travail</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">DÉPOUILLEMENT COMPLET ET CODAGE DES DONNÉES</div>
        <div style="overflow-x: auto;">
            <table id="tableDepouillement">
                <thead>
                    <tr>
                        <th>Code</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Service</th>
                        <th>Score K</th><th>Niveau K</th><th>Score A</th><th>Niveau A</th><th>Score P</th><th>Niveau P</th>
                        <th>Obstacles (#)</th><th>Consult. (Mois)</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">RÉSULTATS DÉTAILLÉS ET ANALYSE DES COMBINAISONS</div>
        
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Effectif Total (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k-perc">0%</div><div>Connaissances (Bonnes)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-a-perc">0%</div><div>Attitudes (Positives)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p-perc">0%</div><div>Pratiques (Correctes)</div></div>
        </div>

        <div class="analysis-box">
            <label><b>ANALYSE DES ASSOCIATIONS (COMBINAISONS)</b></label>
            <table id="associationTable">
                <thead><tr><th>Combinaison de variables</th><th>Fréquence</th><th>Pourcentage</th></tr></thead>
                <tbody id="associationBody"></tbody>
            </table>
        </div>

        <div class="row">
            <div class="analysis-box">
                <label><b>FRÉQUENCE DES OBSTACLES IDENTIFIÉS</b></label>
                <div id="obstacleStats" style="font-size: 13px; margin-top:10px;"></div>
            </div>
            <div class="analysis-box">
                <label><b>FRÉQUENCE DES CONSULTATIONS (CAS SUSPECTS)</b></label>
                <div id="consultationStats" style="font-size: 13px; margin-top:10px;"></div>
            </div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION GLOBALE ET RECOMMANDATIONS</div>
        <div id="summary" style="line-height:1.8; background:#fff; padding:25px; border:1px solid #ddd; border-radius: 8px;">
            En attente de données pour générer la synthèse...
        </div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "METS_TON_URL_ICI"; 

    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
            alert("Accès autorisé : Mode Expert Activé");
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + (n==1?'1':n==2?'2':n==3?'3':'4')).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 2) actualiserTableau();
        if(n === 3) calculerAnalysesFines();
        if(n === 4) genererConclusion();
    }

    async function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        // CODAGE DES SCORES
        let sk = parseInt(fd.get('k1') || 0) + parseInt(fd.get('k2') || 0) + parseInt(fd.get('k3') || 0);
        let sa = parseInt(fd.get('p1') || 0) + parseInt(fd.get('p2') || 0) + parseInt(fd.get('p3') || 0) + parseInt(fd.get('p4') || 0);
        let sp = parseInt(fd.get('pra1') || 0) + parseInt(fd.get('pra2') || 0);
        let countObs = form.querySelectorAll('input[name="obs"]:checked').length;

        const entry = {
            code: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: fd.get('experience'),
            scoreK: sk, levelK: sk >= 2 ? 'Bon' : 'Faible',
            scoreA: sa, levelA: sa >= 14 ? 'Positif' : 'Négatif',
            scoreP: sp, levelP: sp >= 1 ? 'Correct' : 'Incorrect',
            obstacles: countObs,
            consultations: fd.get('nb-cas'),
            listObs: Array.from(form.querySelectorAll('input[name="obs"]:checked')).map(i => i.value)
        };

        db.push(entry);
        alert("Fiche enregistrée localement et prête pour l'analyse.");
        
        try {
            fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
        } catch (e) { console.log("Erreur d'envoi distant"); }
        
        form.reset();
    }

    function actualiserTableau() {
        const tbody = document.querySelector('#tableDepouillement tbody');
        tbody.innerHTML = db.map(d => `
            <tr>
                <td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.service}</td>
                <td>${d.scoreK}/3</td><td>${d.levelK}</td><td>${d.scoreA}/20</td><td>${d.levelA}</td><td>${d.scoreP}/2</td><td>${d.levelP}</td>
                <td>${d.obstacles}</td><td>${d.consultations}</td>
            </tr>
        `).join('');
    }

    function calculerAnalysesFines() {
        let n = db.length; if(n === 0) return;

        // 1. Pourcentages de base
        let kPos = db.filter(d => d.levelK === 'Bon').length;
        let aPos = db.filter(d => d.levelA === 'Positif').length;
        let pPos = db.filter(d => d.levelP === 'Correct').length;

        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k-perc').innerText = Math.round(kPos/n*100) + "%";
        document.getElementById('res-a-perc').innerText = Math.round(aPos/n*100) + "%";
        document.getElementById('res-p-perc').innerText = Math.round(pPos/n*100) + "%";

        // 2. Associations (Combinaisons)
        const combos = [
            { name: "Savoir Bon + Pratique Correcte", fn: d => d.levelK === 'Bon' && d.levelP === 'Correct' },
            { name: "Savoir Faible + Pratique Incorrecte", fn: d => d.levelK === 'Faible' && d.levelP === 'Incorrect' },
            { name: "Attitude Positive + Pratique Correcte", fn: d => d.levelA === 'Positif' && d.levelP === 'Correct' },
            { name: "Savoir Bon + Attitude Négative", fn: d => d.levelK === 'Bon' && d.levelA === 'Négatif' }
        ];

        document.getElementById('associationBody').innerHTML = combos.map(c => {
            let count = db.filter(c.fn).length;
            return `<tr><td>${c.name}</td><td>${count}</td><td>${Math.round(count/n*100)}%</td></tr>`;
        }).join('');

        // 3. Fréquence des obstacles
        let obsCount = {};
        db.forEach(d => d.listObs.forEach(o => obsCount[o] = (obsCount[o] || 0) + 1));
        document.getElementById('obstacleStats').innerHTML = Object.entries(obsCount)
            .map(([key, val]) => `• ${key}: ${val} (${Math.round(val/n*100)}%)`).join('<br>');

        // 4. Fréquence consultations
        let cas0 = db.filter(d => d.consultations == "0").length;
        let cas15 = db.filter(d => d.consultations == "3").length;
        let casPlus = db.filter(d => d.consultations == "6").length;
        document.getElementById('consultationStats').innerHTML = 
            `0 cas suspect: ${Math.round(cas0/n*100)}%<br>1-5 cas: ${Math.round(cas15/n*100)}%<br>>5 cas: ${Math.round(casPlus/n*100)}%`;
    }

    function genererConclusion() {
        let n = db.length; if(n === 0) return;
        let pPos = db.filter(d => d.levelP === 'Correct').length;
        let kPos = db.filter(d => d.levelK === 'Bon').length;
        let pPerc = Math.round(pPos/n*100);
        let kPerc = Math.round(kPos/n*100);

        let synthese = `<b>SYNTHÈSE DE L'ÉTUDE (HGRM) :</b><br>`;
        synthese += `L'analyse de ${n} infirmières montre que ${kPerc}% possèdent des connaissances théoriques suffisantes, alors que seulement ${pPerc}% appliquent correctement les mesures de prévention.<br><br>`;
        synthese += `<b>CONCLUSION :</b> Il existe une rupture entre le savoir et le faire. Les obstacles structurels (manque de salle isolée et coût des examens) prédominent sur le manque de connaissances.<br><br>`;
        synthese += `<b>RECOMMANDATIONS :</b> Intégrer la palpation mammaire dans les fiches de soins standards et doter l'HGRM de matériel didactique (boîtes à images).`;
        
        document.getElementById('summary').innerHTML = synthese;
    }

    function exportCSV() {
        let csv = "Code,Age,Etude,Savoir,Attitude,Pratique,Consultations\n";
        db.forEach(d => { csv += `${d.code},${d.age},${d.etude},${d.levelK},${d.levelA},${d.levelP},${d.consultations}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a'); a.href = url; a.download = 'Analyse_KAP_Expert.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) cs.options.add(new Option("Enquêté ID: " + i, i));
        const as = document.getElementById('age-select');
        for (let i = 18; i <= 65; i++) as.options.add(new Option(i + " ans", i));
        const es = document.getElementById('exp-select');
        for (let i = 0; i <= 35; i++) es.options.add(new Option(i + " ans d'exp", i));
    };
</script>

</body>
</html>
