<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM : Étude Cancer du Sein</title>
    <style>
        :root { --primary: #b03060; --secondary: #fce4ec; --dark: #2c3e50; }
        body { font-family: 'Segoe UI', Tahoma, sans-serif; background: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1150px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 5px 25px rgba(0,0,0,0.1); overflow: hidden; }
        
        /* Menu Navigation */
        .tabs { display: flex; background: #fff; border-bottom: 3px solid var(--primary); position: sticky; top: 0; z-index: 1000; }
        .tab { padding: 15px 20px; font-weight: bold; cursor: pointer; font-size: 12px; color: #555; border-right: 1px solid #eee; transition: 0.3s; flex: 1; text-align: center; }
        .tab.active { background: var(--primary); color: white; }
        .tab:hover:not(.active) { background: #f8f9fa; }

        .content { padding: 30px; display: none; }
        .content.active { display: block; }

        .section-header { background: var(--secondary); color: var(--primary); padding: 15px; border-left: 5px solid var(--primary); font-weight: bold; margin: 25px 0 15px; text-transform: uppercase; font-size: 14px; }
        
        /* Formulaire */
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
        .input-group { display: flex; flex-direction: column; margin-bottom: 15px; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 8px; color: var(--dark); }
        select, input { padding: 12px; border: 1px solid #ccc; border-radius: 6px; outline: none; transition: 0.3s; }
        select:focus { border-color: var(--primary); }

        /* Tables & Matrices */
        table { width: 100%; border-collapse: collapse; margin-top: 15px; font-size: 13px; }
        th, td { border: 1px solid #eee; padding: 12px; text-align: center; }
        th { background: #f8f9fa; color: var(--dark); }
        .text-left { text-align: left; }

        /* Dashboards */
        .kpi-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px; margin-bottom: 30px; }
        .kpi-card { background: white; border: 1px solid #ddd; padding: 20px; border-radius: 10px; text-align: center; border-bottom: 4px solid var(--primary); }
        .kpi-val { font-size: 28px; font-weight: bold; color: var(--primary); }
        .kpi-label { font-size: 12px; color: #777; margin-top: 5px; text-transform: uppercase; }

        .btn-submit { width: 100%; background: var(--primary); color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 20px; }
        .btn-submit:hover { background: #8e264d; }

        .matrix-box { background: #fff; border: 1px solid #ddd; padding: 15px; border-radius: 8px; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <div class="tab active" onclick="openTab(1)">1. COLLECTE (OBJECTIFS 1-3)</div>
        <div class="tab" onclick="openTab(2)">2. DÉPOUILLEMENT</div>
        <div class="tab" onclick="openTab(3)">3. ANALYSE (QUESTIONS RECH.)</div>
        <div class="tab" onclick="openTab(4)">4. RECOMMANDATIONS (OBJ. 4)</div>
    </div>

    <div id="t1" class="content active">
        <form id="kapForm">
            <div class="section-header">I. Profil & Identification (Variable Indépendante)</div>
            <div class="grid">
                <div class="input-group"><label>Code de la fiche</label><input type="text" name="code" placeholder="Ex: INF/001" required></div>
                <div class="input-group">
                    <label>Niveau d'étude</label>
                    <select name="etude" id="f_etude">
                        <option value="A2">A2 (Diplômée)</option>
                        <option value="A1" selected>A1 (Graduée)</option>
                        <option value="L">L (Licenciée)</option>
                        <option value="M">Master / Docteur</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>Service</label>
                    <select name="service">
                        <option>Gynéco-Obstétrique</option>
                        <option>Consultation Prénatale</option>
                        <option>Médecine Interne</option>
                        <option>Chirurgie / Urgences</option>
                    </select>
                </div>
            </div>

            <div class="section-header">II. ÉVALUATION DES CONNAISSANCES (OBJ. 1)</div>
            <div class="grid">
                <div class="input-group">
                    <label>Le cancer du sein est-il curable ?</label>
                    <select name="k1"><option value="1">Oui, si dépistage précoce</option><option value="0">Non / Ne sait pas</option></select>
                </div>
                <div class="input-group">
                    <label>Âge recommandé pour l'AES ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1">Dès 20 ans</option></select>
                </div>
            </div>

            <div class="section-header">III. ATTITUDES & PERCEPTIONS (OBJ. 2)</div>
            <table>
                <thead><tr><th class="text-left">Critères de perception</th><th>1 (Min)</th><th>2</th><th>3</th><th>4</th><th>5 (Max)</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">Importance de la prévention dans mon travail quotidien</td><td><input type="radio" name="a1" value="1"></td><td><input type="radio" name="a1" value="2"></td><td><input type="radio" name="a1" value="3"></td><td><input type="radio" name="a1" value="4"></td><td><input type="radio" name="a1" value="5" checked></td></tr>
                    <tr><td class="text-left">La pudeur est un obstacle majeur au dépistage</td><td><input type="radio" name="a2" value="1"></td><td><input type="radio" name="a2" value="2"></td><td><input type="radio" name="a2" value="3"></td><td><input type="radio" name="a2" value="4"></td><td><input type="radio" name="a2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-header">IV. PRATIQUES & OBSTACLES (OBJ. 3)</div>
            <div class="grid">
                <div class="input-group">
                    <label>Palpation des seins (ECS)</label>
                    <select name="p1"><option value="2">Systématique</option><option value="1">Parfois</option><option value="0">Jamais</option></select>
                </div>
                <div class="input-group">
                    <label>Enseignement de l'AES aux femmes</label>
                    <select name="p2"><option value="2">Démonstration pratique</option><option value="1">Oralement</option><option value="0">Aucun</option></select>
                </div>
            </div>
            <label style="font-size: 13px; font-weight: bold; margin-top: 10px; display: block;">Difficultés rencontrées :</label>
            <div style="display: flex; gap: 20px; flex-wrap: wrap; margin-top: 10px;">
                <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Temps"> Manque de temps</label>
                <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Local"> Absence de local isolé</label>
                <label style="font-weight: normal;"><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
            </div>

            <button type="button" class="btn-submit" onclick="ajouterFiche()">ENREGISTRER LA FICHE D'ENQUÊTE</button>
        </form>
    </div>

    <div id="t2" class="content">
        <div class="section-header">BASE DE DONNÉES BRUTES</div>
        <table id="tableDep">
            <thead><tr><th>Code</th><th>Étude</th><th>Score Savoir</th><th>Attitude</th><th>Pratique</th></tr></thead>
            <tbody></tbody>
        </table>
    </div>

    <div id="t3" class="content">
        <div class="section-header">RÉSULTATS STATISTIQUES (RÉPONSES AUX QUESTIONS DE RECH.)</div>
        <div class="kpi-grid">
            <div class="kpi-card"><div class="kpi-val" id="stat-n">0</div><div class="kpi-label">Échantillon (N)</div></div>
            <div class="kpi-card"><div class="kpi-val" id="stat-k">0%</div><div class="kpi-label">Savoir Satisfaisant</div></div>
            <div class="kpi-card"><div class="kpi-val" id="stat-p">0%</div><div class="kpi-label">Pratique Correcte</div></div>
        </div>

        <div class="matrix-box">
            <label><b>MATRICE DE CORRÉLATION : Niveau d'étude vs Pratique Correcte</b></label>
            <table id="matrixTable">
                <thead><tr><th>Niveau d'étude</th><th>Effectif</th><th>Pratique Correcte (%)</th></tr></thead>
                <tbody id="matrixBody"></tbody>
            </table>
        </div>
    </div>

    <div id="t4" class="content">
        <div class="section-header">INTERPRÉTATION & RECOMMANDATIONS (OBJ. 4)</div>
        <div id="recom-content" style="line-height: 1.8; color: #444;">
            Collectez des données pour générer les recommandations automatiques.
        </div>
    </div>
</div>

<script>
    let db = [];

    function openTab(n) {
        document.querySelectorAll('.content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('t' + n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
        if(n === 3) genererAnalyse();
        if(n === 4) genererRecom();
    }

    function ajouterFiche() {
        const f = new FormData(document.getElementById('kapForm'));
        
        // Calcul des scores selon méthodologie Bloom
        let s_k = parseInt(f.get('k1')) + parseInt(f.get('k2'));
        let s_a = parseInt(f.get('a1')) + parseInt(f.get('a2'));
        let s_p = parseInt(f.get('p1')) + parseInt(f.get('p2'));

        const data = {
            code: f.get('code'),
            etude: f.get('etude'),
            savoir: s_k >= 2 ? 'Satisfaisant' : 'Insuffisant',
            attitude: s_a >= 8 ? 'Positive' : 'Négative',
            pratique: s_p >= 3 ? 'Correcte' : 'Incorrecte',
            obstacles: Array.from(document.querySelectorAll('input[name="obs"]:checked')).length
        };

        db.push(data);
        actualiserDepouillement();
        alert("Fiche enregistrée avec succès !");
        document.getElementById('kapForm').reset();
    }

    function actualiserDepouillement() {
        const tbody = document.querySelector('#tableDep tbody');
        tbody.innerHTML = db.map(d => `<tr><td>${d.code}</td><td>${d.etude}</td><td>${d.savoir}</td><td>${d.attitude}</td><td>${d.pratique}</td></tr>`).join('');
    }

    function genererAnalyse() {
        let n = db.length; if(n === 0) return;
        let kPos = db.filter(d => d.savoir === 'Satisfaisant').length;
        let pPos = db.filter(d => d.pratique === 'Correcte').length;

        document.getElementById('stat-n').innerText = n;
        document.getElementById('stat-k').innerText = Math.round(kPos/n*100) + "%";
        document.getElementById('stat-p').innerText = Math.round(pPos/n*100) + "%";

        // Matrice de corrélation niveau d'étude
        const etudes = ['A2', 'A1', 'L', 'M'];
        let html = "";
        etudes.forEach(e => {
            let totalE = db.filter(d => d.etude === e).length;
            let correctE = db.filter(d => d.etude === e && d.pratique === 'Correcte').length;
            let perc = totalE > 0 ? Math.round(correctE/totalE*100) : 0;
            html += `<tr><td>${e}</td><td>${totalE}</td><td>${perc}%</td></tr>`;
        });
        document.getElementById('matrixBody').innerHTML = html;
    }

    function genererRecom() {
        let n = db.length; if(n === 0) return;
        let pPos = db.filter(d => d.pratique === 'Correcte').length;
        let pPerc = (pPos/n)*100;

        let txt = `<b>Conclusion de la recherche :</b> Au regard des ${n} fiches traitées, `;
        txt += pPerc < 50 ? "la pratique infirmière à l'HGRM est jugée insuffisante. " : "la pratique est globalement satisfaisante. ";
        
        txt += "<br><br><b>Recommandations stratégiques :</b><br>";
        txt += "1. <b>Formation :</b> Organiser des séminaires de recyclage sur l'ECS.<br>";
        txt += "2. <b>Infrastructure :</b> Aménager un box d'intimité dans chaque service pour favoriser l'examen physique.<br>";
        txt += "3. <b>Supervision :</b> Intégrer la palpation mammaire dans la check-list de la consultation prénatale (CPN).";
        
        document.getElementById('recom-content').innerHTML = txt;
    }
</script>

</body>
</html>
