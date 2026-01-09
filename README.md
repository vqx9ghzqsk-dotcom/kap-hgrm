<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Collecte Expert RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1000px; margin: auto; background: white; border-radius: 10px; box-shadow: 0 4px 20px rgba(0,0,0,0.15); overflow: hidden; }
        
        /* Navigation Style Image */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 10px; align-items: center; gap: 8px; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 25px; }
        .section-title { background: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; border-left: 6px solid #b03060; margin: 25px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 15px; margin-bottom: 10px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 12px; font-weight: 700; margin-bottom: 5px; color: #333; }
        select, input { padding: 12px; border: 1px solid #ccc; border-radius: 6px; font-size: 13px; background: #fff; color: #2c3e50; }

        /* Tables Likert */
        table { width: 100%; border-collapse: collapse; margin: 15px 0; font-size: 13px; }
        th, td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 50%; font-weight: 500; }

        /* Checkboxes Custom */
        .checkbox-group { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; background: #f9f9f9; padding: 15px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 12px; cursor: pointer; font-weight: 500; }
        .check-item input { margin-right: 12px; transform: scale(1.3); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 6px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; text-transform: uppercase; box-shadow: 0 4px 6px rgba(176, 48, 96, 0.3); }
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
        <div class="section-title">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
        <div class="row">
            <div class="field">
                <label>Code de l'enquêté(e)</label>
                <select>
                    <option>HGRM-INF-001</option><option>HGRM-INF-002</option>
                    <option>HGRM-INF-003</option><option>HGRM-INF-004</option>
                </select>
            </div>
            <div class="field">
                <label>Consentement Éclairé</label>
                <select><option selected>Oui, j'accepte de participer</option><option>Non, je refuse</option></select>
            </div>
            <div class="field">
                <label>Service d'affectation</label>
                <select>
                    <option>Maternité / Accouchement</option>
                    <option>Gynécologie-Obstétrique</option>
                    <option>Chirurgie Femme</option>
                    <option>Médecine Interne</option>
                    <option>Urgences / Tri</option>
                </select>
            </div>
        </div>

        <div class="section-title">II. DONNÉES SOCIODÉMOGRAPHIQUES (LE PROFIL)</div>
        <div class="row">
            <div class="field">
                <label>Sexe</label>
                <select><option selected>Femme</option><option>Homme</option></select>
            </div>
            <div class="field">
                <label>Âge (Propositions)</label>
                <select id="age-select"></select>
            </div>
            <div class="field">
                <label>État civil</label>
                <select><option>Célibataire</option><option selected>Mariée</option><option>Veuve</option><option>Divorcée</option></select>
            </div>
        </div>
        <div class="row">
            <div class="field">
                <label>Niveau d'études</label>
                <select>
                    <option>Infirmière diplômée (A2)</option>
                    <option selected>Infirmière graduée (A1)</option>
                    <option>Licenciée en Sciences Infirmières (L0/L1)</option>
                    <option>Médecin Généraliste</option>
                </select>
            </div>
            <div class="field">
                <label>Années d'expérience</label>
                <select id="exp-select"></select>
            </div>
            <div class="field">
                <label>Statut professionnel</label>
                <select><option selected>Titulaire</option><option>Contractuelle</option><option>Stagiaire</option><option>Sous-statutaire</option></select>
            </div>
        </div>
        <div class="row">
            <div class="field">
                <label>Antécédents familiaux de cancer ?</label>
                <select><option>Non</option><option>Oui (Mère/Sœur)</option><option>Oui (Autres)</option></select>
            </div>
        </div>

        <div class="section-title">III. ÉVALUATION DES CONNAISSANCES (LE SAVOIR)</div>
        <div class="row">
            <div class="field"><label>Le risque augmente avec l'âge ?</label><select><option selected>Vrai</option><option>Faux</option><option>Ne sait pas</option></select></div>
            <div class="field"><label>L'obésité est un facteur de risque ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>L'allaitement est protecteur ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
        </div>
        <div class="row">
            <div class="field"><label>Le cancer est-il contagieux ? (Mythe)</label><select><option selected>Faux (Correct)</option><option>Vrai</option></select></div>
            <div class="field"><label>L'échographie est utile chez la femme < 35 ans ?</label><select><option selected>Vrai</option><option>Faux</option></select></div>
            <div class="field"><label>Méthode de référence dépistage organisé :</label><select><option selected>Mammographie</option><option>Échographie</option></select></div>
        </div>

        <label style="margin: 10px 0; display:block;">Signes d'alerte identifiés (Cochez les propositions):</label>
        <div class="checkbox-group">
            <label class="check-item"><input type="checkbox" checked> Présence d'une masse ou nodule dur</label>
            <label class="check-item"><input type="checkbox" checked> Aspect 'peau d'orange' sur le sein</label>
            <label class="check-item"><input type="checkbox" checked> Écoulement sanglant par le mamelon</label>
            <label class="check-item"><input type="checkbox" checked> Rétraction du mamelon</label>
            <label class="check-item"><input type="checkbox"> Changement de taille du sein</label>
            <label class="check-item"><input type="checkbox"> Rougeur ou chaleur locale</label>
        </div>

        <div class="section-title">IV. ÉVALUATION DES ATTITUDES (LE SAVOIR-ÊTRE : DE 1 À 5)</div>
        <table>
            <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
            <tbody>
                <tr><td class="text-left">La prévention est une priorité dans mon travail.</td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1" checked></td><td><input type="radio" name="att1"></td></tr>
                <tr><td class="text-left">Je suis à l'aise pour enseigner l'autopalpation.</td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2" checked></td></tr>
                <tr><td class="text-left">Le coût des examens est le principal frein en RDC.</td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3" checked></td></tr>
                <tr><td class="text-left">Le cancer du sein est forcément mortel en RDC.</td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4" checked></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td><td><input type="radio" name="att4"></td></tr>
            </tbody>
        </table>

        <div class="section-title">V. ÉVALUATION DES PRATIQUES (LE SAVOIR-FAIRE)</div>
        <div class="row">
            <div class="field"><label>Pratique personnelle de l'AES :</label><select><option selected>Mensuelle</option><option>Occasionnelle</option><option>Jamais</option></select></div>
            <div class="field"><label>Examen clinique lors des consultations ?</label><select><option selected>Toujours (systématique)</option><option>Parfois</option></select></div>
            <div class="field"><label>Enseignez-vous l'AES aux patientes ?</label><select><option selected>Oui</option><option>Non</option></select></div>
        </div>
        <div class="row">
            <div class="field"><label>Référez-vous pour une mammographie ?</label><select><option selected>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Participé à une activité de sensibilisation ?</label><select><option selected>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Palpations effectuées ce mois (Proposé) :</label><select><option>0-5</option><option selected>5-15</option><option>+ de 15</option></select></div>
        </div>

        <div class="section-title">VI. OBSTACLES & RECOMMANDATIONS</div>
        <label>Obstacles à la prévention à l'HGRM (Cochez tout) :</label>
        <div class="checkbox-group">
            <label class="check-item"><input type="checkbox" checked> Manque de formation du personnel</label>
            <label class="check-item"><input type="checkbox" checked> Manque de matériel (affiches, outils)</label>
            <label class="check-item"><input type="checkbox" checked> Coût élevé des examens</label>
            <label class="check-item"><input type="checkbox"> Tabous culturels ou religieux</label>
            <label class="check-item"><input type="checkbox" checked> Manque de temps / Surcharge de travail</label>
            <label class="check-item"><input type="checkbox"> Distance vers les centres équipés</label>
        </div>
        
        <div class="row" style="margin-top:15px;">
            <div class="field"><label>Besoin de formation supplémentaire ?</label><select><option selected>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Type souhaité :</label><select><option selected>Formation continue / Atelier</option><option>Séminaire</option></select></div>
        </div>

        <div class="field" style="margin-top:10px;">
            <label>Suggestions pour améliorer la lutte à l'HGRM :</label>
            <select>
                <option selected>Organiser des campagnes de dépistage gratuit</option>
                <option>Mettre en place des protocoles écrits de dépistage</option>
                <option>Équiper le service en imagerie spécialisée</option>
            </select>
        </div>

        <button type="button" class="btn-save" onclick="alert('Fiche HGRM enregistrée avec succès !')">ENREGISTRER LA FICHE COMPLÈTE</button>
    </form>
</div>

<script>
    // Génération automatique des âges de 18 à 60 ans
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) {
        let opt = document.createElement('option');
        opt.value = i;
        opt.innerHTML = i + " ans";
        if(i === 32) opt.selected = true; 
        ageSelect.appendChild(opt);
    }

    // Génération des années d'expérience (1 mois à 30 ans)
    const expSelect = document.getElementById('exp-select');
    let m = document.createElement('option'); m.innerHTML = "Moins d'un an"; expSelect.appendChild(m);
    for (let i = 1; i <= 30; i++) {
        let opt = document.createElement('option');
        opt.value = i;
        opt.innerHTML = i + (i === 1 ? " an d'expérience" : " ans d'expérience");
        if(i === 7) opt.selected = true; 
        expSelect.appendChild(opt);
    }
</script>

</body>
</html>
