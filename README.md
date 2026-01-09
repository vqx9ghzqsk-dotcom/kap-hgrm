<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Système Expert CAP - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --secondary: #1e293b; --accent: #db2777; --bg: #f8fafc; --text: #334155; }
        body { font-family: 'Segoe UI', system-ui, sans-serif; background-color: var(--bg); color: var(--text); margin: 0; padding: 0; }
        .container { max-width: 1150px; margin: 20px auto; padding: 20px; }
        
        /* Navigation par onglets */
        .nav-tabs { display: flex; flex-wrap: wrap; gap: 5px; background: #e2e8f0; padding: 5px; border-radius: 10px; position: sticky; top: 0; z-index: 100; }
        .tab-btn { flex: 1; padding: 12px; border: none; border-radius: 8px; cursor: pointer; font-weight: 600; transition: 0.3s; color: #475569; font-size: 12px; }
        .tab-btn.active { background: var(--primary); color: white; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); }

        /* Sections */
        .page { display: none; background: white; padding: 30px; border-radius: 12px; margin-top: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
        .page.active { display: block; }
        
        /* Style du nouveau formulaire intégré */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables Likert */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        /* Checkboxes Grid */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 10px; transform: scale(1.2); }

        /* Analyse & Résultats */
        .stats-card { background: #f1f5f9; border-radius: 8px; padding: 20px; margin-bottom: 20px; border-top: 4px solid var(--primary); }
        .metric { font-size: 2em; font-weight: bold; color: var(--primary); }
        .chart-sim { height: 20px; background: #e2e8f0; border-radius: 10px; margin-top: 10px; overflow: hidden; }
        .chart-bar { height: 100%; background: var(--primary); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; }
        .btn-excel { background: #2e7d32; color: white; border: none; padding: 8px 15px; border-radius: 5px; font-weight: bold; cursor: pointer; font-size: 11px; }
    </style>
</head>
<body>

<div class="container">
    <div class="nav-tabs">
        <button class="tab-btn active" onclick="openPage('recolte')">1. COLLECTE (FORMULAIRE)</button>
        <button class="tab-btn" onclick="openPage('traitement')">2. DÉPOUILLEMENT & MATRICE</button>
        <button class="tab-btn" onclick="openPage('resultats')">3. ANALYSE DES SCORES</button>
        <button class="tab-btn" onclick="openPage('conclusion')">4. SYNTHÈSE & RECOMMANDATIONS</button>
        <button type="button" class="btn-excel" onclick="exportCSV()" style="margin-left:auto; margin-top:5px; margin-bottom:5px; margin-right:5px;">⬇️ EXCEL (CSV)</button>
    </div>

    <div id="recolte" class="page active">
        <form id="formKAP">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field">
                    <label>Code Enquêté(e)</label>
                    <input type="text" name="code" placeholder="Ex: HGRM-2026-01" required>
                </div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Urgences / Médecine Interne</option>
                    </select>
                </div>
                <div class="field">
                    <label>Niveau d'étude</label>
                    <select name="niveau">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="A0">L0/L1 (Licenciée)</option>
                        <option value="Master">Master / Doctorat</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge (Années)</label><input type="number" name="age" min="18" max="65" value="30"></div>
                <div class="field"><label>Années d'expérience</label><input type="number" name="experience" min="0" value="5"></div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>1ère cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="c1"><option value="1">Vrai (Oui)</option><option value="0">Faux (Non)</option><option value="0">Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>Âge recommandé pour débuter l'AES ?</label>
                    <select name="c2"><option value="0">Dès 12 ans</option><option value="1">Dès 20 ans</option><option value="0">Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Meilleur moment pour l'AES ?</label>
                    <select name="c3"><option value="1">7 jours après les règles</option><option value="0">Pendant les règles</option><option value="0">N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060; font-size: 13px;">Signes cliniques d'alerte (Signes à rechercher) :</label>
            <div class="check-group">
                <label class="check-item"><input type="checkbox" name="signe" value="Nodule"> Nodule dur, fixe et indolore</label>
                <label class="check-item"><input type="checkbox" name="signe" value="Ecoulement"> Écoulement séro-sanguinolent</label>
                <label class="check-item"><input type="checkbox" name="signe" value="Retraction"> Rétraction du mamelon</label>
                <label class="check-item"><input type="checkbox" name="signe" value="Orange"> Aspect de "peau d'orange"</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (1 À 5)</div>
            <table>
                <thead>
                    <tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="text-left">Je me sens capable de détecter un nodule suspect.</td>
                        <td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4" checked></td><td><input type="radio" name="att1" value="5"></td>
                    </tr>
                    <tr>
                        <td class="text-left">Le diagnostic de cancer est une sentence de mort en RDC.</td>
                        <td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2" checked></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td>
                    </tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence de la palpation clinique :</label>
                    <select name="p1">
                        <option value="1">Systématique</option>
                        <option value="0.5">Uniquement si plainte</option>
                        <option value="0">Jamais / Rarement</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignement de l'AES :</label>
                    <select name="p2">
                        <option value="1">Démonstration physique</option>
                        <option value="0.5">Explication verbale</option>
                        <option value="0">Non enseigné</option>
                    </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="sauvegarderDonnees()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="traitement" class="page">
        <h1>Dépouillement & Matrice</h1>
        <div class="stats-card">
            <div id="tableContainer">Aucune donnée saisie.</div>
        </div>
    </div>

    <div id="resultats" class="page">
        <h1>Analyse des Scores CAP</h1>
        <div class="grid">
            <div class="stats-card">
                <h3>Niveau de Connaissances</h3>
                <div class="metric" id="res_con">0%</div>
                <div class="chart-sim"><div id="bar_con" class="chart-bar" style="width: 0%;"></div></div>
            </div>
            <div class="stats-card">
                <h3>Score Pratique</h3>
                <div class="metric" id="res_prat">0%</div>
                <div class="chart-sim"><div id="bar_prat" class="chart-bar" style="width: 0%;"></div></div>
            </div>
        </div>
    </div>

    <div id="conclusion" class="page">
        <h1>Synthèse & Recommandations</h1>
        <div class="stats-card" style="border-top-color: #f59e0b;">
            <h3>Recommandations pour l'HGRM Makala</h3>
            <ul id="reco_list">
                <li>Organiser des sessions de formation continue sur les signes précoces.</li>
                <li>Aménager des espaces respectant l'intimité pour la palpation.</li>
                <li>Fournir des boîtes à images pour l'éducation des patientes.</li>
            </ul>
        </div>
    </div>
</div>

<script>
    let database = JSON.parse(localStorage.getItem('memo_makala_final')) || [];

    function openPage(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        if(event) event.currentTarget.classList.add('active');
        
        if(id === 'traitement') afficherDepouillement();
        if(id === 'resultats') calculerResultats();
    }

    function sauvegarderDonnees() {
        const form = document.getElementById('formKAP');
        const formData = new FormData(form);
        const data = Object.fromEntries(formData.entries());
        
        // Gestion des signes (checkboxes multiples)
        data.signes = formData.getAll('signe').join('; ');

        database.push(data);
        localStorage.setItem('memo_makala_final', JSON.stringify(database));
        alert("Données HGRM enregistrées avec succès !");
        form.reset();
    }

    function afficherDepouillement() {
        const container = document.getElementById('tableContainer');
        if(database.length === 0) { container.innerHTML = "Base vide."; return; }

        let html = "<table><tr><th>Code</th><th>Service</th><th>Niveau</th><th>Savoir (Score)</th><th>Pratique</th></tr>";
        database.forEach(d => {
            let scoreSavoir = (parseInt(d.c1)||0) + (parseInt(d.c2)||0) + (parseInt(d.c3)||0);
            html += `<tr><td>${d.code}</td><td>${d.service}</td><td>${d.niveau}</td><td>${scoreSavoir}/3</td><td>${d.p1}</td></tr>`;
        });
        html += "</table>";
        container.innerHTML = html;
    }

    function calculerResultats() {
        const total = database.length;
        if(total === 0) return;

        let totalSavoir = 0;
        let totalPratique = 0;

        database.forEach(d => {
            totalSavoir += (parseInt(d.c1)||0) + (parseInt(d.c2)||0) + (parseInt(d.c3)||0);
            totalPratique += parseFloat(d.p1) + parseFloat(d.p2);
        });

        const percSavoir = ((totalSavoir / (total * 3)) * 100).toFixed(1);
        const percPrat = ((totalPratique / (total * 2)) * 100).toFixed(1);

        document.getElementById('res_con').innerText = percSavoir + "%";
        document.getElementById('bar_con').style.width = percSavoir + "%";
        document.getElementById('res_prat').innerText = percPrat + "%";
        document.getElementById('bar_prat').style.width = percPrat + "%";
    }

    function exportCSV() {
        if(database.length === 0) return alert("Pas de données à exporter.");
        let csv = "Code,Service,Niveau,Age,Exp,Savoir1,Savoir2,Savoir3,Pratique1,Pratique2\n";
        database.forEach(d => {
            csv += `${d.code},${d.service},${d.niveau},${d.age},${d.experience},${d.c1},${d.c2},${d.c3},${d.p1},${d.p2}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'Resultats_HGRM_Makala.csv';
        a.click();
    }
</script>
</body>
</html>
