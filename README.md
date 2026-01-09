<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Application CAP Complète - HGRM Makala</title>
    <style>
        :root { --primary: #be185d; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', sans-serif; background: var(--bg); margin: 0; padding: 10px; }
        .container { max-width: 1100px; margin: auto; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1); }
        .tabs { display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 2px solid #eee; padding-bottom: 10px; }
        .tab-btn { padding: 10px 20px; border: none; background: #eee; cursor: pointer; border-radius: 5px; font-weight: bold; }
        .tab-btn.active { background: var(--primary); color: white; }
        .page { display: none; }
        .page.active { display: block; }
        h2 { color: var(--primary); border-left: 5px solid var(--primary); padding-left: 10px; font-size: 1.1em; margin-top: 20px; background: #fff1f2; padding-top: 5px; padding-bottom: 5px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px; }
        .field { border: 1px solid #ddd; padding: 12px; border-radius: 8px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; font-size: 0.9em; }
        input, select, textarea { width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        .btn-save { background: var(--primary); color: white; border: none; padding: 15px; width: 100%; border-radius: 8px; font-size: 1.1em; cursor: pointer; margin-top: 20px; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.9em; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
    </style>
</head>
<body>

<div class="container">
    <div class="tabs">
        <button class="tab-btn active" onclick="nav('recolte')">1. RÉCOLTE DES DONNÉES</button>
        <button class="tab-btn" onclick="nav('analyse')">2. ANALYSE & RÉSULTATS</button>
    </div>

    <div id="recolte" class="page active">
        <form id="capForm">
            <h2>I. IDENTIFICATION & CONSENTEMENT</h2>
            <div class="grid">
                [span_9](start_span)[span_10](start_span)<div class="field"><label>Code :</label><input type="text" name="code" required>[span_9](end_span)[span_10](end_span)</div>
                [span_11](start_span)[span_12](start_span)<div class="field"><label>Service :</label><input type="text" name="service">[span_11](end_span)[span_12](end_span)</div>
                [span_13](start_span)[span_14](start_span)<div class="field"><label>Consentement :</label><select name="consent"><option value="1">Accepté</option><option value="0">Refusé</option></select>[span_13](end_span)[span_14](end_span)</div>
            </div>

            <h2>II. DONNÉES SOCIODÉMOGRAPHIQUES</h2>
            <div class="grid">
                [span_15](start_span)[span_16](start_span)<div class="field"><label>Sexe :</label><select name="sexe"><option>Femme</option><option>Homme</option></select>[span_15](end_span)[span_16](end_span)</div>
                [span_17](start_span)[span_18](start_span)<div class="field"><label>Âge :</label><input type="number" name="age">[span_17](end_span)[span_18](end_span)</div>
                [span_19](start_span)[span_20](start_span)<div class="field"><label>État Civil :</label><select name="ecivil"><option>Célibataire</option><option>Mariée</option><option>Veuve</option><option>Autre</option></select>[span_19](end_span)[span_20](end_span)</div>
                [span_21](start_span)[span_22](start_span)<div class="field"><label>Niveau d'études :</label><select name="etude"><option>A2</option><option>A1</option><option>A0</option><option>Master</option></select>[span_21](end_span)[span_22](end_span)</div>
                [span_23](start_span)[span_24](start_span)<div class="field"><label>Anciennété (ans) :</label><input type="number" name="exp">[span_23](end_span)[span_24](end_span)</div>
                [span_25](start_span)[span_26](start_span)<div class="field"><label>Statut :</label><select name="statut"><option>Titulaire</option><option>Contractuelle</option><option>Stagiaire</option><option>Autre</option></select>[span_25](end_span)[span_26](end_span)</div>
                [span_27](start_span)[span_28](start_span)<div class="field"><label>Antécédents Familiaux :</label><select name="anteced"><option value="1">Oui</option><option value="0">Non</option></select>[span_27](end_span)[span_28](end_span)</div>
            </div>

            <h2>III. CONNAISSANCES (SAVOIRS)</h2>
            <div class="grid">
                [span_29](start_span)[span_30](start_span)<div class="field"><label>Risque augmente avec l'âge ?</label><select name="c_age"><option value="1">Vrai</option><option value="0">Faux</option></select>[span_29](end_span)[span_30](end_span)</div>
                [span_31](start_span)[span_32](start_span)<div class="field"><label>Obésité = Facteur de risque ?</label><select name="c_obese"><option value="1">Vrai</option><option value="0">Faux</option></select>[span_31](end_span)[span_32](end_span)</div>
                [span_33](start_span)<div class="field"><label>Allaitement maternel protecteur ?</label><select name="c_allait"><option value="1">Vrai</option><option value="0">Faux</option></select>[span_33](end_span)</div>
                [span_34](start_span)[span_35](start_span)<div class="field"><label>Mammographie remplace l'examen clinique ?</label><select name="c_remplace"><option value="1">Vrai</option><option value="0">Faux</option></select>[span_34](end_span)[span_35](end_span)</div>
                [span_36](start_span)[span_37](start_span)<div class="field"><label>Âge conseillé mammographie (Makala) :</label><input type="number" name="age_mammo">[span_36](end_span)[span_37](end_span)</div>
                [span_38](start_span)[span_39](start_span)<div class="field"><label>Usage Échographie :</label><select name="c_echo"><option>En complément</option><option>1ère intention (jeunes)</option><option>NSP</option></select>[span_38](end_span)[span_39](end_span)</div>
            </div>

            <h2>IV. ATTITUDES (LIKERT 1-5)</h2>
            <div class="field">
                <label>Le cancer du sein est forcément mortel en RDC ?</label>
                [span_40](start_span)<input type="range" name="att_mortel" min="1" max="5" step="1">[span_40](end_span)
            </div>

            <h2>V. PRATIQUES</h2>
            <div class="grid">
                [span_41](start_span)[span_42](start_span)<div class="field"><label>Enseignez-vous l'AES ?</label><select name="p_aes"><option value="1">Oui</option><option value="0">Non</option></select>[span_41](end_span)[span_42](end_span)</div>
                [span_43](start_span)[span_44](start_span)<div class="field"><label>Examen clinique systématique ?</label><select name="p_clin"><option>Toujours</option><option>Parfois</option><option>Jamais</option></select>[span_43](end_span)[span_44](end_span)</div>
                [span_45](start_span)<div class="field"><label>Participé à une sensibilisation ?</label><select name="p_sensib"><option value="1">Oui</option><option value="0">Non</option></select>[span_45](end_span)</div>
            </div>

            <h2>VI. OBSTACLES</h2>
            <div class="field">
                <label>Cochez les obstacles :</label>
                [span_46](start_span)[span_47](start_span)<input type="checkbox" name="obs" value="Matériel"> Manque de matériel[span_46](end_span)[span_47](end_span)<br>
                [span_48](start_span)[span_49](start_span)<input type="checkbox" name="obs" value="Formation"> Manque de formation[span_48](end_span)[span_49](end_span)<br>
                [span_50](start_span)[span_51](start_span)<input type="checkbox" name="obs" value="Distance"> Distance vers les centres[span_50](end_span)[span_51](end_span)<br>
                [span_52](start_span)[span_53](start_span)<input type="checkbox" name="obs" value="Surcharge"> Surcharge de travail[span_52](end_span)[span_53](end_span)
            </div>

            <button type="button" class="btn-save" onclick="save()">ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="analyse" class="page">
        <h2>Résultats et Analyse</h2>
        <div id="stats">Collectez des données pour voir les statistiques.</div>
    </div>
</div>

<script>
    let db = JSON.parse(localStorage.getItem('db_cap')) || [];
    function nav(id) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        event.currentTarget.classList.add('active');
        if(id === 'analyse') showStats();
    }
    function save() {
        const data = Object.fromEntries(new FormData(document.getElementById('capForm')).entries());
        db.push(data);
        localStorage.setItem('db_cap', JSON.stringify(db));
        alert("Fiche enregistrée !");
        document.getElementById('capForm').reset();
    }
    function showStats() {
        document.getElementById('stats').innerHTML = "Nombre de fiches : " + db.length;
    }
</script>
</body>
</html>
