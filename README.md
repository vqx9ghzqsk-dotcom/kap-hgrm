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
        
        /* MASQUAGE ADMIN PAR DÉFAUT (Modif Code 1) */
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        /* Grid Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        
        /* Stats */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 28px; font-weight: bold; color: #b03060; }

        /* Champ mot de passe (Modif Code 1) */
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; transition: 0.3s; }
        .admin-login:hover { opacity: 1; }
        .admin-login input { width: 50px; border: 1px solid #ccc; font-size: 10px; padding: 3px; border-radius: 4px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="t2" onclick="showTab(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab admin-only" id="t3" onclick="showTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab admin-only" id="t4" onclick="showTab(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel admin-only" id="be" onclick="exportCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="tab1" class="content-section active">
        <form class="form-content" id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
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
                    <select name="etude" id="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option value="A0">L0/L1 (Licenciée nouveau système)</option>
                        <option value="Master">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="k1"><option value="1" selected>Vrai (Oui)</option><option value="0">Faux (Non)</option></select>
                </div>
                <div class="field">
                    <label>À quel âge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après les règles</option><option value="0">Pendant les règles</option></select>
                </div>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (LIKERT)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Je sais détecter un nodule suspect.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">La pudeur empêche mes patientes de se déshabiller.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
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
                    <select name="pra2"><option value="1" selected>Démonstration physique</option><option value="0">Verbalement</option></select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="validerSaisie()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT (BASE DE DONNÉES)</div>
        <table id="tableDepouillement">
            <thead><tr><th>Code</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Savoir</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE STATISTIQUE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Total (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div>Savoir Elevé</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div>Pratique Correcte</div></div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION ET RECOMMANDATION</div>
        <div id="summary" style="padding:20px; border:1px solid #ddd; background:#fff;">Remplissez les fiches pour générer une conclusion.</div>
    </div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

    // Modif Code 1 : Déblocage par PIN
    function checkAdmin(v) {
        if(v === "1398") {
            document.querySelectorAll('.admin-only').forEach(e => e.style.setProperty('display', 'block', 'important'));
            alert("Accès Admin Activé");
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 3) calculerStatistiques();
    }

    // Modif Code 1 : Envoi vers Google Sheets + Gestion Code 2
    async function validerSaisie() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));

        const entry = {
            code: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: fd.get('experience'),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            attitude: 'Positive',
            pratique: sp >= 1 ? 'Correcte' : 'Incorrecte'
        };

        // Envoi Google Sheets (Code 1)
        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            db.push(entry);
            actualiserTableau();
            alert("Enregistré et envoyé avec succès (ID: " + entry.code + ")");
            form.reset();
        } catch (e) {
            alert("Erreur de connexion.");
        }
    }

    function actualiserTableau() {
        const tbody = document.querySelector('#tableDepouillement tbody');
        tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td></tr>`).join('');
    }

    function calculerStatistiques() {
        let n = db.length; if(n === 0) return;
        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(db.filter(d => d.savoir === 'Bon').length/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(db.filter(d => d.pratique === 'Correcte').length/n*100) + "%";
    }

    function exportCSV() {
        let csv = "Code,Age,Etude,Experience,Savoir,Pratique\n" + db.map(d => `${d.code},${d.age},${d.etude},${d.experience},${d.savoir},${d.pratique}`).join("\n");
        const a = document.createElement('a'); a.href = URL.createObjectURL(new Blob([csv], {type:'text/csv'})); a.download = 'data.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) cs.options.add(new Option("ID: " + i, i));
        const as = document.getElementById('age-select');
        for (let i = 18; i <= 65; i++) as.options.add(new Option(i + " ans", i));
        const es = document.getElementById('exp-select');
        for (let i = 0; i <= 40; i++) es.options.add(new Option(i + " ans", i));
    };
</script>
</body>
</html>
