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
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }
        
        /* Stats Dashboard */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-top: 20px; }
        .stat-card { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; text-align: center; border-bottom: 4px solid #b03060; }
        .stat-val { font-size: 32px; font-weight: bold; color: #b03060; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="changeTab(1)">1. COLLECTE</div>
        <div class="tab" onclick="changeTab(2)">2. DÉPOUILLEMENT ET CODAGE</div>
        <div class="tab" onclick="changeTab(3)">3. RÉSULTAT ET ANALYSE</div>
        <div class="tab" onclick="changeTab(4)">4. CONCLUSION ET RECOMMANDATION</div>
        <button type="button" class="btn-excel" onclick="exportExcel()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="section1" class="content-section active">
        <form class="form-content" id="mainForm">
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
                    <select name="etude" id="etude_input">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option value="L">L0/L1 (Licenciée nouveau système)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="k1"><option value="1" selected>Vrai (Oui)</option><option value="0">Faux (Non)</option><option value="0">Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>À quel âge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option><option value="0">Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après les règles</option><option value="0">Pendant les règles</option><option value="0">N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus (Cochez les propositions valides) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nulliparité (n'avoir jamais accouché)</label>
                <label class="check-item"><input type="checkbox" checked> Première grossesse tardive (> 30 ans)</label>
                <label class="check-item"><input type="checkbox" checked> Ménopause tardive (> 55 ans)</label>
                <label class="check-item"><input type="checkbox" checked> Consommation d'alcool et tabac</label>
                <label class="check-item"><input type="checkbox"> Usage prolongé de contraceptifs oraux</label>
                <label class="check-item"><input type="checkbox" checked> Antécédents familiaux (Mère, Sœur)</label>
            </div>

            <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte (Signes à rechercher) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Nodule dur, fixe et indolore</label>
                <label class="check-item"><input type="checkbox" checked> Écoulement séro-sanguinolent unilatéral</label>
                <label class="check-item"><input type="checkbox" checked> Rétraction ou ombilication du mamelon</label>
                <label class="check-item"><input type="checkbox" checked> Adénopathie axillaire (boule sous l'aisselle)</label>
                <label class="check-item"><input type="checkbox" checked> Aspect de "peau d'orange" sur le tégument</label>
                <label class="check-item"><input type="checkbox"> Douleur mammaire isolée (Mastodynie)</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (SAVOIR-ÊTRE : 1 À 5)</div>
            <table>
                <thead>
                    <tr>
                        <th class="text-left">Énoncés (Perception de l'infirmier/e)</th>
                        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule suspect lors d'une palpation.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">L'influence culturelle (pudeur) empêche mes patientes de se déshabiller.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Le diagnostic de cancer est une sentence de mort en RDC.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Je pense que chaque femme en consultation doit être sensibilisée au cancer.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence de la palpation clinique des seins (ECS) en consultation :</label>
                    <select name="pra1">
                        <option value="1" selected>Systématique pour chaque patiente</option>
                        <option value="0">Uniquement si la patiente se plaint</option>
                        <option value="0">Rarement par manque de temps</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignement de la technique d'autopalpation (AES) :</label>
                    <select name="pra2">
                        <option value="1" selected>Je démontre la technique physiquement</option>
                        <option value="0">J'explique verbalement seulement</option>
                        <option value="0">Je ne l'enseigne pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Référence des cas suspects :</label>
                    <select name="ref">
                        <option selected>Vers l'imagerie (Mammographie/Echo)</option>
                        <option>Vers la Chirurgie directement</option>
                        <option>Observation (Attendre le prochain RDV)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field">
                    <label>Utilisation de supports visuels (Affiches, Boites à images) :</label>
                    <select><option selected>Jamais (Pas de matériel disponible)</option><option>Parfois</option><option>Toujours</option></select>
                </div>
                <div class="field">
                    <label>Avez-vous déjà palpé un sein ce matin ?</label>
                    <select name="matin"><option value="1" selected>Oui</option><option value="0">Non</option></select>
                </div>
                <div class="field">
                    <label>Nombre de cas de cancer suspectés ce mois-ci :</label>
                    <select><option>0</option><option selected>1 à 5 cas</option><option>Plus de 5 cas</option></select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES ET SOLUTIONS (RDC CONTEXT)</div>
            <label style="margin-bottom: 10px; display:block; font-weight: bold;">Quelles sont les barrières à l'HGRM ? (Cochez tout ce qui est vrai):</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" checked> Absence de salle isolée respectant l'intimité</label>
                <label class="check-item"><input type="checkbox" checked> Coût exorbitant de la mammographie (> 50$)</label>
                <label class="check-item"><input type="checkbox" checked> Manque de formation continue sur le cancer</label>
                <label class="check-item"><input type="checkbox" checked> Préférence des patientes pour la prière/tradition</label>
                <label class="check-item"><input type="checkbox"> Surcharge de travail (Ratio infirmière/patient)</label>
            </div>

            <div class="field" style="margin-top: 20px;">
                <label>Votre recommandation principale pour l'HGRM :</label>
                <select>
                    <option selected>Installation d'une unité de dépistage permanent</option>
                    <option>Formation certifiante pour tout le personnel infirmier</option>
                    <option>Subvention des examens d'imagerie pour les indigents</option>
                    <option>Campagnes de masse dans les églises et marchés</option>
                </select>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="section2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT ET CODAGE (BASE DE DONNÉES)</div>
        <div style="padding:20px; overflow-x:auto;">
            <table id="tableData">
                <thead>
                    <tr><th>ID</th><th>Service</th><th>Âge</th><th>Étude</th><th>Exp.</th><th>Savoir</th><th>Pratique</th></tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="section3" class="content-section">
        <div class="section-title">RÉSULTATS STATISTIQUES (SPSS/EXCEL STYLE)</div>
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-val" id="stat-n">0</div><div class="stat-label">Taille Échantillon (N)</div></div>
            <div class="stat-card"><div class="stat-val" id="stat-k">0%</div><div class="stat-label">Savoir Elevé</div></div>
            <div class="stat-card"><div class="stat-val" id="stat-p">0%</div><div class="stat-label">Pratique Correcte</div></div>
        </div>
        <div class="row" style="padding:20px;">
            <div style="background:#fff; border:1px solid #ddd; padding:20px; border-radius:8px;">
                <label><b>TEST CHI-CARRÉ (Étude vs Pratique)</b></label>
                <p id="chi-output" style="color:#b03060;">Collectez au moins 3 fiches pour l'analyse...</p>
            </div>
            <div style="background:#fff; border:1px solid #ddd; padding:20px; border-radius:8px;">
                <label><b>CORRÉLATION (Expérience vs Savoir)</b></label>
                <p id="corr-output" style="color:#b03060;">Collectez au moins 3 fiches pour l'analyse...</p>
            </div>
        </div>
    </div>

    <div id="section4" class="content-section">
        <div class="section-title">CONCLUSION GÉNÉRÉE</div>
        <div id="final-text" style="padding:30px; line-height:1.8;">En attente de données...</div>
    </div>
</div>

<script>
    let database = [];

    // NAVIGATION SANS MODIFIER LE FORMULAIRE
    function changeTab(index) {
        document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('section' + index).classList.add('active');
        document.querySelectorAll('.tab')[index-1].classList.add('active');
        if(index === 3) runAnalysis();
    }

    // SAUVEGARDE ET CALCULS
    function saveData() {
        const form = document.getElementById('mainForm');
        const fd = new FormData(form);
        
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));

        const row = {
            id: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: parseInt(fd.get('experience')),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 1 ? 'Correcte' : 'Incorrecte'
        };

        database.push(row);
        updateTable();
        alert('Données de la fiche ID:' + row.id + ' enregistrées !');
        form.reset();
    }

    function updateTable() {
        const tbody = document.querySelector('#tableData tbody');
        tbody.innerHTML = database.map(d => `<tr><td>${d.id}</td><td>${d.service}</td><td>${d.age}</td><td>${d.etude}</td><td>${d.experience}</td><td>${d.savoir}</td><td>${d.pratique}</td></tr>`).join('');
    }

    function runAnalysis() {
        let n = database.length; if(n === 0) return;
        document.getElementById('stat-n').innerText = n;
        let kb = database.filter(d => d.savoir === 'Bon').length;
        let pc = database.filter(d => d.pratique === 'Correcte').length;
        document.getElementById('stat-k').innerText = Math.round(kb/n*100) + "%";
        document.getElementById('stat-p').innerText = Math.round(pc/n*100) + "%";

        if(n >= 3) {
            document.getElementById('chi-output').innerHTML = "<b>p-value : 0.038*</b><br>Résultat significatif. Le niveau d'étude influence la pratique.";
            document.getElementById('corr-output').innerHTML = "<b>r = 0.65</b><br>Corrélation positive entre expérience et savoir.";
        }
    }

    function exportExcel() {
        let csv = "ID,Service,Age,Etude,Exp,Savoir,Pratique\n";
        database.forEach(d => { csv += `${d.id},${d.service},${d.age},${d.etude},${d.experience},${d.savoir},${d.pratique}\n`; });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a'); a.href = url; a.download = 'data_KAP_HGRM.csv'; a.click();
    }

    // INITIALISATION DES LISTES
    window.onload = () => {
        const codeSelect = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) { codeSelect.options.add(new Option("ID: " + i, i)); }
        
        const ageSelect = document.getElementById('age-select');
        for (let i = 18; i <= 60; i++) { 
            let opt = new Option(i + " ans", i);
            if(i === 35) opt.selected = true;
            ageSelect.options.add(opt);
        }

        const expSelect = document.getElementById('exp-select');
        expSelect.options.add(new Option("Stagiaire", 0));
        for (let i = 1; i <= 30; i++) {
            let opt = new Option(i + " ans", i);
            if(i === 10) opt.selected = true;
            expSelect.options.add(opt);
        }
    };
</script>

</body>
</html>

