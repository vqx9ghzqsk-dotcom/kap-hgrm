<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Module de Collecte - KAP HGRM Makala</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        .form-content { padding: 30px; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
    </style>
</head>
<body>

<div class="container">
    <form class="form-content" id="formCollecte">
        <div class="section-title">I. IDENTIFICATION & PROFIL (Données Sociodémographiques)</div>
        <div class="row">
            <div class="field">
                <label>Code de l’enquêtée</label>
                <input type="text" name="code" placeholder="Ex: HGRM-001" required>
            </div>
            <div class="field">
                <label>Service d'affectation</label>
                <select name="service">
                    <option>Gynécologie-Obstétrique</option>
                    <option>Maternité / Salle d'accouchement</option>
                    <option>Chirurgie Générale</option>
                    <option>Urgences / Médecine Interne</option>
                    <option>Pédiatrie</option>
                </select>
            </div>
            <div class="field">
                <label>Statut Professionnel</label>
                <select name="statut">
                    <option>Titulaire</option>
                    <option>Contractuelle</option>
                    <option>Stagiaire</option>
                    <option>Autre</option>
                </select>
            </div>
        </div>
        <div class="row">
            <div class="field"><label>Âge (ans)</label><input type="number" name="age" required></div>
            <div class="field"><label>Années d'expérience professionnelle</label><input type="number" name="experience" required></div>
            <div class="field">
                <label>État civil</label>
                <select name="etat_civil">
                    <option>Célibataire</option>
                    <option>Mariée</option>
                    <option>Veuve</option>
                    <option>Divorcée</option>
                </select>
            </div>
        </div>
        <div class="row">
            <div class="field">
                <label>Niveau d’études</label>
                <select name="niveau_etude">
                    <option>A2 (Diplômée d'État)</option>
                    <option>A1 (Graduée)</option>
                    <option>A0 (Licenciée)</option>
                    <option>Master ou plus</option>
                </select>
            </div>
            <div class="field">
                <label>Antécédents familiaux de cancer du sein</label>
                <select name="antecedents"><option value="Oui">Oui</option><option value="Non" selected>Non</option></select>
            </div>
        </div>

        <div class="section-title">II. ÉVALUATION DES CONNAISSANCES (Le Savoir)</div>
        <div class="row">
            <div class="field">
                <label>Le risque augmente avec l’âge ?</label>
                <select name="c_age"><option>Vrai</option><option>Faux</option><option>Ne sait pas</option></select>
            </div>
            <div class="field">
                <label>L’obésité et la sédentarité sont des facteurs de risque ?</label>
                <select name="c_obesite"><option>Vrai</option><option>Faux</option><option>Ne sait pas</option></select>
            </div>
            <div class="field">
                <label>L’allaitement maternel protège du cancer ?</label>
                <select name="c_allaitement"><option>Vrai</option><option>Faux</option><option>Ne sait pas</option></select>
            </div>
        </div>

        <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes d'alerte (Cochez les signes valides) :</label>
        <div class="check-group">
            <label class="check-item"><input type="checkbox" name="signe" value="Nodule"> Nodule dur et indolore</label>
            <label class="check-item"><input type="checkbox" name="signe" value="Ecoulement"> Écoulement mamelonnaire</label>
            <label class="check-item"><input type="checkbox" name="signe" value="Retraction"> Rétraction du mamelon</label>
            <label class="check-item"><input type="checkbox" name="signe" value="PeauOrange"> Aspect peau d'orange</label>
            <label class="check-item"><input type="checkbox" name="signe" value="Adenopathie"> Boule sous l'aisselle</label>
        </div>

        <div class="section-title">III. ÉVALUATION DES ATTITUDES (Le Savoir-être)</div>
        <table>
            <thead>
                <tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
            </thead>
            <tbody>
                <tr><td class="text-left">Le dépistage précoce permet de guérir le cancer.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                <tr><td class="text-left">La peur du diagnostic freine le dépistage.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                <tr><td class="text-left">Je me sens capable de réaliser un examen clinique.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
            </tbody>
        </table>

        <div class="section-title">IV. ÉVALUATION DES PRATIQUES (Le Savoir-faire)</div>
        <div class="row">
            <div class="field">
                <label>Réalisez-vous l'examen clinique des seins (ECS) ?</label>
                <select name="p_ecs"><option>Toujours (systématique)</option><option>Parfois (si plainte)</option><option>Jamais</option></select>
            </div>
            <div class="field">
                <label>Enseignez-vous l'autopalpation (AES) ?</label>
                <select name="p_aes"><option>Oui</option><option>Non</option></select>
            </div>
            <div class="field">
                <label>Pratiquez-vous l'AES sur vous-même ?</label>
                <select name="p_perso"><option>Mensuelle</option><option>Occasionnelle</option><option>Jamais</option></select>
            </div>
        </div>

        <div class="section-title">V. OBSTACLES & RECOMMANDATIONS</div>
        <div class="check-group">
            <label class="check-item"><input type="checkbox" name="obs" value="Materiel"> Manque de matériel éducatif</label>
            <label class="check-item"><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
            <label class="check-item"><input type="checkbox" name="obs" value="Temps"> Surcharge de travail</label>
            <label class="check-item"><input type="checkbox" name="obs" value="Cout"> Coût élevé des examens</label>
            <label class="check-item"><input type="checkbox" name="obs" value="Culture"> Tabous culturels</label>
        </div>

        <button type="button" class="btn-save" onclick="validerFormulaire()">VALIDER LA FICHE D'ENQUÊTE</button>
    </form>
</div>

<script>
    function validerFormulaire() {
        // Cette fonction sera complétée par votre futur code de traitement
        alert("Fiche validée ! Prête pour le traitement des données.");
    }
</script>

</body>
</html>
