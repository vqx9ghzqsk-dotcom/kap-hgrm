<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Système Expert CAP - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background-color: var(--bg); color: #334155; margin: 0; padding: 20px; line-height: 1.5; }
        .container { background: white; max-width: 1000px; margin: auto; padding: 30px; border-radius: 12px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); }
        .tabs { display: flex; gap: 10px; margin-bottom: 30px; border-bottom: 2px solid #e2e8f0; }
        .tab-btn { padding: 12px 24px; border: none; background: none; cursor: pointer; font-weight: 600; color: #64748b; border-bottom: 3px solid transparent; }
        .tab-btn.active { color: var(--primary); border-bottom-color: var(--primary); }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        h1 { text-align: center; color: var(--secondary); text-transform: uppercase; font-size: 1.4em; }
        h3 { background: #fff1f2; color: var(--primary); padding: 10px; border-radius: 6px; margin-top: 25px; border-left: 4px solid var(--primary); }
        .form-section { margin-bottom: 20px; padding: 15px; border: 1px solid #f1f5f9; border-radius: 8px; }
        .question { font-weight: 600; display: block; margin-bottom: 10px; }
        .options { margin-left: 10px; margin-bottom: 15px; display: flex; flex-wrap: wrap; gap: 15px; }
        label { cursor: pointer; display: flex; align-items: center; gap: 5px; }
        input[type="text"], input[type="number"], select, textarea { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 6px; margin-top: 5px; }
        table { width: 100%; border-collapse: collapse; margin-top: 15px; }
        th, td { border: 1px solid #e2e8f0; padding: 10px; text-align: center; }
        th { background: #f8fafc; font-size: 0.9em; }
        .btn-save { background: var(--primary); color: white; border: none; padding: 18px; width: 100%; border-radius: 8px; font-size: 1.1em; font-weight: bold; cursor: pointer; margin-top: 20px; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-top: 20px; }
        .card { background: white; border: 1px solid #e2e8f0; padding: 20px; border-radius: 10px; border-top: 4px solid var(--primary); }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="showTab('recolte')">1. RÉCOLTE DES DONNÉES (TOUS ÉLÉMENTS)</button>
        <button class="tab-btn" onclick="showTab('analyse')">2. ANALYSE STATISTIQUE</button>
    </div>

    <div id="recolte" class="tab-content active">
        <h1>Fiche de Collecte : CAP Prévention Cancer du Sein (HGRM)</h1>
        
        <form id="fullCapForm">
            <h3>I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</h3>
            <div class="form-section">
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <label>Code de l’enquêtée : <input type="text" name="code"></label>
                    <label>Date : <input type="text" name="date" placeholder="JJ/MM/AAAA"></label>
                    <label>Service / Affectation : <input type="text" name="service"></label>
                    <label>Enquêteur(trice) : <input type="text" name="enqueteur"></label>
                </div>
                <p class="question">Consentement :</p>
                <div class="options">
                    <label><input type="radio" name="consent" value="Oui" required> J’accepte de participer</label>
                    <label><input type="radio" name="consent" value="Non"> Je refuse de participer</label>
                </div>
            <h3>II. DONNÉES SOCIODÉMOGRAPHIQUES (LE PROFIL)</h3>
            <div class="form-section">
                <label class="question">1. Sexe :</label>
                <div class="options">
                    <label><input type="radio" name="sexe" value="Femme"> Femme</label>
                    <label><input type="radio" name="sexe" value="Homme"> Homme</label>
                </div>
                <label class="question">2. Âge : <input type="number" name="age"> ans</label>
                <label class="question">3. État civil :</label>
                <div class="options">
                    <label><input type="radio" name="etat_civil" value="Célibataire"> Célibataire</label>
                    <label><input type="radio" name="etat_civil" value="Mariée"> Mariée</label>
                    <label><input type="radio" name="etat_civil" value="Veuve"> Veuve</label>
                    <label><input type="radio" name="etat_civil" value="Autre"> Autre</label>
                </div>
                <label class="question">4. Niveau d’études :</label>
                <select name="niveau">
                    <option value="A2">Infirmière diplômée (A2)</option>
                    <option value="A1">Graduée / A1</option>
                    <option value="A0">Licenciée / A0</option>
                    <option value="Master">Master ou plus</option>
                </select>
                <label class="question">5. Années d’expérience professionnelle : <input type="number" name="experience"></label>
                <label class="question">6. Statut professionnel :</label>
                <div class="options">
                    <label><input type="radio" name="statut" value="Titulaire"> Titulaire</label>
                    <label><input type="radio" name="statut" value="Contractuelle"> Contractuelle</label>
                    <label><input type="radio" name="statut" value="Stagiaire"> Stagiaire</label>
                    <label><input type="radio" name="statut" value="Autre"> Autre</label>
                </div>
                <label class="question">7. Antécédents personnels/familiaux de cancer du sein :</label>
                <div class="options">
                    <label><input type="radio" name="antécédents" value="Oui"> Oui</label>
                    <label><input type="radio" name="antécédents" value="Non"> Non</label>
                </div>
                <label>Préciser les antécédents : <input type="text" name="antecedents_detail"></label>
            </div>

            <h3>III. ÉVALUATION DES CONNAISSANCES (LE SAVOIR)</h3>
            <div class="form-section">
                <p><strong>Facteurs de risque (Vrai/Faux/Ne sait pas) :</strong></p>
                <label>Le risque augmente avec l'âge :</label>
                <div class="options">
                    <label><input type="radio" name="c_age" value="Vrai"> Vrai</label><label><input type="radio" name="c_age" value="Faux"> Faux</label><label><input type="radio" name="c_age" value="NSP"> Ne sait pas</label>
                </div>
                <label>L’obésité et la sédentarité sont des facteurs :</label>
                <div class="options">
                    <label><input type="radio" name="c_obesite" value="Vrai"> Vrai</label><label><input type="radio" name="c_obesite" value="Faux"> Faux</label><label><input type="radio" name="c_obesite" value="NSP"> Ne sait pas</label>
                </div>
                <label>Les antécédents familiaux augmentent le risque :</label>
                <div class="options">
                    <label><input type="radio" name="c_famille" value="Vrai"> Vrai</label><label><input type="radio" name="c_famille" value="Faux"> Faux</label><label><input type="radio" name="c_famille" value="NSP"> Ne sait pas</label>
                </div>
                <label>L’allaitement maternel est un facteur protecteur :</label>
                <div class="options">
                    <label><input type="radio" name="c_allaitement" value="Vrai"> Vrai</label><label><input type="radio" name="c_allaitement" value="Faux"> Faux</label><label><input type="radio" name="c_allaitement" value="NSP"> Ne sait pas</label>
                </div>

                <p><strong>Méthodes de détection :</strong></p>
                <label>L’autopalpation permet de détecter des anomalies :</label>
                <div class="options"><label><input type="radio" name="c_aes_util" value="Vrai"> Vrai</label><label><input type="radio" name="c_aes_util" value="Faux"> Faux</label></div>
                <label>L’examen clinique est une méthode efficace :</label>
                <div class="options"><label><input type="radio" name="c_clin_util" value="Vrai"> Vrai</label><label><input type="radio" name="c_clin_util" value="Faux"> Faux</label></div>
                <label>La mammographie est un dépistage secondaire :</label>
                <div class="options"><label><input type="radio" name="c_mammo_sec" value="Vrai"> Vrai</label><label><input type="radio" name="c_mammo_sec" value="Faux"> Faux</label></div>
                <label>La mammographie remplace l'examen clinique :</label>
                <div class="options"><label><input type="radio" name="c_mammo_remp" value="Vrai"> Vrai</label><label><input type="radio" name="c_mammo_remp" value="Faux"> Faux</label></div>

                <p><strong>Signes d’alerte (Cochez tout ce qui s'applique) :</strong></p>
                <div class="options">
                    <label><input type="checkbox" name="signe" value="masse"> Masse ou nodule dur</label>
                    <label><input type="checkbox" name="signe" value="peau"> Aspect "peau d'orange"</label>
                    <label><input type="checkbox" name="signe" value="ecoulement"> Écoulement sanglant</label>
                    <label><input type="checkbox" name="signe" value="retraction"> Rétraction du mamelon</label>
                </div>

                <p><strong>Dépistage par mammographie :</strong></p>
                <label>Âge conseillé pour la mammographie dans votre milieu : <input type="number" name="age_mammo"> ans</label>
                <label class="question">Méthode de référence pour le dépistage organisé :</label>
                <div class="options">
                    <label><input type="radio" name="methode_ref" value="Echo"> Échographie</label>
                    <label><input type="radio" name="methode_ref" value="Mammo"> Mammographie</label>
                    <label><input type="radio" name="methode_ref" value="Radio"> Radiographie thoracique</label>
                </div>
            </div>

            <h3>IV. RESSOURCES ET TECHNIQUES</h3>
            <div class="form-section">
                <label>Votre structure dispose d'un service de mammographie ?</label>
                <div class="options"><label><input type="radio" name="res_mammo" value="Oui"> Oui</label><label><input type="radio" name="res_mammo" value="Non"> Non</label><label><input type="radio" name="res_mammo" value="NSP"> NSP</label></div>
                <label>Si non, savez-vous où référer les patientes ?</label>
                <div class="options"><label><input type="radio" name="ref_pat" value="Oui"> Oui</label><label><input type="radio" name="ref_pat" value="Non"> Non</label></div>
                <label>L’examen clinique doit être réalisé :</label>
                <div class="options"><label><input type="radio" name="freq_clin" value="Annuel"> Chaque année</label><label><input type="radio" name="freq_clin" value="2ans"> Tous les 2 ans</label><label><input type="radio" name="freq_clin" value="NSP"> NSP</label></div>
                <label>L'échographie mammaire est utilisée :</label>
                <div class="options"><label><input type="radio" name="util_echo" value="Comp"> En complément</label><label><input type="radio" name="util_echo" value="Jeune"> 1ère intention (jeunes)</label><label><input type="radio" name="util_echo" value="NSP"> NSP</label></div>
                <label>Savez-vous expliquer l’utilité de la mammographie ?</label>
                <div class="options"><label><input type="radio" name="expl_util" value="Oui"> Oui</label><label><input type="radio" name="expl_util" value="Non"> Non</label></div>
                <label>Savez-vous expliquer le déroulement d'un examen clinique ?</label>
                <div class="options"><label><input type="radio" name="expl_der" value="Oui"> Oui</label><label><input type="radio" name="expl_der" value="Non"> Non</label></div>
            </div>

            <h3>V. ÉVALUATION DES ATTITUDES (ÉCHELLE DE LIKERT 1 À 5)</h3>
            <div class="form-section">
                <p>(1: Pas du tout d'accord → 5: Tout à fait d'accord)</p>
                <table>
                    <tr><th>Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                    <tr><td>La prévention est une priorité dans mon travail.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td>Je suis à l’aise pour expliquer l’autopalpation.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td>L'examen clinique devrait être systématique (femmes à risque).</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                    <tr><td>Le cancer du sein est forcément mortel en RDC.</td><td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td></tr>
                    <tr><td>Le coût des examens est le principal frein.</td><td><input type="radio" name="att5" value="1"></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td></tr>
                    <tr><td>Les patientes sont réceptives aux conseils.</td><td><input type="radio" name="att6" value="1"></td><td><input type="radio" name="att6" value="2"></td><td><input type="radio" name="att6" value="3"></td><td><input type="radio" name="att6" value="4"></td><td><input type="radio" name="att6" value="5"></td></tr>
                    <tr><td>Je peux recommander un dépistage adapté aux ressources.</td><td><input type="radio" name="att7" value="1"></td><td><input type="radio" name="att7" value="2"></td><td><input type="radio" name="att7" value="3"></td><td><input type="radio" name="att7" value="4"></td><td><input type="radio" name="att7" value="5"></td></tr>
                </table>
            </div>

            <h3>VI. ÉVALUATION DES PRATIQUES (LE SAVOIR-FAIRE)</h3>
            <div class="form-section">
                <label>1. Pratique personnelle de l’autopalpation (AES) :</label>
                <div class="options"><label><input type="radio" name="p_perso" value="Oui"> Oui</label><label><input type="radio" name="p_perso" value="Non"> Non</label></div>
                <label>Fréquence :</label>
                <div class="options"><label><input type="radio" name="p_freq" value="Mensuelle"> Mensuelle</label><label><input type="radio" name="p_freq" value="Occasionnelle"> Occasionnelle</label><label><input type="radio" name="p_freq" value="Rare"> Rare</label></div>
                <label>2. Réalisez-vous un examen clinique lors des consultations ?</label>
                <div class="options"><label><input type="radio" name="p_clin" value="Toujours"> Toujours</label><label><input type="radio" name="p_clin" value="Parfois"> Parfois</label><label><input type="radio" name="p_clin" value="Jamais"> Jamais</label></div>
                <label>3. Informez-vous les patientes sur les signes précoces ?</label>
                <div class="options"><label><input type="radio" name="p_info" value="Oui"> Oui</label><label><input type="radio" name="p_info" value="Non"> Non</label><label><input type="radio" name="p_info" value="Parfois"> Parfois</label></div>
                <label>4. Enseignez-vous la technique de l’AES aux patientes ?</label>
                <div class="options"><label><input type="radio" name="p_enseigne" value="Oui"> Oui</label><label><input type="radio" name="p_enseigne" value="Non"> Non</label></div>
                <label>5. Référencez-vous les patientes pour une mammographie ?</label>
                <div class="options"><label><input type="radio" name="p_ref" value="Oui"> Oui</label><label><input type="radio" name="p_ref" value="Non"> Non</label></div>
                <label>6. Avez-vous déjà participé à une activité de sensibilisation ?</label>
                <div class="options"><label><input type="radio" name="p_sens" value="Oui"> Oui</label><label><input type="radio" name="p_sens" value="Non"> Non</label></div>
            </div>

            <h3>VII. OBSTACLES ET RECOMMANDATIONS</h3>
            <div class="form-section">
                <p><strong>Quels sont les obstacles à la prévention à l’HGRM ?</strong></p>
                <div class="options">
                    <label><input type="checkbox" name="obs" value="mat"> Manque de matériel (affiches, outils éducatifs)</label>
                    <label><input type="checkbox" name="obs" value="form"> Manque de formation</label>
                    <label><input type="checkbox" name="obs" value="temps"> Manque de temps</label>
                    <label><input type="checkbox" name="obs" value="cout"> Coût élevé des examens</label>
                    <label><input type="checkbox" name="obs" value="dist"> Distance vers les centres équipés</label>
                    <label><input type="checkbox" name="obs" value="tabou"> Tabous culturels</label>
                    <label><input type="checkbox" name="obs" value="info"> Manque d'information des patientes</label>
                    <label><input type="checkbox" name="obs" value="charge"> Surcharge de travail</label>
                </div>
                <label>Besoin de formation supplémentaire ?</label>
                <div class="options"><label><input type="radio" name="reco_form" value="Oui"> Oui</label><label><input type="radio" name="reco_form" value="Non"> Non</label></div>
                <label>Quel type de formation ?</label>
                <div class="options">
                    <label><input type="checkbox" name="form_type" value="Licence"> Licence</label>
                    <label><input type="checkbox" name="form_type" value="Master"> Master</label>
                    <label><input type="checkbox" name="form_type" value="Cont"> Formation continue</label>
                    <label>Autre : <input type="text" name="form_autre"></label>
                </div>
                <label>Suggestions pour l'HGRM : <textarea name="suggestions"></textarea></label>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="analyse" class="tab-content">
        <h1>Analyse Statistique CAP (Temps Réel)</h1>
        
        <div class="card">
            <strong>Nombre de fiches récoltées :</strong> <span id="totalFiches" style="color:var(--primary); font-size: 1.5em;">0</span>
        </div>

        <div class="stats-grid">
            <div class="card">
                <h3>Connaissances (Scores)</h3>
                <div id="scoreC">En attente de données...</div>
            </div>
            <div class="card">
                <h3>Attitudes (Échelle 1-5)</h3>
                <div id="scoreA">En attente de données...</div>
            </div>
            <div class="card">
                <h3>Pratiques (Proportions)</h3>
                <div id="scoreP">En attente de données...</div>
            </div>
            <div class="card">
                <h3>Obstacles Fréquents</h3>
                <div id="scoreO">En attente de données...</div>
            </div>
        </div>
        
        <button onclick="clearAllData()" style="margin-top: 30px; color: grey; border:none; background:none; cursor:pointer;">Réinitialiser la base de données (Test)</button>
    </div>
</div>


<script>
    let db = JSON.parse(localStorage.getItem('cap_makala_db')) || [];
    updateCounter();

    function showTab(id) {
        document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        if(id === 'analyse') runAnalysis();
    }

    function saveRecord() {
        const form = document.getElementById('fullCapForm');
        const fd = new FormData(form);
        const entry = Object.fromEntries(fd.entries());
        
        // Stockage des cases cochées (signes et obstacles)
        entry.signes = fd.getAll('signe');
        entry.obstacles = fd.getAll('obs');

        db.push(entry);
        localStorage.setItem('cap_makala_db', JSON.stringify(db));
        alert("Fiche enregistrée avec succès !");
        form.reset();
        updateCounter();
    }

    function updateCounter() {
        document.getElementById('totalFiches').innerText = db.length;
    }

    function runAnalysis() {
        const total = db.length;
        if(total === 0) return;

        // Exemple : Calcul % Connaissances Vraies sur l'âge
        const cAgeTrue = db.filter(x => x.c_age === "Vrai").length;
        const pEnseigne = db.filter(x => x.p_enseigne === "Oui").length;
        
        document.getElementById('scoreC').innerHTML = `<p>Connaissance (Âge = Risque) : <b>${((cAgeTrue/total)*100).toFixed(1)}%</b></p>`;
        document.getElementById('scoreP').innerHTML = `<p>Pratique (Enseigne AES) : <b>${((pEnseigne/total)*100).toFixed(1)}%</b></p>`;
        
        // Calcul Moyenne Attitude (Priorité)
        const avgAtt = db.reduce((acc, x) => acc + parseInt(x.att1 || 0), 0) / total;
        document.getElementById('scoreA').innerHTML = `<p>Score moyen Priorité Prévention : <b>${avgAtt.toFixed(2)} / 5</b></p>`;
        
        document.getElementById('scoreO').innerHTML = `<p>Analyse des fréquences d'obstacles disponible après ${total} fiches.</p>`;
    }

    function clearAllData() {
        if(confirm("Effacer toutes les données récoltées ?")) {
            localStorage.removeItem('cap_makala_db');
            location.reload();
</script>

</body>
</html>
