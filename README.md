<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kap-hgrm - Collecte Automatisée</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 950px; margin: auto; background: white; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 2px solid #b03060; padding: 10px; align-items: center; gap: 8px; }
        .tab { padding: 8px 12px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        /* Form Layout */
        .form-content { padding: 20px; }
        .section-title { background: #fce4ec; color: #b03060; padding: 10px; font-weight: bold; border-left: 5px solid #b03060; margin: 20px 0 15px 0; text-transform: uppercase; font-size: 13px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin-bottom: 10px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 12px; font-weight: 600; margin-bottom: 4px; color: #444; }
        input, select { padding: 10px; border: 1px solid #ccc; border-radius: 5px; font-size: 14px; background: #fff; }

        /* Tables */
        table { width: 100%; border-collapse: collapse; margin: 10px 0; font-size: 13px; }
        th, td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .text-left { text-align: left; width: 55%; }

        /* Checkboxes */
        .checkbox-list { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; background: #fafafa; padding: 15px; border: 1px solid #eee; border-radius: 5px; }
        .check-item { display: flex; align-items: center; font-size: 12px; cursor: pointer; }
        .check-item input { margin-right: 10px; transform: scale(1.2); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 15px; border: none; border-radius: 5px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 25px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <a href="#" class="tab active">1. COLLECTE</a>
        <a href="#" class="tab">2. BASE DE DONNÉES</a>
        <a href="#" class="tab">3. ANALYSE CAP</a>
        <button type="button" class="btn-excel">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <form class="form-content">
        <div class="section-title">I. IDENTIFICATION & CONTEXTE PROFESSIONNEL</div>
        <div class="row">
            <div class="field"><label>ID Enquêté *</label><input type="text" value="ENQ-2026-001"></div>
            <div class="field"><label>Service *</label><input type="text" value="Maternité / Gynécologie"></div>
            <div class="field">
                <label>Niveau d'études *</label>
                <select><option selected>A1 (Infirmier Gradué)</option><option>A2</option><option>L0/L1</option></select>
            </div>
        </div>
        <div class="row">
            <div class="field"><label>Ancienneté Pro (ans)</label><input type="number" value="8"></div>
            <div class="field">
                <label>Déjà soigné une patiente cancéreuse ?</label>
                <select><option selected>Oui</option><option>Non</option></select>
            </div>
        </div>

        <div class="section-title">II. CONNAISSANCES APPROFONDIES (SAVOIRS)</div>
        <div class="row">
            <div class="field"><label>La nulliparité est un risque ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>La ménopause tardive est un risque ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>L'AES 7 jours après les règles ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
        </div>
        <div class="row">
            <div class="field"><label>Le risque augmente avec l'âge ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>L'obésité est un facteur ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>Le cancer est contagieux ? (Mythe)</label><select><option selected>Faux</option><option>Vrai</option></select></div>
        </div>

        <label style="margin: 10px 0 5px 0; display:block;">Signes d'alerte (Déjà sélectionnés) :</label>
        <div class="checkbox-list">
            <label class="check-item"><input type="checkbox" checked> Masse ou nodule dur</label>
            <label class="check-item"><input type="checkbox" checked> Aspect 'peau d'orange'</label>
            <label class="check-item"><input type="checkbox" checked> Écoulement de sang</label>
            <label class="check-item"><input type="checkbox"> Rétraction du mamelon</label>
        </div>

        <div class="section-title">III. ATTITUDES & PERCEPTIONS (LIKERT 1-5)</div>
        <table>
            <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
            <tbody>
                <tr><td class="text-left">Médecine traditionnelle peut guérir le cancer.</td><td><input type="radio" name="a1"></td><td><input type="radio" name="a1" checked></td><td><input type="radio" name="a1"></td><td><input type="radio" name="a1"></td><td><input type="radio" name="a1"></td></tr>
                <tr><td class="text-left">Peur de découvrir un nodule lors d'un examen.</td><td><input type="radio" name="a2"></td><td><input type="radio" name="a2"></td><td><input type="radio" name="a2"></td><td><input type="radio" name="a2" checked></td><td><input type="radio" name="a2"></td></tr>
                <tr><td class="text-left">Le dépistage coûte trop cher pour les patientes.</td><td><input type="radio" name="a3"></td><td><input type="radio" name="a3"></td><td><input type="radio" name="a3"></td><td><input type="radio" name="a3"></td><td><input type="radio" name="a3" checked></td></tr>
            </tbody>
        </table>

        <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
        <div class="row">
            <div class="field"><label>Demander l'histoire familiale ?</label><select><option selected>Systématiquement</option><option>Rarement</option></select></div>
            <div class="field"><label>Inspecter les aisselles ?</label><select><option selected>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Remettre des dépliants ?</label><select><option selected>Oui</option><option>Non</option></select></div>
        </div>

        <div class="section-title">V. BARRIÈRES & OBSTACLES (RDC)</div>
        <div class="checkbox-list">
            <label class="check-item"><input type="checkbox" checked> Absence de protocoles écrits</label>
            <label class="check-item"><input type="checkbox" checked> Coût élevé des examens</label>
            <label class="check-item"><input type="checkbox" checked> Manque de matériels (Affiches)</label>
            <label class="check-item"><input type="checkbox"> Influence religieuse</label>
            <label class="check-item"><input type="checkbox" checked> Manque de formation du personnel</label>
            <label class="check-item"><input type="checkbox"> Pudeur de la patiente</label>
        </div>

        <button type="button" class="btn-save" onclick="alert('Fiche enregistrée avec les réponses pré-remplies !')">ENREGISTRER LA FICHE COMPLÈTE</button>
    </form>
</div>

</body>
</html>
