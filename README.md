<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Application CAP - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', Tahoma, sans-serif; background: var(--bg); color: #334155; margin: 0; padding: 10px; }
        .container { max-width: 1200px; margin: auto; background: white; padding: 30px; border-radius: 15px; box-shadow: 0 5px 25px rgba(0,0,0,0.1); }
        
        /* Navigation */
        .tabs { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 25px; border-bottom: 2px solid #e2e8f0; padding-bottom: 10px; sticky; top: 0; background: white; z-index: 1000; }
        .tab-btn { padding: 12px 20px; border: none; background: #e2e8f0; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .tab-btn.active { background: var(--primary); color: white; }

        .page { display: none; }
        .page.active { display: block; }

        /* Formulaire */
        h2 { color: var(--primary); background: #fff1f2; padding: 12px; border-left: 6px solid var(--primary); font-size: 1.1em; margin-top: 25px; text-transform: uppercase; }
        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; }
        .field-box { border: 1px solid #e2e8f0; padding: 15px; border-radius: 8px; background: #fff; }
        label { display: block; font-weight: 600; margin-bottom: 8px; font-size: 0.95em; }
        input[type="text"], input[type="number"], input[type="date"], select, textarea { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 5px; box-sizing: border-box; }
        .check-list { display: flex; flex-direction: column; gap: 8px; }
        
        /* Tableaux & Stats */
        .table-container { overflow-x: auto; margin-top: 20px; }
        table { width: 100%; border-collapse: collapse; font-size: 0.85em; }
        th, td { border: 1px solid #cbd5e1; padding: 10px; text-align: left; }
        th { background: #f1f5f9; position: sticky; top: 0; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px; }
        .stat-card { background: white; border-top: 4px solid var(--primary); padding: 20px; text-align: center; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .stat-val { font-size: 2.2em; font-weight: bold; color: var(--primary); }

        .btn-submit { background: var(--primary); color: white; border: none; padding: 20px; width: 100%; border-radius: 8px; font-size: 1.2em; cursor: pointer; font-weight: bold; margin-top: 30px; box-shadow: 0 4px 6px rgba(190, 24, 93, 0.2); }
        .btn-submit:hover { background: #9d174d; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="nav('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="tab-btn" onclick="nav('depouillement')">2. DÉPOUILLEMENT & CODAGE</button>
        <button class="tab-btn" onclick="nav('resultats')">3. RÉSULTATS & ANALYSE</button>
        <button class="tab-btn" onclick="nav('conclusion')">4. CONCLUSION & RECO</button>
    </div>

    <div id="recolte" class="page active">
        <form id="capForm">
            <h2>I. IDENTIFICATION & CONSENTEMENT ÉCLAIRÉ</h2>
            <div class="form-grid">
                <div class="field-box"><label>Code de l'enquêtée :</label><input type="text" name="code" required></div>
                <div class="field-box"><label>Date :</label><input type="date" name="date"></div>
                <div class="field-box"><label>Service d'affectation :</label><input type="text" name="service"></div>
                <div class="field-box"><label>Enquêteur(trice) :</label><input type="text" name="enqueteur"></div>
                <div class="field-box"><label>Consentement :</label>
                    <select name="consent"><option value="1">J'accepte de participer</option><option value="0">Je refuse de participer</option></select>
                </div>
            </div>

            <h2>II. DONNÉES SOCIODÉMOGRAPHIQUES (Le Profil)</h2>
            <div class="form-grid">
                <div class="field-box"><label>Sexe :</label><select name="sexe"><option>Femme</option><option>Homme</option></select></div>
                <div class="field-box"><label>Âge (ans) :</label><input type="number" name="age"></div>
                <div class="field-box"><label>État civil :</label>
                    <select name="etat_civil"><option>Célibataire</option><option>Mariée</option><option>Veuve</option><option>Autre</option></select>
                </div>
                <div class="field-box"><label>Niveau d'études :</label>
                    <select name="niveau"><option value="A2">Infirmière diplômée (A2)</option><option value="A1">Graduée / A1</option><option value="A0">Licenciée / A0</option><option value="Master">Master ou plus</option></select>
                </div>
                <div class="field-box"><label>Années d'expérience :</label><input type="number" name="exp"></div>
                <div class="field-box"><label>Statut professionnel :</label>
                    <select name="statut"><option>Titulaire</option><option>Contractuelle</option><option>Stagiaire</option><option>Autre</option></select>
                </div>
                <div class="field-box"><label>Antécédents familiaux/perso :</label>
                    <select name="antecedents"><option value="0">Non</option><option value="1">Oui</option></select>
                    <input type="text" name="antecedents_details" placeholder="Préciser si Oui..." style="margin-top:5px;">
                </div>
            </div>

            <h2>III. ÉVALUATION DES CONNAISSANCES (Le Savoir)</h2>
            <div class="form-grid">
                <div class="field-box"><label>Le risque augmente avec l'âge ?</label><select name="c_age"><option value="1">Vrai</option><option value="0">Faux</option><option value="9">Ne sait pas</option></select></div>
                <div class="field-box"><label>L'obésité/sédentarité sont des facteurs ?</label><select name="c_obesite"><option value="1">Vrai</option><option value="0">Faux</option><option value="9">Ne sait pas</option></select></div>
                <div class="field-box"><label>L'allaitement est protecteur ?</label><select name="c_allaitement"><option value="1">Vrai</option><option value="0">Faux</option><option value="9">Ne sait pas</option></select></div>
                <div class="field-box"><label>L'AES détecte les anomalies ?</label><select name="c_aes"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field-box"><label>La mammographie est un dépistage secondaire ?</label><select name="c_mammo_sec"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                <div class="field-box"><label>La mammographie remplace l'examen clinique ?</label><select name="c_remplace"><option value="0">Faux (Correct)</option><option value="1">Vrai</option></select></div>
                <div class="field-box"><label>Âge conseillé pour mammographie (votre milieu) :</label><input type="number" name="age_depistage"></div>
                <div class="field-box"><label>Méthode de référence dépistage organisé :</label>
                    <select name="methode_ref"><option>Mammographie</option><option>Échographie</option><option>Radiographie thoracique</option></select>
                </div>
            </div>

            <div class="field-box" style="margin-top:15px;">
                <label>Signes d'alerte (Cochez tout ce qui s'applique) :</label>
                <div class="check-list">
                    <label><input type="checkbox" name="signe" value="masse"> Présence d'une masse ou nodule dur</label>
                    <label><input type="checkbox" name="signe" value="peau"> Aspect "peau d'orange" sur le sein</label>
                    <label><input type="checkbox" name="signe" value="sang"> Écoulement de sang par le mamelon</label>
                    <label><input type="checkbox" name="signe" value="retraction"> Rétraction du mamelon</label>
                </div>
            </div>

            <div class="form-grid" style="margin-top:15px;">
                <div class="field-box"><label>Votre structure a-t-elle la mammographie ?</label><select name="dispo_mammo"><option>Oui</option><option>Non</option><option>NSP</option></select></div>
                <div class="field-box"><label>Savez-vous où référer si non ?</label><select name="refer_mammo"><option>Oui</option><option>Non</option></select></div>
                <div class="field-box"><label>Fréquence de l'examen clinique :</label><select name="freq_clinique"><option>Chaque année</option><option>Tous les 2 ans</option><option>NSP</option></select></div>
                <div class="field-box"><label>Utilisation échographie mammaire :</label><select name="usage_echo"><option>En complément</option><option>En 1ère intention (femmes jeunes)</option><option>NSP</option></select></div>
                <div class="field-box"><label>Savez-vous expliquer l'utilité de la mammographie ?</label><select name="expl_mammo"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="field-box"><label>Savez-vous expliquer le déroulement de l'examen clinique ?</label><select name="expl_clinique"><option value="1">Oui</option><option value="0">Non</option></select></div>
            </div>

            <h2>IV. ÉVALUATION DES ATTITUDES (Le Savoir-être : de 1 à 5)</h2>
            <div class="table-container">
                <table>
                    <tr><th>Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                    <tr><td>1. La prévention est une priorité dans mon travail.</td>
                        <td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td>
                    </tr>
                    <tr><td>2. Je suis à l'aise pour enseigner l'autopalpation.</td>
                        <td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td>
                    </tr>
                    <tr><td>3. L'examen clinique devrait être systématique.</td>
                        <td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td>
                    </tr>
                    <tr><td>4. Le cancer du sein est forcément mortel en RDC.</td>
                        <td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td>
                    </tr>
                    <tr><td>5. Le coût des examens est le principal frein.</td>
                        <td><input type="radio" name="att5" value="1"></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td>
                    </tr>
                    <tr><td>6. Les patientes sont réceptives aux conseils.</td>
                        <td><input type="radio" name="att6" value="1"></td><td><input type="radio" name="att6" value="2"></td><td><input type="radio" name="att6" value="3"></td><td><input type="radio" name="att6" value="4"></td><td><input type="radio" name="att6" value="5"></td>
                    </tr>
                </table>
            </div>

            <h2>V. ÉVALUATION DES PRATIQUES (Le Savoir-faire)</h2>
            <div class="form-grid">
                <div class="field-box"><label>Pratique personnelle de l'AES :</label><select name="p_perso"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="field-box"><label>Fréquence personnelle :</label><select name="p_perso_freq"><option>Mensuelle</option><option>Occasionnelle</option><option>Rare</option></select></div>
                <div class="field-box"><label>Examen clinique lors des consultations ?</label><select name="p_clinique"><option>Toujours (systématiquement)</option><option>Parfois (si plainte)</option><option>Jamais</option></select></div>
                <div class="field-box"><label>Informez-vous sur les signes précoces ?</label><select name="p_info"><option>Oui</option><option>Non</option><option>Parfois</option></select></div>
                <div class="field-box"><label>Enseignez-vous l'AES aux patientes ?</label><select name="p_enseigne"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="field-box"><label>Référencez-vous pour une mammographie ?</label><select name="p_refer"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="field-box"><label>Participé à une activité de sensibilisation ?</label><select name="p_sensib"><option value="1">Oui</option><option value="0">Non</option></select></div>
            </div>

            <h2>VI. OBSTACLES & RECOMMANDATIONS</h2>
            <div class="field-box">
                <label>Obstacles à la prévention à l'HGRM (Cochez tout) :</label>
                <div class="check-list">
                    <label><input type="checkbox" name="obs" value="Matériel"> Manque de matériel (affiches, outils éducatifs)</label>
                    <label><input type="checkbox" name="obs" value="Formation"> Manque de formation du personnel</label>
                    <label><input type="checkbox" name="obs" value="Temps"> Manque de temps / Surcharge de travail</label>
                    <label><input type="checkbox" name="obs" value="Coût"> Coût élevé des examens</label>
                    <label><input type="checkbox" name="obs" value="Distance"> Distance vers les centres équipés</label>
                    <label><input type="checkbox" name="obs" value="Tabous"> Tabous culturels ou religieux</label>
                    <label><input type="checkbox" name="obs" value="Info"> Manque d'information des patientes</label>
                </div>
                <input type="text" name="obs_autres" placeholder="Autres obstacles..." style="margin-top:10px;">
            </div>

            <div class="form-grid" style="margin-top:15px;">
                <div class="field-box"><label>Besoin de formation supplémentaire ?</label><select name="besoin_form"><option value="1">Oui</option><option value="0">Non</option></select></div>
                <div class="field-box"><label>Type souhaité :</label><select name="type_form"><option>Formation continue</option><option>Licence</option><option>Master</option><option>Autre</option></select></div>
            </div>
            <div class="field-box" style="margin-top:15px;">
                <label>Suggestions pour améliorer la lutte à l'HGRM Makala :</label>
                <textarea name="suggestions" rows="4"></textarea>
            </div>

            <button type="button" class="btn-submit" onclick="enregistrer()">ENREGISTRER LA FICHE COMPLÈTE</button>
        </form>
    </div>

    <div id="depouillement" class="page">
        <h2>Matrice de Dépouillement (Données Brutes)</h2>
        <div class="table-container"><table id="tableMatrix"><thead><tr><th>ID</th><th>Age</th><th>Niveau</th><th>C_Age</th><th>C_Obs</th><th>C_All</th><th>P_Ens</th><th>P_Clin</th></tr></thead><tbody></tbody></table></div>
    </div>

    <div id="resultats" class="page">
        <h2>Analyse Statistique CAP</h2>
        <div class="stats-grid">
            <div class="stat-card"><h3>Échantillon (N)</h3><div id="resN" class="stat-val">0</div></div>
            <div class="stat-card"><h3>Savoir (Connaissances)</h3><div id="resC" class="stat-val">0%</div></div>
            <div class="stat-card"><h3>Attitude Moyenne</h3><div id="resA" class="stat-val">0/5</div></div>
            <div class="stat-card"><h3>Savoir-faire (Pratiques)</h3><div id="resP" class="stat-val">0%</div></div>
        </div>
    </div>

    <div id="conclusion" class="page">
        <h2>Synthèse et Conclusion</h2>
        <div class="field-box">
            <h3>Conclusion Automatique</h3>
            <p id="conclText">Veuillez d'abord collecter des données.</p>
        </div>
    </div>
</div>

<script>
    let database = JSON.parse(localStorage.getItem('makala_cap_db')) || [];

    function nav(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        if(id === 'depouillement') loadMatrix();
        if(id === 'resultats') loadStats();
    }

    function enregistrer() {
        const form = document.getElementById('capForm');
        const data = Object.fromEntries(new FormData(form).entries());
        database.push(data);
        localStorage.setItem('makala_cap_db', JSON.stringify(database));
        alert("Fiche enregistrée ! Total : " + database.length);
        form.reset();
    }

    function loadMatrix() {
        const tbody = document.querySelector('#tableMatrix tbody');
        tbody.innerHTML = database.map(d => `<tr><td>${d.code}</td><td>${d.age}</td><td>${d.niveau}</td><td>${d.c_age}</td><td>${d.c_obesite}</td><td>${d.c_allaitement}</td><td>${d.p_enseigne}</td><td>${d.p_clinique}</td></tr>`).join('');
    }

    function loadStats() {
        const n = database.length;
        if(n === 0) return;
        const sumC = database.reduce((acc, d) => acc + (parseInt(d.c_age||0) + parseInt(d.c_obesite||0) + parseInt(d.c_allaitement||0))/3, 0);
        const sumP = database.reduce((acc, d) => acc + (parseInt(d.p_enseigne||0) + (d.p_clinique.includes('Toujours')?1:0.5))/2, 0);
        
        document.getElementById('resN').innerText = n;
        document.getElementById('resC').innerText = ((sumC/n)*100).toFixed(1) + "%";
        document.getElementById('resP').innerText = ((sumP/n)*100).toFixed(1) + "%";
        document.getElementById('conclText').innerText = "Sur " + n + " fiches, le taux de connaissances est de " + ((sumC/n)*100).toFixed(1) + "%.";
    }
</script>
</body>
</html>
