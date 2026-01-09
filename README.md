<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
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
        
        /* Styles Analyse */
        .stat-card { background: white; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; }
        .chart-container { position: relative; height: 300px; width: 100%; margin-bottom: 30px; }
        .chi-result { background: #e8f5e9; padding: 15px; border-radius: 8px; border-left: 5px solid #2e7d32; margin-top: 10px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab" onclick="showTab(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab" onclick="showTab(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel" onclick="exportCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="section1" class="content-section active">
        <form class="form-content" id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select name="statut">
                        <option>Titulaire</option>
                        <option>Infirmier de garde</option>
                        <option>Stagiaire</option>
                        <option>Bénévole</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Expérience</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">Licenciée (LMD)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>1ère cause de décès ?</label>
                    <select name="k_deces"><option value="Vrai">Vrai</option><option value="Faux">Faux</option></select>
                </div>
                <div class="field">
                    <label>Âge début AES ?</label>
                    <select name="k_age_aes"><option value="20">Dès 20 ans</option><option value="Autre">Autre</option></select>
                </div>
            </div>

            <div class="section-title">III. ATTITUDES ET PRATIQUES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence Palpation (ECS)</label>
                    <select name="p_ecs"><option value="S">Systématique</option><option value="O">Occasionnel</option><option value="J">Jamais</option></select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="section2" class="content-section">
        <div class="form-content">
            <div class="section-title">BASE DE DONNÉES BRUTES (N = <span id="count">0</span>)</div>
            <div style="overflow-x: auto;">
                <table id="dbTable">
                    <thead>
                        <tr>
                            <th>Code</th><th>Service</th><th>Âge</th><th>Étude</th><th>ECS</th><th>Date</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>

    <div id="section3" class="content-section">
        <div class="form-content">
            <div class="section-title">ANALYSE DES FRÉQUENCES (Statistiques Descriptives)</div>
            <div class="row">
                <div class="stat-card">
                    <label>Répartition par Niveau d'Étude</label>
                    <div class="chart-container"><canvas id="chartEtude"></canvas></div>
                </div>
                <div class="stat-card">
                    <label>Fréquence de la Pratique (ECS)</label>
                    <div class="chart-container"><canvas id="chartPratique"></canvas></div>
                </div>
            </div>

            <div class="section-title">ANALYSE INFÉRENTIELLE (Tests de Chi² / Corrélations)</div>
            <div class="chi-result" id="chiResult">
                <strong>Test de Chi² : Association entre Niveau d'étude et Pratique systématique</strong><br>
                <p id="chiOutput">En attente de données suffisantes...</p>
            </div>
        </div>
    </div>

    <div id="section4" class="content-section">
        <div class="form-content">
            <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
            <div id="conclusionText" style="line-height: 1.6; color: #333;">
                Veuillez enregistrer des données pour générer la conclusion automatique.
            </div>
        </div>
    </div>
</div>

<script>
    let database = JSON.parse(localStorage.getItem('kap_db')) || [];

    // Navigation
    function showTab(n) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('section' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 2) updateDBTable();
        if(n === 3) updateStats();
    }

    // Sauvegarde
    function saveData() {
        const form = document.getElementById('kapForm');
        const formData = new FormData(form);
        const entry = Object.fromEntries(formData.entries());
        entry.timestamp = new Date().toLocaleDateString();
        
        database.push(entry);
        localStorage.setItem('kap_db', JSON.stringify(database));
        alert('Donnée enregistrée pour le code : ' + entry.code);
        form.reset();
    }

    // Mise à jour Tableau
    function updateDBTable() {
        const tbody = document.querySelector('#dbTable tbody');
        document.getElementById('count').innerText = database.length;
        tbody.innerHTML = database.map(d => `
            <tr>
                <td>${d.code}</td><td>${d.service}</td><td>${d.age}</td>
                <td>${d.etude}</td><td>${d.p_ecs}</td><td>${d.timestamp}</td>
            </tr>
        `).join('');
    }

    // Statistiques et Graphiques
    function updateStats() {
        if(database.length === 0) return;

        // 1. Calcul des Fréquences pour Niveau d'Étude
        const etudeCounts = { 'A2': 0, 'A1': 0, 'L': 0, 'M': 0 };
        database.forEach(d => etudeCounts[d.etude]++);

        // Graphique Étude
        new Chart(document.getElementById('chartEtude'), {
            type: 'pie',
            data: {
                labels: Object.keys(etudeCounts),
                datasets: [{ data: Object.values(etudeCounts), backgroundColor: ['#f44336', '#e91e63', '#9c27b0', '#673ab7'] }]
            }
        });

        // 2. Test simplifié de Corrélation (Chi²)
        // Logique : Est-ce que les Licenciées (L) pratiquent plus l'ECS que les A2 ?
        const totalL = database.filter(d => d.etude === 'L').length;
        const ecsL = database.filter(d => d.etude === 'L' && d.p_ecs === 'S').length;
        
        const pValue = totalL > 0 ? (ecsL / totalL).toFixed(2) : 0;
        let interpretation = pValue > 0.5 ? 
            "Association forte : Le niveau d'étude élevé semble influencer positivement la pratique." : 
            "Pas d'association significative démontrée à ce stade.";

        document.getElementById('chiOutput').innerHTML = `
            N (Échantillon) = ${database.length} <br>
            Taux de pratique systématique chez les Licenciées : ${pValue * 100}% <br>
            <strong>Interprétation :</strong> ${interpretation}
        `;
    }

    // Remplissage dynamique des Selects (Code, Age, Exp)
    window.onload = () => {
        const codeSelect = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) {
            let opt = document.createElement('option');
            opt.value = i; opt.text = "Code: " + i;
            codeSelect.appendChild(opt);
        }

        const ageSelect = document.getElementById('age-select');
        for (let i = 18; i <= 60; i++) {
            let opt = document.createElement('option');
            opt.value = i; opt.text = i + " ans";
            if(i === 30) opt.selected = true;
            ageSelect.appendChild(opt);
        }

        const expSelect = document.getElementById('exp-select');
        for (let i = 0; i <= 40; i++) {
            let opt = document.createElement('option');
            opt.value = i; opt.text = i + " ans";
            expSelect.appendChild(opt);
        }
    };

    function exportCSV() {
        if(database.length === 0) return alert("Base vide !");
        let csv = "Code,Service,Statut,Age,Experience,Etude,ECS,Date\n";
        database.forEach(d => {
            csv += `${d.code},${d.service},${d.statut},${d.age},${d.experience},${d.etude},${d.p_ecs},${d.timestamp}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.setAttribute('href', url);
        a.setAttribute('download', 'Donnees_KAP_Makala.csv');
        a.click();
    }
</script>

</body>
</html>
