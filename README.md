<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        
        /* Header & Tabs */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; sticky: top; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        .form-content { padding: 30px; }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables Likert */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        /* Grid Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <a href="#" class="tab active">1. COLLECTE</a>
        <a href="#" class="tab">2. BASE DE DONNÃES</a>
        <a href="#" class="tab">3. ANALYSE CAP</a>
        <button type="button" class="btn-excel">ð EXPORT EXCEL (CSV)</button>
    </div>

    <form class="form-content">
        <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
        <div class="row">
            <div class="field">
                <label>Code EnquÃªtÃ©(e)</label>
                <select><option>HGRM-2026-01</option><option>HGRM-2026-02</option><option>HGRM-2026-03</option></select>
            </div>
            <div class="field">
                <label>Service / DÃ©partement</label>
                <select>
                    <option selected>GynÃ©cologie-ObstÃ©trique</option>
                    <option>MaternitÃ© / Salle d'accouchement</option>
                    <option>Chirurgie GÃ©nÃ©rale</option>
                    <option>Oncologie (si existant)</option>
                </select>
            </div>
            <div class="field">
                <label>Statut Professionnel</label>
                <select>
                    <option selected>Titulaire du service</option>
                    <option>Infirmier(e) de garde</option>
                    <option>Stagiaire (Fin de cycle)</option>
                    <option>Sous-statutaire (BÃ©nÃ©vole)</option>
                </select>
            </div>
        </div>
        <div class="row">
            <div class="field"><label>Ãge de l'infirmier(e)</label><select id="age-select"></select></div>
            <div class="field"><label>AnnÃ©es d'expÃ©rience professionnelle</label><select id="exp-select"></select></div>
            <div class="field">
                <label>Niveau d'Ã©tude le plus Ã©levÃ©</label>
                <select>
                    <option>A2 (DiplÃ´mÃ©e d'Ãtat)</option>
                    <option selected>A1 (GraduÃ©e en Sciences InfirmiÃ¨res)</option>
                    <option>L0/L1 (LicenciÃ©e nouveau systÃ¨me)</option>
                    <option>Master / Doctorat</option>
                </select>
            </div>
        </div>

        <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
        <div class="row">
            <div class="field">
                <label>Le cancer du sein est-il la premiÃ¨re cause de dÃ©cÃ¨s par cancer chez la femme en RDC ?</label>
                <select><option selected>Vrai (Oui)</option><option>Faux (Non)</option><option>Ne sait pas</option></select>
            </div>
            <div class="field">
                <label>Ã quel Ã¢ge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                <select><option>DÃ¨s 12 ans</option><option selected>DÃ¨s 20 ans</option><option>AprÃ¨s 40 ans</option></select>
            </div>
            <div class="field">
                <label>Quel est le meilleur moment pour l'AES ?</label>
                <select><option selected>7 jours aprÃ¨s les rÃ¨gles</option><option>Pendant les rÃ¨gles</option><option>N'importe quand</option></select>
            </div>
        </div>

        <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus (Cochez les propositions valides) :</label>
        <div class="check-group">
            <label class="check-item"><input type="checkbox" checked> NulliparitÃ© (n'avoir jamais accouchÃ©)</label>
            <label class="check-item"><input type="checkbox" checked> PremiÃ¨re grossesse tardive (> 30 ans)</label>
            <label class="check-item"><input type="checkbox" checked> MÃ©nopause tardive (> 55 ans)</label>
            <label class="check-item"><input type="checkbox" checked> Consommation d'alcool et tabac</label>
            <label class="check-item"><input type="checkbox"> Usage prolongÃ© de contraceptifs oraux</label>
            <label class="check-item"><input type="checkbox" checked> AntÃ©cÃ©dents familiaux (MÃ¨re, SÅur)</label>
        </div>

        <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte (Signes Ã  rechercher) :</label>
        <div class="check-group">
            <label class="check-item"><input type="checkbox" checked> Nodule dur, fixe et indolore</label>
            <label class="check-item"><input type="checkbox" checked> Ãcoulement sÃ©ro-sanguinolent unilatÃ©ral</label>
            <label class="check-item"><input type="checkbox" checked> RÃ©traction ou ombilication du mamelon</label>
            <label class="check-item"><input type="checkbox" checked> AdÃ©nopathie axillaire (boule sous l'aisselle)</label>
            <label class="check-item"><input type="checkbox" checked> Aspect de "peau d'orange" sur le tÃ©gument</label>
            <label class="check-item"><input type="checkbox"> Douleur mammaire isolÃ©e (Mastodynie)</label>
        </div>

        <div class="section-title">III. ATTITUDES ET PERCEPTIONS (SAVOIR-ÃTRE : 1 Ã 5)</div>
        <table>
            <thead>
                <tr>
                    <th class="text-left">ÃnoncÃ©s (Perception de l'infirmier/e)</th>
                    <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                </tr>
            </thead>
            <tbody>
                <tr><td class="text-left">Je me sens capable de dÃ©tecter un nodule suspect lors d'une palpation.</td><td><input type="radio" name="p1"></td><td><input type="radio" name="p1"></td><td><input type="radio" name="p1"></td><td><input type="radio" name="p1" checked></td><td><input type="radio" name="p1"></td></tr>
                <tr><td class="text-left">L'influence culturelle (pudeur) empÃªche mes patientes de se dÃ©shabiller.</td><td><input type="radio" name="p2"></td><td><input type="radio" name="p2"></td><td><input type="radio" name="p2"></td><td><input type="radio" name="p2"></td><td><input type="radio" name="p2" checked></td></tr>
                <tr><td class="text-left">Le diagnostic de cancer est une sentence de mort en RDC.</td><td><input type="radio" name="p3"></td><td><input type="radio" name="p3" checked></td><td><input type="radio" name="p3"></td><td><input type="radio" name="p3"></td><td><input type="radio" name="p3"></td></tr>
                <tr><td class="text-left">Je pense que chaque femme en consultation doit Ãªtre sensibilisÃ©e au cancer.</td><td><input type="radio" name="p4"></td><td><input type="radio" name="p4"></td><td><input type="radio" name="p4"></td><td><input type="radio" name="p4"></td><td><input type="radio" name="p4" checked></td></tr>
            </tbody>
        </table>

        <div class="section-title">IV. PRATIQUES PROFESSIONNELLES (SAVOIR-FAIRE)</div>
        <div class="row">
            <div class="field">
                <label>FrÃ©quence de la palpation clinique des seins (ECS) en consultation :</label>
                <select>
                    <option selected>SystÃ©matique pour chaque patiente</option>
                    <option>Uniquement si la patiente se plaint</option>
                    <option>Rarement par manque de temps</option>
                </select>
            </div>
            <div class="field">
                <label>Enseignement de la technique d'autopalpation (AES) :</label>
                <select>
                    <option selected>Je dÃ©montre la technique physiquement</option>
                    <option>J'explique verbalement seulement</option>
                    <option>Je ne l'enseigne pas</option>
                </select>
            </div>
            <div class="field">
                <label>RÃ©fÃ©rence des cas suspects :</label>
                <select>
                    <option selected>Vers l'imagerie (Mammographie/Echo)</option>
                    <option>Vers la Chirurgie directement</option>
                    <option>Observation (Attendre le prochain RDV)</option>
                </select>
            </div>
        </div>
        <div class="row">
            <div class="field">
                <label>Utilisation de supports visuels (Affiches, Boites Ã  images) :</label>
                <select><option selected>Jamais (Pas de matÃ©riel disponible)</option><option>Parfois</option><option>Toujours</option></select>
            </div>
            <div class="field">
                <label>Avez-vous dÃ©jÃ  palpÃ© un sein ce matin ?</label>
                <select><option selected>Oui</option><option>Non</option></select>
            </div>
            <div class="field">
                <label>Nombre de cas de cancer suspectÃ©s ce mois-ci :</label>
                <select><option>0</option><option selected>1 Ã  5 cas</option><option>Plus de 5 cas</option></select>
            </div>
        </div>

        <div class="section-title">V. OBSTACLES ET SOLUTIONS (RDC CONTEXT)</div>
        <label style="margin-bottom: 10px; display:block; font-weight: bold;">Quelles sont les barriÃ¨res Ã  l'HGRM ? (Cochez tout ce qui est vrai):</label>
        <div class="check-group">
            <label class="check-item"><input type="checkbox" checked> Absence de salle isolÃ©e respectant l'intimitÃ©</label>
            <label class="check-item"><input type="checkbox" checked> CoÃ»t exorbitant de la mammographie (> 50$)</label>
            <label class="check-item"><input type="checkbox" checked> Manque de formation continue sur le cancer</label>
            <label class="check-item"><input type="checkbox" checked> PrÃ©fÃ©rence des patientes pour la priÃ¨re/tradition</label>
            <label class="check-item"><input type="checkbox"> Surcharge de travail (Ratio infirmiÃ¨re/patient)</label>
        </div>

        <div class="field" style="margin-top: 20px;">
            <label>Votre recommandation principale pour l'HGRM :</label>
            <select>
                <option selected>Installation d'une unitÃ© de dÃ©pistage permanent</option>
                <option>Formation certifiante pour tout le personnel infirmier</option>
                <option>Subvention des examens d'imagerie pour les indigents</option>
                <option>Campagnes de masse dans les Ã©glises et marchÃ©s</option>
            </select>
        </div>

        <button type="button" class="btn-save" onclick="alert('DonnÃ©es KAP-HGRM sauvegardÃ©es !')">VALIDER ET ENREGISTRER LA FICHE</button>
    </form>
</div>

<script>
    // Remplissage automatique de l'Ãge (18 Ã  60)
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = i + " ans";
        if(i === 35) opt.selected = true;
        ageSelect.appendChild(opt);
    }

    // Remplissage automatique ExpÃ©rience (1 mois Ã  30 ans)
    const expSelect = document.getElementById('exp-select');
    let m = document.createElement('option'); m.text = "Stagiaire / Moins d'un an"; expSelect.appendChild(m);
    for (let i = 1; i <= 30; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = i + (i === 1 ? " an" : " ans") + " d'expÃ©rience";
        if(i === 10) opt.selected = true;
        expSelect.appendChild(opt);
    }
</script>

</body>
</html>