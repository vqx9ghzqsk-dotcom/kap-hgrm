<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Base de Données Simplifiée</title>
    <style>
        /* --- STYLE --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1); min-height: 800px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; cursor: pointer; font-weight: bold;}
        
        .form-content { padding: 25px; display: none; }
        .form-content.active { display: block; }
        
        .section-title { background: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; border-left: 6px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 5px; color: #333; }
        select, input { padding: 10px; border: 1px solid #ccc; border-radius: 6px; font-size: 14px; width: 100%; }

        table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        
        .btn-save { width: 100%; background: #b03060; color: white; padding: 18px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 20px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 7px; border-radius: 10px; font-size: 10px; margin-left: 4px;}
        
        /* Graphiques simples */
        .stat-card { background: #fff; border: 1px solid #eee; padding: 15px; border-radius: 8px; margin-bottom: 10px;}
        .bar-container { display: flex; align-items: center; margin-bottom: 5px; }
        .bar-label { width: 140px; font-size: 12px; }
        .bar-track { flex-grow: 1; background: #eee; height: 15px; border-radius: 3px; overflow: hidden; margin: 0 10px; }
        .bar-fill { height: 100%; background: #b03060; transition: width 0.3s; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. SAISIE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. BASE DE DONNÉES</button>
        <button class="tab" onclick="switchTab(3)">3. ANALYSE</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION</div>
            <div class="row">
                <div class="field"><label>ID Enquêté</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie</option><option>Maternité</option><option>Chirurgie</option><option>Autre</option></select></div>
                <div class="field"><label>Niveau Étude</label><select id="niveau"><option>A2</option><option selected>A1 (Graduée)</option><option>L0/L1 (Licenciée)</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES ET PRATIQUES</div>
            <div class="row">
                <div class="field">
                    <label>Quand faire l'AES ? (Savoir)</label>
                    <select id="q-savoir-moment">
                        <option value="0">Pendant les règles</option>
                        <option value="1">2 à 7 jours après les règles</option>
                        <option value="0">N'importe quand / Ne sait pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Technique de palpation utilisée (Pratique)</label>
                    <select id="q-pratique-tech">
                        <option value="insatisfaisant">Palpation rapide sans méthode précise</option>
                        <option value="satisfaisant">Méthode systématique (Quadrant par quadrant)</option>
                        <option value="expert">Méthode complète (Quadrant + creux axillaire + mamelon)</option>
                    </select>
                </div>
            </div>

            <div class="section-title">III. ATTITUDE ET ENSEIGNEMENT</div>
            <div class="row">
                <div class="field">
                    <label>Enseignez-vous l'AES aux patientes ?</label>
                    <select id="q-enseignement">
                        <option>Oui, systématiquement</option>
                        <option>Oui, si la patiente est réceptive</option>
                        <option>Rarement / Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>Principal obstacle à la pratique</label>
                    <select id="q-obstacle">
                        <option>Manque de formation</option>
                        <option>Manque de temps / Surcharge</option>
                        <option>Pudeur des patientes</option>
                        <option>Oubli / Pas de protocole</option>
                    </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">LISTE DES ENQUÊTES ENREGISTRÉES</div>
        <table>
            <thead>
                <tr>
                    <th>Code</th>
                    <th>Service</th>
                    <th>Savoir Moment</th>
                    <th>Qualité Technique</th>
                    <th>Enseignement</th>
                </tr>
            </thead>
            <tbody id="db-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">RÉSULTATS STATISTIQUES</div>
        <div class="stat-card">
            <strong>Maîtrise de la Technique de Palpation :</strong>
            <div id="graph-tech" style="margin-top:10px;"></div>
        </div>
        <div class="stat-card">
            <strong>Obstacles Prédominants :</strong>
            <div id="graph-obs" style="margin-top:10px;"></div>
        </div>
        <div id="synthèse-rapide" style="font-style: italic; color: #555; margin-top: 20px;"></div>
    </div>

</div>

<script>
    let database = [];

    // Initialisation ID
    const codeS = document.getElementById('code-enquete');
    for(let i=1; i<=100; i++) { let o=document.createElement('option'); o.value="INF-"+i; o.text="Fiche n°"+i; codeS.appendChild(o); }

    function saveRecord() {
        let rec = {
            id: document.getElementById('code-enquete').value,
            service: document.getElementById('service').value,
            savoir: document.getElementById('q-savoir-moment').value == "1" ? "Correct" : "Incorrect",
            technique: document.getElementById('q-pratique-tech').value,
            enseignement: document.getElementById('q-enseignement').value,
            obstacle: document.getElementById('q-obstacle').value
        };

        database.push(rec);
        document.getElementById('count-badge').textContent = database.length;
        codeS.selectedIndex++; // Passe au suivant
        
        updateDisplay();
        alert("Enregistré !");
    }

    function updateDisplay() {
        // Table
        const tbody = document.getElementById('db-body');
        tbody.innerHTML = '';
        database.forEach(r => {
            tbody.innerHTML += `<tr><td>${r.id}</td><td>${r.service}</td><td>${r.savoir}</td><td>${r.technique}</td><td>${r.enseignement}</td></tr>`;
        });

        // Stats
        let sat = database.filter(r => r.technique !== 'insatisfaisant').length;
        let pct = database.length > 0 ? Math.round((sat/database.length)*100) : 0;
        
        document.getElementById('graph-tech').innerHTML = `
            <div class="bar-container">
                <div class="bar-label">Satisfaisant/Expert :</div>
                <div class="bar-track"><div class="bar-fill" style="width:${pct}%;"></div></div>
                <span>${pct}%</span>
            </div>
        `;

        document.getElementById('synthèse-rapide').innerHTML = `Analyse basée sur ${database.length} fiches.`;
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "ID,Service,Savoir,Technique,Enseignement,Obstacle\n";
        database.forEach(r => csv += `${r.id},${r.service},${r.savoir},${r.technique},${r.enseignement},${r.obstacle}\n`);
        let link = document.createElement("a");
        link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "data_memoire_HGRM.csv";
        link.click();
    }
</script>

</body>
</html>
