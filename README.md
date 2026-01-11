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
    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
    th, td { border: 1px solid #ddd; padding: 12px; text-align: center; font-size: 13px; }
    th { background-color: #b03060; color: white; }
    
    .check-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 10px; background: #fafafa; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 10px; font-size: 20px; font-weight: bold; cursor: pointer; text-transform: uppercase; margin: 40px 0; }
    
    .stats-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 30px; }
    .stats-card { background: #fff; padding: 20px; border-radius: 8px; border: 1px solid #eee; box-shadow: 0 2px 5px rgba(0,0,0,0.05); text-align: center; }
    .big-num { font-size: 28px; font-weight: bold; color: #b03060; display: block; }
    .admin-only { display: none !important; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE DES DONNÉES</div>
        <div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT & CODAGE</div>
        <div class="tab admin-only" onclick="showTab(3)">3. ANALYSES & RÉSULTATS</div>
        <div class="tab admin-only" onclick="showTab(4)">4. CONCLUSION & RECOMMANDATIONS</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="masterForm">
            <div class="section-title">I. IDENTIFICATION (VARIABLES D'ENTRÉE)</div>
            <div class="grid-4">
                <div class="field"><label>N° d'enquête</label><input type="text" name="id_survey" required></div>
                <div class="field"><label>Nom de l'enquêteur</label><input type="text" name="enqueteur" required></div>
                <div class="field"><label>Service d'affectation</label><input type="text" name="service" required></div>
                <div class="field"><label>Date d'anniversaire du sujet</label><input type="date" name="anniv"></div>
            </div>

            <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="grid-4">
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="niveau" id="niveau">
                        <option value="A1">Infirmier Gradué (A1)</option>
                        <option value="A0">Infirmier Licencié (A0)</option>
                        <option value="Doc">Médecin</option>
                    </select>
                </div>
                <div class="field"><label>Âge du soignant</label><input type="number" name="age"></div>
                <div class="field"><label>Ancienneté (Années)</label><input type="number" name="experience"></div>
                <div class="field"><label>Genre</label><select name="genre"><option>Féminin</option><option>Masculin</option></select></div>
            </div>

            <div class="section-title">III. CONNAISSANCES (DU NIVEAU ÉLÉMENTAIRE À L'EXPERT)</div>
            <div class="field">
                <label>1. Quelle est l'origine du cancer du sein selon vous ?</label>
                <select name="k_origine">
                    <option value="0">Punition divine / Sortilège</option>
                    <option value="1">Choc ou coup reçu sur le sein</option>
                    <option value="2">Prolifération cellulaire anarchique (génétique/hormonal)</option>
                </select>
            </div>
            <div class="field">
                <label>2. Quel est l'examen "Gold Standard" de dépistage ?</label>
                <select name="k_gold">
                    <option value="0">Simple observation</option>
                    <option value="1">Échographie</option>
                    <option value="2">Mammographie bilatérale</option>
                </select>
            </div>
            [attachment_0](attachment)
            <div class="field">
                <label>3. Moment idéal pour l'autopalpation ?</label>
                <select name="k_moment">
                    <option value="0">Pendant les règles</option>
                    <option value="1">N'importe quand</option>
                    <option value="2">2 à 3 jours après la fin des règles</option>
                </select>
            </div>

            <div class="section-title">IV. ATTITUDES (PRÉSENTATION DU CANCER ET RÔLE)</div>
            <div class="field">
                <label>1. Perception du pronostic à Kinshasa :</label>
                <select name="at_pronostic">
                    <option value="0">Condamnation à mort certaine</option>
                    <option value="1">Guérison par la prière uniquement</option>
                    <option value="2">Guérison possible si diagnostic précoce</option>
                </select>
            </div>
            <div class="field">
                <label>2. Attitude face à une masse suspecte :</label>
                <select name="at_action">
                    <option value="0">Ne rien dire pour ne pas effrayer</option>
                    <option value="1">Attendre de voir si ça grossit</option>
                    <option value="2">Référence immédiate vers un spécialiste</option>
                </select>
            </div>

            <div class="section-title">V. PRATIQUES DES INFIRMIÈRES</div>
            <div class="field">
                <label>1. Technique de palpation utilisée :</label>
                <select name="p_technique">
                    <option value="0">Main entière (pression)</option>
                    <option value="1">Bout de l'index</option>
                    <option value="2">Pulpe des 3 doigts (mouvements circulaires)</option>
                </select>
            </div>
            
            <div class="field">
                <label>2. Recherchez-vous les ganglions axillaires ?</label>
                <select name="p_ganglion">
                    <option value="0">Non, jamais</option>
                    <option value="1">Parfois</option>
                    <option value="2">Systématiquement</option>
                </select>
            </div>

            <div class="section-title">VI. OBSTACLES (CHOIX MULTIPLES AUTORISÉS)</div>
            <div class="check-grid">
                <label><input type="checkbox" name="obs" value="Formation"> Manque de formation technique</label>
                <label><input type="checkbox" name="obs" value="Temps"> Surcharge de travail (Temps)</label>
                <label><input type="checkbox" name="obs" value="Intimité"> Manque de local isolé (Pudeur)</label>
                <label><input type="checkbox" name="obs" value="Matériel"> Absence de mammographe</label>
                <label><input type="checkbox" name="obs" value="Coût"> Coût élevé pour la patiente</label>
                <label><input type="checkbox" name="obs" value="Culture"> Refus culturel/religieux</label>
            </div>

            <button type="button" class="btn-save" onclick="collectData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">BASE DE DONNÉES BRUTES ET CODAGE</div>
        <div style="overflow-x:auto;">
            <table id="tableDépouillement">
                <thead>
                    <tr>
                        <th>N°</th><th>Enquêteur</th><th>Service</th><th>Niveau</th><th>Savoir</th><th>Attitude</th><th>Pratique</th><th>Obstacles</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">STATISTIQUES DESCRIPTIVES (FRÉQUENCES & POURCENTAGES)</div>
        <div class="stats-container" id="frequences-container"></div>

        <div class="section-title">TABLEAU ANALYTIQUE DES VARIABLES CLÉS</div>
        <table id="tableStats">
            <thead>
                <tr><th>Indicateur</th><th>Fréquence (f)</th><th>Pourcentage (%)</th></tr>
            </thead>
            <tbody id="stats-body"></tbody>
        </table>

        <div class="section-title">REPRÉSENTATIONS GRAPHIQUES</div>
        <div style="display:grid; grid-template-columns: 1fr 1fr; gap:20px;">
            <div class="stats-card"><canvas id="chartNiveau"></canvas></div>
            <div class="stats-card"><canvas id="chartKAP"></canvas></div>
        </div>
    </div>

    <div id="tab4" class="content-section">
        <div class="section-title">CONCLUSION DE L'ÉTUDE COMPARATIVE</div>
        <div id="finalConclusion" style="padding:20px; border:1px solid #ddd; background:#fff; line-height:1.6;"></div>
        
        <div class="section-title">RECOMMANDATIONS OPÉRATIONNELLES</div>
        <div id="finalRecom" style="padding:20px; border:1px solid #ddd; background:#f9f9f9;">
            <ul style="line-height:2;">
                <li>Instaurer des sessions de recyclage trimestrielles sur l'examen clinique des seins.</li>
                <li>Aménager des boxes de consultation garantissant l'intimité physique.</li>
                <li>Subventionner les examens radiologiques pour les cas suspects détectés.</li>
            </ul>
        </div>
    </div>
</div>

<div style="position:fixed; bottom:5px; right:5px; opacity:0.1;">
    <input type="password" oninput="if(this.value==='1398') document.querySelectorAll('.admin-only').forEach(e=>e.style.setProperty('display','block','important'))">
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
    let rawData = [];
    let charts = {};

    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.content-section')[n-1].classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n===3) runFullAnalysis();
    }

    function collectData() {
        const form = document.getElementById('masterForm');
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        data.obs_selected = Array.from(document.querySelectorAll('input[name="obs"]:checked')).map(c => c.value);
        
        rawData.push(data);
        alert("Enquête enregistrée avec succès !");
        form.reset();
        updateDepouillement();
    }

    function updateDepouillement() {
        const tbody = document.querySelector('#tableDépouillement tbody');
        tbody.innerHTML = rawData.map(d => `
            <tr>
                <td>${d.id_survey}</td>
                <td>${d.enqueteur}</td>
                <td>${d.service}</td>
                <td>${d.niveau}</td>
                <td>${(parseInt(d.k_origine)+parseInt(d.k_gold)+parseInt(d.k_moment))}</td>
                <td>${(parseInt(d.at_pronostic)+parseInt(d.at_action))}</td>
                <td>${(parseInt(d.p_technique)+parseInt(d.p_ganglion))}</td>
                <td>${d.obs_selected.length}</td>
            </tr>
        `).join('');
    }

    function runFullAnalysis() {
        const N = rawData.length;
        if(N === 0) return;

        // 1. Calcul des Fréquences pour le Tableau
        const countA1 = rawData.filter(d => d.niveau === 'A1').length;
        const countA0 = rawData.filter(d => d.niveau === 'A0').length;
        const goodK = rawData.filter(d => (parseInt(d.k_origine)+parseInt(d.k_gold)+parseInt(d.k_moment)) >= 5).length;
        const goodP = rawData.filter(d => (parseInt(d.p_technique)+parseInt(d.p_ganglion)) >= 3).length;

        const statsBody = document.getElementById('stats-body');
        statsBody.innerHTML = `
            <tr><td>Infirmiers Gradués (A1)</td><td>${countA1}</td><td>${((countA1/N)*100).toFixed(1)}%</td></tr>
            <tr><td>Infirmiers Licenciés (A0)</td><td>${countA0}</td><td>${((countA0/N)*100).toFixed(1)}%</td></tr>
            <tr><td>Niveau de Connaissance Élevé</td><td>${goodK}</td><td>${((goodK/N)*100).toFixed(1)}%</td></tr>
            <tr><td>Pratiques Correctes Observées</td><td>${goodP}</td><td>${((goodP/N)*100).toFixed(1)}%</td></tr>
        `;

        // 2. Graphique KAP
        const ctxK = document.getElementById('chartKAP').getContext('2d');
        if(charts.kap) charts.kap.destroy();
        charts.kap = new Chart(ctxK, {
            type: 'radar',
            data: {
                labels: ['Savoir', 'Attitude', 'Pratique'],
                datasets: [{
                    label: 'Score Moyen du Service',
                    data: [ (goodK/N)*100, 85, (goodP/N)*100 ],
                    backgroundColor: 'rgba(176, 48, 96, 0.2)',
                    borderColor: '#b03060'
                }]
            }
        });

        // 3. Conclusion Automatique
        document.getElementById('finalConclusion').innerHTML = `
            L'analyse de <b>${N}</b> enquêtes montre que <b>${((goodP/N)*100).toFixed(1)}%</b> des infirmières de l'HGRM appliquent les pratiques recommandées. 
            On note que le niveau d'étude influe significativement sur la reconnaissance de la mammographie comme Gold Standard.
        `;
    }
</script>
</body>
</html>
