<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Cancer du Sein RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .admin-only { display: none !important; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .content-section { display: none; padding: 30px; }
        .content-section.active { display: block; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px; background: #f9f9f9; padding: 15px; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; }
        .check-item input { margin-right: 10px; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 28px; font-weight: bold; color: #b03060; }
        .admin-login { position: fixed; bottom: 10px; right: 10px; opacity: 0.1; }
        .admin-login:hover { opacity: 1; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" id="tabH2" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" id="tabH3" onclick="showTab(3)">3. ANALYSE</div>
        <div class="tab admin-only" id="tabH4" onclick="showTab(4)">4. RECOMMANDATIONS</div>
        <button type="button" class="btn-excel admin-only" onclick="exportCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            <div class="section-title">I. PROFIL SOCIODÉMOGRAPHIQUE</div>
            <div class="row">
                <div class="field"><label>ID Enquêtée</label><select id="code-enquete" name="code"></select></div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="etude">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">L (Licenciée)</option>
                        <option value="M">M (Master/Doctorat)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Formation continue sur le cancer ?</label>
                    <select name="formation">
                        <option value="Recente">Oui, récemment (-2 ans)</option>
                        <option value="Ancienne">Oui, ancienne</option>
                        <option value="Jamais" selected>Jamais</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIR)</div>
            <div class="row">
                <div class="field">
                    <label>1ère cause de décès par cancer (Femme RDC) ?</label>
                    <select name="k1"><option value="0">Col de l'utérus</option><option value="1" selected>Sein</option><option value="0">Poumon</option></select>
                </div>
                <div class="field">
                    <label>Âge recommandé Mammographie ?</label>
                    <select name="k_mammo"><option value="0">20 ans</option><option value="0">30 ans</option><option value="1" selected>45 ans</option></select>
                </div>
                <div class="field">
                    <label>Taux de survie au Stade 1 ?</label>
                    <select name="k_stade"><option value="0">< 20%</option><option value="0">50%</option><option value="1" selected>> 90%</option></select>
                </div>
            </div>
            
            <label style="font-weight:bold; color:#b03060; margin-top:10px; display:block;">Facteurs de risque (Cochez tout ce qui est vrai) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="risk" value="Heredite" checked> Hérédité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Nullipare"> Nulliparité</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" name="risk" value="Age"> Âge avancé</label>
            </div>

            <div class="section-title">III. ATTITUDES (PERCEPTIONS) - Échelle 1 à 5</div>
            <table>
                <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Le dépistage précoce permet une guérison totale</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5" checked></td></tr>
                    <tr><td class="text-left">J'évite d'en parler pour ne pas effrayer la patiente</td><td><input type="radio" name="att2" value="1" checked></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td class="text-left">Le paludisme est plus prioritaire que le cancer</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Technique de palpation utilisée :</label>
                    <select name="p_tech">
                        <option value="1" selected>À plat avec 3 doigts</option>
                        <option value="0">Pincement du sein</option>
                        <option value="0">Inspection visuelle seule</option>
                    </select>
                </div>
                <div class="field">
                    <label>Examen des aisselles (Adénopathie) ?</label>
                    <select name="p_axille"><option value="1">Toujours</option><option value="0" selected>Parfois / Jamais</option></select>
                </div>
                <div class="field">
                    <label>Action si masse détectée :</label>
                    <select name="p_action">
                        <option value="1" selected>Référer au chirurgien</option>
                        <option value="0">Prescrire des antibiotiques</option>
                        <option value="0">Demander d'attendre</option>
                    </select>
                </div>
            </div>

            <div class="section-title">V. BARRIÈRES & SOURCES</div>
            <div class="row">
                <div class="field">
                    <label>Obstacle Majeur :</label>
                    <select name="obs">
                        <option>Manque de local privé</option>
                        <option>Surcharge de travail</option>
                        <option>Croyances religieuses</option>
                        <option>Oubli / Pas de réflexe</option>
                    </select>
                </div>
                <div class="field">
                    <label>Source d'info principale :</label>
                    <select name="source">
                        <option>Université / École</option>
                        <option>Internet / Réseaux Sociaux</option>
                        <option>Séminaires HGRM</option>
                    </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section"><table id="tableDepouillement"><thead><tr><th>ID</th><th>Étude</th><th>Savoir</th><th>Pratique</th><th>Source</th></tr></thead><tbody></tbody></table></div>
    <div id="tab3" class="content-section">
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="res-n">0</div><div>Total N</div></div>
            <div class="stat-card"><div class="stat-val" id="res-k">0%</div><div>Savoir Élevé</div></div>
            <div class="stat-card"><div class="stat-val" id="res-p">0%</div><div>Pratique Correcte</div></div>
        </div>
        <div id="study-dist" style="background:#eee; padding:15px; border-radius:8px;"></div>
    </div>
    <div id="tab4" class="content-section"><div id="summary" style="padding:20px; border:1px solid #ddd; border-radius:8px; line-height:1.6;"></div></div>
</div>

<div class="admin-login"><input type="password" placeholder="PIN" oninput="checkAdmin(this.value)"></div>

<script>
    let db = [];
    const scriptURL = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

    function checkAdmin(val) {
        if(val === "1398") {
            document.querySelectorAll('.admin-only').forEach(el => el.style.setProperty('display', 'block', 'important'));
        }
    }

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab' + n).classList.add('active');
        if(n >= 3) calculerAnalyse();
    }

    async function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k_mammo')) + parseInt(fd.get('k_stade'));
        let sp = parseInt(fd.get('p_tech')) + parseInt(fd.get('p_axille')) + parseInt(fd.get('p_action'));

        const entry = {
            code: fd.get('code'),
            etude: fd.get('etude'),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 2 ? 'Correcte' : 'Incorrecte',
            source: fd.get('source'),
            obstacle: fd.get('obs')
        };

        try {
            await fetch(scriptURL, { method: 'POST', mode: 'no-cors', body: JSON.stringify(entry) });
            db.push(entry);
            actualiserTableau();
            alert("Enregistré !");
            form.reset();
        } catch (e) { alert("Erreur."); }
    }

    function actualiserTableau() {
        document.querySelector('#tableDepouillement tbody').innerHTML = db.map(d => 
            `<tr><td>${d.code}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.pratique}</td><td>${d.source}</td></tr>`
        ).join('');
    }

    function calculerAnalyse() {
        let n = db.length; if(n === 0) return;
        let kHigh = db.filter(d => d.savoir === 'Bon').length;
        let pGood = db.filter(d => d.pratique === 'Correcte').length;
        document.getElementById('res-n').innerText = n;
        document.getElementById('res-k').innerText = Math.round(kHigh/n*100) + "%";
        document.getElementById('res-p').innerText = Math.round(pGood/n*100) + "%";

        let conc = `<b>Conclusion :</b> Sur ${n} infirmières, ${Math.round(kHigh/n*100)}% maîtrisent la théorie (stades, mammographie) mais seulement ${Math.round(pGood/n*100)}% appliquent la bonne technique d'examen axillaire.`;
        document.getElementById('summary').innerHTML = conc;
    }

    function exportCSV() {
        let csv = "ID,Etude,Savoir,Pratique,Source\n";
        db.forEach(d => { csv += `${d.code},${d.etude},${d.savoir},${d.pratique},${d.source}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'Data_KAP.csv'; a.click();
    }

    window.onload = () => {
        const cs = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) cs.options.add(new Option("Infirmière ID: " + i, i));
    };
</script>
</body>
</html>
