<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM : Logiciel de Collecte & Base de Données</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 90vh; }
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 10px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 20px; font-weight: bold; font-size: 13px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }

        /* Styles Formulaire Collecte */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 12px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tableaux Base de Données */
        table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 12px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; color: #b03060; position: sticky; top: 0; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }

        /* Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; cursor: pointer; font-size: 13px; }
        .check-item input { margin-right: 12px; transform: scale(1.3); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 30px; text-transform: uppercase; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showSection('collecte', this)">1. COLLECTE</div>
        <div class="tab" onclick="showSection('database', this)">2. BASE DE DONNÉES</div>
        <div class="tab" onclick="showSection('analyse', this)">3. ANALYSE CAP</div>
        <button type="button" class="btn-excel" onclick="exportCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="collecte" class="content-section active">
        <form id="formKAP">
            <div class="section-title">I. IDENTIFICATION DU PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>ID Enquêté(e)</label><select id="id_enq"><option>ENQ-001</option><option>ENQ-002</option><option>ENQ-003</option><option>ENQ-004</option></select></div>
                <div class="field"><label>Âge (18-60 ans)</label><select id="age-select"></select></div>
                <div class="field"><label>Niveau d'étude</label><select id="etude"><option>A2 (Diplômée)</option><option selected>A1 (Graduée)</option><option>L1 (Licenciée)</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>Expérience Pro (1-30 ans)</label><select id="exp-select"></select></div>
                <div class="field"><label>Statut Professionnel</label><select id="statut"><option selected>Titulaire</option><option>Stagiaire</option><option>Contractuelle</option></select></div>
                <div class="field"><label>Service Affectation</label><select id="service"><option>Maternité</option><option>Gynécologie</option><option>Chirurgie</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES MÉDICALES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>Risque augmente avec l'âge ?</label><select id="k1"><option selected>Vrai</option><option>Faux</option></select></div>
                <div class="field"><label>Allaitement est protecteur ?</label><select id="k2"><option selected>Vrai</option><option>Faux</option></select></div>
                <div class="field"><label>Moment idéal AES</label><select id="k3"><option selected>7j après règles</option><option>Pendant règles</option></select></div>
            </div>
            <label style="font-size: 12px; font-weight: bold; margin-bottom: 10px; display: block;">Signes d'alerte (Cochez les propositions) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" class="signe" value="Nodule" checked> Nodule dur/indolore</label>
                <label class="check-item"><input type="checkbox" class="signe" value="Peau Orange" checked> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" class="signe" value="Ecoulement" checked> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" class="signe" value="Rétraction"> Rétraction mamelon</label>
            </div>

            <div class="section-title">III. ATTITUDES & PRATIQUES (LIKERT / ACTIONS)</div>
            <div class="row">
                <div class="field"><label>Enseignez-vous l'AES ?</label><select id="p1"><option selected>Oui, systématiquement</option><option>Rarement</option><option>Jamais</option></select></div>
                <div class="field"><label>Référence mammographie</label><select id="p2"><option selected>Oui, si suspect</option><option>Non</option></select></div>
                <div class="field"><label>Sentiment d'efficacité (1-5)</label><select id="a1"><option>1</option><option>2</option><option>3</option><option selected>4</option><option>5</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="saveToDatabase()">VALIDER ET AJOUTER À LA BASE DE DONNÉES</button>
        </form>
    </div>

    <div id="database" class="content-section">
        <div class="section-title">BASE DE DONNÉES DES INFIRMIÈRES (HGRM)</div>
        <div style="overflow-x: auto;">
            <table id="dbTable">
                <thead>
                    <tr>
                        <th>Date</th>
                        <th>ID</th>
                        <th>Âge</th>
                        <th>Étude</th>
                        <th>Exp.</th>
                        <th>Service</th>
                        <th>K (Savoir)</th>
                        <th>P (Pratique)</th>
                        <th>Signes cochés</th>
                    </tr>
                </thead>
                <tbody>
                    </tbody>
            </table>
        </div>
    </div>

    <div id="analyse" class="content-section">
        <div class="section-title">ANALYSE STATISTIQUE CAP</div>
        <p>Cette section calcule automatiquement les pourcentages de réussite pour votre mémoire après enregistrement.</p>
    </div>
</div>

<script>
    let database = [];

    // Gestion de la navigation
    function showSection(id, element) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        element.classList.add('active');
    }

    // Génération automatique Âge (18-60)
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) { ageSelect.add(new Option(i + " ans", i)); }
    ageSelect.value = 30;

    // Génération automatique Expérience (1-30)
    const expSelect = document.getElementById('exp-select');
    for (let i = 1; i <= 30; i++) { expSelect.add(new Option(i + " ans", i)); }
    expSelect.value = 5;

    // Fonction de sauvegarde
    function saveToDatabase() {
        const signes = Array.from(document.querySelectorAll('.signe:checked')).map(c => c.value).join('|');
        
        const entry = {
            date: new Date().toLocaleDateString(),
            id: document.getElementById('id_enq').value,
            age: document.getElementById('age-select').value,
            etude: document.getElementById('etude').value,
            exp: document.getElementById('exp-select').value,
            service: document.getElementById('service').value,
            savoir: document.getElementById('k1').value === "Vrai" ? "Bon" : "Faible",
            pratique: document.getElementById('p1').value,
            signes: signes
        };

        database.push(entry);
        updateTable();
        alert("Fiche enregistrée ! Consultez l'onglet Base de Données.");
        showSection('database', document.querySelectorAll('.tab')[1]);
    }

    // Mise à jour du tableau
    function updateTable() {
        const tbody = document.querySelector('#dbTable tbody');
        tbody.innerHTML = "";
        database.forEach(item => {
            const row = `<tr>
                <td>${item.date}</td>
                <td><b>${item.id}</b></td>
                <td>${item.age}</td>
                <td>${item.etude}</td>
                <td>${item.exp} ans</td>
                <td>${item.service}</td>
                <td>${item.savoir}</td>
                <td>${item.pratique}</td>
                <td>${item.signes}</td>
            </tr>`;
            tbody.innerHTML += row;
        });
    }

    // Export CSV pour Excel
    function exportCSV() {
        if(database.length === 0) return alert("Aucune donnée à exporter.");
        let csv = "Date,ID,Age,Etude,Experience,Service,Savoir,Pratique,Signes\n";
        database.forEach(r => {
            csv += `${r.date},${r.id},${r.age},${r.etude},${r.exp},${r.service},${r.savoir},${r.pratique},${r.signes}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'Base_Donnees_Memoire.csv';
        a.click();
    }
</script>

</body>
</html>
</html>
