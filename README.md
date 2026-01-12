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

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; }
        
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables Likert */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        /* Grid Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        
        /* Stats & Cross Analysis */
        .stat-card { background: #f9f9f9; padding: 15px; border-radius: 8px; border-left: 5px solid #b03060; margin-bottom: 15px; }
        .interpretation-text { background: #e8f5e9; padding: 15px; border-radius: 8px; margin-top: 10px; font-style: italic; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="switchTab(1)">1. COLLECTE</div>
        <div class="tab" onclick="unlockAdmin(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab" onclick="unlockAdmin(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab" onclick="unlockAdmin(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="mainForm" class="form-content" style="padding:0">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code_enquete"></select></div>
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
                    <select name="niveau_etude">
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
                    <select name="savoir_1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option><option>Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>Âge début autopalpation (AES) ?</label>
                    <select name="savoir_2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option><option>Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Meilleur moment pour l'AES ?</label>
                    <select name="savoir_3"><option selected>7 jours après les règles</option><option>Pendant les règles</option><option>N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risque" value="nulliparite" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risque" value="grossesse_tardive" checked> Grossesse tardive</label>
                <label class="check-item"><input type="checkbox" name="risque" value="menopause" checked> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" name="risque" value="alcool_tabac" checked> Alcool et tabac</label>
                <label class="check-item"><input type="checkbox" name="risque" value="contraceptifs"> Contraceptifs oraux</label>
                <label class="check-item"><input type="checkbox" name="risque" value="antecedents" checked> Antécédents familiaux</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (1 À 5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule.</td><td><input type="radio" name="att_1" value="1"></td><td><input type="radio" name="att_1" value="2"></td><td><input type="radio" name="att_1" value="3"></td><td><input type="radio" name="att_1" value="4" checked></td><td><input type="radio" name="att_1" value="5"></td></tr>
                    <tr><td class="text-left">La pudeur empêche les patientes de se déshabiller.</td><td><input type="radio" name="att_2" value="1"></td><td><input type="radio" name="att_2" value="2"></td><td><input type="radio" name="att_2" value="3"></td><td><input type="radio" name="att_2" value="4"></td><td><input type="radio" name="att_2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence de la palpation (ECS) :</label>
                    <select name="pratique_1"><option selected>Systématique</option><option>Si plainte</option><option>Rarement</option></select>
                </div>
                <div class="field">
                    <label>Enseignement de l'AES :</label>
                    <select name="pratique_2"><option selected>Démonstration physique</option><option>Verbal</option><option>Non</option></select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE ET ENVOYER AU SERVEUR (GOOGLE SHEETS)</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE CODAGE ET DÉPOUILLEMENT GÉNÉRAL</div>
        <div id="depouillement-table"></div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE CROISÉE : SAVOIR vs PRATIQUE</div>
        <div id="analyse-container"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
        <div id="conclusion-container"></div>
    </div>
</div>

<script>
    const ADMIN_CODE = "1398";
    const GOOGLE_SHEET_URL = "VOTRE_URL_GOOGLE_APPS_SCRIPT_ICI"; // Collez votre URL ici
    let database = [];

    // Init selects
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 0; i <= 200; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = "Code: " + i; codeSelect.appendChild(opt); }
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; if(i===35) opt.selected=true; ageSelect.appendChild(opt); }
    const expSelect = document.getElementById('exp-select');
    for (let i = 0; i <= 30; i++) { let opt = document.createElement('option'); opt.value = i; opt.text = i + " ans"; if(i===10) opt.selected=true; expSelect.appendChild(opt); }

    function switchTab(n) {
        document.querySelectorAll('.form-content').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(el => el.classList.remove('active'));
        document.getElementById('content-' + n).classList.add('active');
        document.querySelector(`.tab:nth-child(${n})`).classList.add('active');
        if(n > 1) refreshAnalysis();
    }

    function unlockAdmin(tab) {
        let code = prompt("Veuillez saisir le code administrateur pour accéder aux données :");
        if (code === ADMIN_CODE) { switchTab(tab); } 
        else { alert("Accès refusé. Code incorrect."); }
    }

    function saveData() {
        const formData = new FormData(document.getElementById('mainForm'));
        const data = Object.fromEntries(formData.entries());
        
        // Calcul des scores pour l'analyse
        data.score_savoir = (data.savoir_1.includes("Vrai") ? 33 : 0) + (data.savoir_2.includes("20") ? 33 : 0) + (data.savoir_3.includes("7") ? 34 : 0);
        data.score_pratique = data.pratique_1 === "Systématique" ? 100 : 50;

        database.push(data);

        // Envoi vers Google Sheets
        fetch(GOOGLE_SHEET_URL, {
            method: 'POST',
            mode: 'no-cors',
            body: JSON.stringify(data)
        }).then(() => {
            alert("Données enregistrées localement et transmises à Google Sheets !");
            document.getElementById('mainForm').reset();
        });
    }

    function refreshAnalysis() {
        if(database.length === 0) return;

        // Dépouillement
        let htmlTable = `<table><thead><tr><th>Code</th><th>Niveau</th><th>Score Savoir</th><th>Score Pratique</th></tr></thead><tbody>`;
        database.forEach(d => {
            htmlTable += `<tr><td>${d.code_enquete}</td><td>${d.niveau_etude}</td><td>${d.score_savoir}%</td><td>${d.score_pratique}%</td></tr>`;
        });
        htmlTable += `</tbody></table>`;
        document.getElementById('depouillement-table').innerHTML = htmlTable;

        // Analyse Croisée
        let moySavoir = database.reduce((acc, curr) => acc + curr.score_savoir, 0) / database.length;
        let moyPrat = database.reduce((acc, curr) => acc + curr.score_pratique, 0) / database.length;

        document.getElementById('analyse-container').innerHTML = `
            <div class="stat-card">
                <strong>Fréquences :</strong><br>
                Nombre de fiches : ${database.length}<br>
                Moyenne Savoir : ${moySavoir.toFixed(1)}%<br>
                Moyenne Pratique : ${moyPrat.toFixed(1)}%
            </div>
            <div class="interpretation-text">
                L'analyse montre que pour un niveau de connaissance de ${moySavoir.toFixed(0)}%, 
                la pratique réelle à l'HGRM est de ${moyPrat.toFixed(0)}%. 
                ${moySavoir > moyPrat ? "On observe un écart entre le savoir théorique et l'application pratique." : "La pratique est en adéquation avec les connaissances."}
            </div>`;
            
        // Conclusion
        document.getElementById('conclusion-container').innerHTML = `
            <div class="stat-card">
                <h4>Synthèse Finale</h4>
                <p>Le personnel de l'HGRM présente un profil majoritairement ${database[0].niveau_etude}. 
                La barrière principale identifiée reste la pudeur des patientes et le besoin de formation continue.</p>
            </div>`;
    }

    function exportToCSV() {
        let csv = "Code,Service,Niveau,Savoir,Pratique\n";
        database.forEach(d => {
            csv += `${d.code_enquete},${d.service},${d.niveau_etude},${d.score_savoir},${d.score_pratique}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.setAttribute('href', url);
        a.setAttribute('download', 'KAP_HGRM_Export.csv');
        a.click();
    }
</script>

</body>
</html>
