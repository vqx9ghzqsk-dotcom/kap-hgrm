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
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top:0; z-index:100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* GESTION ADMIN (CACHÉ PAR DÉFAUT) */
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; }
        .content-section { display: none; }
        .content-section.active { display: block; }

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
        
        /* Stats Dashboard */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-top: 20px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 32px; font-weight: bold; color: #b03060; }

        /* Login Float discret */
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.2; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 50px; border: 1px solid #ccc; font-size: 10px; padding: 3px; border-radius: 4px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="changeTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tab2" onclick="changeTab(2)">2. BASE DE DONNÉES</div>
        <div class="tab admin-only" id="tab3" onclick="changeTab(3)">3. ANALYSE STAT</div>
        <div class="tab admin-only" id="tab4" onclick="changeTab(4)">4. CONCLUSION</div>
        <button type="button" class="btn-excel admin-only" onclick="exportExcel()">📊 EXPORT EXCEL</button>
    </div>

    <div id="section1" class="content-section active">
        <form class="form-content" id="mainForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select name="statut">
                        <option selected>Titulaire du service</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire</option>
                        <option>Bénévole</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Expérience (ans)</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude" id="etude_input">
                        <option value="A2">A2 (Diplômée)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">L0/L1 (Licenciée)</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>1ère cause de décès en RDC ?</label>
                    <select name="k1"><option value="1" selected>Vrai</option><option value="0">Faux</option></select>
                </div>
                <div class="field">
                    <label>Âge début AES ?</label>
                    <select name="k2"><option value="0">12 ans</option><option value="1" selected>20 ans</option></select>
                </div>
                <div class="field">
                    <label>Meilleur moment AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après règles</option><option value="0">Pendant règles</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nulliparité</label>
                <label class="check-item"><input type="checkbox" checked> Grossesse tardive</label>
                <label class="check-item"><input type="checkbox" checked> Ménopause tardive</label>
                <label class="check-item"><input type="checkbox" checked> Tabac/Alcool</label>
                <label class="check-item"><input type="checkbox" checked> Antécédents familiaux</label>
            </div>

            <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nodule dur/indolore</label>
                <label class="check-item"><input type="checkbox" checked> Écoulement sanglant</label>
                <label class="check-item"><input type="checkbox" checked> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" checked> Adénopathie axillaire</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (LIKERT 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je sais détecter un nodule suspect.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">La pudeur empêche le dépistage.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence Palpation (ECS) :</label>
                    <select name="pra1"><option value="1" selected>Systématique</option><option value="0">Rarement</option></select>
                </div>
                <div class="field">
                    <label>Enseignement AES :</label>
                    <select name="pra2"><option value="1" selected>Démontre physiquement</option><option value="0">Verbalement/Non</option></select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES (HGRM)</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Absence de salle isolée</label>
                <label class="check-item"><input type="checkbox" checked> Coût mammographie</label>
                <label class="check-item"><input type="checkbox" checked> Manque de formation</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER</button>
        </form>
    </div>

    <div id="section2" class="content-section">
        <div class="section-title">BASE DE DONNÉES LOCALE</div>
        <div style="padding:20px; overflow-x:auto;"><table id="tableData"><thead><tr><th>ID</th><th>Savoir</th><th>Pratique</th><th>Service</th></tr></thead><tbody></tbody></table></div>
    </div>

    <div id="section3" class="content-section">
        <div class="section-title">STATISTIQUES RAPIDES</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="stat-n">0</div><div>Effectif (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="stat-k">0%</div><div>Savoir Bon</div></div>
        </div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let localDB = [];
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

    function checkAdmin(v) {
        if(v === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
            alert("Accès Administrateur Déverrouillé");
        }
    }

    function changeTab(i) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('section' + i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }

    async function saveData() {
        const form = document.getElementById('mainForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));

        const row = {
            code: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: fd.get('experience'),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 1 ? 'Correcte' : 'Incorrecte'
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(row) });
            localDB.push(row);
            updateAdminTable();
            alert('Fiche Enregistrée avec succès !');
            form.reset();
        } catch (e) { alert("Erreur d'envoi vers Google Sheets."); }
    }

    function updateAdminTable() {
        const tb = document.querySelector('#tableData tbody');
        tb.innerHTML = localDB.map(d => `<tr><td>${d.code}</td><td>${d.savoir}</td><td>${d.pratique}</td><td>${d.service}</td></tr>`).join('');
        document.getElementById('stat-n').innerText = localDB.length;
    }

    window.onload = () => {
        const cSel = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) { cSel.options.add(new Option("ID: " + i, i)); }
        const aSel = document.getElementById('age-select');
        for (let i = 18; i <= 65; i++) { aSel.options.add(new Option(i + " ans", i)); }
        const eSel = document.getElementById('exp-select');
        for (let i = 0; i <= 40; i++) { eSel.options.add(new Option(i + " ans", i)); }
    };

    function exportExcel() {
        let csv = "ID,Savoir,Pratique,Service\n" + localDB.map(d => `${d.code},${d.savoir},${d.pratique},${d.service}`).join("\n");
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'export_KAP.csv'; a.click();
    }
</script>
</body>
</html>
