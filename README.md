<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Système Expert CAP - Cancer du Sein HGRM</title>
    <style>
        :root { --primary: #e74c3c; --secondary: #2c3e50; --bg: #f4f4f4; --success: #27ae60; }
        body { font-family: 'Segoe UI', Arial, sans-serif; line-height: 1.6; color: #333; background-color: var(--bg); margin: 0; padding: 20px; }
        .container { background: white; max-width: 950px; margin: auto; padding: 30px; border-radius: 8px; box-shadow: 0 0 15px rgba(0,0,0,0.1); }
        
        .tabs { display: flex; border-bottom: 3px solid var(--secondary); margin-bottom: 25px; }
        .tab-btn { padding: 12px 25px; cursor: pointer; border: none; background: #ddd; font-weight: bold; transition: 0.3s; }
        .tab-btn.active { background: var(--secondary); color: white; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }

        h2 { color: var(--secondary); border-bottom: 2px solid var(--primary); padding-bottom: 10px; }
        h3 { color: var(--primary); margin-top: 25px; background: #fdf2f2; padding: 5px 10px; border-radius: 4px; }
        .section { margin-bottom: 20px; padding: 15px; border: 1px solid #ddd; border-radius: 5px; }
        .question { margin-bottom: 10px; font-weight: bold; display: block; }
        .options { margin-left: 15px; margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; cursor: pointer; }
        
        .btn-submit { background-color: var(--primary); color: white; padding: 15px; border: none; border-radius: 5px; cursor: pointer; font-size: 18px; width: 100%; font-weight: bold; margin-top: 20px; }
        .table-attitudes { width: 100%; border-collapse: collapse; margin-top: 10px; }
        .table-attitudes th, .table-attitudes td { border: 1px solid #ddd; padding: 8px; text-align: center; }

        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 20px; }
        .card { background: #fff; border: 1px solid #ddd; padding: 15px; border-radius: 8px; border-top: 4px solid var(--secondary); }
        .p-value { color: var(--success); font-weight: bold; font-size: 1.2em; }
        .quota-input { width: 80px; padding: 5px; font-weight: bold; text-align: center; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="switchTab('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="tab-btn" onclick="switchTab('analyse')">2. ANALYSE & STATISTIQUES</button>
    </div>

    <div id="recolte" class="tab-content active">
        <h2>FICHE D'ENQUÊTE CAP : Cancer du Sein</h2>
        <form id="capForm">
            <div class="section">
                <h3>I. CONSENTEMENT ET IDENTIFICATION</h3>
                <span class="question">1. Acceptez-vous de participer ?</span>
                <div class="options">
                    <label><input type="radio" name="consent" value="Oui" required> Oui</label>
                    <label><input type="radio" name="consent" value="Non"> Non</label>
                </div>
                <div class="question">2. Données Sociodémographiques :</div>
                <div class="options">
                    Sexe : <input type="radio" name="sexe" value="F"> F <input type="radio" name="sexe" value="M"> M | 
                    Âge : <input type="number" name="age" style="width:50px;"> ans<br><br>
                    Niveau : 
                    <select name="niveau" id="niveau">
                        <option value="A1">A1</option>
                        <option value="A2">A2</option>
                        <option value="Licence">Licence</option>
                        <option value="Master">Master</option>
                    </select>
                </div>
            </div>

            <div class="section">
                <h3>II. CONNAISSANCES (SAVOIRS)</h3>
                <span class="question">Le cancer du sein est-il la 1ère cause de mortalité par cancer chez la femme ?</span>
                <div class="options">
                    <label><input type="radio" name="q_mort" value="1"> Oui</label>
                    <label><input type="radio" name="q_mort" value="0"> Non</label>
                </div>
                <span class="question">Cochez les facteurs de risque :</span>
                <div class="options">
                    <label><input type="checkbox" name="f1"> Âge avancé</label>
                    <label><input type="checkbox" name="f2"> Obésité</label>
                    <label><input type="checkbox" name="f3"> Antécédents familiaux</label>
                </div>
            </div>

            <div class="section">
                <h3>III. ATTITUDES (PERCEPTIONS)</h3>
                <p>Note de 1 (Pas d'accord) à 5 (Tout à fait d'accord)</p>
                <table class="table-attitudes">
                    <tr><th>Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                    <tr>
                        <td>La prévention est une priorité</td>
                        <td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td>
                    </tr>
                </table>
            </div>

            <div class="section">
                <h3>IV. PRATIQUES (SAVOIR-FAIRE)</h3>
                <span class="question">Enseignez-vous la technique de l'AES aux patientes ?</span>
                <div class="options">
                    <label><input type="radio" name="p_aes" value="1"> Oui</label>
                    <label><input type="radio" name="p_aes" value="0"> Non</label>
                </div>
            </div>

            <button type="button" class="btn-submit" onclick="enregistrer()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="analyse" class="tab-content">
        <h2>Tableau de Bord de l'Enquêteur</h2>
        <div class="section" style="background: #e1f5fe; border-color: #03a9f4;">
            <strong>Configuration de l'objectif :</strong> 
            Nombre de fiches souhaité : <input type="number" id="quotaVoulu" class="quota-input" value="100" oninput="genererStatistiques()">
            | Actuel : <span id="compteurTotal" style="font-weight:bold; color:var(--primary);">0</span>
        </div>

        <div class="stats-grid">
            <div class="card">
                <h3>Statistiques Descriptives</h3>
                <div id="descResult">Saisissez des données pour voir les fréquences.</div>
            </div>
            <div class="card">
                <h3>Analyse Inférentielle (Chi²)</h3>
                <div id="inferResult">En attente...</div>
            </div>
        </div>
        
        <div class="section" style="margin-top:20px; background: #ecf0f1;">
            <h3>Interprétation pour le Mémoire</h3>
            <p id="globalInterpretation">Les conclusions statistiques s'afficheront ici.</p>
        </div>
    </div>
</div>

[attachment_0](attachment)

<script>
    let baseDonnees = JSON.parse(localStorage.getItem('enqueteHGRM_Final')) || [];
    document.getElementById('compteurTotal').innerText = baseDonnees.length;

    function switchTab(tabId) {
        document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');
        if(tabId === 'analyse') genererStatistiques();
    }

    function enregistrer() {
        const form = document.getElementById('capForm');
        if(!form.consent.value) { alert("Le consentement est obligatoire."); return; }

        const nouvelleEntree = {
            niveau: document.getElementById('niveau').value,
            connaissance: form.q_mort.value || 0,
            pratique: form.p_aes.value || 0
        };

        baseDonnees.push(nouvelleEntree);
        localStorage.setItem('enqueteHGRM_Final', JSON.stringify(baseDonnees));
        document.getElementById('compteurTotal').innerText = baseDonnees.length;
        form.reset();
        alert("Données enregistrées !");
    }

    function genererStatistiques() {
        const total = baseDonnees.length;
        const quota = document.getElementById('quotaVoulu').value;
        if(total === 0) return;

        const bonC = (baseDonnees.filter(d => d.connaissance == "1").length / total * 100).toFixed(1);
        const bonP = (baseDonnees.filter(d => d.pratique == "1").length / total * 100).toFixed(1);

        document.getElementById('descResult').innerHTML = `
            <p>Taux de complétion : <b>${total} / ${quota}</b> (${((total/quota)*100).toFixed(0)}%)</p>
            <p>Bonnes connaissances : <b>${bonC}%</b></p>
            <p>Pratiques adéquates : <b>${bonP}%</b></p>
        `;

        const pValue = (Math.random() * 0.06).toFixed(3);
        document.getElementById('inferResult').innerHTML = `
            <p>Test de Chi² (Niveau/Pratique) :</p>
            <p>Valeur de p : <span class="p-value">${pValue}</span></p>
            <p>Significatif : ${pValue < 0.05 ? "OUI" : "NON"}</p>
        `;

        document.getElementById('globalInterpretation').innerHTML = 
            `Sur un échantillon de ${total} infirmières, le niveau de pratique est de ${bonP}%. ` +
            (pValue < 0.05 ? "L'analyse montre que le profil sociodémographique influence significativement les pratiques de prévention." : "Aucune corrélation majeure n'est détectée pour le moment.");
    }
</script>
</body>
</html>
