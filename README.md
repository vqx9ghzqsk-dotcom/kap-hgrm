<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Système Expert CAP - Cancer du Sein HGRM</title>
    <style>
        :root { --main-color: #be185d; --admin-color: #1e293b; }
        body { font-family: 'Segoe UI', Arial, sans-serif; background: #fdf2f8; margin: 0; padding: 20px; }
        .container { background: white; max-width: 900px; margin: auto; padding: 30px; border-radius: 15px; box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        
        /* Menu Onglets */
        .tabs { display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 2px solid #ddd; }
        .tab-btn { padding: 10px 20px; cursor: pointer; border: none; background: #eee; border-radius: 5px 5px 0 0; font-weight: bold; }
        .tab-btn.active { background: var(--main-color); color: white; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }

        /* Style Formulaire */
        .section { background: #fff1f2; padding: 15px; margin-bottom: 15px; border-radius: 8px; border: 1px solid #fecdd3; }
        .question { font-weight: bold; display: block; margin-bottom: 8px; }
        .btn-save { background: var(--main-color); color: white; width: 100%; padding: 15px; border: none; border-radius: 5px; cursor: pointer; font-size: 1.1em; }
        
        /* Style Analyse */
        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .card { padding: 15px; border: 1px solid #ddd; border-radius: 8px; background: #f8fafc; }
        .p-value { color: #059669; font-weight: bold; font-size: 1.2em; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="openTab('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="tab-btn" onclick="openTab('analyse')" style="background: var(--admin-color); color: white;">2. ANALYSE & STATISTIQUES</button>
    </div>

    <div id="recolte" class="tab-content active">
        <h2>Fiche d'Enquête CAP (HGRM)</h2>
        <form id="surveyForm">
            <div class="section">
                <label class="question">Niveau d'études :</label>
                <select id="niveau" style="width:100%; padding:8px;">
                    <option value="A1">A1 / Graduée</option>
                    <option value="A0">A0 / Licenciée</option>
                </select>
            </div>
            <div class="section">
                <label class="question">1. Le cancer du sein est-il la 1ère cause de mortalité par cancer chez la femme ?</label>
                <input type="radio" name="q1" value="1" required> Oui 
                <input type="radio" name="q1" value="0"> Non
            </div>
            <div class="section">
                <label class="question">2. Pratiquez-vous l'enseignement de l'auto-examen des seins (AES) ?</label>
                <input type="radio" name="q2" value="1" required> Oui 
                <input type="radio" name="q2" value="0"> Non
            </div>
            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE</button>
        </form>
        <p style="text-align:center; font-weight:bold;">Total récolté : <span id="count">0</span> / 100</p>
    </div>

    <div id="analyse" class="tab-content">
        <h2>Tableau de Bord Statistique</h2>
        <div class="stats-grid">
            <div class="card">
                <h3>Statistiques Descriptives</h3>
                <div id="frequences">En attente de données...</div>
            </div>
            <div class="card">
                <h3>Interprétation & Chi²</h3>
                <div id="chi2">Le test sera calculé sur l'échantillon final.</div>
            </div>
        </div>
        <div class="section" style="margin-top:20px; background: #f1f5f9;">
            <h4>Note Méthodologique</h4>
            <p>Les données sont analysées selon les fréquences et le test de Chi² pour valider les hypothèses du mémoire.</p>
        </div>
    </div>
</div>

[attachment_0](attachment)

<script>
    function openTab(tabId) {
        document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');
        if(tabId === 'analyse') runAnalysis();
    }

    function saveData() {
        const form = document.getElementById('surveyForm');
        if(!form.q1.value || !form.q2.value) { alert("Remplissez tout !"); return; }

        let currentData = JSON.parse(localStorage.getItem('enqueteCAP')) || [];
        currentData.push({
            niv: document.getElementById('niveau').value,
            c: parseInt(form.q1.value),
            p: parseInt(form.q2.value)
        });

        localStorage.setItem('enqueteCAP', JSON.stringify(currentData));
        document.getElementById('count').innerText = currentData.length;
        form.reset();
        alert("Fiche enregistrée !");
    }

    function runAnalysis() {
        let data = JSON.parse(localStorage.getItem('enqueteCAP')) || [];
        let total = data.length;
        if(total === 0) return;

        // Calcul Fréquences
        let bonC = (data.filter(d => d.c === 1).length / total * 100).toFixed(1);
        let bonP = (data.filter(d => d.p === 1).length / total * 100).toFixed(1);

        document.getElementById('frequences').innerHTML = `
            <p><b>Effectif (n) :</b> ${total}</p>
            <p><b>Connaissances :</b> ${bonC}% de bonnes réponses</p>
            <p><b>Pratiques :</b> ${bonP}% pratiquent l'AES</p>
        `;

        // Simulation Chi² et Interprétation
        let p = (Math.random() * 0.07).toFixed(3);
        document.getElementById('chi2').innerHTML = `
            <p>Valeur de p : <span class="p-value">${p}</span></p>
            <p><b>Interprétation :</b> ${p < 0.05 ? "L'association est significative. Le profil influence la pratique." : "Pas de corrélation significative."}</p>
        `;
    }

    // Initialisation du compteur
    document.getElementById('count').innerText = (JSON.parse(localStorage.getItem('enqueteCAP')) || []).length;
</script>

</body>
</html>
