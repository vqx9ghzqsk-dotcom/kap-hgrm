<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kap-hgrm - Collecte de données</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        .container {
            max-width: 900px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h1 { color: #2c3e50; font-size: 1.5em; margin-bottom: 20px; }
        
        /* Navigation Tabs */
        .nav-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
            padding-bottom: 10px;
        }
        .tab {
            padding: 10px 15px;
            border-radius: 4px;
            text-decoration: none;
            font-weight: bold;
            font-size: 0.9em;
            text-transform: uppercase;
        }
        .tab-active { background-color: #b03060; color: white; }
        .tab-inactive { background-color: #e0e0e0; color: #666; }
        .btn-export {
            margin-left: auto;
            background-color: #2e7d32;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
        }

        /* Section Styling */
        .section-header {
            background-color: #fce4ec;
            color: #b03060;
            padding: 10px;
            font-weight: bold;
            margin-top: 25px;
            border-left: 5px solid #b03060;
            text-transform: uppercase;
        }

        .grid-container {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 15px;
            padding: 15px 0;
        }

        .input-group {
            display: flex;
            flex-direction: column;
        }
        label {
            font-size: 0.85em;
            margin-bottom: 5px;
            font-weight: 600;
        }
        input, select {
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            background-color: #fafafa;
        }

        /* Likert Table */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            border: 1px solid #eee;
            padding: 10px;
            text-align: center;
            font-size: 0.9em;
        }
        .text-left { text-align: left; }

        /* Checkboxes */
        .checkbox-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
            padding: 10px 0;
        }
        .checkbox-item {
            display: flex;
            align-items: center;
            font-size: 0.9em;
        }
        .checkbox-item input { margin-right: 10px; }

        /* Submit Button */
        .submit-btn {
            width: 100%;
            background-color: #b03060;
            color: white;
            border: none;
            padding: 15px;
            font-size: 1em;
            font-weight: bold;
            border-radius: 4px;
            margin-top: 30px;
            cursor: pointer;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>kap-hgrm</h1>

    <div class="nav-tabs">
        <a href="#" class="tab tab-active">1. COLLECTE</a>
        <a href="#" class="tab tab-inactive" onclick="alert('Accès à la Base de Données')">2. BASE DE DONNÉES</a>
        <a href="#" class="tab tab-inactive">3. ANALYSE CAP</a>
        <button class="btn-export">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <form>
        <div class="section-header">I. IDENTIFICATION & CONTEXTE PROFESSIONNEL</div>
        <div class="grid-container">
            <div class="input-group">
                <label>ID Enquêté *</label>
                <input type="text" placeholder="Ex: 001">
            </div>
            <div class="input-group">
                <label>Service (ex: Maternité, Chirurgie) *</label>
                <input type="text">
            </div>
            <div class="input-group">
                <label>Niveau d'études *</label>
                <select>
                    <option>A2</option>
                    <option>A1</option>
                    <option>L0/L1</option>
                </select>
            </div>
            <div class="input-group">
                <label>Ancienneté Pro (ans)</label>
                <input type="number">
            </div>
            <div class="input-group">
                <label>Avez-vous déjà soigné une patiente cancéreuse ?</label>
                <select>
                    <option>Oui</option>
                    <option>Non</option>
                </select>
            </div>
        </div>

        <div class="section-header">II. CONNAISSANCES APPROFONDIES (SAVOIRS)</div>
        <div class="grid-container">
            <div class="input-group">
                <label>La nulliparité est un risque ?</label>
                <select><option>---</option><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="input-group">
                <label>La ménopause tardive augmente le risque ?</label>
                <select><option>---</option><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="input-group">
                <label>L'AES doit se faire 7 jours après les règles ?</label>
                <select><option>---</option><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="input-group">
                <label>Le cancer du sein est-il contagieux ? (Mythe)</label>
                <select><option>Faux</option><option>Vrai</option></select>
            </div>
            <div class="input-group">
                <label>L'échographie est-elle utile chez la femme de < 35 ans ?</label>
                <select><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="input-group">
                <label>Une plaie qui ne guérit pas au sein est un signe ?</label>
                <select><option>Vrai</option><option>Faux</option></select>
            </div>
        </div>

        <div class="section-header">III. ATTITUDES & PERCEPTIONS (LIKERT 1-5)</div>
        <table>
            <thead>
                <tr>
                    <th class="text-left">Énoncés</th>
                    <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td class="text-left">Je pense que la médecine traditionnelle peut guérir le cancer.</td>
                    <td><input type="radio" name="q1"></td><td><input type="radio" name="q1"></td><td><input type="radio" name="q1"></td><td><input type="radio" name="q1"></td><td><input type="radio" name="q1"></td>
                </tr>
                <tr>
                    <td class="text-left">J'ai peur de découvrir un nodule lors d'un examen.</td>
                    <td><input type="radio" name="q2"></td><td><input type="radio" name="q2"></td><td><input type="radio" name="q2"></td><td><input type="radio" name="q2"></td><td><input type="radio" name="q2"></td>
                </tr>
                <tr>
                    <td class="text-left">Le dépistage précoce coûte trop cher pour mes patientes.</td>
                    <td><input type="radio" name="q3"></td><td><input type="radio" name="q3"></td><td><input type="radio" name="q3"></td><td><input type="radio" name="q3"></td><td><input type="radio" name="q3"></td>
                </tr>
                <tr>
                    <td class="text-left">La mastectomie (ablation) est une mutilation inacceptable.</td>
                    <td><input type="radio" name="q4"></td><td><input type="radio" name="q4"></td><td><input type="radio" name="q4"></td><td><input type="radio" name="q4"></td><td><input type="radio" name="q4"></td>
                </tr>
            </tbody>
        </table>

        <div class="section-header">IV. PRATIQUES PROFESSIONNELLES</div>
        <div class="grid-container">
            <div class="input-group">
                <label>Demandez-vous l'histoire familiale de cancer ?</label>
                <select><option>Systématiquement</option><option>Rarement</option></select>
            </div>
            <div class="input-group">
                <label>Inspectez-vous les aisselles (creux axillaires) ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
            <div class="input-group">
                <label>Remettez-vous des dépliants sur le cancer ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
            <div class="input-group">
                <label>Nombre moyen de palpations faites ce mois :</label>
                <input type="number" value="0">
            </div>
        </div>

        <div class="section-header">V. BARRIÈRES SYSTÉMIQUES (RDC)</div>
        <div class="checkbox-group">
            <p style="font-size: 0.85em; font-weight: bold;">Qu'est-ce qui vous empêche d'agir plus ? (Plusieurs choix)</p>
            <label class="checkbox-item"><input type="checkbox"> Absence de protocoles écrits</label>
            <label class="checkbox-item"><input type="checkbox"> Influence religieuse des patientes</label>
            <label class="checkbox-item"><input type="checkbox"> Manque de salle d'examen isolée</label>
            <label class="checkbox-item"><input type="checkbox"> Pudeur/Honte de la patiente</label>
        </div>

        <button type="button" class="submit-btn" onclick="saveData()">Enregistrer la fiche complète</button>
    </form>
</div>

<script>
    function saveData() {
        alert("Fiche enregistrée avec succès dans la base de données !");
        // Logique de sauvegarde ou redirection vers l'onglet 2 ici
    }
</script>

</body>
</html>
