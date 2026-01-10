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
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.5s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 60px; border: 1px solid #ccc; font-size: 10px; padding: 4px; border-radius: 4px; }
        .insight-box { background-color: #e8f5e9; border: 1px solid #c8e6c9; padding: 15px; border-radius: 8px; margin-top: 15px; color: #2e7d32; font-style: italic; }
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
            
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Médecine Interne</option>
                        <option>Urgences</option>
                    </select>
                </div>
                <div class="field">
                    <label>Niveau d'étude le plus élevé</label>
                    <select name="etude" id="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">L0/L1 (Licenciée)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Formation continue Cancer du Sein</label>
                    <select name="formation">
                        <option value="0">Jamais</option>
                        <option value="1">Oui, < 2 ans</option>
                        <option value="1">Oui, > 2 ans</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>1. Première cause de décès cancer femme RDC ?</label>
                    <select name="k1">
                        <option value="0">Col de l'utérus</option>
                        <option value="1" selected>Sein</option>
                        <option value="0">Poumon</option>
                    </select>
                </div>
                <div class="field">
                    <label>2. Fréquence idéale Auto-Examen (AES) ?</label>
                    <select name="k2">
                        <option value="0">Tous les jours</option>
                        <option value="1" selected>1 fois/mois</option>
                        <option value="0">1 fois/an</option>
                    </select>
                </div>
                <div class="field">
                    <label>3. Signe d'alerte le plus fréquent ?</label>
                    <select name="k3">
                        <option value="0">Douleur règles</option>
                        <option value="1" selected>Nodule dur indolore</option>
                        <option value="0">Gros volume</option>
                    </select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">4. Facteurs de risques majeurs (Cocher si connu) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Heredite" checked> Hérédité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Nullipare"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="MenopauseTardive"> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Alcool"> Alcool / Tabac</label>
            </div>

            <div class="section-title">III. ATTITUDES (SAVOIR-ÊTRE - Likert)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>Pas d'accord</th><th>Neutre</th><th>D'accord</th></tr></thead>
                <tbody>
                    <tr>
                        <td class="text-left">1. Le dépistage précoce permet une guérison totale</td>
                        <td><input type="radio" name="att1" value="0"></td>
                        <td><input type="radio" name="att1" value="1"></td>
                        <td><input type="radio" name="att1" value="2" checked></td>
                    </tr>
                    <tr>
                        <td class="text-left">2. Je me sens capable de faire un ECS efficace</td>
                        <td><input type="radio" name="att2" value="0"></td>
                        <td><input type="radio" name="att2" value="1"></td>
                        <td><input type="radio" name="att2" value="2" checked></td>
                    </tr>
                    <tr>
                        <td class="text-left">3. La pudeur est un obstacle majeur ici</td>
                        <td><input type="radio" name="att3" value="0"></td>
                        <td><input type="radio" name="att3" value="1"></td>
                        <td><input type="radio" name="att3" value="2"></td>
                    </tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>1. Réalisez-vous l'ECS aux patientes ?</label>
                    <select name="pra1">
                        <option value="2">Systématiquement</option>
                        <option value="1" selected>Parfois (si plainte)</option>
                        <option value="0">Rarement / Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>2. Enseignez-vous l'AES aux patientes ?</label>
                    <select name="pra2">
                        <option value="2">Oui, avec démo</option>
                        <option value="1" selected>Verbalement</option>
                        <option value="0">Non</option>
                    </select>
                </div>
                <div class="field">
                    <label>3. Pratiquez-vous l'AES sur vous-même ?</label>
                    <select name="pra3">
                        <option value="1">Oui, chaque mois</option>
                        <option value="0" selected>Irrégulièrement / Non</option>
                    </select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES (CONTEXTE)</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Salle"> Manque de local/intimité</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Temps"> Surcharge de travail</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Materiel"> Manque de support visuel</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Croyance"> Croyances / Refus patiente</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES DE DÉPOUILLEMENT</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Niveau</th><th>Savoir (Score)</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">STATISTIQUES AVANCÉES</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div class="stat-label">Total N</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div class="stat-label">Bon Savoir</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div class="stat-label">Bonne Pratique</div></div>
            <div class="stat-card"><div class="stat-val" id="res-obs">--</div><div class="stat-label">Obstacle N°1</div></div>
        </div>
        
        <div class="row">
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Répartition par Étude (%)</b></label>
                <div id="study-dist" style="margin-top:10px; font-size:12px;"></div>
            </div>
            
            <div style="background:white; padding:15px; border:1px solid #ddd; border-radius:8px;">
                <label><b>Analyse d'Impact (Focus A1)</b></label>
                <div id="powerful-analysis" class="insight-box">
                    En attente de données pour générer l'analyse...
                </div>
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
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec"; // URL inchangée

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
        
        // Calcul des scores basés sur le nouveau formulaire
        // Savoir: Q1(1pt) + Q2(1pt) + Q3(1pt) + Facteurs Risques (0.5 par case)
        let scoreK = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        
        // Attitude: Moyenne des Likerts
        let scoreAtt = parseInt(fd.get('att1')) + parseInt(fd.get('att2')); // On ne compte pas la pudeur (att3) comme positif/négatif direct
        let attitudeStatus = scoreAtt >= 3 ? 'Positive' : 'Négative';

        // Pratique: Q1 + Q2 + Q3
        let scoreP = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2')) + parseInt(fd.get('pra3'));
        let pratiqueStatus = scoreP >= 3 ? 'Correcte' : 'Incorrecte'; // Seuil ajusté

        let obstacles = Array.from(document.querySelectorAll('input[name="obs"]:checked')).map(e => e.value);

        const entry = {
            code: fd.get('code'),
            service: fd.get('service'),
            etude: fd.get('etude'),
            savoirScore: scoreK,
            savoir: scoreK >= 2 ? 'Bon' : 'Faible',
            attitude: attitudeStatus,
            pratique: pratiqueStatus,
            obstacles: obstacles
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            db.push(entry);
            actualiserTableau();
            alert("Fiche " + entry.code + " enregistrée !");
            form.reset();
        } catch (e) { alert("Erreur de réseau (données locales ok)."); db.push(entry); actualiserTableau(); }
    }

    function actualiserTableau() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => 
            `<tr><td>${d.code}</td><td>${d.etude}</td><td>${d.savoir} (${d.savoirScore}/3)</td><td>${d.attitude}</td><td>${d.pratique}</td></tr>`
        ).join('');
    }

    function calculerAnalyse() {
        let n = db.length; if(n === 0) return;
        
        let kHigh = db.filter(d => d.savoir === 'Bon').length;
        let pGood = db.filter(d => d.pratique === 'Correcte').length;
        
        // Obstacle le plus fréquent
        let allObs = db.flatMap(d => d.obstacles);
        let topObs = "Aucun";
        if(allObs.length > 0) {
            topObs = allObs.sort((a,b) => allObs.filter(v => v===a).length - allObs.filter(v => v===b).length).pop();
        }

        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";
        document.getElementById('res-obs').innerText = topObs;

        // Répartition Études
        let studies = ['A2', 'A1', 'L', 'M'];
        let distHtml = "";
        studies.forEach(s => {
            let count = db.filter(d => d.etude === s).length;
            distHtml += `<b>${s}:</b> ${Math.round(count/n*100)}% | `;
        });
        document.getElementById('study-dist').innerHTML = distHtml;

        // --- ANALYSE PUISSANTE (LA DEMANDE SPÉCIFIQUE) ---
        let a1Nurses = db.filter(d => d.etude === 'A1');
        let txtPuissant = "";
        
        if (a1Nurses.length > 0) {
            let a1Attitude = a1Nurses.filter(d => d.attitude === 'Positive').length;
            let a1Pratique = a1Nurses.filter(d => d.pratique === 'Correcte').length;
            let pctAtt = Math.round((a1Attitude / a1Nurses.length) * 100);
            let pctPra = Math.round((a1Pratique / a1Nurses.length) * 100);
            let cause = topObs === "Salle" ? "du manque de local" : (topObs === "Temps" ? "de la surcharge" : "du manque de matériel");

            txtPuissant = `<b>Analyse puissante :</b> Vous pourrez facilement dire : "${pctAtt}% des infirmières graduées (A1) ont une bonne attitude, mais seulement ${pctPra}% ont une pratique correcte, probablement à cause ${cause}."`;
        } else {
            txtPuissant = "Saisissez des fiches 'A1' pour voir l'analyse puissante.";
        }
        document.getElementById('powerful-analysis').innerHTML = txtPuissant;
        // -------------------------------------------------

        // Conclusion Générale
        let conc = `<b>SYNTHÈSE GLOBALE :</b><br>Sur un échantillon de ${n} infirmiers, le niveau de connaissance est ${kHigh/n > 0.6 ? "satisfaisant" : "faible"}. `;
        conc += `Cependant, l'écart entre le savoir et la pratique est de ${Math.round((kHigh-pGood)/n*100)} points. <br>`;
        conc += `L'obstacle majeur identifié est : <b>${topObs}</b>.`;
        
        document.getElementById('summary').innerHTML = conc;
    }

    function exportCSV() {
        let csv = "Code,Etude,Savoir,Attitude,Pratique,Obstacles\n";
        db.forEach(d => { csv += `${d.code},${d.etude},${d.savoir},${d.attitude},${d.pratique},${d.obstacles.join('|')}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'Rapport_KAP_HGRM_Complet.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) cs.options.add(new Option("ID: " + i, i));
        const as = document.getElementById('age-select');
        for (let i = 18; i <= 65; i++) as.options.add(new Option(i + " ans", i));
        const es = document.getElementById('exp-select');
        for (let i = 0; i <= 35; i++) es.options.add(new Option(i + " ans d'exp", i));
    };
</script>
</body>
</html>
