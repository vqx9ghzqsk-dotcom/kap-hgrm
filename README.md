<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kap-hgrm - Collecte</title>
    <style>
        :root {
            --primary-pink: #b03060;
            --soft-pink: #fce4ec;
            --bg-body: #f8f9fa;
            --border-color: #dee2e6;
            --text-dark: #2d3436;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-body);
            margin: 0;
            padding: 20px;
            color: var(--text-dark);
        }

        .container {
            max-width: 1000px;
            margin: auto;
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.08);
        }

        /* Menu Navigation */
        .nav-tabs {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 30px;
            border-bottom: 2px solid var(--soft-pink);
            padding-bottom: 15px;
        }
        .tab {
            padding: 10px 20px;
            border-radius: 6px;
            text-decoration: none;
            font-weight: 700;
            font-size: 0.85rem;
            transition: all 0.3s;
        }
        .tab-active { background-color: var(--primary-pink); color: white; }
        .tab-inactive { background-color: #eee; color: #888; }
        .tab-inactive:hover { background-color: #e2e2e2; }
        
        .btn-export {
            margin-left: auto;
            background-color: #27ae60;
            color: white;
            border: none;
            padding: 10px 18px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* Amélioration de la Section Collecte */
        .section-header {
            background-color: var(--soft-pink);
            color: var(--primary-pink);
            padding: 12px 15px;
            font-weight: 800;
            margin-top: 30px;
            border-radius: 6px;
            border-left: 6px solid var(--primary-pink);
            letter-spacing: 0.5px;
        }

        .grid-layout {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            padding: 20px 0;
        }

        .field-card {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        label {
            font-size: 0.9rem;
            font-weight: 600;
            color: #4a4a4a;
        }

        input[type="text"], 
        input[type="number"], 
        select {
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            background-color: #fff;
            font-size: 0.95rem;
            transition: border-color 0.2s;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--primary-pink);
            box-shadow: 0 0 0 3px rgba(176, 48, 96, 0.1);
        }

        /* Table Likert améliorée */
        .table-responsive {
            overflow-x: auto;
            margin-top: 15px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            background: #fff;
        }
        th {
            background-color: #fcfcfc;
            padding: 15px;
            font-size: 0.85rem;
            color: #777;
            border-bottom: 2px solid var(--soft-pink);
        }
        td {
            padding: 15px;
            border-bottom: 1px solid #f0f0f0;
            text-align: center;
        }
        .text-left { text-align: left; font-weight: 500; width: 50%; }

        /* Custom Radio Buttons */
        input[type="radio"] {
            transform: scale(1.3);
            accent-color: var(--primary-pink);
            cursor: pointer;
        }

        /* Barrières Systémiques */
        .checkbox-container {
            background: #fafafa;
            padding: 20px;
            border-radius: 8px;
            margin-top: 15px;
        }
        .check-item {
            display: flex;
            align-items: center;
            margin-bottom: 12px;
            cursor: pointer;
            font-size: 0.95rem;
        }
        .check-item input {
            margin-right: 12px;
            width: 18px;
            height: 18px;
            accent-color: var(--primary-pink);
        }

        .submit-btn {
            width: 100%;
            background: linear-gradient(to right, #b03060, #8e244d);
            color: white;
            border: none;
            padding: 18px;
            font-size: 1.1rem;
            font-weight: bold;
            border-radius: 8px;
            margin-top: 40px;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(176, 48, 96, 0.3);
        }

    </style>
</head>
<body>

<div class="container">
    <header>
        <h2 style="color: var(--primary-pink); margin-top: 0;">kap-hgrm</h2>
        <div class="nav-tabs">
            <a href="#" class="tab tab-active">1. COLLECTE</a>
            <a href="#" class="tab tab-inactive">2. BASE DE DONNÉES</a>
            <a href="#" class="tab tab-inactive">3. ANALYSE CAP</a>
            <button class="btn-export">📥 EXPORT EXCEL (CSV)</button>
        </div>
    </header>

    <form id="collectForm">
        <div class="section-header">I. IDENTIFICATION & CONTEXTE PROFESSIONNEL</div>
        <div class="grid-layout">
            <div class="field-card">
                <label>ID Enquêté *</label>
                <input type="text" placeholder="Entrez l'identifiant">
            </div>
            <div class="field-card">
                <label>Service (ex: Maternité, Chirurgie) *</label>
                <input type="text" placeholder="Nom du service">
            </div>
            <div class="field-card">
                <label>Niveau d'études *</label>
                <select>
                    <option value="A2">A2</option>
                    <option value="A1">A1</option>
                    <option value="L0/L1">L0 / L1</option>
                </select>
            </div>
            <div class="field-card">
                <label>Ancienneté Pro (ans)</label>
                <input type="number" min="0">
            </div>
            <div class="field-card">
                <label>Avez-vous déjà soigné une patiente cancéreuse ?</label>
                <select>
                    <option value="Oui">Oui</option>
                    <option value="Non">Non</option>
                </select>
            </div>
        </div>

        <div class="section-header">II. CONNAISSANCES APPROFONDIES (SAVOIRS)</div>
        <div class="grid-layout">
            <div class="field-card">
                <label>La nulliparité est un risque ?</label>
                <select><option>---</option><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="field-card">
                <label>La ménopause tardive augmente le risque ?</label>
                <select><option>---</option><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="field-card">
                <label>L'AES doit se faire 7 jours après les règles ?</label>
                <select><option>---</option><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="field-card">
                <label>Le cancer du sein est-il contagieux ? (Mythe)</label>
                <select><option value="Faux">Faux</option><option value="Vrai">Vrai</option></select>
            </div>
            <div class="field-card">
                <label>L'échographie est-elle utile chez la femme de < 35 ans ?</label>
                <select><option value="Vrai">Vrai</option><option value="Faux">Faux</option></select>
            </div>
            <div class="field-card">
                <label>Une plaie qui ne guérit pas au sein est un signe ?</label>
                <select><option value="Vrai">Vrai</option><option value="Faux">Faux</option></select>
            </div>
        </div>

        <div class="section-header">III. ATTITUDES & PERCEPTIONS (LIKERT 1-5)</div>
        <div class="table-responsive">
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
                        <td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td>
                    </tr>
                    <tr>
                        <td class="text-left">J'ai peur de découvrir un nodule lors d'un examen.</td>
                        <td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td>
                    </tr>
                    <tr>
                        <td class="text-left">Le dépistage précoce coûte trop cher pour mes patientes.</td>
                        <td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td>
                    </tr>
                    <tr>
                        <td class="text-left">La mastectomie (ablation) est une mutilation inacceptable.</td>
                        <td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="section-header">IV. PRATIQUES PROFESSIONNELLES</div>
        <div class="grid-layout">
            <div class="field-card">
                <label>Demandez-vous l'histoire familiale de cancer ?</label>
                <select><option>Systématiquement</option><option>Rarement</option><option>Jamais</option></select>
            </div>
            <div class="field-card">
                <label>Inspectez-vous les aisselles (creux axillaires) ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
            <div class="field-card">
                <label>Remettez-vous des dépliants sur le cancer ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
            <div class="field-card">
                <label>Nombre moyen de palpations faites ce mois :</label>
                <input type="number" value="0">
            </div>
        </div>

        <div class="section-header">V. BARRIÈRES SYSTÉMIQUES (RDC)</div>
        <div class="checkbox-container">
            <p style="margin-top:0; font-weight:700; color: #666; font-size: 0.85rem;">Qu'est-ce qui vous empêche d'agir plus ? (Plusieurs choix possibles)</p>
            <label class="check-item"><input type="checkbox"> Absence de protocoles écrits</label>
            <label class="check-item"><input type="checkbox"> Influence religieuse des patientes</label>
            <label class="check-item"><input type="checkbox"> Manque de salle d'examen isolée</label>
            <label class="check-item"><input type="checkbox"> Pudeur / Honte de la patiente</label>
        </div>

        <button type="button" class="submit-btn" onclick="saveData()">ENREGISTRER LA FICHE COMPLÈTE</button>
    </form>
</div>

<script>
    function saveData() {
        alert("Succès : Les données de collecte ont été ajoutées à la base de données.");
    }
</script>

</body>
</html>

