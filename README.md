<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Expert-KAP Breast Cancer HGRM</title>
<style>
    body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f4f7f6; margin: 0; padding: 10px; }
    .container { max-width: 1200px; margin: auto; background: white; border-radius: 8px; box-shadow: 0 2px 15px rgba(0,0,0,0.1); overflow: hidden; }
    .header-tabs { display: flex; background: #fff; border-bottom: 4px solid #b03060; padding: 10px; gap: 5px; position: sticky; top: 0; z-index: 1000; }
    .tab { padding: 12px 18px; font-weight: bold; font-size: 13px; border-radius: 5px; border: 1px solid #ddd; color: #555; background: #f9f9f9; cursor: pointer; transition: 0.3s; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    .admin-only { display: none !important; }
    .content-section { display: none; padding: 25px; }
    .content-section.active { display: block; }
    .section-title { background: #fff0f5; color: #b03060; padding: 15px; font-weight: bold; border-left: 6px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; letter-spacing: 1px; }
    .field { display: flex; flex-direction: column; margin-bottom: 20px; }
    label { font-size: 14px; font-weight: 700; margin-bottom: 10px; color: #333; line-height: 1.4; }
    select, input, textarea { padding: 12px; border: 1.5px solid #ccc; border-radius: 6px; font-size: 14px; transition: 0.3s; }
    select:focus { border-color: #b03060; outline: none; }
    .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 10px; padding: 15px; background: #fafafa; border-radius: 8px; }
    .check-item { display: flex; align-items: flex-start; gap: 10px; font-size: 13px; cursor: pointer; padding: 5px; }
    .check-item input { margin-top: 3px; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; text-transform: uppercase; margin-top: 30px; }
    table { width: 100%; border-collapse: collapse; margin-top: 10px; }
    th, td { border: 1px solid #eee; padding: 12px; text-align: center; }
    .text-left { text-align: left; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE DES DONNÉES</div>
        <div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" onclick="showTab(3)">3. ANALYSE ET CROISEMENT</div>
        <div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION & CONSENTEMENT</div>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                <div class="field"><label>Code d'identification (ID unique)</label><input type="text" name="id_inf" required placeholder="Ex: INF-001"></div>
                <div class="field"><label>Date de l'enquête</label><input type="date" name="date_coll" required></div>
            </div>
            <div style="background: #e3f2fd; padding: 15px; border-radius: 5px; border: 1px solid #90caf9;">
                <label class="check-item"><input type="checkbox" required> <b>Consentement éclairé :</b> Je certifie avoir été informé des objectifs de cette recherche et j'accepte d'y participer de manière volontaire et anonyme.</label>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                <div class="field"><label>Âge</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Sexe</label><select name="sexe"><option>Féminin</option><option>Masculin</option></select></div>
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="niveau" required>
                        <option value="A1">Infirmier Gradué (A1)</option>
                        <option value="A0">Infirmier Licencié (A0)</option>
                        <option value="Doc">Médecin Généraliste / Spécialiste</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté (Années)</label><select name="exp" id="exp-select"></select></div>
            </div>
            <div class="field"><label>Service affecté</label><input type="text" name="service" placeholder="Ex: Oncologie, Maternité, Urgences..."></div>

            <div class="section-title">III. ÉVALUATION DES CONNAISSANCES (SAVOIR)</div>
            
            <div class="field">
                <label>1. Selon vous, quelle est l'origine principale du cancer du sein ?</label>
                <select name="k_origine">
                    <option value="0">Une punition divine ou un sortilège (Niveau 0)</option>
                    <option value="1">Un choc traumatique ou un coup reçu sur le sein (Croyance erronée)</option>
                    <option value="2">Une prolifération anarchique de cellules due à des facteurs génétiques et hormonaux (Scientifique)</option>
                </select>
            </div>

            <div class="field">
                <label>2. Quels sont les facteurs de risque que vous identifiez ? (Choix multiple)</label>
                <div class="check-group">
                    <label class="check-item"><input type="checkbox" name="k_f1"> Consommation de piment et épices (Erroné)</label>
                    <label class="check-item"><input type="checkbox" name="k_f2"> Nulliparité ou première grossesse après 30 ans (Avancé)</label>
                    <label class="check-item"><input type="checkbox" name="k_f3"> Ménopause précoce avant 40 ans (Piège - c'est l'inverse)</label>
                    <label class="check-item"><input type="checkbox" name="k_f4"> Antécédents familiaux de cancer (BRCA1/2) (Expert)</label>
                </div>
            </div>

            <div class="field">
                <label>3. Quel est l'examen "Gold Standard" pour le dépistage précoce ?</label>
                <select name="k_examen">
                    <option value="0">La simple observation visuelle par la patiente</option>
                    <option value="1">L'échographie mammaire systématique</option>
                    <option value="2">La mammographie bilatérale (Standard international)</option>
                    <option value="3">La biopsie systématique de tout nodule (Inapproprié en dépistage)</option>
                </select>
            </div>

            <div class="field">
                <label>4. Quels signes cliniques évoquent un stade de gravité avancé ?</label>
                <select name="k_signe">
                    <option value="0">Une simple rougeur passagère</option>
                    <option value="1">Une boule qui fait très mal (La douleur est rarement un signe de cancer débutant)</option>
                    <option value="2">Peau d'orange, rétraction du mamelon et adénopathie axillaire fixe (Expert)</option>
                </select>
            </div>

            <div class="section-title">IV. ATTITUDES (POSTURE PROFESSIONNELLE)</div>
            
            <div class="field">
                <label>1. Que pensez-vous du pronostic du cancer du sein à Kinshasa ?</label>
                <select name="att_pronostic">
                    <option value="0">C'est une condamnation à mort inévitable</option>
                    <option value="1">On peut guérir par la prière uniquement</option>
                    <option value="2">La guérison est possible si le diagnostic est précoce et médical</option>
                </select>
            </div>

            <div class="field">
                <label>2. Si vous découvrez une masse chez une patiente, quelle est votre réaction intérieure ?</label>
                <select name="att_react">
                    <option value="0">Évitement : Je préfère ne pas lui dire pour ne pas l'effrayer</option>
                    <option value="1">Attentisme : Je lui demande de revenir si la boule grossit</option>
                    <option value="2">Action : Je ressens l'urgence de lancer le protocole de référence</option>
                </select>
            </div>

            <div class="field">
                <label>3. L'enseignement de l'autopalpation par l'infirmier est pour vous :</label>
                <select name="att_auto">
                    <option value="0">Une tâche inutile qui surcharge l'infirmier</option>
                    <option value="1">Une tâche qui devrait être réservée uniquement aux médecins</option>
                    <option value="2">Une mission éducative essentielle du personnel infirmier</option>
                </select>
            </div>

            <div class="section-title">V. PRATIQUES CLINIQUES</div>
            
            <div class="field">
                <label>1. À quelle fréquence examinez-vous les seins d'une patiente venant pour un autre motif ?</label>
                <select name="pra_freq">
                    <option value="0">Jamais, ce n'est pas le motif de consultation</option>
                    <option value="1">Rarement, si j'y pense</option>
                    <option value="2">Régulièrement pour les femmes de plus de 40 ans</option>
                </select>
            </div>

            <div class="field">
                <label>2. Comment réalisez-vous l'examen physique des seins ?</label>
                <select name="pra_tech">
                    <option value="0">Simple inspection visuelle rapide</option>
                    <option value="1">Palpation avec le bout des doigts uniquement</option>
                    <option value="2">Palpation avec la pulpe des 3 doigts, quadrants par quadrants et aires ganglionnaires (Correct)</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES RENCONTRÉS À L'HGRM</div>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="obs_1"> Manque de paravent ou de salle isolée pour l'examen</label>
                <label class="check-item"><input type="checkbox" name="obs_2"> Absence de matériel didactique (prothèses de démonstration)</label>
                <label class="check-item"><input type="checkbox" name="obs_3"> Refus des patientes pour des raisons religieuses</label>
                <label class="check-item"><input type="checkbox" name="obs_4"> Manque de formation continue sur les cancers</label>
                <label class="check-item"><input type="checkbox" name="obs_5"> Le coût du transport pour référer les patientes</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS</div>
            <div class="field">
                <label>Selon votre expérience, que faut-il changer en priorité à l'HGRM ?</label>
                <textarea name="recom" rows="4" placeholder="Ex: Installer une unité de mammographie, former les infirmiers de triage..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">Valider l'entrée et mettre à jour l'analyse</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">Dépouillement des fiches</div>
        <div id="tableContainer"></div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">Analyse Comparative & Graphiques</div>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
            <canvas id="chartSavoir"></canvas>
            <canvas id="chartPratique"></canvas>
        </div>
        <div id="analysisSummary" style="margin-top:20px; padding:15px; background:#f0f7f4;"></div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">Conclusion de l'étude</div>
        <div id="conclusionText" style="line-height:1.8;"></div>
    </div>
</div>

<div style="position:fixed; bottom:10px; right:10px; opacity:0.1;">
    <input type="password" placeholder="PIN" oninput="if(this.value==='1398') document.querySelectorAll('.admin-only').forEach(e=>e.style.setProperty('display','block','important'))">
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
    let db = [];

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.content-section')[n-1].classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n===3) updateAnalysis();
    }

    function saveData() {
        const form = document.getElementById('kapForm');
        if(!form.checkValidity()) { alert("Veuillez remplir les champs obligatoires"); return; }
        
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        
        // Calcul des scores pour l'analyse
        data.scoreSavoir = parseInt(data.k_origine || 0) + parseInt(data.k_examen || 0) + parseInt(data.k_signe || 0);
        data.scorePratique = parseInt(data.pra_freq || 0) + parseInt(data.pra_tech || 0);
        
        db.push(data);
        alert("Données enregistrées. " + db.length + " fiches en base.");
        form.reset();
        renderTable();
    }

    function renderTable() {
        let html = `<table><tr><th>ID</th><th>Niveau</th><th>Savoir</th><th>Pratique</th></tr>`;
        db.forEach(d => {
            html += `<tr><td>${d.id_inf}</td><td>${d.niveau}</td><td>${d.scoreSavoir}/6</td><td>${d.scorePratique}/4</td></tr>`;
        });
        document.getElementById('tableContainer').innerHTML = html + `</table>`;
    }

    function updateAnalysis() {
        if(db.length === 0) return;
        
        // Exemple de croisement : Moyenne Savoir par Niveau d'étude
        const a1Savoir = db.filter(d => d.niveau === 'A1').reduce((a, b) => a + b.scoreSavoir, 0) / db.filter(d => d.niveau === 'A1').length || 0;
        const a0Savoir = db.filter(d => d.niveau === 'A0').reduce((a, b) => a + b.scoreSavoir, 0) / db.filter(d => d.niveau === 'A0').length || 0;

        const ctxS = document.getElementById('chartSavoir').getContext('2d');
        new Chart(ctxS, {
            type: 'bar',
            data: {
                labels: ['Niveau A1', 'Niveau A0'],
                datasets: [{ label: 'Score Savoir Moyen', data: [a1Savoir, a0Savoir], backgroundColor: ['#f8bbd0', '#b03060'] }]
            }
        });

        document.getElementById('analysisSummary').innerHTML = `
            <h4>Observation statistique :</h4>
            <p>Le score de savoir moyen des Licenciés (A0) est de <b>${a0Savoir.toFixed(1)}/6</b> contre <b>${a1Savoir.toFixed(1)}/6</b> pour les Gradués (A1).</p>
        `;
    }

    window.onload = () => {
        const as = document.getElementById('age-select');
        for(let i=20; i<=65; i++) as.options.add(new Option(i+" ans", i));
        const es = document.getElementById('exp-select');
        for(let i=0; i<=40; i++) es.options.add(new Option(i+" ans", i));
    };
</script>
</body>
</html>
