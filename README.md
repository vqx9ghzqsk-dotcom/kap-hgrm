<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Étude Prévention Cancer du Sein</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f4f7f6; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1); }
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        .form-content { padding: 25px; display: none; }
        .form-content.active { display: block; }

        .section-title { background: #fff1f6; color: #b03060; padding: 12px; font-weight: bold; border-left: 5px solid #b03060; margin: 20px 0 15px 0; text-transform: uppercase; font-size: 13px; }
        
        .question-block { margin-bottom: 15px; padding: 10px; border-bottom: 1px solid #eee; }
        .question-text { font-weight: 600; font-size: 14px; margin-bottom: 8px; color: #333; }
        
        .options-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 8px; }
        .option-item { display: flex; align-items: center; font-size: 13px; background: #fdfdfd; padding: 8px; border: 1px solid #eee; border-radius: 5px; cursor: pointer; }
        .option-item:hover { background: #f5f5f5; }
        .option-item input { margin-right: 10px; }

        select, input[type="text"] { padding: 10px; border: 1px solid #ccc; border-radius: 4px; width: 100%; box-sizing: border-box; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; }
        .consent-box { background: #e3f2fd; padding: 15px; border-radius: 8px; border: 1px solid #bbdefb; font-size: 13px; line-height: 1.5; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        
        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 15px; margin-top: 10px; font-size: 14px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 6px; border-radius: 10px; font-size: 10px; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. ANALYSE CROISÉE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSIONS</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            
            <div class="section-title">1. Identification de l'Enquête</div>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                <div class="field"><label>Code de la Fiche</label><input type="text" id="code-fiche" placeholder="Ex: INF-001"></div>
                <div class="field"><label>Date de l'entretien</label><input type="text" id="date-entretien" value="12/01/2026"></div>
            </div>

            <div class="section-title">2. Consentement Éclairé</div>
            <div class="consent-box">
                "Je confirme avoir été informée des objectifs de cette étude sur la prévention du cancer du sein à l'HGRM. 
                Je participe volontairement et je sais que mes réponses sont anonymes."
                <div style="margin-top: 10px;">
                    <label><input type="radio" name="consent" value="oui" checked> <b>Oui, je consens</b></label>
                    <label style="margin-left: 20px;"><input type="radio" name="consent" value="non"> Non, je refuse</label>
                </div>
            </div>

            <div class="section-title">3. Données Sociodémographiques</div>
            <div class="options-grid">
                <div class="field"><label>Service</label>
                    <select id="service"><option>Gynéco-Obstétrique</option><option>Maternité</option><option>Chirurgie</option><option>Oncologie</option><option>Médecine Interne</option></select>
                </div>
                <div class="field"><label>Niveau d'étude</label>
                    <select id="niveau"><option>A2 (Diplômée)</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option><option>Master</option></select>
                </div>
                <div class="field"><label>Ancienneté (Années)</label>
                    <select id="anciennete"><option>0-5 ans</option><option>6-10 ans</option><option>+10 ans</option></select>
                </div>
            </div>

            <div class="section-title">4. Connaissances Générales (Prévention)</div>
            
            <div class="question-block">
                <div class="question-text">Q1. Quelle est la fréquence recommandée pour l'auto-examen des seins (AES) ?</div>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="q_aes_freq" value="0"> Chaque semaine</label>
                    <label class="option-item"><input type="radio" name="q_aes_freq" value="1"> Une fois par mois</label>
                    <label class="option-item"><input type="radio" name="q_aes_freq" value="0"> Une fois par an</label>
                </div>
            </div>

            <div class="question-block">
                <div class="question-text">Q2. Quel est le moment idéal pour pratiquer l'AES chez une femme réglée ?</div>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="q_aes_moment" value="0"> Pendant les règles</label>
                    <label class="option-item"><input type="radio" name="q_aes_moment" value="1"> 7 à 10 jours après les règles</label>
                    <label class="option-item"><input type="radio" name="q_aes_moment" value="0"> Avant les règles</label>
                </div>
            </div>

            <div class="question-block">
                <div class="question-text">Q3. La douleur est-elle le premier signe d'alerte d'un cancer du sein débutant ?</div>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="q_douleur" value="0"> Oui</label>
                    <label class="option-item"><input type="radio" name="q_douleur" value="1"> Non (souvent indolore)</label>
                </div>
            </div>

            <div class="question-block">
                <div class="question-text">Q4. Quel est l'examen de référence (Gold Standard) pour le dépistage ?</div>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="q_gold" value="0"> Échographie</label>
                    <label class="option-item"><input type="radio" name="q_gold" value="1"> Mammographie</label>
                    <label class="option-item"><input type="radio" name="q_gold" value="0"> Biopsie</label>
                </div>
            </div>

            <div class="section-title">5. Attitudes vis-à-vis du Dépistage (1-5)</div>
            <p style="font-size: 12px; color: #666;">(1: Pas d'accord, 5: Tout à fait d'accord)</p>
            <table>
                <tr><th style="text-align:left">Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                <tr><td style="text-align:left">Le dépistage précoce peut sauver une vie</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5" checked></td></tr>
                <tr><td style="text-align:left">Je me sens capable d'enseigner l'AES</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4" checked></td><td><input type="radio" name="att2" value="5"></td></tr>
            </table>

            <div class="section-title">6. Pratiques de l'Infirmière</div>
            <div class="question-block">
                <div class="question-text">Pratiquez-vous l'auto-examen sur vous-même ?</div>
                <select id="prac1"><option>Régulièrement</option><option>Rarement</option><option>Jamais</option></select>
            </div>
            <div class="question-block">
                <div class="question-text">Réalisez-vous l'examen clinique des seins (ECS) pour vos patientes ?</div>
                <select id="prac2"><option>Systématiquement</option><option>Si plainte</option><option>Jamais</option></select>
            </div>

            <div class="section-title">7. Obstacles identifiés</div>
            <div class="options-grid">
                <label class="option-item"><input type="checkbox" class="obs" value="Manque_Temps"> Manque de temps</label>
                <label class="option-item"><input type="checkbox" class="obs" value="Pudeur"> Pudeur culturelle</label>
                <label class="option-item"><input type="checkbox" class="obs" value="Formation"> Manque de formation</label>
                <label class="option-item"><input type="checkbox" class="obs" value="Materiel"> Manque de matériel</label>
            </div>

            <div class="section-title">8. Recommandations de l'Infirmière</div>
            <div class="field">
                <label>Quelle action prioritaire proposez-vous pour l'HGRM ?</label>
                <select id="recommandation">
                    <option>Organiser des séances de formation continue</option>
                    <option>Installer un service de mammographie</option>
                    <option>Créer des brochures de sensibilisation</option>
                    <option>Rendre l'examen des seins obligatoire en consultation</option>
                </select>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <table id="table-depouillement">
            <thead>
                <tr><th>ID</th><th>Niveau</th><th>Ancienneté</th><th>Savoir (%)</th><th>Attitude (/5)</th><th>Pratique (%)</th><th>Rec. Prioritaire</th></tr>
            </thead>
            <tbody id="db-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE CROISÉE (SAVOIR vs PRATIQUE)</div>
        <table id="analysis-table">
            <thead><tr><th>Groupe</th><th>Effectif</th><th>Score Pratique Moyen</th></tr></thead>
            <tbody id="analysis-body"></tbody>
        </table>
        <div id="interpretation" class="interpretation-box"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSIONS DE L'ÉTUDE</div>
        <div id="conclusion-text" style="line-height:1.6; font-size:15px;">En attente de données...</div>
    </div>

</div>

<script>
    let database = [];
    const urlCloud = "https://script.google.com/macros/s/AKfycbz-a9ZgcGRrxTDWXLlbuTnsIzUsdj4ZY5FVgTc7pHAMyyOPdrNQY8lT4HxxXngYGTNy/exec";

    function saveRecord() {
        // Collecte des points de savoir (Q1 à Q4)
        let s1 = parseInt(document.querySelector('input[name="q_aes_freq"]:checked')?.value || 0);
        let s2 = parseInt(document.querySelector('input[name="q_aes_moment"]:checked')?.value || 0);
        let s3 = parseInt(document.querySelector('input[name="q_douleur"]:checked')?.value || 0);
        let s4 = parseInt(document.querySelector('input[name="q_gold"]:checked')?.value || 0);
        
        let scoreSavoir = Math.round(((s1 + s2 + s3 + s4) / 4) * 100);

        // Attitude
        let a1 = parseInt(document.querySelector('input[name="att1"]:checked').value);
        let a2 = parseInt(document.querySelector('input[name="att2"]:checked').value);
        let scoreAttitude = ((a1 + a2) / 2).toFixed(1);

        // Pratique
        let p1Val = document.getElementById('prac1').value;
        let p2Val = document.getElementById('prac2').value;
        let scorePratique = (p1Val === "Régulièrement" ? 50 : 10) + (p2Val === "Systématiquement" ? 50 : 10);

        let record = {
            id: document.getElementById('code-fiche').value || "Inconnu",
            service: document.getElementById('service').value,
            niveau: document.getElementById('niveau').value,
            anciennete: document.getElementById('anciennete').value,
            scoreSavoir: scoreSavoir,
            scoreAttitude: scoreAttitude,
            scorePratique: scorePratique,
            recommandation: document.getElementById('recommandation').value,
            obstacles: Array.from(document.querySelectorAll('.obs:checked')).map(c => c.value).join('|')
        };

        database.push(record);
        document.getElementById('count-badge').textContent = database.length;

        // Envoi au Cloud
        fetch(urlCloud, { method: "POST", mode: "no-cors", body: JSON.stringify(record) });

        alert("Fiche enregistrée !");
        updateAll();
        document.getElementById('kapForm').reset();
    }

    function updateAll() {
        // Onglet 2
        document.getElementById('db-body').innerHTML = database.map(r => 
            `<tr><td>${r.id}</td><td>${r.niveau}</td><td>${r.anciennete}</td><td>${r.scoreSavoir}%</td><td>${r.scoreAttitude}</td><td>${r.scorePratique}%</td><td>${r.recommandation}</td></tr>`
        ).join('');

        // Onglet 3
        let highSavoir = database.filter(r => r.scoreSavoir >= 75);
        let lowSavoir = database.filter(r => r.scoreSavoir < 75);
        let avgHigh = highSavoir.length ? (highSavoir.reduce((a,b)=>a+b.scorePratique,0)/highSavoir.length).toFixed(1) : 0;
        let avgLow = lowSavoir.length ? (lowSavoir.reduce((a,b)=>a+b.scorePratique,0)/lowSavoir.length).toFixed(1) : 0;

        document.getElementById('analysis-body').innerHTML = `
            <tr><td>Savoir Satisfaisant (>=75%)</td><td>${highSavoir.length}</td><td>${avgHigh}%</td></tr>
            <tr><td>Savoir Insuffisant (<75%)</td><td>${lowSavoir.length}</td><td>${avgLow}%</td></tr>
        `;

        document.getElementById('interpretation').innerHTML = `L'analyse montre que les infirmières ayant un savoir satisfaisant ont une pratique moyenne de ${avgHigh}%, ce qui souligne l'impact de la connaissance sur l'action clinique.`;

        // Onglet 4
        document.getElementById('conclusion-text').innerHTML = `L'étude porte sur ${database.length} infirmières. La recommandation la plus citée est : <b>${database[database.length-1].recommandation}</b>.`;
    }

    function switchTab(idx) {
        document.querySelectorAll('.form-content').forEach(d => d.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
        document.getElementById('content-'+idx).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${idx})`).classList.add('active');
    }
</script>
</body>
</html>
