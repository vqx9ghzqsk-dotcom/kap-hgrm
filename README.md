<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Analyse Expert & Techniques de Palpation</title>
    <style>
        /* --- STYLE EXISTANT --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; width: 100%; box-sizing: border-box; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #f9f9f9; padding: 15px; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { width: auto; margin-right: 10px; transform: scale(1.2); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 150px; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; color: white; display: flex; align-items: center; justify-content: center; font-size: 10px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. MATRICE DE DONNÉES</button>
        <button class="tab" onclick="switchTab(3)">3. ANALYSE STATISTIQUE</button>
        <button class="tab" onclick="switchTab(4)">4. SYNTHÈSE</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. PROFIL DE L'INFIRMIER(E)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie</option><option>Maternité</option><option>Chirurgie</option><option>Médecine</option></select></div>
                <div class="field"><label>Ancienneté</label><select id="exp-select"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES THÉORIQUES & TECHNIQUES</div>
            <div class="row">
                <div class="field"><label>Moment idéal pour l'AES ?</label><select id="q-moment"><option>Pendant les règles</option><option selected>2 à 7 jours après les règles</option><option>N'importe quand</option></select></div>
                <div class="field"><label>Position pour l'inspection ?</label><select id="q-position"><option>Assise uniquement</option><option selected>Devant un miroir (bras levés/baissés)</option><option>Couchée sur le côté</option></select></div>
            </div>

            <label style="display:block; margin:15px 0 10px 0; font-weight:bold; color:#b03060;">Maîtrise de la technique de palpation (Cochez les étapes connues) :</label>
            <div class="check-group" id="group-tech-savoir">
                <label class="check-item"><input type="checkbox" value="3doigts"> Utilisation de la pulpe des 3 doigts du milieu</label>
                <label class="check-item"><input type="checkbox" value="pression"> Trois niveaux de pression (légère, moyenne, profonde)</label>
                <label class="check-item"><input type="checkbox" value="mouvement"> Mouvements circulaires, verticaux ou en rayons de roue</label>
                <label class="check-item"><input type="checkbox" value="aisselle"> Extension de la palpation jusqu'à l'aisselle (creux axillaire)</label>
                <label class="check-item"><input type="checkbox" value="mamelon"> Pressions douces du mamelon (recherche d'écoulement)</label>
            </div>

            <div class="section-title">III. ATTITUDES</div>
            <table>
                <thead><tr><th class="text-left">Énoncé</th><th>D'accord (1)</th><th>Neutre (2)</th><th>Pas d'accord (3)</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">L'AES est efficace pour réduire la mortalité.</td><td><input type="radio" name="att1" value="1" checked></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td></tr>
                    <tr><td class="text-left">La palpation est gênante pour les patientes.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (TECHNIQUES DE PALPATION APPLIQUÉES)</div>
            <div class="row">
                <div class="field">
                    <label>Niveau de technique utilisé :</label>
                    <select id="prac-methode">
                        <option value="rapide">1. Palpation rapide sans méthode précise</option>
                        <option value="systematique" selected>2. Méthode systématique (Quadrant par quadrant)</option>
                        <option value="complete">3. Méthode complète (Quadrant + creux axillaire + mamelon)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignez-vous la technique aux patientes ?</label>
                    <select id="prac-teach">
                        <option>Oui, avec démonstration</option>
                        <option>Oui, verbalement uniquement</option>
                        <option>Non, pas par manque de temps</option>
                    </select>
                </div>
            </div>

            <label style="display:block; margin:15px 0 10px 0; font-weight:bold; color:#b03060;">Anomalies recherchées lors de la pratique :</label>
            <div class="check-group" id="group-signes-recherche">
                <label class="check-item"><input type="checkbox" value="nodule"> Masse ou nodule dur</label>
                <label class="check-item"><input type="checkbox" value="adenopathie"> Ganglions sous l'aisselle</label>
                <label class="check-item"><input type="checkbox" value="peau"> Modification cutanée (peau d'orange)</label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER LA FICHE ENQUÊTÉ</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DES DONNÉES</div>
        <table id="main-table">
            <thead>
                <tr>
                    <th>Code</th>
                    <th>Service</th>
                    <th>Score Tech (%)</th>
                    <th>Pratique (Niveau)</th>
                    <th>Statut</th>
                </tr>
            </thead>
            <tbody id="db-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE DES COMPÉTENCES TECHNIQUES</div>
        <div class="row">
            <div class="stat-card">
                <div id="graph-tech"></div>
            </div>
            <div class="stat-card">
                <div id="graph-prac"></div>
            </div>
        </div>
        <div id="interpret-box" style="padding:15px; background:#e3f2fd; border-radius:8px;"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE DU MÉMOIRE</div>
        <div id="conclusion-text"></div>
    </div>
</div>

<script>
    let db = [];

    // Init selects
    const codeS = document.getElementById('code-enquete');
    for(let i=1; i<=100; i++) { let o = document.createElement('option'); o.value="INF-"+i; o.text="Infirmier(e) "+i; codeS.appendChild(o); }
    const expS = document.getElementById('exp-select');
    for(let i=0; i<=30; i++) { let o = document.createElement('option'); o.value=i; o.text=i+" ans"; expS.appendChild(o); }

    function saveRecord() {
        let rec = {
            id: document.getElementById('code-enquete').value,
            service: document.getElementById('service').value,
            techCount: document.querySelectorAll('#group-tech-savoir input:checked').length,
            methode: document.getElementById('prac-methode').value,
            teach: document.getElementById('prac-teach').value
        };

        // Scoring Savoir (max 7)
        let scoreBase = rec.techCount;
        if(document.getElementById('q-moment').value.includes('7 jours')) scoreBase++;
        if(document.getElementById('q-position').value.includes('miroir')) scoreBase++;
        rec.scoreFinal = Math.round((scoreBase / 7) * 100);

        db.push(rec);
        document.getElementById('count-badge').textContent = db.length;
        
        document.querySelectorAll('input[type="checkbox"]').forEach(c => c.checked = false);
        codeS.selectedIndex++;
        
        updateUI();
        alert("Fiche enregistrée avec succès !");
    }

    function updateUI() {
        const tbody = document.getElementById('db-body');
        tbody.innerHTML = '';
        db.forEach(r => {
            let labelMethode = "";
            if(r.methode === "rapide") labelMethode = "1. Rapide";
            else if(r.methode === "systematique") labelMethode = "2. Systématique";
            else labelMethode = "3. Complète";

            tbody.innerHTML += `<tr>
                <td>${r.id}</td><td>${r.service}</td>
                <td style="color:${r.scoreFinal > 70 ? 'green':'red'}">${r.scoreFinal}%</td>
                <td>${labelMethode}</td>
                <td>${r.scoreFinal >= 70 && r.methode === 'complete' ? '🟢 Expert' : '🔴 À renforcer'}</td>
            </tr>`;
        });

        let high = db.filter(r => r.scoreFinal >= 70).length;
        let complete = db.filter(r => r.methode === 'complete').length;

        document.getElementById('graph-tech').innerHTML = `<strong>Niveau de Maîtrise Théorique</strong><br><br>
            <div class="bar-container"><div class="bar-label">Satisfaisant</div><div class="bar-track"><div class="bar-fill" style="width:${Math.round(high/db.length*100 || 0)}%; background:green;">${Math.round(high/db.length*100 || 0)}%</div></div></div>`;
        
        document.getElementById('graph-prac').innerHTML = `<strong>Pratique de la Méthode Complète</strong><br><br>
            <div class="bar-container"><div class="bar-label">Complète</div><div class="bar-track"><div class="bar-fill" style="width:${Math.round(complete/db.length*100 || 0)}%; background:#b03060;">${Math.round(complete/db.length*100 || 0)}%</div></div></div>`;

        document.getElementById('conclusion-text').innerHTML = `
            <h3>Analyse des Pratiques à l'HGRM</h3>
            <p>Sur ${db.length} infirmiers, seulement <strong>${complete}</strong> pratiquent la méthode complète (incluant le creux axillaire et le mamelon).</p>
        `;
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(e => e.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "ID,Service,ScoreTechnique,Methode\n";
        db.forEach(r => csv += `${r.id},${r.service},${r.scoreFinal},${r.methode}\n`);
        let link = document.createElement("a");
        link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "donnees_KAP_HGRM.csv";
        link.click();
    }
</script>

</body>
</html>
