<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Étude KAP Intégrale - Cancer du Sein HGRM</title>
<style>
    body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f4f7f6; margin: 0; padding: 10px; }
    .container { max-width: 1350px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 5px 30px rgba(0,0,0,0.2); }
    
    .header-tabs { display: flex; background: #fff; border-bottom: 5px solid #b03060; padding: 15px; gap: 10px; position: sticky; top: 0; z-index: 1000; overflow-x: auto; }
    .tab { padding: 12px 20px; font-weight: bold; font-size: 13px; border-radius: 6px; border: 1px solid #ddd; color: #555; background: #f9f9f9; cursor: pointer; white-space: nowrap; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    
    .content-section { display: none; padding: 30px; }
    .content-section.active { display: block; }
    
    .section-title { background: #fff0f5; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 35px 0 15px 0; text-transform: uppercase; font-size: 14px; }
    .field { display: flex; flex-direction: column; margin-bottom: 25px; }
    label { font-size: 14px; font-weight: 800; margin-bottom: 12px; color: #1a1a1a; }
    select, input, textarea { padding: 14px; border: 2px solid #ddd; border-radius: 8px; font-size: 14px; }
    
    .grid-4 { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; margin-bottom: 30px; }
    th, td { border: 1px solid #ddd; padding: 12px; text-align: center; font-size: 13px; }
    th { background-color: #b03060; color: white; }
    
    .check-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 10px; background: #fafafa; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 10px; font-size: 20px; font-weight: bold; cursor: pointer; text-transform: uppercase; margin: 40px 0; }
    
    .stats-card { background: #fff; padding: 20px; border-radius: 8px; border: 1px solid #eee; box-shadow: 0 2px 5px rgba(0,0,0,0.05); text-align: center; margin-bottom: 20px; }
    .big-num { font-size: 32px; font-weight: bold; color: #b03060; }
    .admin-only { display: none !important; }
    .chart-box { max-width: 600px; margin: auto; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT & CODAGE</div>
        <div class="tab admin-only" onclick="showTab(3)">3. ANALYSES & RÉSULTATS</div>
        <div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION & RECOMMANDATIONS</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="masterForm">
            <div class="section-title">I. IDENTIFICATION COMPLÈTE</div>
            <div class="grid-4">
                <div class="field"><label>Numéro d'enquête</label><input type="text" name="n_enquete" required></div>
                <div class="field"><label>Nom de l'enquêteur</label><input type="text" name="enqueteur" required></div>
                <div class="field"><label>Service d'affectation</label>
                    <select name="service" required>
                        <option value="Chirurgie">Chirurgie</option>
                        <option value="Gynécologie">Gynécologie</option>
                        <option value="Médecine Interne">Médecine Interne</option>
                        <option value="Urgences">Urgences</option>
                        <option value="Pédiatrie">Pédiatrie</option>
                    </select>
                </div>
                <div class="field"><label>Date d'anniversaire du sujet</label><input type="date" name="anniv"></div>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="grid-4">
                <div class="field"><label>Niveau d'Étude Professionnel</label>
                    <select name="niveau" required>
                        <option value="A1">Infirmier Gradué (A1)</option>
                        <option value="A0">Infirmier Licencié (A0)</option>
                        <option value="Doc">Médecin</option>
                    </select>
                </div>
                <div class="field"><label>Âge actuel</label><input type="number" name="age"></div>
                <div class="field"><label>Ancienneté (Années)</label><input type="number" name="experience"></div>
            </div>

            <div class="section-title">III. ÉVALUATION DES CONNAISSANCES</div>
            <div class="field">
                <label>1. Quel est l'examen de référence (Gold Standard) pour le dépistage ?</label>
                <select name="k_ref">
                    <option value="0">Échographie mammaire simple</option>
                    <option value="0">La ponction à l'aiguille fine</option>
                    <option value="2">La mammographie bilatérale</option>
                    <option value="0">L'IRM mammaire systématique</option>
                </select>
            </div>
            
            <div class="field">
                <label>2. Quels sont les signes évocateurs d'un cancer du sein ?</label>
                <select name="k_signe">
                    <option value="0">Douleur mammaire bilatérale pendant les règles</option>
                    <option value="1">Un écoulement de lait chez une femme allaitante</option>
                    <option value="2">Un nodule dur, fixe, indolore avec rétraction cutanée</option>
                    <option value="0">Augmentation globale du volume des deux seins</option>
                </select>
            </div>
            

            <div class="section-title">IV. ATTITUDES VIS-À-VIS DU CANCER</div>
            <div class="field">
                <label>3. Selon votre conviction, quelle est la cause réelle ?</label>
                <select name="at_cause">
                    <option value="0">Une punition divine ou un mauvais sort</option>
                    <option value="1">Un choc ou un coup reçu sur le sein</option>
                    <option value="2">Une mutation génétique et facteurs environnementaux</option>
                </select>
            </div>
            <div class="field">
                <label>4. Que pensez-vous du pronostic au stade 1 ?</label>
                <select name="at_pro">
                    <option value="0">La mort est inévitable peu importe le stade</option>
                    <option value="1">La guérison dépend surtout de la foi</option>
                    <option value="2">La guérison est très probable avec un traitement précoce</option>
                </select>
            </div>

            <div class="section-title">V. PRATIQUES PROFESSIONNELLES</div>
            <div class="field">
                <label>5. À quelle fréquence pratiquez-vous l'examen physique des seins ?</label>
                <select name="p_freq">
                    <option value="0">Jamais (Ce n'est pas mon rôle)</option>
                    <option value="1">Seulement si la patiente se plaint</option>
                    <option value="2">Systématiquement pour toute femme en âge de procréer</option>
                </select>
            </div>
            

            <div class="section-title">VI. OBSTACLES AU DÉPISTAGE (PLUSIEURS CHOIX POSSIBLES)</div>
            <div class="check-grid">
                <label><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
                <label><input type="checkbox" name="obs" value="Temps"> Surcharge de travail</label>
                <label><input type="checkbox" name="obs" value="Intimité"> Manque de local isolé</label>
                <label><input type="checkbox" name="obs" value="Coût"> Coût élevé des examens</label>
                <label><input type="checkbox" name="obs" value="Culture"> Croyances culturelles / Refus</label>
                <label><input type="checkbox" name="obs" value="Plateau"> Absence de plateau technique</label>
            </div>

            <div class="section-title">VII. RECOMMANDATIONS</div>
            <textarea name="recom" rows="4" placeholder="Vos solutions pour l'HGRM..."></textarea>

            <button type="button" class="btn-save" onclick="collectData()">Enregistrer la fiche d'enquête</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT GÉNÉRAL (BASE DE DONNÉES)</div>
        <div style="overflow-x:auto;">
            <table id="tableDepouillement">
                <thead>
                    <tr>
                        <th>N° Enquête</th><th>Enquêteur</th><th>Service</th><th>Niveau</th><th>Score Savoir</th><th>Score Attitude</th><th>Score Pratique</th><th>Obstacles</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE DES FRÉQUENCES ET POURCENTAGES</div>
        <div class="grid-4">
            <div class="stats-card"><div>Effectif Total (N)</div><div class="big-num" id="stat-n">0</div></div>
            <div class="stats-card"><div>Connaissances (%)</div><div class="big-num" id="stat-k">0%</div></div>
            <div class="stats-card"><div>Attitudes Positives (%)</div><div class="big-num" id="stat-a">0%</div></div>
            <div class="stats-card"><div>Pratiques Correctes (%)</div><div class="big-num" id="stat-p">0%</div></div>
        </div>

        <div class="section-title">TABLEAUX DES DONNÉES IMPORTANTES</div>
        <div id="dynamic-tables"></div>

        <div class="section-title">REPRÉSENTATIONS GRAPHIQUES</div>
        <div class="chart-box"><canvas id="mainChart"></canvas></div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">SYNTHÈSE ET CONCLUSION GÉNÉRALE</div>
        <div id="finalConclusion" style="background:#fff; padding:20px; border:1px solid #ddd; line-height:1.6;"></div>
        
        <div class="section-title">RECOMMANDATIONS ISSUES DE L'ÉTUDE</div>
        <ul id="finalRecoms" style="line-height:2;"></ul>
    </div>
</div>

<div style="position:fixed; bottom:5px; right:5px; opacity:0.1;">
    <input type="password" oninput="if(this.value==='1398') document.querySelectorAll('.admin-only').forEach(e=>e.style.setProperty('display','block','important'))">
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
    let db = [];
    let myChart = null;

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.content-section')[n-1].classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 3) runAnalysis();
    }

    function collectData() {
        const form = document.getElementById('masterForm');
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        data.obs_list = Array.from(document.querySelectorAll('input[name="obs"]:checked')).map(c => c.value);
        
        db.push(data);
        alert("Enquête n°" + data.n_enquete + " enregistrée avec succès.");
        form.reset();
        updateDepouillement();
    }

    function updateDepouillement() {
        const tbody = document.querySelector('#tableDepouillement tbody');
        tbody.innerHTML = db.map(d => `
            <tr>
                <td>${d.n_enquete}</td><td>${d.enqueteur}</td><td>${d.service}</td><td>${d.niveau}</td>
                <td>${d.k_ref}/2</td><td>${d.at_cause}/2</td><td>${d.p_freq}/2</td><td>${d.obs_list.join(', ')}</td>
            </tr>
        `).join('');
    }

    function runAnalysis() {
        const N = db.length;
        if(N === 0) return;
        document.getElementById('stat-n').innerText = N;

        // Calculs KAP
        let kGood = db.filter(d => d.k_ref == "2").length;
        let aGood = db.filter(d => d.at_pro == "2").length;
        let pGood = db.filter(d => d.p_freq == "2").length;

        document.getElementById('stat-k').innerText = ((kGood/N)*100).toFixed(1) + "%";
        document.getElementById('stat-a').innerText = ((aGood/N)*100).toFixed(1) + "%";
        document.getElementById('stat-p').innerText = ((pGood/N)*100).toFixed(1) + "%";

        // Génération des Tableaux de Fréquence
        const generateTable = (title, field, options) => {
            let html = `<h4>${title}</h4><table><tr><th>Option</th><th>f</th><th>%</th></tr>`;
            options.forEach(opt => {
                let f = db.filter(d => d[field] == opt.v || (Array.isArray(d[field]) && d[field].includes(opt.v))).length;
                html += `<tr><td>${opt.l}</td><td>${f}</td><td>${((f/N)*100).toFixed(1)}%</td></tr>`;
            });
            return html + "</table>";
        };

        let tableHtml = generateTable("Répartition par Service", "service", [
            {v:'Chirurgie', l:'Chirurgie'}, {v:'Gynécologie', l:'Gynécologie'}, 
            {v:'Médecine Interne', l:'Médecine Interne'}, {v:'Urgences', l:'Urgences'}
        ]);
        
        tableHtml += generateTable("Obstacles rencontrés", "obs_list", [
            {v:'Formation', l:'Manque de formation'}, {v:'Temps', l:'Surcharge de travail'},
            {v:'Intimité', l:'Manque de local'}, {v:'Coût', l:'Coût élevé'},
            {v:'Culture', l:'Culture/Refus'}, {v:'Plateau', l:'Absence plateau technique'}
        ]);

        document.getElementById('dynamic-tables').innerHTML = tableHtml;

        // Graphique
        const ctx = document.getElementById('mainChart').getContext('2d');
        if(myChart) myChart.destroy();
        myChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['Connaissances Correctes', 'Attitudes Positives', 'Pratiques Systématiques'],
                datasets: [{
                    label: '% de réussite à l\'HGRM',
                    data: [(kGood/N)*100, (aGood/N)*100, (pGood/N)*100],
                    backgroundColor: ['#f8bbd0', '#f06292', '#b03060']
                }]
            },
            options: { scales: { y: { beginAtZero: true, max: 100 } } }
        });

        // Conclusion & Recoms
        document.getElementById('finalConclusion').innerText = `Sur un échantillon de ${N} personnels, l'étude révèle que la pratique systématique du dépistage reste faible (${((pGood/N)*100).toFixed(1)}%). Les obstacles logistiques et le manque de formation sont les freins majeurs identifiés.`;
        document.getElementById('finalRecoms').innerHTML = db.map(d => d.recom ? `<li>${d.recom}</li>` : '').join('');
    }
</script>
</body>
</html>
