<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kap-hgrm - Système de Collecte</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 950px; margin: auto; background: white; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); overflow: hidden; }
        
        /* Navigation & Header */
        .header-tabs { display: flex; background: #fff; border-bottom: 2px solid #e91e63; padding: 10px; align-items: center; gap: 5px; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 13px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        /* Form Styling */
        .form-content { padding: 20px; }
        .section-title { background: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; border-left: 6px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 600; margin-bottom: 6px; color: #444; }
        input[type="text"], input[type="number"], select { padding: 10px; border: 1px solid #ccc; border-radius: 5px; font-size: 14px; background: #f9f9f9; }

        /* Table Likert */
        table { width: 100%; border-collapse: collapse; margin: 15px 0; }
        th, td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; }

        /* Multi-choice specific */
        .checkbox-list { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 5px; }
        .check-item { display: flex; align-items: center; font-size: 13px; }
        .check-item input { margin-right: 10px; }

        .submit-area { margin-top: 30px; border-top: 1px solid #eee; padding-top: 20px; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 18px; border: none; border-radius: 5px; font-size: 16px; font-weight: bold; cursor: pointer; text-transform: uppercase; }
        .btn-save:hover { background: #8e244d; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <a href="#" class="tab active">1. COLLECTE</a>
        <a href="#" class="tab">2. BASE DE DONNÉES</a>
        <a href="#" class="tab">3. ANALYSE CAP</a>
        <button class="btn-excel">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <form class="form-content">
        <div class="section-title">I. IDENTIFICATION & CONTEXTE PROFESSIONNEL</div>
        <div class="row">
            <div class="field"><label>ID Enquêté *</label><input type="text" required></div>
            <div class="field"><label>Service (ex: Maternité, Chirurgie) *</label><input type="text" required></div>
            <div class="field">
                <label>Niveau d'études *</label>
                <select><option>A2</option><option>A1</option><option>L0/L1</option><option>Médecin</option></select>
            </div>
        </div>
        <div class="row">
            <div class="field"><label>Ancienneté Pro (ans)</label><input type="number"></div>
            <div class="field">
                <label>Avez-vous déjà soigné une patiente cancéreuse ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
        </div>

        <div class="section-title">II. CONNAISSANCES APPROFONDIES (SAVOIRS)</div>
        <div class="row">
            <div class="field"><label>La nulliparité est un risque ?</label><select><option>---</option><option>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>La ménopause tardive augmente le risque ?</label><select><option>---</option><option>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>L'AES doit se faire 7 jours après les règles ?</label><select><option>---</option><option>Vrai</option><option>Faux</option></select></div>
        </div>
        <div class="row">
            <div class="field"><label>Le risque augmente avec l'âge ?</label><select><option>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>L'obésité/sédentarité sont des facteurs ?</label><select><option>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>L'allaitement est protecteur ?</label><select><option>Vrai</option><option>Faux</option></select></div>
        </div>
        <div class="row">
            <div class="field"><label>Le cancer du sein est-il contagieux ? (Mythe)</label><select><option>Faux</option><option>Vrai</option></select></div>
            <div class="field"><label>L'échographie utile chez la femme < 35 ans ?</label><select><option>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>Une plaie qui ne guérit pas est un signe ?</label><select><option>Vrai</option><option>Faux</option></select></div>
        </div>

        <label style="margin-top:10px; display:block;">Signes d'alerte identifiés (Cochez tout ce qui s'applique) :</label>
        <div class="checkbox-list" style="margin-bottom:15px;">
            <label class="check-item"><input type="checkbox"> Présence d'une masse ou nodule dur</label>
            <label class="check-item"><input type="checkbox"> Aspect 'peau d'orange' sur le sein</label>
            <label class="check-item"><input type="checkbox"> Écoulement de sang par le mamelon</label>
            <label class="check-item"><input type="checkbox"> Rétraction du mamelon</label>
        </div>

        <div class="section-title">III. ATTITUDES & PERCEPTIONS (LIKERT 1-5)</div>
        <table>
            <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
            <tbody>
                <tr><td class="text-left">Je pense que la médecine traditionnelle peut guérir le cancer.</td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td></tr>
                <tr><td class="text-left">J'ai peur de découvrir un nodule lors d'un examen.</td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td></tr>
                <tr><td class="text-left">Le dépistage précoce coûte trop cher pour mes patientes.</td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td></tr>
                <tr><td class="text-left">La mastectomie est une mutilation inacceptable.</td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td></tr>
            </tbody>
        </table>

        <div class="section-title">IV. PRATIQUES PROFESSIONNELLES (SAVOIR-FAIRE)</div>
        <div class="row">
            <div class="field"><label>Demandez-vous l'histoire familiale de cancer ?</label><select><option>Systématiquement</option><option>Souvent</option><option>Rarement</option></select></div>
            <div class="field"><label>Inspectez-vous les aisselles (creux axillaires) ?</label><select><option>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Remettez-vous des dépliants sur le cancer ?</label><select><option>Oui</option><option>Non</option></select></div>
        </div>
        <div class="row">
            <div class="field"><label>Pratique personnelle de l'AES :</label><select><option>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Fréquence de l'examen clinique en consultation :</label><select><option>Toujours (systématique)</option><option>Parfois</option></select></div>
            <div class="field"><label>Nombre moyen de palpations ce mois :</label><input type="number" value="0"></div>
        </div>

        <div class="section-title">V. BARRIÈRES SYSTÉMIQUES & OBSTACLES (RDC)</div>
        <label>Qu'est-ce qui vous empêche d'agir plus ? (Obstacles identifiés) :</label>
        <div class="checkbox-list">
            <label class="check-item"><input type="checkbox"> Absence de protocoles écrits</label>
            <label class="check-item"><input type="checkbox"> Influence religieuse/tabous des patientes</label>
            <label class="check-item"><input type="checkbox"> Manque de salle d'examen isolée (Pudeur)</label>
            <label class="check-item"><input type="checkbox"> Coût élevé des examens (Mammographie)</label>
            <label class="check-item"><input type="checkbox"> Manque de matériels (Affiches, outils éducatifs)</label>
            <label class="check-item"><input type="checkbox"> Manque de formation du personnel</label>
            <label class="check-item"><input type="checkbox"> Surcharge de travail / Manque de temps</label>
            <label class="check-item"><input type="checkbox"> Distance vers les centres équipés</label>
        </div>

        <div class="submit-area">
            <button type="button" class="btn-save" onclick="alert('Données enregistrées localement !')">ENREGISTRER LA FICHE COMPLÈTE</button>
        </div>
    </form>
</div>

</body>
</html>
