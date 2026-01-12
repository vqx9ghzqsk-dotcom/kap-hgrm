<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Étude Scientifique Cancer du Sein</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f0f2f5; margin: 0; padding: 20px; color: #333; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 15px; box-shadow: 0 5px 25px rgba(0,0,0,0.15); min-height: 900px; overflow: hidden; }
        
        /* HEADER & TABS */
        .header-tabs { display: flex; background: #fff; border-bottom: 4px solid #b03060; padding: 0; position: sticky; top: 0; z-index: 100; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .tab { flex: 1; padding: 18px; text-align: center; font-weight: 600; font-size: 13px; color: #666; cursor: pointer; transition: 0.3s; border: none; background: transparent; text-transform: uppercase; letter-spacing: 0.5px; }
        .tab:hover { background: #fff0f5; color: #b03060; }
        .tab.active { background: #b03060; color: white; border-bottom: 4px solid #880e4f; }
        
        /* CONTENT */
        .form-content { padding: 40px; display: none; animation: fadeIn 0.4s ease-out; }
        .form-content.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* TITRES */
        .section-title { background: #fce4ec; color: #880e4f; padding: 12px 20px; font-weight: 700; border-left: 6px solid #b03060; margin: 30px 0 20px 0; border-radius: 0 8px 8px 0; font-size: 15px; display: flex; justify-content: space-between; align-items: center; }

        /* GRILLES */
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 25px; margin-bottom: 20px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 600; margin-bottom: 8px; color: #444; }
        select, input[type="text"] { padding: 12px; border: 1px solid #ccc; border-radius: 6px; font-size: 14px; background: #fff; transition: 0.3s; }
        select:focus { border-color: #b03060; outline: none; box-shadow: 0 0 0 3px rgba(176, 48, 96, 0.1); }

        /* TABLEAUX LIKERT */
        table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 13px; background: #fff; border: 1px solid #eee; }
        th { background: #f8f9fa; padding: 15px; border-bottom: 2px solid #ddd; color: #555; font-weight: 600; }
        td { border-bottom: 1px solid #eee; padding: 12px; text-align: center; }
        .question-text { text-align: left; padding-left: 15px; width: 50%; }

        /* BOUTONS */
        .btn-save { width: 100%; background: linear-gradient(135deg, #b03060 0%, #880e4f 100%); color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; box-shadow: 0 4px 15px rgba(176, 48, 96, 0.3); transition: transform 0.2s; }
        .btn-save:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(176, 48, 96, 0.4); }
        
        .btn-export { background: #2e7d32; color: white; border: none; padding: 10px 20px; border-radius: 4px; cursor: pointer; font-weight: bold; float: right; margin-top: -50px; }

        /* ANALYSE RESULTS */
        .stat-card { background: #fff; border: 1px solid #eee; border-radius: 8px; padding: 20px; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .result-badge { padding: 4px 8px; border-radius: 4px; font-weight: bold; font-size: 12px; }
        .good { background: #e8f5e9; color: #2e7d32; }
        .medium { background: #fff3e0; color: #ef6c00; }
        .bad { background: #ffebee; color: #c62828; }

        .interpretation-box { margin-top: 20px; padding: 20px; background: #e3f2fd; border-left: 5px solid #1976d2; color: #0d47a1; line-height: 1.6; border-radius: 4px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE DES DONNÉES</button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. ANALYSE STATISTIQUE</button>
        <button class="tab" onclick="switchTab(4)">4. INTERPRÉTATION & RAPPORT</button>
    </div>

    <div id="content-1" class="form-content active">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;">
            <h2 style="color:#b03060; margin:0;">Nouvelle Fiche d'Enquête</h2>
            <span style="background:#eee; padding:5px 10px; border-radius:15px; font-size:12px; font-weight:bold;">Total Fiches : <span id="count-badge">0</span></span>
        </div>

        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION SOCIO-PROFESSIONNELLE</div>
            <div class="row">
                <div class="field"><label>Code Fiche</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Maternité</option><option>Gynécologie</option><option>Chirurgie</option><option>Médecine Interne</option><option>Urgences</option></select></div>
                <div class="field"><label>Niveau d'étude</label><select id="niveau"><option value="A2">A2 (Secondaire)</option><option value="A1" selected>A1 (Graduat)</option><option value="L2">L2 (Licence)</option></select></div>
                <div class="field"><label>Années d'expérience</label><select id="experience"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIR) - Prévention & Dépistage</div>
            <div class="row">
                <div class="field">
                    <label>Q1. Quelle est la fréquence recommandée pour l'Auto-Examen des Seins (AES) ?</label>
                    <select id="k1">
                        <option value="0">Une fois par semaine</option>
                        <option value="1">Une fois par mois</option> <option value="0">Une fois par an</option>
                        <option value="0">Ne sait pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Q2. Quel est le moment idéal pour faire l'AES (femme réglée) ?</label>
                    <select id="k2">
                        <option value="0">N'importe quand dans le cycle</option>
                        <option value="0">Pendant les règles</option>
                        <option value="1">7 à 10 jours après le début des règles</option> <option value="0">Juste avant les règles</option>
                    </select>
                </div>
            </div>

            <div class="row">
                <div class="field">
                    <label>Q3. Quel signe clinique N'EST PAS un signe précoce habituel ? (Le piège)</label>
                    <select id="k3">
                        <option value="0">Un nodule dur et fixe</option>
                        <option value="0">Un écoulement mamelonnaire</option>
                        <option value="1">Une douleur vive au sein</option> <option value="0">Une peau d'orange</option>
                    </select>
                </div>
                <div class="field">
                    <label>Q4. À partir de quel âge recommande-t-on la mammographie de dépistage ?</label>
                    <select id="k4">
                        <option value="0">Dès 20 ans</option>
                        <option value="1">À partir de 40-50 ans</option> <option value="0">Uniquement si on sent une boule</option>
                    </select>
                </div>
            </div>

            <div class="row">
                <div class="field">
                    <label>Q5. Lequel est un facteur de risque prouvé ?</label>
                    <select id="k5">
                        <option value="1">Avoir une mère ou sœur ayant eu le cancer</option> <option value="0">Porter des soutiens-gorge à armature</option> <option value="0">Recevoir un coup sur le sein</option> <option value="0">L'utilisation de déodorants</option> </select>
                </div>
            </div>

            <div class="section-title">III. ATTITUDES (Perceptions et Croyances)</div>
            <p style="font-size:12px; color:#666; margin-bottom:10px;">Échelle : 1 (Pas du tout d'accord) à 5 (Tout à fait d'accord)</p>
            <table>
                <thead><tr><th class="question-text">Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr>
                        <td class="question-text">A1. Je me sens capable d'enseigner l'AES à mes patientes.</td>
                        <td><input type="radio" name="a1" value="1"></td><td><input type="radio" name="a1" value="2"></td><td><input type="radio" name="a1" value="3"></td><td><input type="radio" name="a1" value="4"></td><td><input type="radio" name="a1" value="5" checked></td>
                    </tr>
                    <tr>
                        <td class="question-text">A2. L'éducation sur le cancer du sein fait partie de mon rôle.</td>
                        <td><input type="radio" name="a2" value="1"></td><td><input type="radio" name="a2" value="2"></td><td><input type="radio" name="a2" value="3"></td><td><input type="radio" name="a2" value="4"></td><td><input type="radio" name="a2" value="5" checked></td>
                    </tr>
                    <tr>
                        <td class="question-text">A3. Le cancer du sein est une fatalité, c'est la mort assurée.</td>
                        <td><input type="radio" name="a3" value="5" checked></td><td><input type="radio" name="a3" value="4"></td><td><input type="radio" name="a3" value="3"></td><td><input type="radio" name="a3" value="2"></td><td><input type="radio" name="a3" value="1"></td>
                    </tr>
                    <tr>
                        <td class="question-text">A4. Je suis à l'aise pour examiner les seins d'une patiente (Pudeur).</td>
                        <td><input type="radio" name="a4" value="1"></td><td><input type="radio" name="a4" value="2"></td><td><input type="radio" name="a4" value="3"></td><td><input type="radio" name="a4" value="4"></td><td><input type="radio" name="a4" value="5" checked></td>
                    </tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (Technique et Action)</div>
            <div class="row">
                <div class="field">
                    <label>P1. Pratiquez-vous l'AES sur vous-même ?</label>
                    <select id="p1">
                        <option value="0">Jamais</option>
                        <option value="5">Rarement</option>
                        <option value="10">Chaque mois (Régulièrement)</option> </select>
                </div>
                <div class="field">
                    <label>P2. Quelle partie de la main utilisez-vous pour palper ? (Technique)</label>
                    <select id="p2">
                        <option value="0">Le bout des doigts (pointes)</option>
                        <option value="0">La paume de la main</option>
                        <option value="10">La pulpe des 3 doigts du milieu</option> <option value="0">Je pince le sein</option>
                    </select>
                </div>
                <div class="field">
                    <label>P3. Éduquez-vous les patientes sur le cancer du sein ?</label>
                    <select id="p3">
                        <option value="0">Non, jamais</option>
                        <option value="5">Seulement si elles demandent</option>
                        <option value="10">Oui, systématiquement</option> </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER L'ENQUÊTE ET CALCULER LES SCORES</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <button class="btn-export" onclick="exportCSV()">📥 Exporter CSV</button>
        <div class="section-title">MATRICE DE DONNÉES BRUTES</div>
        <table style="font-size:12px;">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Niveau</th>
                    <th>Score Savoir /5</th>
                    <th>Score Attitude /20</th>
                    <th>Score Pratique /30</th>
                    <th>Interprétation</th>
                </tr>
            </thead>
            <tbody id="table-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">RÉSULTATS DE L'ÉTUDE</div>
        
        <div class="stat-card">
            <h3>1. Niveau de Connaissances (Savoir)</h3>
            <p>Capacité à identifier les risques et normes de dépistage.</p>
            <div id="stats-savoir" style="font-weight:bold; color:#b03060;">En attente de données...</div>
        </div>

        <div class="stat-card">
            <h3>2. Corrélation Savoir vs Pratique</h3>
            <p>Est-ce que mieux connaître la maladie pousse à mieux agir ?</p>
            <table class="cross-table">
                <thead>
                    <tr>
                        <th>Groupe</th>
                        <th>Pratique Moyenne (%)</th>
                    </tr>
                </thead>
                <tbody id="cross-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">RAPPORT D'INTERPRÉTATION AUTOMATIQUE</div>
        <div id="final-report" class="interpretation-box">
            Veuillez saisir des données pour générer le rapport scientifique.
        </div>
    </div>

</div>

<script>
    // --- 1. INITIALISATION ---
    let database = [];

    // Remplir les listes déroulantes dynamiquement
    const codeSelect = document.getElementById('code-enquete');
    for(let i=1; i<=200; i++) { let opt=document.createElement('option'); opt.value="N-"+i; opt.text="Infirmière "+i; codeSelect.appendChild(opt); }
    const expSelect = document.getElementById('experience');
    for(let i=0; i<=40; i++) { let opt=document.createElement('option'); opt.value=i; opt.text=i+" ans"; expSelect.appendChild(opt); }

    // --- 2. FONCTION DE SAUVEGARDE ET SCORING ---
    function saveRecord() {
        // A. Récupération des valeurs
        let k1 = parseInt(document.getElementById('k1').value);
        let k2 = parseInt(document.getElementById('k2').value);
        let k3 = parseInt(document.getElementById('k3').value);
        let k4 = parseInt(document.getElementById('k4').value);
        let k5 = parseInt(document.getElementById('k5').value);

        // Attitude (Notez que A3 est inversé dans le HTML : value=5 pour "Pas du tout d'accord")
        let a1 = parseInt(document.querySelector('input[name="a1"]:checked').value);
        let a2 = parseInt(document.querySelector('input[name="a2"]:checked').value);
        let a3 = parseInt(document.querySelector('input[name="a3"]:checked').value); // Déjà inversé dans le HTML value
        let a4 = parseInt(document.querySelector('input[name="a4"]:checked').value);

        // Pratique
        let p1 = parseInt(document.getElementById('p1').value);
        let p2 = parseInt(document.getElementById('p2').value);
        let p3 = parseInt(document.getElementById('p3').value);

        // B. Calcul des Scores
        let scoreSavoir = k1 + k2 + k3 + k4 + k5; // Max 5 points
        let scoreSavoirPct = (scoreSavoir / 5) * 100;

        let scoreAttitude = a1 + a2 + a3 + a4; // Max 20 points
        let scoreAttitudePct = (scoreAttitude / 20) * 100;

        let scorePratique = p1 + p2 + p3; // Max 30 points
        let scorePratiquePct = (scorePratique / 30) * 100;

        // C. Création de l'objet Enquête
        let record = {
            id: document.getElementById('code-enquete').value,
            niveau: document.getElementById('niveau').value,
            savoir: scoreSavoirPct,
            attitude: scoreAttitudePct,
            pratique: scorePratiquePct
        };

        // D. Sauvegarde
        database.push(record);
        document.getElementById('count-badge').textContent = database.length;
        
        // E. Feedback et Reset
        alert(`✅ Fiche enregistrée !\n\nSavoir : ${scoreSavoirPct}%\nAttitude : ${scoreAttitudePct}%\nPratique : ${scorePratiquePct}%`);
        updateAnalysis();
        
        // Passer à la fiche suivante
        codeSelect.selectedIndex += 1;
        window.scrollTo(0,0);
    }

    // --- 3. ANALYSE ET AFFICHAGE ---
    function updateAnalysis() {
        const tbody = document.getElementById('table-body');
        tbody.innerHTML = '';
        
        let sumSavoir = 0;
        let sumPratique = 0;

        // Génération Tableau Dépouillement
        database.forEach(r => {
            sumSavoir += r.savoir;
            sumPratique += r.pratique;

            let badgeClass = r.savoir >= 70 ? 'good' : (r.savoir >= 50 ? 'medium' : 'bad');
            let badgeText = r.savoir >= 70 ? 'Bon' : (r.savoir >= 50 ? 'Moyen' : 'Insuffisant');

            tbody.innerHTML += `
                <tr>
                    <td>${r.id}</td>
                    <td>${r.niveau}</td>
                    <td>${(r.savoir/20).toFixed(1)}/5 (${r.savoir}%)</td>
                    <td>${(r.attitude/5).toFixed(1)}/20</td>
                    <td>${r.pratique}%</td>
                    <td><span class="result-badge ${badgeClass}">${badgeText}</span></td>
                </tr>
            `;
        });

        // Analyse Croisée
        let highKnow = database.filter(r => r.savoir >= 60); // Seuil de "Bon savoir" fixé à 60% pour l'exercice
        let lowKnow = database.filter(r => r.savoir < 60);

        let avgPracHigh = highKnow.length ? (highKnow.reduce((s,c)=>s+c.pratique,0)/highKnow.length).toFixed(1) : 0;
        let avgPracLow = lowKnow.length ? (lowKnow.reduce((s,c)=>s+c.pratique,0)/lowKnow.length).toFixed(1) : 0;

        document.getElementById('stats-savoir').innerHTML = `Moyenne globale du savoir : ${(sumSavoir/database.length).toFixed(1)}%`;

        document.getElementById('cross-body').innerHTML = `
            <tr><td>Infirmières avec <b>Bonnes Connaissances</b> (Savoir ≥ 60%)</td><td style="color:green; font-weight:bold;">${avgPracHigh}%</td></tr>
            <tr><td>Infirmières avec <b>Connaissances Faibles</b> (Savoir < 60%)</td><td style="color:red; font-weight:bold;">${avgPracLow}%</td></tr>
        `;

        // Interprétation
        let conclusion = `<h3>Synthèse pour ${database.length} enquêtées</h3>`;
        conclusion += `<p>Le niveau de connaissance moyen est de <strong>${(sumSavoir/database.length).toFixed(1)}%</strong>.</p>`;
        
        if(avgPracHigh > avgPracLow + 15) {
            conclusion += `<p>✅ <strong>Hypothèse validée :</strong> On observe clairement que les infirmières qui connaissent les normes de dépistage (moment de l'AES, âge mammographie) ont une pratique beaucoup plus rigoureuse (${avgPracHigh}%) que celles qui ne savent pas (${avgPracLow}%).</p>`;
        } else {
            conclusion += `<p>⚠️ <strong>Constat alarmant :</strong> Même les infirmières qui ont les connaissances théoriques peinent à les mettre en pratique (Score pratique moyen : ${avgPracHigh}%). Cela suggère des barrières autres que le manque de savoir (manque de temps, manque de matériel ou manque de motivation).</p>`;
        }

        document.getElementById('final-report').innerHTML = conclusion;
    }

    // --- UTILS ---
    function switchTab(id) {
        document.querySelectorAll('.form-content').forEach(d => d.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+id).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${id})`).classList.add('active');
    }

    function exportCSV() {
        let csv = "ID,Niveau,Savoir_Pct,Attitude_Pct,Pratique_Pct\n";
        database.forEach(r => csv += `${r.id},${r.niveau},${r.savoir},${r.attitude},${r.pratique}\n`);
        let link = document.createElement('a');
        link.href = 'data:text/csv;charset=utf-8,' + encodeURI(csv);
        link.download = 'Resultats_KAP.csv';
        link.click();
    }
</script>

</body>
</html>
