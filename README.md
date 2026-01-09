<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        
        /* Header & Tabs */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content, .tab-content { padding: 30px; }
        .hidden { display: none; }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; color: #333; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .text-left { text-align: left; font-weight: 500; padding-left: 15px; }

        /* Grid Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }
        
        /* Stats Styles */
        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .stat-card { border: 1px solid #ddd; padding: 15px; border-radius: 8px; background: white; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div onclick="showTab('collecte')" id="t1" class="tab active">1. COLLECTE</div>
        <div onclick="showTab('depouillement')" id="t2" class="tab">2. DÉPOUILLEMENT ET CODAGE</div>
        <div onclick="showTab('analyse')" id="t3" class="tab">3. RÉSULTAT ET ANALYSE</div>
        <div onclick="showTab('conclusion')" id="t4" class="tab">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="collecte" class="tab-content">
        <form id="formKAP">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field">
                    <label>Code Enquêté(e)</label>
                    <select id="code-enquete" name="code"></select>
                </div>
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
                    <select name="etudes">
                        <option>A2 (Diplômée d'État)</option>
                        <option selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option>L0/L1 (Licenciée nouveau système)</option>
                        <option>Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès ?</label>
                    <select name="k1"><option value="1">Vrai (Oui)</option><option value="0">Faux (Non)</option><option value="99">Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>Âge début autopalpation (AES) ?</label>
                    <select name="k2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option><option>Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Meilleur moment pour l'AES ?</label>
                    <select name="k3"><option selected>7 jours après les règles</option><option>Pendant les règles</option><option>N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="fr" value="Nulliparité" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="fr" value="GrossesseTardive" checked> Grossesse tardive</label>
                <label class="check-item"><input type="checkbox" name="fr" value="Menopause" checked> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" name="fr" value="Alcool" checked> Alcool et tabac</label>
                <label class="check-item"><input type="checkbox" name="fr" value="Contraceptifs"> Contraceptifs oraux</label>
                <label class="check-item"><input type="checkbox" name="fr" value="Heredite" checked> Antécédents familiaux</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (1 À 5)</div>
            <table>
                <thead>
                    <tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                </thead>
                <tbody>
                    <tr><td class="text-left">Capacité de détection nodule</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4" checked></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="text-left">Influence culturelle (pudeur)</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence palpation clinique (ECS) :</label>
                    <select name="pra1"><option>Systématique</option><option>Si plainte</option><option>Rarement</option></select>
                </div>
                <div class="field">
                    <label>Enseignement technique (AES) :</label>
                    <select name="pra2"><option>Démonstration physique</option><option>Verbalement</option><option>Non</option></select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="depouillement" class="tab-content hidden">
        <div class="section-title">Base de Données Brutes (N=200) - Format Export SPSS/Excel</div>
        <div style="overflow-x: auto;">
            <table id="tableDonnees">
                <thead>
                    <tr>
                        <th>ID</th><th>Service</th><th>Âge</th><th>Exp.</th><th>Études</th><th>Savoir %</th><th>Attitude /5</th><th>Pratique</th>
                    </tr>
                </thead>
                <tbody id="bodyDonnees">
                    </tbody>
            </table>
        </div>
    </div>

    <div id="analyse" class="tab-content hidden">
        <div class="section-title">Statistiques Descriptives & Tests Chi²</div>
        <div class="stats-grid">
            <div class="stat-card">
                <h3>Répartition par Niveau d'Étude</h3>
                <div id="stats-etudes">Aucune donnée</div>
            </div>
            <div class="stat-card">
                <h3>Niveau de Connaissance Global</h3>
                <div id="stats-savoir">Bon: 0% | Médiocre: 0%</div>
            </div>
        </div>
    </div>

    <div id="conclusion" class="tab-content hidden">
        <div class="section-title">Conclusions et Recommandations</div>
        <p><i>Cette section synthétisera les résultats après analyse complète de la cohorte.</i></p>
    </div>
</div>

<script>
    let database = [];

    // Navigation entre onglets
    function showTab(id) {
        document.querySelectorAll('.tab-content').forEach(t => t.classList.add('hidden'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById(id).classList.remove('hidden');
        if(id === 'collecte') document.getElementById('t1').classList.add('active');
        if(id === 'depouillement') { document.getElementById('t2').classList.add('active'); updateTable(); }
        if(id === 'analyse') { document.getElementById('t3').classList.add('active'); runAnalyse(); }
        if(id === 'conclusion') document.getElementById('t4').classList.add('active');
    }

    // Sauvegarde des données
    function saveData() {
        const form = document.getElementById('formKAP');
        const formData = new FormData(form);
        const entry = Object.fromEntries(formData.entries());
        
        // Calcul score rapide connaissance (exemple)
        entry.scoreK = entry.k1 === "1" ? 100 : 0; 
        
        database.push(entry);
        alert('Données enregistrées pour le Code ' + entry.code + '. (Total: ' + database.length + ')');
        form.reset();
    }

    // Mise à jour du tableau de dépouillement
    function updateTable() {
        const body = document.getElementById('bodyDonnees');
        body.innerHTML = database.map(d => `
            <tr>
                <td>${d.code}</td><td>${d.service}</td><td>${d.age}</td>
                <td>${d.experience}</td><td>${d.etudes}</td><td>${d.scoreK}%</td>
                <td>${d.att1}</td><td>${d.pra1}</td>
            </tr>
        `).join('');
    }

    // Analyse statistique basique (Faisabilité Chi²)
    function runAnalyse() {
        if(database.length === 0) return;
        const total = database.length;
        const etudesCount = database.reduce((acc, curr) => {
            acc[curr.etudes] = (acc[curr.etudes] || 0) + 1;
            return acc;
        }, {});

        let html = "<ul>";
        for(let key in etudesCount) {
            let pct = ((etudesCount[key]/total)*100).toFixed(1);
            html += `<li>${key}: ${etudesCount[key]} (${pct}%)</li>`;
        }
        html += "</ul>";
        document.getElementById('stats-etudes').innerHTML = html;
    }

    // Export Excel/CSV
    function exportToCSV() {
        if(database.length === 0) return alert("Aucune donnée à exporter");
        let csv = "ID;Service;Age;Experience;Etudes;Score_Savoir;Attitude;Pratique\n";
        database.forEach(d => {
            csv += `${d.code};${d.service};${d.age};${d.experience};${d.etudes};${d.scoreK};${d.att1};${d.pra1}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'KAP_HGRM_Makala_Export.csv';
        a.click();
    }

    // Remplissage des menus déroulants
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 0; i <= 200; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = "Code: " + i;
        codeSelect.appendChild(opt);
    }

    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = i + " ans";
        if(i === 35) opt.selected = true;
        ageSelect.appendChild(opt);
    }

    const expSelect = document.getElementById('exp-select');
    let m = document.createElement('option'); m.text = "Stagiaire / < 1 an"; expSelect.appendChild(m);
    for (let i = 1; i <= 30; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = i + " ans d'exp.";
        if(i === 10) opt.selected = true;
        expSelect.appendChild(opt);
    }
</script>

</body>
</html>
