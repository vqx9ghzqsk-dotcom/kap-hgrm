<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Système Expert CAP - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --accent: #db2777; --bg: #f8fafc; --text: #334155; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background-color: var(--bg); color: var(--text); margin: 0; padding: 0; }
        .container { max-width: 1100px; margin: 20px auto; padding: 20px; }
        
        /* Navigation par onglets */
        .nav-tabs { display: flex; flex-wrap: wrap; gap: 5px; background: #e2e8f0; padding: 5px; border-radius: 10px; sticky; top: 0; z-index: 100; }
        .tab-btn { flex: 1; padding: 12px; border: none; border-radius: 8px; cursor: pointer; font-weight: 600; transition: 0.3s; color: #475569; }
        .tab-btn.active { background: var(--primary); color: white; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); }

        /* Sections */
        .page { display: none; background: white; padding: 30px; border-radius: 12px; margin-top: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
        .page.active { display: block; }
        
        h1, h2 { color: var(--secondary); border-bottom: 2px solid var(--primary); padding-bottom: 10px; }
        h3 { color: var(--primary); margin-top: 25px; border-left: 4px solid var(--primary); padding-left: 10px; background: #fff1f2; padding-top: 5px; padding-bottom: 5px; }

        /* Formulaire Collecte */
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
        .field { margin-bottom: 15px; }
        label { display: block; font-weight: 600; margin-bottom: 5px; font-size: 0.9em; }
        input, select, textarea { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 6px; box-sizing: border-box; }
        .radio-group { display: flex; gap: 15px; flex-wrap: wrap; margin-top: 5px; }
        
        /* Analyse & Résultats */
        .stats-card { background: #f1f5f9; border-radius: 8px; padding: 20px; margin-bottom: 20px; border-top: 4px solid var(--primary); }
        .metric { font-size: 2em; font-weight: bold; color: var(--primary); }
        .chart-sim { height: 20px; background: #e2e8f0; border-radius: 10px; margin-top: 10px; overflow: hidden; }
        .chart-bar { height: 100%; background: var(--primary); }

        .btn-action { background: var(--primary); color: white; border: none; padding: 15px 30px; border-radius: 8px; font-weight: bold; cursor: pointer; width: 100%; font-size: 1.1em; }
        .btn-action:hover { background: var(--accent); }
        
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { border: 1px solid #e2e8f0; padding: 10px; text-align: left; }
        th { background: #f8fafc; color: var(--secondary); }
    </style>
</head>
<body>

<div class="container">
    <div class="nav-tabs">
        <button class="tab-btn active" onclick="openPage('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="tab-btn" onclick="openPage('traitement')">2. DÉPOUILLEMENT & TRAITEMENT</button>
        <button class="tab-btn" onclick="openPage('resultats')">3. PRÉSENTATION DES RÉSULTATS</button>
        <button class="tab-btn" onclick="openPage('discussion')">4. ANALYSE & DISCUSSION</button>
        <button class="tab-btn" onclick="openPage('conclusion')">5. CONCLUSION & RECOMMANDATIONS</button>
    </div>

    <div id="recolte" class="page active">
        <h1>Collecte de Données (HGRM Makala)</h1>
        <form id="formCollecte">
            <h3>I. Identification & Consentement</h3>
            <div class="grid">
                <div class="field"><label>Code :</label><input type="text" name="code" placeholder="Ex: INF-01"></div>
                <div class="field"><label>Date :</label><input type="date" name="date_recolte"></div>
                <div class="field"><label>Service :</label><input type="text" name="service"></div>
                <div class="field"><label>Consentement :</label>
                    <select name="consentement"><option value="Oui">Accepté</option><option value="Non">Refusé</option></select>
                </div>
            </div>

            <h3>II. Profil Sociodémographique</h3>
            <div class="grid">
                <div class="field"><label>Sexe :</label><select name="sexe"><option>Femme</option><option>Homme</option></select></div>
                <div class="field"><label>Âge :</label><input type="number" name="age"></div>
                <div class="field"><label>Niveau d'études :</label>
                    <select name="niveau"><option value="A2">A2</option><option value="A1">A1</option><option value="A0">A0</option><option value="Master">Master</option></select>
                </div>
                <div class="field"><label>Expérience (Années) :</label><input type="number" name="experience"></div>
            </div>

            <h3>III. Connaissances (Exemple Variables)</h3>
            <div class="field">
                <label>Le risque augmente avec l'âge ?</label>
                <div class="radio-group">
                    <label><input type="radio" name="c_age" value="Vrai"> Vrai</label>
                    <label><input type="radio" name="c_age" value="Faux"> Faux</label>
                    <label><input type="radio" name="c_age" value="NSP"> NSP</label>
                </div>
            </div>
            
            <h3>IV. Pratiques</h3>
            <div class="field">
                <label>Enseignez-vous l'autopalpation aux patientes ?</label>
                <div class="radio-group">
                    <label><input type="radio" name="p_enseigne" value="Oui"> Oui</label>
                    <label><input type="radio" name="p_enseigne" value="Non"> Non</label>
                </div>
            </div>

            <button type="button" class="btn-action" onclick="sauvegarderDonnees()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="traitement" class="page">
        <h1>Dépouillement & Codage</h1>
        <div class="stats-card">
            <h3>Base de données brute</h3>
            <div id="tableContainer">Aucune donnée saisie.</div>
        </div>
        <div class="stats-card">
            <h3>Codage des variables (Matrice)</h3>
            <p><i>Transformation : Oui=1, Non=0 | A0=3, A1=2, A2=1</i></p>
            <div id="codageContainer"></div>
        </div>
    </div>

    <div id="resultats" class="page">
        <h1>Présentation des Résultats</h1>
        <div class="grid">
            <div class="stats-card">
                <h3>Niveau de Connaissances</h3>
                <div class="metric" id="res_con">0%</div>
                <p>Taux de réponses correctes (Savoir)</p>
                <div class="chart-sim"><div id="bar_con" class="chart-bar" style="width: 0%;"></div></div>
            </div>
            <div class="stats-card">
                <h3>Pratiques Effectives</h3>
                <div class="metric" id="res_prat">0%</div>
                <p>Application de l'enseignement AES</p>
                <div class="chart-sim"><div id="bar_prat" class="chart-bar" style="width: 0%;"></div></div>
            </div>
        </div>
    </div>

    <div id="discussion" class="page">
        <h1>Analyse et Discussion</h1>
        <div class="stats-card">
            <h3>Analyse Bivariée (Croisement)</h3>
            <p id="analyse_texte">En attente de données pour corréler le <b>Niveau d'étude</b> avec la <b>Pratique</b>.</p>
        </div>
        <div class="stats-card">
            <h3>Discussion théorique</h3>
            <p><i>Comparaison avec les données de la littérature (OMS, Etudes RDC)...</i></p>
            <textarea style="height:150px" placeholder="Saisissez vos commentaires ici..."></textarea>
        </div>
    </div>

    <div id="conclusion" class="page">
        <h1>Conclusion & Recommandations</h1>
        <div class="stats-card" style="border-top-color: #10b981;">
            <h3>Conclusion Générale</h3>
            <p id="concl_gen">Le diagnostic montre un écart entre...</p>
        </div>
        <div class="stats-card" style="border-top-color: #f59e0b;">
            <h3>Recommandations Spécifiques (HGRM)</h3>
            <ul id="reco_list">
                <li>Renforcer la formation continue du personnel infirmier.</li>
                <li>Mettre à disposition des outils didactiques.</li>
            </ul>
        </div>
    </div>
</div>

<script>
    let database = JSON.parse(localStorage.getItem('memo_makala_db')) || [];

    function openPage(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        
        if(id === 'traitement') afficherDépouillement();
        if(id === 'resultats') calculerResultats();
        if(id === 'discussion') genererAnalyse();
    }

    function sauvegarderDonnees() {
        const form = document.getElementById('formCollecte');
        const data = Object.fromEntries(new FormData(form).entries());
        database.push(data);
        localStorage.setItem('memo_makala_db', JSON.stringify(database));
        alert("Fiche ajoutée au dépouillement !");
        form.reset();
    }

    function afficherDépouillement() {
        let html = "<table><tr><th>Code</th><th>Age</th><th>Niveau</th><th>C_Age</th><th>P_Ens</th></tr>";
        database.forEach(d => {
            html += `<tr><td>${d.code}</td><td>${d.age}</td><td>${d.niveau}</td><td>${d.c_age}</td><td>${d.p_enseigne}</td></tr>`;
        });
        html += "</table>";
        document.getElementById('tableContainer').innerHTML = html;
    }

    function calculerResultats() {
        const total = database.length;
        if(total === 0) return;

        const correctCon = database.filter(d => d.c_age === 'Vrai').length;
        const correctPrat = database.filter(d => d.p_enseigne === 'Oui').length;

        const pourcCon = (correctCon / total * 100).toFixed(1);
        const pourcPrat = (correctPrat / total * 100).toFixed(1);

        document.getElementById('res_con').innerText = pourcCon + "%";
        document.getElementById('bar_con').style.width = pourcCon + "%";
        document.getElementById('res_prat').innerText = pourcPrat + "%";
        document.getElementById('bar_prat').style.width = pourcPrat + "%";
    }

    function genererAnalyse() {
        const total = database.length;
        if(total < 2) return;
        document.getElementById('analyse_texte').innerHTML = `Sur un échantillon de <b>${total}</b> infirmières, le croisement des données suggère que le niveau de pratique est de ${document.getElementById('res_prat').innerText}.`;
    }
</script>
</body>
</html>
