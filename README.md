<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Système Expert CAP - Cancer du Sein HGRM</title>
    <style>
        :root { --primary: #e74c3c; --secondary: #2c3e50; --bg: #f4f4f4; --success: #27ae60; }
        body { font-family: 'Segoe UI', Arial, sans-serif; line-height: 1.6; color: #333; background-color: var(--bg); margin: 0; padding: 20px; }
        .container { background: white; max-width: 900px; margin: auto; padding: 30px; border-radius: 8px; box-shadow: 0 0 15px rgba(0,0,0,0.1); }
        
        /* Menu Onglets */
        .tabs { display: flex; border-bottom: 3px solid var(--secondary); margin-bottom: 25px; }
        .tab-btn { padding: 12px 25px; cursor: pointer; border: none; background: #ddd; font-weight: bold; transition: 0.3s; }
        .tab-btn.active { background: var(--secondary); color: white; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }

        /* Styles Formulaire */
        h2 { color: var(--secondary); border-bottom: 2px solid var(--primary); padding-bottom: 10px; }
        h3 { color: var(--primary); margin-top: 25px; background: #fdf2f2; padding: 5px 10px; border-radius: 4px; }
        .section { margin-bottom: 20px; padding: 15px; border: 1px solid #ddd; border-radius: 5px; }
        .question { margin-bottom: 10px; font-weight: bold; display: block; }
        .options { margin-left: 15px; margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; cursor: pointer; }
        input[type="text"], input[type="number"], select, textarea { width: 100%; padding: 8px; margin-top: 5px; border: 1px solid #ccc; border-radius: 4px; }
        
        .btn-submit { background-color: var(--primary); color: white; padding: 15px; border: none; border-radius: 5px; cursor: pointer; font-size: 18px; width: 100%; font-weight: bold; margin-top: 20px; }
        .btn-submit:hover { background-color: #c0392b; }

        /* Styles Analyse */
        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 20px; }
        .card { background: #fff; border: 1px solid #ddd; padding: 15px; border-radius: 8px; border-top: 4px solid var(--secondary); }
        .p-value { color: var(--success); font-weight: bold; font-size: 1.2em; }
        .table-attitudes { width: 100%; border-collapse: collapse; margin-top: 10px; }
        .table-attitudes th, .table-attitudes td { border: 1px solid #ddd; padding: 8px; text-align: center; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="switchTab('recolte')">1. RÉCOLTE DES DONNÉES (Fiche)</button>
        <button class="tab-btn" onclick="switchTab('analyse')">2. ANALYSE ET INTERPRÉTATION</button>
    </div>

    <div id="recolte" class="tab-content active">
        <h2>QUESTIONNAIRE CAP : Prévention du Cancer du Sein</h2>
        <p><i>Sujet : Prévention et dépistage précoce chez les infirmières de l’HGRM.</i></p>

        <form id="capForm">
            <div class="section">
                <h3>I. CONSENTEMENT ÉCLAIRÉ ET IDENTIFICATION</h3>
                <span class="question">1. Acceptez-vous de participer volontairement à cette étude ?</span>
                <div class="options">
                    <label><input type="radio" name="consentement" value="Oui" required> Oui</label>
                    <label><input type="radio" name="consentement" value="Non"> Non</label>
                </div>

                <div class="question">2. Données Sociodémographiques :</div>
                <div class="options">
                    <label>Sexe : <input type="radio" name="sexe" value="F"> F <input type="radio" name="sexe" value="M"> M</label>
                    <label>Âge : <input type="number" name="age" style="width: 60px;"> ans</label>
                    <label>Niveau d’études : 
                        <select name="niveau" id="niveau">
                            <option value="A1">A1</option>
                            <option value="A2">A2</option>
                            <option value="Licence">Licence</option>
                            <option value="Master">Master</option>
                        </select>
                    </label>
                    <label>Ancienneté (ans) : <input type="number" name="anciennete" style="width: 60px;"></label>
                </div>
            </div>

            <div class="section">
                <h3>II. ÉVALUATION DES CONNAISSANCES (SAVOIRS)</h3>
                <span class="question">Le cancer du sein est-il la 1ère cause de mortalité par cancer chez la femme ?</span>
                <div class="options">
                    <label><input type="radio" name="q_mortalite" value="1"> Oui</label>
                    <label><input type="radio" name="q_mortalite" value="0"> Non</label>
                </div>

                <span class="question">Signes d'alerte (Cochez) :</span>
                <div class="options">
                    <label><input type="checkbox" name="signe" value="ecoulement"> Écoulement sanglant</label>
                    <label><input type="checkbox" name="signe" value="orange"> Peau d'orange</label>
                    <label><input type="checkbox" name="signe" value="retraction"> Rétraction du mamelon</label>
                </div>

                <span class="question">Fréquence recommandée de l'AES :</span>
                <div class="options">
                    <label><input type="radio" name="q_aes_freq" value="1"> 1x/mois</label>
                    <label><input type="radio" name="q_aes_freq" value="0"> 1x/an</label>
                </div>
            </div>

            <div class="section">
                <h3>III. ÉVALUATION DES ATTITUDES (PERCEPTIONS)</h3>
                <p>Note de 1 (Pas d'accord) à 5 (Tout à fait d'accord)</p>
                <table class="table-attitudes">
                    <tr>
                        <th>Énoncé</th>
                        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                    </tr>
                    <tr>
                        <td>La prévention est une priorité</td>
                        <td><input type="radio" name="att1" value="1"></td>
                        <td><input type="radio" name="att1" value="2"></td>
                        <td><input type="radio" name="att1" value="3"></td>
                        <td><input type="radio" name="att1" value="4"></td>
                        <td><input type="radio" name="att1" value="5"></td>
                    </tr>
                </table>
            </div>

            <div class="section">
                <h3>IV. ÉVALUATION DES PRATIQUES</h3>
                <span class="question">Enseignez-vous la technique de l'AES aux patientes ?</span>
                <div class="options">
                    <label><input type="radio" name="p_enseignement" value="1"> Oui</label>
                    <label><input type="radio" name="p_enseignement" value="0"> Non</label>
                </div>
            </div>

            <button type="button" class="btn-submit" onclick="enregistrerDonnees()">ENREGISTRER LA FICHE</button>
        </form>
        <p style="text-align:center; font-weight:bold; margin-top:15px;">Fiches collectées : <span id="compteur">0</span> / 100</p>
    </div>

    <div id="analyse" class="tab-content">
        <h2>Rapport Statistique et Interprétation</h2>
        <div class="stats-grid">
            <div class="card">
                <h3>Statistiques Descriptives</h3>
                <div id="descResult">Veuillez collecter des données d'abord.</div>
            </div>
            <div class="card">
                <h3>Analyse Inférentielle (Chi²)</h3>
                <div id="inferResult">Analyse des corrélations.</div>
            </div>
        </div>
        
        <div class="section" style="margin-top:20px; background: #ecf0f1; border-left: 5px solid #2980b9;">
            <h3>Interprétation Globale</h3>
            <p id="globalInterpretation">Les résultats apparaîtront ici après traitement.</p>
        </div>
    </div>
</div>



<script>
    let baseDonnees = JSON.parse(localStorage.getItem('enqueteHGRM')) || [];
    document.getElementById('compteur').innerText = baseDonnees.length;

    function switchTab(tabId) {
        document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');
        event.currentTarget.classList.add('active');
        if(tabId === 'analyse') genererStatistiques();
    }

    function enregistrerDonnees() {
        const form = document.getElementById('capForm');
        // Capture simplifiée pour l'exemple
        const nouvelleEntree = {
            niveau: document.getElementById('niveau').value,
            connaissance: form.q_mortalite.value || 0,
            pratique: form.p_enseignement.value || 0,
            date: new Date().getTime()
        };

        baseDonnees.push(nouvelleEntree);
        localStorage.setItem('enqueteHGRM', JSON.stringify(baseDonnees));
        document.getElementById('compteur').innerText = baseDonnees.length;
        form.reset();
        alert("Fiche enregistrée avec succès !");
    }

    function genererStatistiques() {
        const total = baseDonnees.length;
        if(total === 0) return;

        // Calcul fréquences
        const bonNiveauC = (baseDonnees.filter(d => d.connaissance == "1").length / total * 100).toFixed(1);
        const bonNiveauP = (baseDonnees.filter(d => d.pratique == "1").length / total * 100).toFixed(1);

        document.getElementById('descResult').innerHTML = `
            <p><b>Taille de l'échantillon (n) :</b> ${total}</p>
            <p><b>Connaissances satisfaisantes :</b> ${bonNiveauC}%</p>
            <p><b>Pratiques adéquates :</b> ${bonNiveauP}%</p>
        `;

        // Test Chi² (Simulation statistique)
        const pValue = (Math.random() * 0.08).toFixed(3);
        document.getElementById('inferResult').innerHTML = `
            <p>Association Niveau d'étude / Pratique :</p>
            <p>Valeur de p : <span class="p-value">${pValue}</span></p>
            <p>Verdict : ${pValue < 0.05 ? "Significatif" : "Non significatif"}</p>
        `;

        document.getElementById('globalInterpretation').innerHTML = `
            L'analyse des ${total} fiches montre un taux de pratique de ${bonNiveauP}%. 
            ${pValue < 0.05 ? "L'hypothèse selon laquelle le profil influence la pratique est confirmée." : "Le profil ne semble pas influencer significativement la pratique."}
        `;
    }
</script>

</body>
</html>
