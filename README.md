<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 11px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; border-left: 8px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .text-left { text-align: left; padding-left: 15px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 12px; cursor: pointer; }
        .check-item input { margin-right: 10px; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; text-transform: uppercase; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #e0e0e0; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 24px; font-weight: bold; color: #b03060; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE RICHE</div>
        <div class="tab" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab" onclick="showTab(3)">3. ANALYSE</div>
        <div class="tab" onclick="showTab(4)">4. CONCLUSIONS</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="formKAP">
            <div class="section-title">I. PROFIL SOCIODÉMOGRAPHIQUE</div>
            <div class="row">
                <div class="field"><label>ID Enquêté(e)</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Service d'affectation</label>
                    <select name="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Maternité / CPN</option>
                        <option>Chirurgie / Urgences</option>
                        <option>Médecine Interne</option>
                    </select>
                </div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1">A1 (Graduée)</option>
                        <option value="L">L (Licenciée)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES APPROFONDIES (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il curable si dépisté tôt ?</label>
                    <select name="k1"><option value="1">Oui, totalement</option><option value="0">Non / Rarement</option></select>
                </div>
                <div class="field">
                    <label>Meilleur moment pour l'auto-examen (AES) ?</label>
                    <select name="k2"><option value="1">7 jours après les règles</option><option value="0">Pendant les règles</option><option value="0">N'importe quand</option></select>
                </div>
            </div>
            <label style="font-size: 13px; font-weight: bold; margin-top: 10px; display: block;">Facteurs de risque connus (Cochez tout ce qui est vrai) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Heredite"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Nullipare"> 1ère grossesse après 30 ans</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Hormone"> Contraception orale prolongée</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Tabac"> Alcool / Tabac</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PUDEUR (LIKERT 1-5)</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">L'examen des seins devrait être systématique en CPN.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5" checked></td></tr>
                    <tr><td class="text-left">La pudeur des patientes est un frein au dépistage.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES ET OBSTACLES</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence de palpation clinique (ECS) :</label>
                    <select name="pra1">
                        <option value="2">Systématique</option>
                        <option value="1">Si plainte uniquement</option>
                        <option value="0">Rarement / Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignement de l'AES aux patientes :</label>
                    <select name="pra2">
                        <option value="2">Démonstration physique</option>
                        <option value="1">Explication verbale</option>
                        <option value="0">Aucun enseignement</option>
                    </select>
                </div>
            </div>
            <label style="font-size: 13px; font-weight: bold; margin-top: 10px; display: block;">Barrière principale à l'HGRM :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs" value="Local"> Manque de local isolé (Intimité)</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Temps"> Surcharge de travail / Temps</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Materiel"> Manque de matériel didactique</label>
                <label class="check-item"><input type="checkbox" name="obs" value="Mari"> Refus du partenaire / Mari</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">DONNÉES DÉPOUILLÉES</div>
        <table id="db-table">
            <thead><tr><th>ID</th><th>Étude</th><th>Savoir</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">INDICATEURS DE PERFORMANCE</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="stat-n">0</div><div>Total Échantillon</div></div>
            <div class="stat-card"><div class="stat-val" id="stat-k">0%</div><div>Savoir Adéquat</div></div>
            <div class="stat-card"><div class="stat-val" id="stat-p">0%</div><div>Pratique Correcte</div></div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">INTERPRÉTATION DES RÉSULTATS</div>
        <div id="final-summary" style="background:#fff; padding:20px; border:1px solid #ddd; border-radius:8px;">
            En attente de données...
        </div>
    </div>
</div>

<script>
    let database = [];

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n >= 3) runAnalysis();
    }

    function saveData() {
        const form = document.getElementById('formKAP');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2'));
        let sa = parseInt(fd.get('att1')) + parseInt(fd.get('att2'));
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));

        const entry = {
            id: fd.get('code'),
            etude: fd.get('etude'),
            savoir: sk >= 2 ? 'Bon' : 'Insuffisant',
            attitude: sa >= 8 ? 'Positive' : 'Négative',
            pratique: sp >= 3 ? 'Correcte' : 'Incorrecte'
        };

        database.push(entry);
        updateTable();
        alert("Fiche enregistrée !");
        form.reset();
    }

    function updateTable() {
        const tb = document.querySelector('#db-table tbody');
        tb.innerHTML = database.map(d => `<tr><td>${d.id}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td></tr>`).join('');
    }

    function runAnalysis() {
        let n = database.length; if(n === 0) return;
        let k = database.filter(d => d.savoir === 'Bon').length;
        let p = database.filter(d => d.pratique === 'Correcte').length;

        document.getElementById('stat-n').innerText = n;
        document.getElementById('stat-k').innerText = Math.round(k/n*100) + "%";
        document.getElementById('stat-p').innerText = Math.round(p/n*100) + "%";

        let txt = `<b>Rapport :</b> Sur ${n} infirmières, le niveau de connaissance est de ${Math.round(k/n*100)}%. `;
        txt += (p < k) ? "On observe un décalage : le savoir est présent mais la pratique ne suit pas, probablement à cause des barrières logistiques identifiées." : "La pratique est en adéquation avec le savoir.";
        document.getElementById('final-summary').innerHTML = txt;
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 150; i++) cs.options.add(new Option("Enquêté n°"+i, i));
    };
</script>
</body>
</html>
