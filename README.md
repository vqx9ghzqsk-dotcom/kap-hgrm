<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Expert-KAP HGRM - Étude de Corrélation</title>
<style>
    body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f0f2f5; margin: 0; padding: 10px; }
    .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.15); }
    .header-tabs { display: flex; background: #fff; border-bottom: 4px solid #b03060; padding: 12px; gap: 8px; position: sticky; top: 0; z-index: 1000; }
    .tab { padding: 12px 20px; font-weight: bold; font-size: 13px; border-radius: 6px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    .admin-only { display: none !important; }
    .content-section { display: none; padding: 30px; }
    .content-section.active { display: block; }
    .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
    .field { display: flex; flex-direction: column; margin-bottom: 20px; }
    label { font-size: 14px; font-weight: 700; margin-bottom: 10px; color: #222; }
    select, input, textarea { padding: 12px; border: 1.5px solid #bbb; border-radius: 8px; font-size: 14px; }
    .grid-ans { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; background: #f9f9f9; padding: 20px; border-radius: 8px; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 10px; font-size: 18px; font-weight: bold; cursor: pointer; transition: 0.3s; }
    .btn-save:hover { background: #8e244d; }
    .corroboration-note { font-size: 11px; color: #d81b60; font-style: italic; margin-top: -5px; margin-bottom: 10px; display: block; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" onclick="showTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab admin-only" onclick="showTab(3)">3. ANALYSE STATISTIQUE</div>
    </div>

    <div id="tab1" class="content-section active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION ET PROFIL (VARIABLES INDÉPENDANTES)</div>
            <div class="grid-ans">
                <div class="field"><label>Code de l'enquêté</label><input type="text" name="id_inf" required placeholder="Ex: INF-HGRM-01"></div>
                <div class="field"><label>Niveau d'Étude</label>
                    <select name="niveau" id="niveau-etude" required>
                        <option value="A1">Gradué (A1)</option>
                        <option value="A0">Licencié (A0)</option>
                        <option value="Doc">Médecin</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté (Années)</label><select name="exp" id="exp-select"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (CROISEMENT SCIENTIFIQUE)</div>
            
            <div class="field">
                <label>1. Quel est l'âge moyen à partir duquel le risque augmente drastiquement ?</label>
                <select name="k_age_risque">
                    <option value="0">Dès la puberté (12-15 ans)</option>
                    <option value="1">Vers 25 ans</option>
                    <option value="2">À partir de 40-50 ans (Réponse correcte)</option>
                </select>
            </div>

            <div class="field">
                <label>2. [Corrélation] Si une patiente a une masse fixe, quel signe cutané recherchez-vous en priorité ?</label>
                <span class="corroboration-note">Corrobore la capacité de diagnostic clinique différentiel.</span>
                <select name="k_corr_signe">
                    <option value="0">Une simple démangeaison</option>
                    <option value="1">Une augmentation de la chaleur locale (Inflammation simple)</option>
                    <option value="2">L'aspect en "peau d'orange" ou une ombilication du mamelon (Signe malin)</option>
                </select>
            </div>
            

            <div class="field">
                <label>3. [Corrélation] Devant une suspicion clinique, quel est le premier examen à réaliser selon vous ?</label>
                <span class="corroboration-note">Corrobore le choix du plateau technique (Écho vs Mammo).</span>
                <select name="k_corr_examen">
                    <option value="0">Une ponction à l'aveugle avec une seringue (Dangereux/Incomplet)</option>
                    <option value="1">Échographie mammaire (Souvent seul choix disponible, mais insuffisant après 40 ans)</option>
                    <option value="2">Mammographie bilatérale couplée à l'échographie (Standard expert)</option>
                </select>
            </div>

            <div class="section-title">III. ATTITUDES ET CONVICTIONS (VARIABLES DE CROISEMENT)</div>
            
            <div class="field">
                <label>1. [Corrélation] Pensez-vous que la mastectomie (ablation) est la seule issue pour tout cancer du sein ?</label>
                <span class="corroboration-note">Évalue le degré d'optimisme thérapeutique et l'attitude face au traitement.</span>
                <select name="att_conv_traitement">
                    <option value="0">Oui, et c'est pour cela que les femmes refusent de venir (Attitude de peur)</option>
                    <option value="1">Non, il existe des traitements conservateurs si on dépiste tôt (Attitude informée)</option>
                    <option value="2">Le traitement dépend du stade TNM et du profil hormonal (Attitude experte)</option>
                </select>
            </div>

            <div class="field">
                <label>2. Que faites-vous si une amie vous confie avoir une boule au sein ?</label>
                <select name="att_personnelle">
                    <option value="0">Je la rassure en lui disant que c'est sûrement bénin (Attitude de déni)</option>
                    <option value="1">Je lui conseille de prier et d'attendre (Attitude culturelle/religieuse)</option>
                    <option value="2">Je l'oblige à consulter immédiatement en milieu hospitalier (Attitude proactive)</option>
                </select>
            </div>

            <div class="section-title">IV. PRATIQUES (VÉRIFICATION DES ACTES)</div>
            
            <div class="field">
                <label>1. [Corrélation] Pendant la palpation, comment disposez-vous la patiente ?</label>
                <span class="corroboration-note">Corrobore la réalité de la pratique (Vérification technique).</span>
                <select name="pra_corr_pos">
                    <option value="0">Uniquement assise sur une chaise</option>
                    <option value="1">Debout, les mains sur les hanches</option>
                    <option value="2">Position couchée (décubitus dorsal) avec le bras relevé (Position optimale de palpation)</option>
                </select>
            </div>
            

            <div class="field">
                <label>2. À quelle fréquence recommandez-vous l'autopalpation à vos patientes ?</label>
                <select name="pra_recom">
                    <option value="0">Jamais, je n'y pense pas</option>
                    <option value="1">Rarement, seulement si elles ont des antécédents</option>
                    <option value="2">À chaque contact infirmier-patiente (Pratique idéale)</option>
                </select>
            </div>

            <div class="section-title">V. OBSTACLES ET RECOMMANDATIONS (VARIABLES D'ACTION)</div>
            
            <div class="field">
                <label>Quel est, selon vous, l'obstacle n°1 à l'HGRM ?</label>
                <select name="obs_principal">
                    <option value="cout">Le coût trop élevé pour la population</option>
                    <option value="formation">Le manque de formation du personnel</option>
                    <option value="tabou">Le tabou lié à la nudité et au corps</option>
                    <option value="materiel">L'absence d'unité de mammographie sur place</option>
                </select>
            </div>

            <div class="field">
                <label>Votre recommandation majeure pour le comité de direction :</label>
                <textarea name="recom" rows="4" placeholder="Ex: Organiser des dépistages gratuits tous les mois..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE ET GÉNÉRER L'ANALYSE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">TABLEAU DE DÉPOUILLEMENT</div>
        <div id="tableContainer"></div>
    </div>

    <div id="tab3" class="content-section">
        <div class="section-title">ANALYSE COMPARATIVE (GRADUÉS vs LICENCIÉS)</div>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
            <canvas id="compareSavoir"></canvas>
            <canvas id="comparePratique"></canvas>
        </div>
        <div id="conclusionAutomatique" style="margin-top:30px; padding:20px; background:#e8f5e9; border-radius:10px;"></div>
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
        if(n===3) generateAnalysis();
    }

    function saveData() {
        const form = document.getElementById('kapForm');
        if(!form.checkValidity()) { alert("Champs manquants !"); return; }
        
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        
        // Scores pour les croisements
        data.scoreS = parseInt(data.k_age_risque||0) + parseInt(data.k_corr_signe||0) + parseInt(data.k_corr_examen||0);
        data.scoreP = parseInt(data.pra_corr_pos||0) + parseInt(data.pra_recom||0);
        
        db.push(data);
        alert("Données sauvegardées ! Total fiches : " + db.length);
        form.reset();
        renderTable();
    }

    function renderTable() {
        let html = `<table><tr><th>ID</th><th>Niveau</th><th>Score Savoir</th><th>Score Pratique</th></tr>`;
        db.forEach(d => {
            html += `<tr><td>${d.id_inf}</td><td>${d.niveau}</td><td>${d.scoreS}/6</td><td>${d.scoreP}/4</td></tr>`;
        });
        document.getElementById('tableContainer').innerHTML = html + `</table>`;
    }

    function generateAnalysis() {
        if(db.length === 0) return;
        
        const a1 = db.filter(d => d.niveau === 'A1');
        const a0 = db.filter(d => d.niveau === 'A0');

        const avgA1 = a1.reduce((sum, d) => sum + d.scoreS, 0) / a1.length || 0;
        const avgA0 = a0.reduce((sum, d) => sum + d.scoreS, 0) / a0.length || 0;

        const ctx = document.getElementById('compareSavoir').getContext('2d');
        new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['Gradués (A1)', 'Licenciés (A0)'],
                datasets: [{ label: 'Performance Savoir', data: [avgA1, avgA0], backgroundColor: ['#f8bbd0', '#b03060'] }]
            }
        });

        document.getElementById('conclusionAutomatique').innerHTML = `
            <h3>Conclusion Statistique Préliminaire</h3>
            <p>On observe que le niveau <b>${avgA0 > avgA1 ? 'A0' : 'A1'}</b> possède une meilleure maîtrise théorique.</p>
            <p>Cependant, le croisement avec les obstacles montre que <b>${db.filter(d=>d.obs_principal==='materiel').length}</b> enquêtés pointent le manque de matériel comme frein majeur.</p>
        `;
    }

    window.onload = () => {
        for(let i=20; i<=65; i++) document.getElementById('exp-select').options.add(new Option(i+" ans", i));
    };
</script>
</body>
</html>
