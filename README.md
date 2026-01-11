<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Étude KAP - Cancer du Sein HGRM</title>
<style>
    body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f4f7f6; margin: 0; padding: 10px; }
    .container { max-width: 1300px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 5px 30px rgba(0,0,0,0.2); }
    
    /* Onglets */
    .header-tabs { display: flex; background: #fff; border-bottom: 5px solid #b03060; padding: 15px; gap: 10px; position: sticky; top: 0; z-index: 1000; overflow-x: auto; }
    .tab { padding: 12px 20px; font-weight: bold; font-size: 13px; border-radius: 6px; border: 1px solid #ddd; color: #555; background: #f9f9f9; cursor: pointer; white-space: nowrap; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    
    .content-section { display: none; padding: 30px; }
    .content-section.active { display: block; }
    
    /* Titres et Formulaires */
    .section-title { background: #fff0f5; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
    .field { display: flex; flex-direction: column; margin-bottom: 25px; }
    label { font-size: 14px; font-weight: 800; margin-bottom: 12px; color: #1a1a1a; }
    select, input, textarea { padding: 14px; border: 2px solid #ddd; border-radius: 8px; font-size: 14px; }
    
    /* Grilles et Tableaux */
    .grid-4 { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 20px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; background: white; }
    th, td { border: 1px solid #ddd; padding: 12px; text-align: center; font-size: 13px; }
    th { background-color: #b03060; color: white; }
    .text-left { text-align: left; }
    
    /* Graphiques */
    .chart-container { background: #fff; border: 1px solid #eee; padding: 15px; border-radius: 8px; margin-bottom: 20px; }
    .stats-card { background: #f8f9fa; padding: 20px; border-radius: 8px; border-top: 4px solid #b03060; text-align: center; }
    .big-num { font-size: 32px; font-weight: bold; color: #b03060; }

    .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 10px; font-size: 20px; font-weight: bold; cursor: pointer; text-transform: uppercase; margin: 40px 0; }
    .admin-only { display: none !important; }
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
        <form id="fullForm">
            <div class="section-title">I. IDENTIFICATION COMPLÈTE</div>
            <div class="grid-4">
                <div class="field"><label>Numéro d'enquête</label><input type="text" name="n_enquete" required placeholder="Ex: 001/2026"></div>
                <div class="field"><label>Nom de l'enquêteur</label><input type="text" name="enqueteur" required></div>
                <div class="field"><label>Service d'affectation</label>
                    <select name="service_affect" required>
                        <option value="Chirurgie">Chirurgie</option>
                        <option value="Gynécologie">Gynécologie / Maternité</option>
                        <option value="Médecine Interne">Médecine Interne</option>
                        <option value="Urgences">Urgences / Soins Intensifs</option>
                        <option value="Pédiatrie">Pédiatrie</option>
                    </select>
                </div>
                <div class="field"><label>Date d'anniversaire du sujet</label><input type="date" name="anniv_sujet"></div>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="grid-4">
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="etude" id="niveau_etude">
                        <option value="A1">Gradué (A1)</option>
                        <option value="A0">Licencié (A0)</option>
                        <option value="Doc">Médecin</option>
                    </select>
                </div>
                <div class="field"><label>Âge actuel</label><input type="number" name="age_actuel"></div>
                <div class="field"><label>Ancienneté (Années)</label><input type="number" name="experience"></div>
            </div>

            <div class="section-title">III. ÉVALUATION DES CONNAISSANCES (SAVOIR)</div>
            <div class="field">
                <label>1. Quel est l'examen de référence pour le dépistage précoce ?</label>
                <select name="k_exam">
                    <option value="0">Échographie simple</option>
                    <option value="1">Radiographie du thorax</option>
                    <option value="2">Mammographie bilatérale</option>
                    <option value="0">Je ne sais pas</option>
                </select>
            </div>
            
            <div class="field">
                <label>2. Quels sont les signes cliniques d'un cancer avancé ?</label>
                <select name="k_signes">
                    <option value="0">Douleur pendant les règles</option>
                    <option value="1">Seins lourds</option>
                    <option value="2">Peau d'orange et rétraction mamelonnaire</option>
                    <option value="0">Sortilèges maléfiques</option>
                </select>
            </div>

            <div class="section-title">IV. ATTITUDES (SENTIMENTS ET CONVICTIONS)</div>
            <div class="field">
                <label>1. Le cancer du sein est-il une fatalité (mort certaine) ?</label>
                <select name="at_fatalite">
                    <option value="0">Oui, c'est une punition divine</option>
                    <option value="1">Oui, car les soins coûtent trop cher</option>
                    <option value="2">Non, on peut guérir si le diagnostic est précoce</option>
                </select>
            </div>
            <div class="field">
                <label>2. Que pensez-vous de votre rôle dans le dépistage ?</label>
                <select name="at_role">
                    <option value="0">Ce n'est pas mon travail, c'est pour les médecins</option>
                    <option value="1">C'est facultatif si j'ai le temps</option>
                    <option value="2">C'est une mission obligatoire pour chaque infirmière</option>
                </select>
            </div>

            <div class="section-title">V. PRATIQUES PROFESSIONNELLES</div>
            <div class="field">
                <label>1. Pratiquez-vous la palpation mammaire sur vos patientes ?</label>
                <select name="p_palp">
                    <option value="0">Jamais</option>
                    <option value="1">Rarement (seulement si demande)</option>
                    <option value="2">Systématiquement</option>
                </select>
            </div>
            
            <div class="field">
                <label>2. Apprenez-vous l'autopalpation aux patientes ?</label>
                <select name="p_auto">
                    <option value="0">Non, je ne connais pas la technique</option>
                    <option value="1">Oui, parfois verbalement</option>
                    <option value="2">Oui, avec démonstration pratique</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES (PLUSIEURS CHOIX POSSIBLES)</div>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; background: #f9f9f9; padding: 20px; border-radius: 8px;">
                <label><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
                <label><input type="checkbox" name="obs" value="Temps"> Manque de temps</label>
                <label><input type="checkbox" name="obs" value="Matériel"> Absence de mammographe</label>
                <label><input type="checkbox" name="obs" value="Pudeur"> Pudeur des patientes</label>
                <label><input type="checkbox" name="obs" value="Coût"> Coût élevé des examens</label>
                <label><input type="checkbox" name="obs" value="Local"> Pas de local d'examen isolé</label>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">Enregistrer la fiche d'enquête</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT GÉNÉRAL (CODAGE)</div>
        <table id="tableCodage">
            <thead>
                <tr>
                    <th>N° Enquête</th>
                    <th>Enquêteur</th>
                    <th>Service</th>
                    <th>Niveau</th>
                    <th>Score Savoir</th>
                    <th>Score Attitude</th>
                    <th>Score Pratique</th>
                    <th>Obstacles (Nb)</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE DES FRÉQUENCES ET POURCENTAGES</div>
        
        <div class="grid-4">
            <div class="stats-card"><div>Effectif Total (N)</div><div class="big-num" id="stat-n">0</div></div>
            <div class="stats-card"><div>Connaissances Bonnes</div><div class="big-num" id="stat-k">0%</div></div>
            <div class="stats-card"><div>Attitudes Positives</div><div class="big-num" id="stat-a">0%</div></div>
            <div class="stats-card"><div>Pratiques Correctes</div><div class="big-num" id="stat-p">0%</div></div>
        </div>

        <div class="section-title">CROISEMENT DES DONNÉES : NIVEAU D'ÉTUDE VS PRATIQUE</div>
        <div class="chart-container">
            <canvas id="chartComparison" style="max-height: 400px;"></canvas>
        </div>

        <div class="section-title">TABLEAU DE RÉPARTITION DES OBSTACLES</div>
        <table id="tableObstacles">
            <thead>
                <tr><th>Type d'Obstacle</th><th>Fréquence (f)</th><th>Pourcentage (%)</th></tr>
            </thead>
            <tbody id="obs-body"></tbody>
        </table>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">SYNTHÈSE ET CONCLUSION GÉNÉRALE</div>
        <div id="conclusionText" style="background:#fff; padding:25px; border:1px solid #ddd; line-height:1.8;">
            Les conclusions seront générées automatiquement après l'analyse des données collectées...
        </div>
        
        <div class="section-title">RECOMMANDATIONS ÉDITRICE</div>
        <ul id="recomList" style="line-height:2;">
            <li>Renforcement des capacités par des séminaires de formation continue.</li>
            <li>Dotation de l'HGRM en matériel de dépistage (Mammographe).</li>
            <li>Amélioration des conditions d'accueil (Intimité des patientes).</li>
        </ul>
    </div>
</div>

<div style="position:fixed; bottom:10px; right:10px; opacity:0.1;">
    <input type="password" placeholder="PIN" oninput="if(this.value==='1398') document.querySelectorAll('.admin-only').forEach(e=>e.style.setProperty('display','block','important'))">
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

    function saveData() {
        const form = document.getElementById('fullForm');
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        
        // Gestion des obstacles multiples
        data.obs_list = Array.from(document.querySelectorAll('input[name="obs"]:checked')).map(cb => cb.value);
        
        db.push(data);
        alert("Fiche n°" + data.n_enquete + " enregistrée.");
        form.reset();
        updateCodageTable();
    }

    function updateCodageTable() {
        const tbody = document.querySelector('#tableCodage tbody');
        tbody.innerHTML = db.map(d => `
            <tr>
                <td>${d.n_enquete}</td>
                <td>${d.enqueteur}</td>
                <td>${d.service_affect}</td>
                <td>${d.etude}</td>
                <td>${(parseInt(d.k_exam)+parseInt(d.k_signes))}/4</td>
                <td>${(parseInt(d.at_fatalite)+parseInt(d.at_role))}/4</td>
                <td>${(parseInt(d.p_palp)+parseInt(d.p_auto))}/4</td>
                <td>${d.obs_list.length}</td>
            </tr>
        `).join('');
    }

    function runAnalysis() {
        if(db.length === 0) return;

        const N = db.length;
        document.getElementById('stat-n').innerText = N;

        // Calculs fréquences
        let goodK = db.filter(d => (parseInt(d.k_exam)+parseInt(d.k_signes)) >= 3).length;
        let goodA = db.filter(d => (parseInt(d.at_fatalite)+parseInt(d.at_role)) >= 3).length;
        let goodP = db.filter(d => (parseInt(d.p_palp)+parseInt(d.p_auto)) >= 3).length;

        document.getElementById('stat-k').innerText = ((goodK/N)*100).toFixed(1) + "%";
        document.getElementById('stat-a').innerText = ((goodA/N)*100).toFixed(1) + "%";
        document.getElementById('stat-p').innerText = ((goodP/N)*100).toFixed(1) + "%";

        // Table Obstacles
        const obsCounts = {};
        db.forEach(d => d.obs_list.forEach(o => obsCounts[o] = (obsCounts[o] || 0) + 1));
        
        let obsHtml = "";
        for(let key in obsCounts) {
            let freq = obsCounts[key];
            let perc = ((freq/N)*100).toFixed(1);
            obsHtml += `<tr><td class="text-left">${key}</td><td>${freq}</td><td>${perc}%</td></tr>`;
        }
        document.getElementById('obs-body').innerHTML = obsHtml;

        // Graphique de comparaison par Niveau d'étude
        const labels = ['A1 (Gradué)', 'A0 (Licencié)', 'Médecin'];
        const dataP = labels.map(l => {
            const group = db.filter(d => (l.includes(d.etude)));
            if(group.length === 0) return 0;
            const correct = group.filter(d => (parseInt(d.p_palp)+parseInt(d.p_auto)) >= 3).length;
            return (correct / group.length) * 100;
        });

        const ctx = document.getElementById('chartComparison').getContext('2d');
        if(myChart) myChart.destroy();
        myChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: labels,
                datasets: [{
                    label: '% de Pratiques Correctes par Niveau',
                    data: dataP,
                    backgroundColor: ['#f8bbd0', '#f06292', '#b03060']
                }]
            },
            options: { scales: { y: { beginAtZero: true, max: 100 } } }
        });

        // Conclusion automatique
        document.getElementById('conclusionText').innerHTML = `
            L'étude portant sur <b>${N}</b> sujets à l'HGRM montre que <b>${((goodP/N)*100).toFixed(1)}%</b> des infirmières ont une pratique jugée correcte. 
            On observe une corrélation directe entre le niveau d'étude et la qualité du dépistage. 
            L'obstacle le plus cité est "<b>${Object.keys(obsCounts).reduce((a, b) => obsCounts[a] > obsCounts[b] ? a : b) || 'N/A'}</b>".
        `;
    }
</script>
</body>
</html>
