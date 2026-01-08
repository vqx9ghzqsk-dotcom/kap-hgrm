<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Collecte CAP - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: var(--bg); color: #334155; margin: 0; padding: 10px; line-height: 1.6; }
        .container { background: white; max-width: 900px; margin: 20px auto; padding: 30px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08); }
        
        .tabs { display: flex; gap: 10px; margin-bottom: 25px; border-bottom: 2px solid #e2e8f0; }
        .tab-btn { padding: 12px 20px; border: none; background: none; cursor: pointer; font-weight: bold; color: #64748b; border-bottom: 3px solid transparent; }
        .tab-btn.active { color: var(--primary); border-bottom-color: var(--primary); }
        .tab-content { display: none; }
        .tab-content.active { display: block; }

        h1 { font-size: 1.5rem; text-align: center; color: var(--secondary); text-transform: uppercase; border-bottom: 2px solid var(--primary); padding-bottom: 10px; }
        h3 { background: #fff1f2; color: var(--primary); padding: 10px; border-radius: 5px; margin-top: 25px; font-size: 1.1rem; }
        
        .question-block { margin-bottom: 15px; padding: 10px; border-bottom: 1px solid #f1f5f9; }
        .label-q { font-weight: 600; display: block; margin-bottom: 8px; }
        
        input[type="text"], input[type="number"], select, textarea { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 6px; box-sizing: border-box; }
        .radio-group, .check-group { display: flex; flex-wrap: wrap; gap: 15px; margin-top: 5px; }
        label { cursor: pointer; display: flex; align-items: center; gap: 5px; }

        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { border: 1px solid #e2e8f0; padding: 10px; text-align: center; }
        th { background: #f8fafc; font-size: 0.85rem; }

        .btn-save { background: var(--primary); color: white; border: none; padding: 15px; width: 100%; border-radius: 8px; font-size: 1.1rem; font-weight: bold; cursor: pointer; margin-top: 30px; }
        .btn-save:hover { background: #9d174d; }

        .dashboard-card { background: white; border: 1px solid #e2e8f0; padding: 20px; border-radius: 10px; margin-bottom: 20px; border-top: 5px solid var(--primary); }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="switchTab('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="tab-btn" onclick="switchTab('analyse')">2. ANALYSE STATISTIQUE</button>
    </div>

    <div id="recolte" class="tab-content active">
        <h1>FICHE DE COLLECTE</h1>
        <p style="text-align:center; font-weight:bold;">Connaissances, attitudes et pratiques des infirmières sur la prévention du cancer du sein à l’Hôpital Général de Référence de Makala (HGRM)</p>

        <form id="capForm">
            <div class="section">
                <h3>I. IDENTIFICATION</h3>
                <div class="question-block">
                    <label class="label-q">Code de l’enquêtée :</label>
                    <input type="text" name="code">
                </div>
                <div class="question-block">
                    <label class="label-q">Date :</label>
                    <input type="text" name="date_collecte" placeholder="JJ / MM / AAAA">
                </div>
                <div class="question-block">
                    <label class="label-q">Service :</label>
                    <input type="text" name="service">
                </div>
                <div class="question-block">
                    <label class="label-q">Enquêteur(trice) :</label>
                    <input type="text" name="enqueteur">
                </div>
            </div>

            <div class="section">
                <h3>II. CONSENTEMENT ÉCLAIRÉ</h3>
                <div class="question-block">
                    <div class="radio-group">
                        <label><input type="radio" name="consentement" value="Oui" required> J’accepte de participer</label>
                        <label><input type="radio" name="consentement" value="Non"> Je refuse de participer</label>
                    </div>
                </div>
            </div>

            <div class="section">
                <h3>III. DONNÉES SOCIODÉMOGRAPHIQUES</h3>
                <div class="question-block">
                    <span class="label-q">1. Sexe :</span>
                    <div class="radio-group">
                        <label><input type="radio" name="sexe" value="Femme"> Femme</label>
                        <label><input type="radio" name="sexe" value="Homme"> Homme</label>
                    </div>
                </div>
                <div class="question-block">
                    <label class="label-q">2. Âge :</label>
                    <input type="number" name="age" placeholder="ans">
                </div>
                <div class="question-block">
                    <span class="label-q">3. État civil :</span>
                    <div class="radio-group">
                        <label><input type="radio" name="etat_civil" value="Célibataire"> Célibataire</label>
                        <label><input type="radio" name="etat_civil" value="Mariée"> Mariée</label>
                        <label><input type="radio" name="etat_civil" value="Autre"> Autre</label>
                    </div>
                </div>
                <div class="question-block">
                    <span class="label-q">4. Niveau d’études :</span>
                    <div class="radio-group">
                        <label><input type="radio" name="niveau_etude" value="A1"> Infirmière diplômée</label>
                        <label><input type="radio" name="niveau_etude" value="Licence"> Licence</label>
                        <label><input type="radio" name="niveau_etude" value="Master"> Master</label>
                        <label><input type="radio" name="niveau_etude" value="Autre"> Autre</label>
                    </div>
                </div>
                <div class="question-block">
                    <label class="label-q">5. Années d’expérience :</label>
                    <input type="number" name="experience">
                </div>
                <div class="question-block">
                    <span class="label-q">6. Statut professionnel :</span>
                    <div class="radio-group">
                        <label><input type="radio" name="statut" value="Titulaire"> Titulaire</label>
                        <label><input type="radio" name="statut" value="Contractuelle"> Contractuelle</label>
                        <label><input type="radio" name="statut" value="Stagiaire"> Stagiaire</label>
                        <label><input type="radio" name="statut" value="Autre"> Autre</label>
                    </div>
                </div>
                <div class="question-block">
                    <span class="label-q">8. Antécédents personnels/familiaux de cancer du sein :</span>
                    <div class="radio-group">
                        <label><input type="radio" name="antecedents" value="Oui"> Oui</label>
                        <label><input type="radio" name="antecedents" value="Non"> Non</label>
                    </div>
                </div>
            </div>

            <div class="section">
                <h3>IV. CONNAISSANCES</h3>
                <div class="question-block">
                    <span class="label-q">1. Le risque de cancer du sein augmente avec l’âge.</span>
                    <label><input type="radio" name="c1" value="Vrai"> Vrai</label> <label><input type="radio" name="c1" value="Faux"> Faux</label>
                </div>
                <div class="question-block">
                    <span class="label-q">2. L’obésité est un facteur de risque.</span>
                    <label><input type="radio" name="c2" value="Vrai"> Vrai</label> <label><input type="radio" name="c2" value="Faux"> Faux</label>
                </div>
                <div class="question-block">
                    <span class="label-q">3. Antécédents familiaux augmentent le risque.</span>
                    <label><input type="radio" name="c3" value="Vrai"> Vrai</label> <label><input type="radio" name="c3" value="Faux"> Faux</label>
                </div>
                <div class="question-block">
                    <span class="label-q">4. L’autopalpation permet de détecter des anomalies précoces.</span>
                    <label><input type="radio" name="c4" value="Vrai"> Vrai</label> <label><input type="radio" name="c4" value="Faux"> Faux</label>
                </div>
            </div>

            <div class="section">
                <h3>V. SIGNES D’ALERTE</h3>
                <div class="question-block">
                    <span class="label-q">Quels sont les signes d’alerte du cancer du sein ? (Cochez)</span>
                    <div class="check-group">
                        <label><input type="checkbox" name="signe" value="Masse"> Masse ou nodule</label>
                        <label><input type="checkbox" name="signe" value="Peau"> Changement de peau (peau d'orange)</label>
                        <label><input type="checkbox" name="signe" value="Ecoulement"> Écoulement mamelonnaire</label>
                        <label><input type="checkbox" name="signe" value="Douleur"> Douleur inhabituelle</label>
                    </div>
                </div>
            </div>

            <div class="section">
                <h3>VI. ATTITUDES</h3>
                <p>Notez de 1 à 5 (1=Pas du tout d'accord, 5=Tout à fait d'accord)</p>
                <table>
                    <tr>
                        <th>Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                    </tr>
                    <tr>
                        <td style="text-align:left">La prévention est une priorité.</td>
                        <td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td>
                    </tr>
                    <tr>
                        <td style="text-align:left">Le coût de la mammographie est un obstacle.</td>
                        <td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td>
                    </tr>
                </table>
            </div>

            <div class="section">
                <h3>VII. PRATIQUES</h3>
                <div class="question-block">
                    <span class="label-q">1. Pratique personnelle de l’autopalpation :</span>
                    <label><input type="radio" name="p1" value="Oui"> Oui</label> <label><input type="radio" name="p1" value="Non"> Non</label>
                </div>
                <div class="question-block">
                    <span class="label-q">2. Réalisez-vous un examen clinique lors des consultations ?</span>
                    <label><input type="radio" name="p2" value="Toujours"> Toujours</label>
                    <label><input type="radio" name="p2" value="Parfois"> Parfois</label>
                    <label><input type="radio" name="p2" value="Jamais"> Jamais</label>
                </div>
                <div class="question-block">
                    <span class="label-q">4. Enseignez-vous l’autopalpation aux patientes ?</span>
                    <label><input type="radio" name="p3" value="Oui"> Oui</label> <label><input type="radio" name="p3" value="Non"> Non</label>
                </div>
            </div>

            <div class="section">
                <h3>VIII. OBSTACLES</h3>
                <div class="check-group">
                    <label><input type="checkbox" name="obs" value="Matériel"> Manque de matériel</label>
                    <label><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
                    <label><input type="checkbox" name="obs" value="Temps"> Manque de temps</label>
                    <label><input type="checkbox" name="obs" value="Tabous"> Tabous culturels</label>
                </div>
            </div>

            <div class="section">
                <h3>IX. RECOMMANDATIONS</h3>
                <textarea name="recommandations" rows="3" placeholder="Vos besoins et suggestions..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="enregistrerDonnees()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="analyse" class="tab-content">
        <h1>Rapport de Recherche (Makala)</h1>
        
        <div class="dashboard-card">
            <strong>Progression :</strong> <span id="compteurTotal">0</span> fiches enregistrées.
            | <strong>Quota :</strong> <input type="number" id="quota" value="100" style="width:50px;" oninput="calculerStats()">
        </div>

        <div class="dashboard-card">
            <h3>Niveau de Connaissances (Objectif Spécifique 1)</h3>
            <div id="statsC">En attente de données...</div>
        </div>

        <div class="dashboard-card">
            <h3>Pratiques & Obstacles (Objectif Spécifique 3)</h3>
            <div id="statsP">Calcul automatique...</div>
        </div>
    </div>
</div>



<script>
    let db = JSON.parse(localStorage.getItem('db_memo_makala')) || [];
    document.getElementById('compteurTotal').innerText = db.length;

    function switchTab(id) {
        document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        if(id === 'analyse') {
            document.querySelectorAll('.tab-btn')[1].classList.add('active');
            calculerStats();
        } else {
            document.querySelectorAll('.tab-btn')[0].classList.add('active');
        }
    }

    function enregistrerDonnees() {
        const form = document.getElementById('capForm');
        if(!form.consentement.value) { alert("Le consentement est requis."); return; }

        const entry = {
            c_vrai: (form.c1.value === "Vrai" ? 1 : 0) + (form.c2.value === "Vrai" ? 1 : 0) + (form.c4.value === "Vrai" ? 1 : 0),
            p_enseigne: form.p3.value === "Oui" ? 1 : 0,
            niveau: form.niveau_etude.value
        };

        db.push(entry);
        localStorage.setItem('db_memo_makala', JSON.stringify(db));
        document.getElementById('compteurTotal').innerText = db.length;
        form.reset();
        alert("Fiche ajoutée avec succès !");
    }

    function calculerStats() {
        const total = db.length;
        if(total === 0) return;
        
        const bonnesRep = (db.reduce((acc, curr) => acc + curr.c_vrai, 0) / (total * 3) * 100).toFixed(1);
        const enseignement = (db.reduce((acc, curr) => acc + curr.p_enseigne, 0) / total * 100).toFixed(1);

        document.getElementById('statsC').innerHTML = `<p>Taux de réponses correctes aux questions théoriques : <b>${bonnesRep}%</b></p>`;
        document.getElementById('statsP').innerHTML = `<p>Proportion d'infirmières enseignant l'AES : <b>${enseignement}%</b></p>`;
    }
</script>

</body>
</html>
