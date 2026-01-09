<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Collecte de Données</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f7f6; margin: 0; padding: 20px; color: #333; }
        .container { max-width: 1000px; margin: auto; background: white; padding: 20px; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.08); }
        
        /* Navigation */
        .nav-tabs { display: flex; gap: 10px; margin-bottom: 25px; border-bottom: 2px solid #b03060; padding-bottom: 10px; align-items: center; }
        .tab { padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; font-size: 0.85em; text-transform: uppercase; border: 1px solid #ddd; }
        .tab-active { background-color: #b03060; color: white; border-color: #b03060; }
        .tab-inactive { background-color: #f8f9fa; color: #666; }
        .btn-export { margin-left: auto; background-color: #2e7d32; color: white; border: none; padding: 10px 20px; border-radius: 6px; font-weight: bold; cursor: pointer; }

        /* Sections */
        .section-header { background-color: #fce4ec; color: #b03060; padding: 12px; font-weight: bold; margin-top: 30px; border-left: 6px solid #b03060; text-transform: uppercase; font-size: 0.95em; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; padding: 20px 0; }
        
        .field { display: flex; flex-direction: column; }
        label { font-size: 0.85em; margin-bottom: 8px; font-weight: 600; color: #444; }
        select, input[type="text"] { padding: 12px; border: 1px solid #ccc; border-radius: 6px; background-color: #fff; font-size: 0.95em; }

        /* Likert & Tables */
        table { width: 100%; border-collapse: collapse; margin: 15px 0; background: #fff; }
        th, td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 50%; font-size: 0.9em; }

        /* Checkboxes */
        .check-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; padding: 15px; background: #fafafa; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 0.9em; cursor: pointer; }
        .check-item input { margin-right: 12px; width: 18px; height: 18px; }

        .btn-submit { width: 100%; background-color: #b03060; color: white; border: none; padding: 20px; font-size: 1.1em; font-weight: bold; border-radius: 8px; margin-top: 40px; cursor: pointer; transition: 0.3s; }
        .btn-submit:hover { background-color: #8e244d; }
    </style>
</head>
<body>

<div class="container">
    <div class="nav-tabs">
        <a href="#" class="tab tab-active">1. COLLECTE</a>
        <a href="#" class="tab tab-inactive">2. BASE DE DONNÉES</a>
        <a href="#" class="tab tab-inactive">3. ANALYSE CAP</a>
        <button class="btn-export">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <form>
        <div class="section-header">I. IDENTIFICATION ET CONSENTEMENT ÉCLAIRÉ</div>
        <div class="grid">
            <div class="field">
                <label>Code de l'enquêté(e) *</label>
                <select required>
                    <option value="INF-01">INF-01</option><option value="INF-02">INF-02</option>
                    <option value="INF-03">INF-03</option><option value="INF-04">INF-04</option>
                </select>
            </div>
            <div class="field">
                <label>Consentement *</label>
                <select required>
                    <option value="Oui">Oui, j'accepte de participer</option>
                    <option value="Non">Non, je refuse de participer</option>
                </select>
            </div>
            <div class="field">
                <label>Service / Affectation</label>
                <select>
                    <option>Maternité</option><option>Chirurgie</option>
                    <option>Gynécologie</option><option>Urgences</option>
                </select>
            </div>
        </div>

        <div class="section-header">II. DONNÉES SOCIODÉMOGRAPHIQUES (LE PROFIL)</div>
        <div class="grid">
            <div class="field">
                <label>Sexe</label>
                <select><option>Femme</option><option>Homme</option></select>
            </div>
            <div class="field">
                <label>Âge (Choisir)</label>
                <select id="age-select"></select>
            </div>
            <div class="field">
                <label>État Civil</label>
                <select>
                    <option>Célibataire</option><option>Marié(e)</option>
                    <option>Veuf/Veuve</option><option>Divorcé(e)</option>
                </select>
            </div>
            <div class="field">
                <label>Niveau d'études</label>
                <select>
                    <option>Infirmière diplômée (A2)</option>
                    <option>Infirmière graduée (A1)</option>
                    <option>Licenciée (L0/L1)</option>
                    <option>Médecin</option>
                </select>
            </div>
            <div class="field">
                <label>Années d'expérience</label>
                <select id="exp-select"></select>
            </div>
            <div class="field">
                <label>Statut professionnel</label>
                <select>
                    <option>Titulaire</option>
                    <option>Stagiaire</option>
                    <option>Contractuelle</option>
                    <option>Autre</option>
                </select>
            </div>
        </div>

        <div class="section-header">III. ÉVALUATION DES CONNAISSANCES (LE SAVOIR)</div>
        <div class="grid">
            <div class="field">
                <label>Le risque augmente avec l'âge ?</label>
                <select><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="field">
                <label>L'obésité est un facteur de risque ?</label>
                <select><option>Vrai</option><option>Faux</option></select>
            </div>
            <div class="field">
                <label>L'allaitement est un facteur protecteur ?</label>
                <select><option>Vrai</option><option>Faux</option></select>
            </div>
        </div>

        <label style="font-size: 0.85em; font-weight: bold; margin-left: 5px;">Signes d'alerte cliniques (Choisir):</label>
        <div class="check-grid">
            <label class="check-item"><input type="checkbox" checked> Masse indolore / Nodule dur</label>
            <label class="check-item"><input type="checkbox" checked> Peau d'orange</label>
            <label class="check-item"><input type="checkbox"> Écoulement sanglant</label>
            <label class="check-item"><input type="checkbox"> Rétraction du mamelon</label>
        </div>

        <div class="section-header">IV. ÉVALUATION DES ATTITUDES (ÉCHELLE DE LIKERT 1 À 5)</div>
        <table>
            <thead><tr><th class="text-left">Énoncés</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
            <tbody>
                <tr><td class="text-left">La prévention est une priorité quotidienne.</td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1"></td><td><input type="radio" name="att1" checked></td><td><input type="radio" name="att1"></td></tr>
                <tr><td class="text-left">Le coût des examens est un obstacle majeur.</td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2"></td><td><input type="radio" name="att2" checked></td></tr>
                <tr><td class="text-left">Le cancer du sein est forcément mortel en RDC.</td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3" checked></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td><td><input type="radio" name="att3"></td></tr>
            </tbody>
        </table>

        <div class="section-header">V. ÉVALUATION DES PRATIQUES (LE SAVOIR-FAIRE)</div>
        <div class="grid">
            <div class="field">
                <label>Enseignez-vous l'autopalpation aux patientes ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
            <div class="field">
                <label>Réalisez-vous un examen clinique des seins ?</label>
                <select>
                    <option>Toujours (systématique)</option>
                    <option>Rarement</option>
                    <option>Jamais</option>
                </select>
            </div>
            <div class="field">
                <label>Pratique personnelle de l'AES ?</label>
                <select><option>Oui</option><option>Non</option></select>
            </div>
        </div>

        <div class="section-header">VI. OBSTACLES & RECOMMANDATIONS</div>
        <div class="check-grid">
            <label class="check-item"><input type="checkbox" checked> Manque de formation</label>
            <label class="check-item"><input type="checkbox"> Manque de temps</label>
            <label class="check-item"><input type="checkbox" checked> Tabous culturels ou religieux</label>
            <label class="check-item"><input type="checkbox" checked> Coût élevé des examens</label>
            <label class="check-item"><input type="checkbox"> Manque de matériels (affiches)</label>
        </div>
        
        <div class="field" style="margin-top: 20px;">
            <label>Suggestions pour l'HGRM</label>
            <select>
                <option>Organiser des formations continues</option>
                <option>Mettre à disposition des dépliants éducatifs</option>
                <option>Réduire les coûts des mammographies</option>
            </select>
        </div>

        <button type="button" class="btn-submit" onclick="alert('Fiche de collecte enregistrée avec succès !')">ENREGISTRER LA FICHE COMPLÈTE</button>
    </form>
</div>

<script>
    // Génération automatique des âges de 18 à 60 ans
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) {
        let opt = document.createElement('option');
        opt.value = i;
        opt.innerHTML = i + " ans";
        if(i === 30) opt.selected = true; // Valeur par défaut
        ageSelect.appendChild(opt);
    }

    // Génération des années d'expérience (1 mois à 30 ans)
    const expSelect = document.getElementById('exp-select');
    let m = document.createElement('option'); m.innerHTML = "1 à 11 mois"; expSelect.appendChild(m);
    for (let i = 1; i <= 30; i++) {
        let opt = document.createElement('option');
        opt.value = i;
        opt.innerHTML = i + (i === 1 ? " an" : " ans");
        if(i === 5) opt.selected = true; // Valeur par défaut
        expSelect.appendChild(opt);
    }
</script>

</body>
</html>
