<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top:0; z-index:100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* CACHÉ PAR DÉFAUT (ADMIN) */
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; }
        .content-section { display: none; }
        .content-section.active { display: block; }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 5px; color: #222; }
        select, input { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .text-left { text-align: left; padding-left: 10px; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; }
        .check-item input { margin-right: 10px; transform: scale(1.2); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; text-transform: uppercase; }
        
        /* Login Float */
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.3; transition: 0.3s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 60px; padding: 5px; border-radius: 4px; border: 1px solid #ccc; font-size: 10px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="changeTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tab2" onclick="changeTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="tab3" onclick="changeTab(3)">3. ANALYSE STAT</div>
        <button type="button" class="btn-excel admin-only" id="btnEx" onclick="exportExcel()">📊 EXPORT EXCEL</button>
    </div>

    <div id="section1" class="content-section active">
        <form class="form-content" id="mainForm">
            <div class="section-title">I. IDENTIFICATION (HGRM MAKALA)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete" name="code"></select></div>
                <div class="field"><label>Service</label><select name="service"><option>Gynécologie</option><option>Maternité</option><option>Chirurgie</option><option>Médecine Interne</option></select></div>
                <div class="field"><label>Niveau d'étude</label><select name="etude"><option value="A2">A2</option><option value="A1" selected>A1</option><option value="L">Licence</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field"><label>Cause 1ère mortalité ?</label><select name="k1"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field"><label>Âge début AES</label><select name="k2"><option value="1">20 ans</option><option value="0">40 ans</option></select></div>
            </div>
            
            <p style="font-size:12px; font-weight:bold; color:#b03060; margin-top:15px;">Signes d'alerte :</p>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nodule dur/indolore</label>
                <label class="check-item"><input type="checkbox" checked> Peau d'orange</label>
                <label class="check-item"><input type="checkbox" checked> Écoulement sanglant</label>
            </div>

            <div class="section-title">III. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field"><label>Palpation clinique</label><select name="pra1"><option value="1">Systématique</option><option value="0">Rarement</option></select></div>
                <div class="field"><label>Démonstration AES</label><select name="pra2"><option value="1">Oui, physique</option><option value="0">Non/Verbal</option></select></div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENVOYER LA FICHE</button>
        </form>
    </div>

    <div id="section2" class="content-section">
        <div class="section-title">BASE DE DONNÉES EN TEMPS RÉEL</div>
        <div style="padding:20px; overflow-x:auto;">
            <table id="tableData">
                <thead><tr><th>ID</th><th>Service</th><th>Étude</th><th>Savoir</th><th>Pratique</th></tr></thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="section3" class="content-section" style="padding:20px;">
        <div class="section-title">RÉSULTATS STATISTIQUES</div>
        <p id="stats-summary">Chargement des données...</p>
    </div>
</div>

<div class="admin-login">
    <input type="password" id="adminCode" placeholder="Admin PIN" oninput="checkAdmin(this.value)">
</div>

<script>
    let localDB = [];

    // FONCTION POUR ACTIVER LES ONGLETS CACHÉS AVEC LE CODE 1398
    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
            alert("Mode Administrateur Activé !");
        }
    }

    function changeTab(idx) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('section' + idx).classList.add('active');
        document.querySelectorAll('.tab')[idx-1].classList.add('active');
    }

    async function saveData() {
        const form = document.getElementById('mainForm');
        const fd = new FormData(form);
        const row = {
            code: fd.get('code'),
            service: fd.get('service'),
            etude: fd.get('etude'),
            savoir: (parseInt(fd.get('k1')) + parseInt(fd.get('k2'))) >= 1 ? 'Bon' : 'Faible',
            pratique: (parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'))) >= 1 ? 'Correcte' : 'Incorrecte'
        };

        const url = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

        try {
            await fetch(url, { method: 'POST', mode: 'no-cors', body: JSON.stringify(row) });
            localDB.push(row); // Garde une copie locale pour l'affichage admin
            updateAdminView();
            alert('Fiche transmise !');
            form.reset();
        } catch (e) { alert("Erreur d'envoi"); }
    }

    function updateAdminView() {
        const tbody = document.querySelector('#tableData tbody');
        tbody.innerHTML = localDB.map(d => `<tr><td>${d.code}</td><td>${d.service}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
        document.getElementById('stats-summary').innerHTML = `Total fiches : ${localDB.length}`;
    }

    window.onload = () => {
        const sel = document.getElementById('code-enquete');
        for(let i=1; i<=100; i++) sel.options.add(new Option("Enquêté n°"+i, i));
    };
</script>

</body>
</html>
