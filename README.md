<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Étude Transversale Cancer du Sein</title>
    <style>
        /* --- DESIGN & SYSTÈME DE GRILLE --- */
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f7f6; margin: 0; padding: 20px; color: #333; }
        .container { max-width: 1250px; margin: auto; background: #fff; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); overflow: hidden; }
        
        .header-tabs { display: flex; background: #fff; border-bottom: 4px solid #b03060; padding: 15px; gap: 10px; position: sticky; top: 0; z-index: 1000; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .tab { padding: 12px 20px; font-weight: bold; border-radius: 8px; border: 1px solid #ddd; background: #f9f9f9; cursor: pointer; transition: 0.3s; font-size: 13px; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .tab:hover:not(.active) { background: #fce4ec; }

        .form-content { padding: 40px; display: none; }
        .form-content.active { display: block; animation: slideUp 0.4s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: 800; border-left: 10px solid #b03060; margin: 35px 0 20px 0; text-transform: uppercase; letter-spacing: 1px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; margin-bottom: 20px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 8px; color: #444; }
        select, input { padding: 12px; border: 2px solid #eee; border-radius: 8px; font-size: 14px; outline: none; transition: 0.2s; }
        select:focus { border-color: #b03060; }

        /* --- TABLEAUX & SCORING --- */
        table { width: 100%; border-collapse: collapse; margin: 25px 0; border-radius: 8px; overflow: hidden; }
        th { background: #f8f9fa; padding: 15px; border: 1px solid #eee; font-size: 13px; }
        td { border: 1px solid #f1f1f1; padding: 15px; text-align: center; }
        .text-left { text-align: left; font-weight: 600; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 12px; background: #fafafa; padding: 25px; border-radius: 12px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 8px; border-radius: 5px; transition: 0.2s; }
        .check-item:hover { background: #fff; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .check-item input { margin-right: 15px; width: 18px; height: 18px; accent-color: #b03060; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 10px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; box-shadow: 0 5px 15px rgba(176, 48, 96, 0.3); }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }

        /* --- ANALYSE TRANSVERSALE --- */
        .stat-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; }
        .stat-card { background: #fff; border: 1px solid #eee; border-radius: 12px; padding: 20px; }
        .bar-container { margin-bottom: 15px; }
        .bar-label { font-size: 12px; font-weight: 600; margin-bottom: 5px; display: flex; justify-content: space-between; }
        .bar-track { background: #eee; height: 12px; border-radius: 10px; overflow: hidden; }
        .bar-fill { height: 100%; background: #b03060; transition: width 0.8s ease-in-out; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">📝 1. COLLECTE (STUDY DATA)</button>
        <button class="tab" onclick="switchTab(2)">📊 2. MATRICE TRANSVERSALE</button>
        <button class="tab" onclick="switchTab(3)">📈 3. ANALYSE STATISTIQUE</button>
        <button class="tab" onclick="switchTab(4)">🏁 4. CONCLUSIONS & RECOMMANDATIONS</button>
    </div>

    <div id="content-1" class="form-content active">
        <div style="background: #fff3e0; border-left: 5px solid #ff9800; padding: 15px; margin-bottom: 25px;">
            <strong>Méthodologie :</strong> Étude transversale descriptive et analytique menée à l'HGRM Makala.
        </div>

        <form id="kapForm">
            <div class="section-title">I. CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="row">
                <div class="field"><label>ID Participant</label><input type="text" id="part-id" placeholder="Ex: INF-01"></div>
                <div class="field"><label>Tranche d'Âge</label>
                    <select id="age-cat">
                        <option>20-30 ans</option>
                        <option>31-40 ans</option>
                        <option>41-50 ans</option>
                        <option>+50 ans</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté</label>
                    <select id="exp-cat">
                        <option>< 5 ans</option>
                        <option>5-10 ans</option>
                        <option>> 10 ans</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE DÉPISTAGE (SAVOIR)</div>
            <div class="row">
                <div class="field"><label>Signe le plus précoce ?</label>
                    <select id="k1"><option>Douleur</option><option selected>Nodule indolore</option><option>Écoulement</option></select>
                </div>
                <div class="field"><label>Périodicité de l'AES ?</label>
                    <select id="k2"><option>Chaque jour</option><option selected>Une fois par mois</option><option>Une fois par an</option></select>
                </div>
            </div>

            <label style="display:block; margin:20px 0 10px 0; font-weight:bold;">Techniques de Palpation (Savoir théorique) :</label>
            <div class="check-group" id="savoir-tech">
                <label class="check-item"><input type="checkbox" value="1"> Utiliser la pulpe des 3 doigts du milieu</label>
                <label class="check-item"><input type="checkbox" value="1"> Palper tout le sein (cadran par cadran)</label>
                <label class="check-item"><input type="checkbox" value="1"> Vérifier le creux de l'aisselle (ganglions)</label>
                <label class="check-item"><input type="checkbox" value="1"> Presser le mamelon (recherche d'écoulement)</label>
                <label class="check-item"><input type="checkbox" value="1"> Faire l'examen devant un miroir (inspection)</label>
            </div>

            <div class="section-title">III. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field"><label>Réalisez-vous la palpation clinique ?</label>
                    <select id="p1">
                        <option value="2">Systématiquement</option>
                        <option value="1">Parfois</option>
                        <option value="0">Jamais</option>
                    </select>
                </div>
                <div class="field"><label>Éduquez-vous les patientes à l'AES ?</label>
                    <select id="p2">
                        <option value="2">Oui, démonstration pratique</option>
                        <option value="1">Oui, explication verbale</option>
                        <option value="0">Non, jamais</option>
                    </select>
                </div>
            </div>

            <div class="section-title">IV. OBSTACLES (ÉVALUATION TRANSVERSALE)</div>
            <div class="check-group" id="obstacles">
                <label class="check-item"><input type="checkbox" value="Charge de travail"> Surcharge de travail</label>
                <label class="check-item"><input type="checkbox" value="Formation"> Manque de formation spécifique</label>
                <label class="check-item"><input type="checkbox" value="Pudeur"> Pudeur des patientes</label>
                <label class="check-item"><input type="checkbox" value="Matériel"> Manque de brochures/matériel éducatif</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER L'OBSERVATION</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT (N = <span id="n-total">0</span>)</div>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Âge</th>
                    <th>Exp.</th>
                    <th>Score Savoir (%)</th>
                    <th>Score Pratique (%)</th>
                    <th>Qualité</th>
                </tr>
            </thead>
            <tbody id="db-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">RÉSULTATS STATISTIQUES</div>
        <div class="stat-grid">
            <div class="stat-card">
                <h4>Niveau de Connaissance (Moyenne)</h4>
                <div id="chart-knowledge"></div>
            </div>
            <div class="stat-card">
                <h4>Adéquation de la Pratique</h4>
                <div id="chart-practice"></div>
            </div>
        </div>

        <div class="section-title">ANALYSE CROISÉE (ASSOCIATIONS)</div>
        <p>Association entre l'ancienneté et la maîtrise technique :</p>
        <table style="background: #fff; border: 1px solid #ddd;">
            <thead style="background:#333; color:#white;">
                <tr><th>Ancienneté</th><th>Savoir Moyen</th><th>Pratique Moyenne</th></tr>
            </thead>
            <tbody id="cross-table"></tbody>
        </table>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSION DE L'ÉTUDE</div>
        <div id="final-report" style="line-height: 1.8; font-size: 16px; color: #444;">
            Veuillez saisir des données pour générer le rapport final...
        </div>
        <button class="btn-save" style="background:#2e7d32;" onclick="exportData()">📥 EXPORTER LES DONNÉES POUR EXCEL</button>
    </div>
</div>

<script>
    let dataset = [];

    function saveRecord() {
        const techCheck = document.querySelectorAll('#savoir-tech input:checked').length;
        const obstCheck = Array.from(document.querySelectorAll('#obstacles input:checked')).map(c => c.value);

        let data = {
            id: document.getElementById('part-id').value || "N/A",
            age: document.getElementById('age-cat').value,
            exp: document.getElementById('exp-cat').value,
            savoirScore: Math.round(((techCheck + (document.getElementById('k1').value === 'Nodule indolore' ? 1 : 0) + (document.getElementById('k2').value === 'Une fois par mois' ? 1 : 0)) / 7) * 100),
            pratiqueScore: Math.round(((parseInt(document.getElementById('p1').value) + parseInt(document.getElementById('p2').value)) / 4) * 100),
            obstacles: obstCheck
        };

        dataset.push(data);
        document.getElementById('n-total').innerText = dataset.length;
        alert("Enquête enregistrée !");
        updateAnalysis();
        document.getElementById('kapForm').reset();
    }

    function updateAnalysis() {
        // Matrice
        const body = document.getElementById('db-body');
        body.innerHTML = '';
        dataset.forEach(d => {
            body.innerHTML += `<tr><td>${d.id}</td><td>${d.age}</td><td>${d.exp}</td><td>${d.savoirScore}%</td><td>${d.pratiqueScore}%</td><td>${d.pratiqueScore > 50 ? '🟢 Adéquat' : '🔴 Insuffisant'}</td></tr>`;
        });

        // Graphiques
        renderBar('chart-knowledge', getAvg('savoirScore'), "Savoir Global");
        renderBar('chart-practice', getAvg('pratiqueScore'), "Pratique Globale");

        // Analyse Croisée (Simplifiée)
        const categories = ["< 5 ans", "5-10 ans", "> 10 ans"];
        const crossBody = document.getElementById('cross-table');
        crossBody.innerHTML = '';
        categories.forEach(cat => {
            let filtered = dataset.filter(d => d.exp === cat);
            let sAvg = filtered.length ? (filtered.reduce((a,b) => a + b.savoirScore, 0) / filtered.length).toFixed(1) : 0;
            let pAvg = filtered.length ? (filtered.reduce((a,b) => a + b.pratiqueScore, 0) / filtered.length).toFixed(1) : 0;
            crossBody.innerHTML += `<tr><td>${cat}</td><td>${sAvg}%</td><td>${pAvg}%</td></tr>`;
        });

        // Rapport Final
        document.getElementById('final-report').innerHTML = `
            <p>L'étude transversale réalisée auprès de <b>${dataset.length} infirmières</b> à l'HGRM Makala révèle un niveau de connaissance moyen de <b>${getAvg('savoirScore')}%</b>.</p>
            <p>La pratique clinique de la palpation reste <b>${getAvg('pratiqueScore') < 50 ? 'alarmante' : 'modérée'}</b>. Les obstacles majeurs identifiés sont la formation et la charge de travail.</p>
            <p><i>Recommandation :</i> Organiser des ateliers de simulation sur mannequins pour standardiser la technique de palpation en 5 étapes.</p>
        `;
    }

    function getAvg(prop) {
        if(!dataset.length) return 0;
        return Math.round(dataset.reduce((a,b) => a + b[prop], 0) / dataset.length);
    }

    function renderBar(id, val, label) {
        document.getElementById(id).innerHTML = `
            <div class="bar-container">
                <div class="bar-label"><span>${label}</span> <span>${val}%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:${val}%"></div></div>
            </div>
        `;
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(e => e.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }

    function exportData() {
        let csv = "ID,Age,Experience,Savoir,Pratique,Obstacles\n";
        dataset.forEach(d => { csv += `${d.id},${d.age},${d.exp},${d.savoirScore},${d.pratiqueScore},${d.obstacles.join('|')}\n`; });
        let blob = new Blob([csv], { type: 'text/csv' });
        let url = window.URL.createObjectURL(blob);
        let a = document.createElement('a');
        a.href = url; a.download = 'Resultats_Etude_Makala.csv'; a.click();
    }
</script>
</body>
</html>
