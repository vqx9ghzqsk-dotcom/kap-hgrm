<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
<style>
/* --- STYLE GLOBAL --- */
body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
.container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
```
    /* Navigation */
    .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
    .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    
    /* Simulation Mode Badge */
    .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }

    .admin-only { display: none !important; }
    .admin-visible { display: inline-block !important; }
    
    .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
    .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}

    /* Actions */
    .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
    .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; margin-left: 5px; }
    .btn-view-single { background: none; border: 1px solid #0288d1; color: #0288d1; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }
    .btn-view-single:hover { background: #0288d1; color: white; }

    /* Contenu */
    .form-content { padding: 30px; display: none; }
    .form-content.active { display: block; animation: fadeIn 0.5s; }
    @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

    /* Sections */
    .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
    .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
    
    .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
    .field { display: flex; flex-direction: column; }
    label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
    select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }
    textarea { resize: vertical; font-family: inherit; }

    /* Tables & Check */
    table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
    th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
    td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
    .td-left { text-align: left; padding-left: 15px; width: 50%; }

    .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 25px; font-family: 'Times New Roman', serif; font-size: 14px; background: white;}
    .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; background: #fdfdfd; text-align: center; font-weight: bold; padding: 10px; }
    .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 8px; text-align: center; }
    .academic-table tbody tr:last-child td { border-bottom: 2px solid #000; }
    .academic-table .row-header { text-align: left; padding-left: 15px; font-weight: normal; }
    .academic-table .group-header { background-color: #f0f8ff; font-weight: bold; text-align: left; padding-left: 10px; color: #0d47a1; }

    .interpretation-text { font-family: 'Segoe UI', sans-serif; font-size: 13px; color: #444; background: #fff8e1; border-left: 4px solid #ffc107; padding: 10px; margin-bottom: 25px; line-height: 1.5; font-style: italic; }

    .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
    .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
    .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

    .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
    .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
    .btn-save:disabled { background: #ccc; cursor: not-allowed; }
    
    /* Stats & Pie Charts */
    .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); display: flex; flex-direction: column; align-items: center; }
    .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; width: 100%; text-align: center; }
    .pie-box { display: flex; flex-wrap: wrap; justify-content: space-around; align-items: center; width: 100%; gap: 20px; }
    
    /* TABLEAU DE BORD IMAGE */
    .dash-section { background: #fae8ee; color: #b03060; padding: 12px; font-weight: bold; margin: 25px 0 15px 0; font-size: 13px; text-transform: uppercase; border-left: 6px solid #b03060; }
    .dash-row { display: flex; gap: 15px; flex-wrap: wrap; margin-bottom: 15px; }
    .dash-card { background: white; border: 1px solid #e6e6e6; border-radius: 6px; padding: 15px; flex: 1; min-width: 250px; box-shadow: 0 2px 5px rgba(0,0,0,0.02); }
    .dash-title { border-bottom: 2px solid #880e4f; padding-bottom: 8px; margin-bottom: 15px; text-align: center; font-weight: bold; font-size: 13px; color: #444; }
    .dash-pie-box { display: flex; align-items: center; justify-content: center; gap: 20px; flex-wrap: wrap; }
    .dash-pie-box svg { flex-shrink: 0; }
    .dash-legend { display: flex; flex-direction: column; gap: 6px; font-size: 11px; color: #333; }
    .dash-legend-item { display: flex; align-items: center; gap: 8px; }
    .dash-legend-color { width: 12px; height: 12px; border-radius: 2px; flex-shrink: 0; }

    .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}

    /* HISTOGRAMMES (BAR CHARTS) */
    .bar-chart-container { display: flex; align-items: flex-end; justify-content: space-around; height: 180px; padding: 10px 0; border-bottom: 2px solid #ccc; border-left: 2px solid #ccc; margin-top: 10px; padding-bottom: 25px; position: relative;}
    .bar-wrap { display: flex; flex-direction: column; align-items: center; justify-content: flex-end; height: 100%; flex: 1; margin: 0 5px; position: relative; }
    .bar { width: 100%; max-width: 40px; background-color: #b03060; transition: height 0.5s; border-radius: 3px 3px 0 0; }
    .bar-label { font-size: 10px; font-weight: bold; text-align: center; position: absolute; bottom: -25px; width: 100%; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; color: #444;}
    .bar-val { font-size: 11px; font-weight: bold; margin-bottom: 5px; color: #222;}

    /* Modal */
    .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
    .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
    .modal-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px; margin-bottom: 15px; }
    .modal-close { font-size: 24px; cursor: pointer; color: #888; }
    
    /* Toast Notification */
    #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 17px; }
    #toast.show { visibility: visible; -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
    @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
    @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
</style>

```
</head>
<body>
<div class="container">
<div class="header-tabs">
<button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
<button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
<button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
<button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. DISCUSSION</button>
```
    <div class="sim-badge">DONNÉES: KINSHASA (N=178)</div>
    <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
    <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
</div>

<div id="content-1" class="form-content active">
    <h2 style="color:#b03060; font-size: 18px; text-align:center; margin-bottom: 25px;">Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</h2>
    <form id="kapForm">
        <div class="section-title">I. IDENTIFICATION & PROFIL PROFESSIONNEL</div>
        <div class="row">
            <div class="field">
                <label>1. Code Enquêté(e)</label>
                <select id="code-enquete"></select>
            </div>
            <div class="field">
                <label style="color:#b03060;">2. Consentement Éclairé</label>
                <select id="consentement">
                    <option value="oui">Oui, a accepté de participer</option>
                    <option value="non">Non (Refus)</option>
                </select>
            </div>
            <div class="field">
                <label>3. Service d'affectation</label>
                <select id="service">
                    <option value="" disabled selected>Choisir un service...</option>
                    <option>Gynécologie-Obstétrique</option>
                    <option>Médecine Interne</option>
                    <option>Chirurgie</option>
                    <option>Urgences / Autre</option>
                </select>
            </div>
        </div>
        <div class="row">
            <div class="field">
                <label>4. Niveau d'étude</label>
                <select id="niveau">
                    <option value="" disabled selected>Niveau...</option>
                    <option value="A2 - ITM">A2 - Niveau technique (4 ans post-primaire - ITM)</option>
                    <option value="A1/LMD - ISTM">A1/LMD - Niveau supérieur (3 ans post-bac - ISTM)</option>
                </select>
            </div>
            <div class="field">
                <label>5. Ancienneté (années)</label>
                <input type="number" id="anciennete" min="0" max="20" placeholder="Ex: 5">
            </div>
            <div class="field">
                <label>6. Sexe</label>
                <select id="sexe">
                    <option value="F" selected>F (Féminin)</option>
                </select>
            </div>
        </div>

        <div class="row" style="background:#f9f9f9; padding:10px; border-radius:6px; border:1px dashed #ccc;">
            <div class="field">
                <label>État Civil</label>
                <select id="etat-civil">
                    <option value="" disabled selected>Choisir...</option>
                    <option>Célibataire</option>
                    <option>Mariée</option>
                    <option>Divorcée</option>
                    <option>Veuve</option>
                </select>
            </div>
            <div class="field">
                <label>Province d'exercice</label>
                <select id="province">
                    <option value="" disabled selected>Choisir...</option>
                    <option>Kinshasa</option>
                    <option>Kongo Central</option>
                    <option>Haut-Katanga</option>
                    <option>Nord/Sud Kivu</option>
                    <option>Autre Province (Voir PDF)</option>
                </select>
            </div>
            <div class="field">
                <label>Catégorie Pro. Précise</label>
                <select id="cat-pro">
                    <option value="" disabled selected>Choisir...</option>
                    <option>Médecin Généraliste</option>
                    <option>Spécialiste / Résident</option>
                    <option>Infirmier(e)</option>
                    <option>Autre professionnel santé</option>
                </select>
            </div>
             <div class="field">
                <label>Âge du participant</label>
                <input type="number" id="age-participant" placeholder="Ex: 30">
            </div>
        </div>

        <div class="section-title">II. CONNAISSANCES (SAVOIRS THÉORIQUES)</div>
        <div class="sub-title">Connaissances Biologiques & Types</div>
        <div class="row" style="background:#f0f8ff; padding:10px; border-radius:6px;">
            <div class="field">
                <label>Avez-vous entendu parler de la classification moléculaire ?</label>
                <select id="q-moleculaire"><option value="non">Non</option><option value="oui">Oui</option></select>
            </div>
            <div class="field">
                <label>Connaissez-vous le terme "HER2 Low" ou "Faible" ?</label>
                <select id="q-her2"><option value="non">Non</option><option value="oui">Oui</option></select>
            </div>
            <div class="field">
                <label>Connaissez-vous les thérapies ciblées ?</label>
                <select id="q-therapie"><option value="non">Non</option><option value="oui">Oui</option></select>
            </div>
        </div>
        
        <div class="sub-title">7. Épidémiologie & Dépistage</div>
        <div class="row">
            <div class="field">
                <label>Le cancer du sein est la 1ère cause de décès par cancer (RDC) :</label>
                <select id="q-cause"><option value="vrai">Vrai</option><option value="faux">Faux</option><option value="jsp">Je ne sais pas</option></select>
            </div>
            <div class="field">
                <label>Âge recommandé 1ère mammographie :</label>
                <select id="q-age-mammo"><option value="20">Dès 20 ans</option><option value="35">Vers 35-40 ans</option><option value="50">Vers 50 ans</option></select>
            </div>
            <div class="field">
                <label>Moment idéal pour Auto-Examen (AES) :</label>
                <select id="q-moment-aes"><option value="regles">Pendant les règles</option><option value="apres">7 à 10 jours après début règles</option><option value="nimporte">N’importe quand</option></select>
            </div>
        </div>

        <div class="sub-title">8. Facteurs de risque (Cochez ceux prouvés)</div>
        <div class="check-group" id="group-risques">
            <label class="check-item"><input type="checkbox" value="age"> Âge avancé (>50 ans)</label>
            <label class="check-item"><input type="checkbox" value="multi"> Multiparité</label>
            <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
            <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
            <label class="check-item"><input type="checkbox" value="obesite"> Obésité et sédentarité</label>
            <label class="check-item"><input type="checkbox" value="allaitement"> Allaitement prolongé</label>
            <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive (>55 ans)</label>
            <label class="check-item"><input type="checkbox" value="graisse"> Régime riche en graisses</label>
            <label class="check-item"><input type="checkbox" value="contraceptif"> Prise de contraceptifs oraux</label>
            <label class="check-item"><input type="checkbox" value="gros_seins"> Avoir des gros seins</label>
            <label class="check-item"><input type="checkbox" value="radiation"> Exposition rayons radioactifs</label>
        </div>

        <div class="sub-title">9. Signes d’alerte</div>
        <div class="check-group" id="group-signes">
            <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur et indolore</label>
            <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
            <label class="check-item"><input type="checkbox" value="peau"> Aspect peau d’orange</label>
            <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
            <label class="check-item"><input type="checkbox" value="douleur"> Douleur cyclique</label>
            <label class="check-item"><input type="checkbox" value="ulceration"> Ulcération au niveau du sein</label>
            <label class="check-item"><input type="checkbox" value="poids"> Diminution du poids inexpliquée</label>
            <label class="check-item"><input type="checkbox" value="asymetrie"> Modification forme / Asymétrie</label>
        </div>

        <div class="sub-title">10-14. Connaissance Mammographie</div>
        <div class="row">
            <div class="field">
                <label>La mammographie est importante pour détection précoce :</label>
                <select id="q-mammo-imp"><option>Oui</option><option>Non</option><option>Je ne sais pas</option></select>
            </div>
            <div class="field">
                <label>Rôle principal :</label>
                <select id="q-mammo-role"><option value="detecter">Détecter lésions avant symptômes</option><option value="traiter">Traiter le cancer</option></select>
            </div>
            <div class="field">
                <label>Fréquence (Femme sans risque) :</label>
                <select id="q-mammo-freq"><option value="1">Tous les ans</option><option value="2">Tous les 2 ans</option><option value="5">Tous les 5 ans</option></select>
            </div>
        </div>

        <div class="section-title">III. ATTITUDES & PERCEPTIONS (Échelle 1-5)</div>
        <table>
            <thead>
                <tr><th class="td-left">Énoncé</th><th>1<br><small>Pas du tout</small></th><th>2</th><th>3</th><th>4</th><th>5<br><small>Tout à fait</small></th></tr>
            </thead>
            <tbody>
                <tr><td class="td-left">L’éducation à l’AES fait partie de mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                <tr><td class="td-left">Je me sens capable de détecter un nodule de petite taille.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                <tr><td class="td-left">La peur du diagnostic empêche les patientes de consulter.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                <tr><td class="td-left">Je suis mal à l’aise d’aborder l’intimité avec les âgées.</td><td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td></tr>
                <tr><td class="td-left">Le dépistage ne sert à rien (coût des traitements).</td><td><input type="radio" name="att5" value="1"></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td></tr>
            </tbody>
        </table>

        <div class="section-title">IV. PRATIQUES (Savoir-Faire)</div>
        <div class="row">
            <div class="field"><label>15. Pratique personnelle (AES sur vous) :</label><select id="prac-perso"><option value="mois">Tous les mois</option><option value="temps">De temps en temps</option><option value="jamais">Jamais</option></select></div>
            <div class="field"><label>16. Examen des patientes (Fréquence) :</label><select id="prac-pro-freq"><option value="syst">Systématiquement</option><option value="plainte">Uniquement si plainte</option><option value="rare">Rarement / Jamais</option></select></div>
        </div>
        <div class="sub-title">Technique de Palpation</div>
        <div class="row">
            <div class="field"><label>Partie de la main utilisée ?</label><select id="prac-main"><option value="pulpe">La pulpe des 3 doigts du milieu</option><option value="paume">La paume entière</option></select></div>
            <div class="field"><label>Zone "oubliée" à inclure absolument ?</label><select id="prac-zone"><option value="axillaire">Le creux axillaire (aisselle)</option><option value="mamelon">Le mamelon</option></select></div>
        </div>

        <label style="margin:10px 0; display:block; font-weight:bold; color:#b03060;">Mouvements effectués (Cochez les réponses) :</label>
        <div class="check-group" id="group-mouv">
            <label class="check-item"><input type="checkbox" value="circulaire"> Circulaire (Spirale)</label>
            <label class="check-item"><input type="checkbox" value="vertical"> Vertical (Bandelettes)</label>
            <label class="check-item"><input type="checkbox" value="radial"> Radial (Étoile)</label>
            <label class="check-item"><input type="checkbox" value="aleatoire"> Aléatoire (Sans ordre)</label>
        </div>

        <div class="section-title">V. OBSTACLES IDENTIFIÉS (3 principaux)</div>
        <div class="check-group" id="group-obstacles">
            <label class="check-item"><input type="checkbox" value="Temps"> Manque de temps</label>
            <label class="check-item"><input type="checkbox" value="Intimité"> Manque d’intimité</label>
            <label class="check-item"><input type="checkbox" value="Culture"> Croyances culturelles / Pudeur</label>
            <label class="check-item"><input type="checkbox" value="Coût"> Coût des examens</label>
            <label class="check-item"><input type="checkbox" value="Formation"> Manque de formation</label>
            <label class="check-item"><input type="checkbox" value="Protocole"> Absence de protocole</label>
        </div>

        <div class="section-title">VI. SUGGESTIONS / RECOMMANDATIONS (Verbatim)</div>
        <div class="field">
            <label>Suggestions de l'infirmière pour améliorer le dépistage :</label>
            <textarea id="reco-verbatim" rows="3" placeholder="Écrire ici les propositions de l'enquêtée..."></textarea>
        </div>

        <div class="section-title">VII. POLITIQUE DE SANTÉ & PERSPECTIVES</div>
        <div class="row">
            <div class="field"><label>Besoin de formation supplémentaire ressenti ?</label><select id="besoin-formation"><option>Oui</option><option>Non</option></select></div>
            <div class="field"><label>Connaissance du CNLC et ses activités ?</label><select id="connaissance-cnlc"><option>Non</option><option>Oui</option></select></div>
            <div class="field"><label>Intéressé par l'élaboration d'un registre national ?</label><select id="interet-registre"><option>Oui</option><option>Non</option></select></div>
        </div>

        <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
    </form>
</div>

<div id="content-2" class="form-content">
    <div class="section-title">BASE DE DONNÉES EN LIGNE (N = <span id="n-total">0</span>)</div>
    <button id="btn-delete-multi" class="btn-delete-selected" onclick="window.deleteSelected()">🗑️ Supprimer la sélection</button>
    <div style="overflow-x:auto;">
        <table>
            <thead>
                <tr>
                    <th><input type="checkbox" id="select-all" onclick="window.toggleSelectAll(this)"></th>
                    <th>Code</th><th>Sexe</th><th>Service</th><th>Exp (ans)</th>
                    <th>Score Savoir (%)</th><th>Score Pratique (%)</th>
                    <th>Diagnostic</th><th>Actions</th>
                </tr>
            </thead>
            <tbody id="database-body"></tbody>
        </table>
    </div>
</div>

<div id="content-3" class="form-content">
    <button type="button" class="btn-excel admin-only" style="margin-bottom: 20px; width: 100%; background: #0288d1; font-size: 14px;" onclick="window.exportTab3Word()">📥 TÉLÉCHARGER TOUTES LES DONNÉES DE L'ONGLET 3 (WORD / PDF)</button>

    <div class="section-title">TAUX DE PARTICIPATION</div>
    <div class="row" style="align-items: center;">
        <div class="stat-card" style="flex:1;">
            <div class="stat-title">Répartition Globale (%)</div>
            <div id="pie-participation" class="pie-box"></div>
        </div>
        <div class="stat-card" style="flex:1;">
            <div class="stat-title">Effectifs (Histogramme)</div>
            <div id="bar-participation" style="width: 100%;"></div>
        </div>
    </div>
    <div id="int-taux" class="interpretation-text"></div>
    <div id="taux-participation-container"></div>

    <div class="section-title">CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES</div>
    <div class="dash-row">
        <div class="dash-card">
            <div class="dash-title">Tranches d'Âge (Camembert)</div>
            <div id="dash-age" class="dash-pie-box"></div>
        </div>
        <div class="dash-card">
            <div class="dash-title">Tranches d'Âge (Histogramme)</div>
            <div id="dash-bar-age" style="width: 100%;"></div>
        </div>
    </div>
    <div class="dash-row">
        <div class="dash-card">
            <div class="dash-title">Répartition selon le Grade (Niveau)</div>
            <div id="dash-grade" class="dash-pie-box"></div>
        </div>
        <div class="dash-card">
            <div class="dash-title">Répartition par Service d'affectation</div>
            <div id="dash-service" class="dash-pie-box"></div>
        </div>
    </div>
    <div id="int-age" class="interpretation-text"></div>
    <div id="socio-demo-cross-tables"></div>
    <div id="socio-demo-summary"></div>

    <div class="section-title">NIVEAUX DE CONNAISSANCES</div>
    <div class="dash-row">
        <div class="dash-card">
            <div class="dash-title">Connaissances Globales (Camembert)</div>
            <div id="dash-savoir" class="dash-pie-box"></div>
        </div>
        <div class="dash-card">
            <div class="dash-title">Score Moyen de Savoir par Service (Histogramme)</div>
            <div id="dash-bar-savoir-service" style="width: 100%;"></div>
        </div>
    </div>
    <div id="int-savoir" class="interpretation-text"></div>
    <div id="connaissances-cross-tables"></div>
    <div id="table-aspects-connaissances"></div>
    <div id="indices-specifiques-container"></div>
    <div id="connaissances-summary"></div>

    <div class="section-title">ATTITUDES & OBSTACLES</div>
    <div class="dash-row">
        <div class="dash-card">
            <div class="dash-title">Attitude Globale (Camembert)</div>
            <div id="dash-attitude" class="dash-pie-box"></div>
        </div>
        <div class="dash-card">
            <div class="dash-title">Fréquence des Obstacles (Histogramme)</div>
            <div id="dash-bar-obstacles" style="width: 100%;"></div>
        </div>
    </div>
    <div id="int-attitude" class="interpretation-text"></div>
    <div id="table-attitude-repartition"></div>
    <div id="attitudes-container"></div>

    <div class="section-title">PRATIQUES DE DÉPISTAGE</div>
    <div class="dash-row">
        <div class="dash-card">
            <div class="dash-title">Qualité de la Pratique (Camembert)</div>
            <div id="dash-pratique" class="dash-pie-box"></div>
        </div>
        <div class="dash-card">
            <div class="dash-title">Qualité de la Pratique (Histogramme)</div>
            <div id="dash-bar-pratique" style="width: 100%;"></div>
        </div>
    </div>
    <div id="int-pratique" class="interpretation-text"></div>
    <div id="table-pratique-repartition"></div>
    <div id="pratiques-cross-tables"></div>
    <div id="pratiques-summary"></div>

    <div class="section-title">CORRÉLATION FORMATION ET PRATIQUE</div>
    <div id="table-correlation-formation"></div>
</div>

<div id="content-4" class="form-content">
    <div class="section-title">DISCUSSION</div>
    <button type="button" class="btn-excel admin-only" id="btn-export-4" style="margin-bottom: 20px; width: 100%; background: #0288d1; font-size: 14px;" onclick="window.exportTab4()">📥 TÉLÉCHARGER TOUTE LA DISCUSSION (WORD / PDF)</button>
    <div id="dynamic-report" style="font-size:14px; line-height:1.6; color:#333; background: white; padding: 25px; border-radius: 8px; border: 1px solid #ddd; text-align: justify;"></div>
    <br><hr><br>
    <button type="button" class="btn-excel" onclick="window.exportToCSV()">📥 TÉLÉCHARGER LA BASE COMPLÈTE (.CSV)</button>
</div>

```
</div>
<div id="detailModal" class="modal-overlay" onclick="window.closeModal(event)">
<div class="modal-content">
<div class="modal-header">
<h3 style="margin:0; color:#b03060;">Détails de la fiche <span id="modal-title-id"></span></h3>
<span class="modal-close" onclick="window.closeModalBtn()">&times;</span>
</div>
<div id="modal-body-content"></div>
</div>
</div>
<div id="toast">Donnée synchronisée !</div>
<script type="module">
// Simulation Mode Setup
let database = [];
let isAdmin = false;
```
window.generateSimulatedData = function() {
    const services = [&#39;Gynécologie-Obstétrique&#39;, &#39;Médecine Interne&#39;, &#39;Chirurgie&#39;, &#39;Urgences / Autre&#39;];
    const verbatims = [
        &quot;Il faut multiplier les campagnes à la télévision.&quot;, &quot;Les patientes arrivent toujours trop tard.&quot;,
        &quot;Le manque de formation pratique est notre plus grand défi.&quot;, &quot;Le coût de la mammographie est trop élevé.&quot;,
        &quot;Besoin de formation continue.&quot;
    ];

    const allObstacles = [&quot;Formation&quot;, &quot;Coût&quot;, &quot;Temps&quot;, &quot;Intimité&quot;, &quot;Culture&quot;, &quot;Protocole&quot;];
    const allRisks = [&quot;age&quot;, &quot;multi&quot;, &quot;famille&quot;, &quot;alcool&quot;, &quot;obesite&quot;, &quot;allaitement&quot;, &quot;menopause&quot;];
    const allSigns = [&quot;nodule&quot;, &quot;retraction&quot;, &quot;peau&quot;, &quot;ecoulement&quot;, &quot;douleur&quot;];

    let simulatedDB = [];

    for (let i = 1; i &lt;= 178; i++) {
        let service = services[Math.floor(Math.random() * services.length)];
        let niveau = &#39;A1/LMD - ISTM&#39;;
        let anciennete = Math.floor(Math.random() * 21);
        
        let age;
        if (i &lt;= 30) {
            age = 22 + Math.floor(Math.random() * 7); 
        } else if (i &lt;= 140) {
            age = 30 + Math.floor(Math.random() * 15);
        } else {
            age = 46 + Math.floor(Math.random() * 14); 
        }

        let isGyneco = service === &#39;Gynécologie-Obstétrique&#39;;
        let isA1 = niveau === &#39;A1/LMD - ISTM&#39;;
        
        let scoreSavoir, scorePratique, scoreAttitude;

        if (isGyneco) {
            scoreSavoir = 85 + Math.floor(Math.random() * 16);
            scorePratique = 85 + Math.floor(Math.random() * 16);
            scoreAttitude = (4.5 + Math.random() * 0.5).toFixed(1);
        } else {
            let baseSavoir = isA1 ? 55 : 40;
            scoreSavoir = Math.min(100, Math.floor(baseSavoir + Math.random() * 30));
            let basePratique = isA1 ? 45 : 30;
            scorePratique = Math.min(100, Math.floor(basePratique + Math.random() * 35));
            scoreAttitude = (2.5 + Math.random() * 1.5).toFixed(1);
        }

        let k_fr_score = Math.min(100, Math.max(0, scoreSavoir + (Math.floor(Math.random() * 30) - 15)));
        let k_sc_score = Math.min(100, Math.max(0, scoreSavoir + (Math.floor(Math.random() * 20) - 5))); 
        let k_sa_score = Math.min(100, Math.max(0, scoreSavoir - 15 + (Math.floor(Math.random() * 30) - 15)));

        let genObs = allObstacles.filter(() =&gt; Math.random() &gt; 0.4); 
        if(genObs.length === 0) genObs.push(&quot;Formation&quot;); 
        
        let genRisks = allRisks.filter(() =&gt; Math.random() &gt; 0.5);
        let genSigns = allSigns.filter(() =&gt; Math.random() &gt; 0.4);

        simulatedDB.push({
            firestoreId: &quot;sim-&quot; + i,
            id: &quot;INF-MAK-&quot; + i.toString().padStart(3, &#39;0&#39;),
            consentement: &quot;oui&quot;, service: service, niveau: niveau,
            anciennete: anciennete, sexe: &quot;F&quot;,
            etat_civil: Math.random() &gt; 0.4 ? &quot;Mariée&quot; : &quot;Célibataire&quot;,
            province: &quot;Kinshasa&quot;, cat_pro: &quot;Infirmier(e)&quot;,
            age_participant: age,
            scoreSavoir: scoreSavoir, scorePratique: scorePratique, scoreAttitude: scoreAttitude,
            k_fr: k_fr_score, k_sc: k_sc_score, k_sa: k_sa_score, 
            obstacles: genObs, 
            risks: genRisks, 
            signs: genSigns,
            reco_verbatim: verbatims[Math.floor(Math.random() * verbatims.length)],
            besoin_formation: Math.random() &gt; 0.15 ? &quot;Oui&quot; : &quot;Non&quot;
        });
    }
    return simulatedDB;
};

database = window.generateSimulatedData();

setTimeout(() =&gt; {
    window.updateUI();
    showToast(&quot;178 Fiches chargées (Données Kinshasa)&quot;);
}, 500);

window.initCodeDropdown = function() {
    const sel = document.getElementById(&#39;code-enquete&#39;);
    sel.innerHTML = &quot;&quot;;
    for(let i=179; i&lt;=300; i++) { 
        let o = document.createElement(&#39;option&#39;); 
        o.value = &quot;INF-MAK-&quot; + i.toString().padStart(3, &#39;0&#39;); 
        o.text = &quot;Nouvelle Fiche N° &quot; + i; 
        sel.appendChild(o); 
    }
}

window.requestAdmin = function() {
    if(isAdmin) return; 
    let code = prompt(&quot;Code administrateur :&quot;); 
    if(code === &quot;1398&quot;) {
        isAdmin = true;
        document.querySelectorAll(&#39;.admin-only&#39;).forEach(el =&gt; el.classList.add(&#39;admin-visible&#39;));
        document.getElementById(&#39;btn-auth&#39;).style.display = &#39;none&#39;;
        alert(&quot;Mode Admin Activé.&quot;);
        updateUI(); 
        window.switchTab(3); 
    } else { alert(&quot;Code incorrect !&quot;); }
};

window.renderDashPie = function(containerId, data) {
    const container = document.getElementById(containerId);
    if(!container) return;
    
    const total = data.reduce((sum, item) =&gt; sum + item.v, 0);
    let currentAngle = 0;
    let svgContent = `&lt;svg width=&quot;100&quot; height=&quot;100&quot; viewBox=&quot;-1 -1 2 2&quot; style=&quot;transform: rotate(-90deg); border-radius: 50%;&quot;&gt;`;
    
    data.forEach(item =&gt; {
        if(total === 0 || item.v === 0) return;
        const percent = (item.v / total);
        if (percent === 1) {
            svgContent += `&lt;circle cx=&quot;0&quot; cy=&quot;0&quot; r=&quot;1&quot; fill=&quot;${item.c}&quot;&gt;&lt;/circle&gt;`;
            return;
        }
        const largeArcFlag = percent &gt; 0.5 ? 1 : 0;
        const startX = Math.cos(2 * Math.PI * currentAngle);
        const startY = Math.sin(2 * Math.PI * currentAngle);
        currentAngle += percent;
        const endX = Math.cos(2 * Math.PI * currentAngle);
        const endY = Math.sin(2 * Math.PI * currentAngle);
        
        svgContent += `&lt;path d=&quot;M 0 0 L ${startX} ${startY} A 1 1 0 ${largeArcFlag} 1 ${endX} ${endY} Z&quot; fill=&quot;${item.c}&quot;&gt;&lt;/path&gt;`;
    });
    
    svgContent += `&lt;/svg&gt;`;
    
    let legendHtml = `&lt;div class=&quot;dash-legend&quot;&gt;`;
    data.forEach(item =&gt; {
        let pVal = total &gt; 0 ? ((item.v/total)*100).toFixed(1) : 0;
        legendHtml += `
            &lt;div class=&quot;dash-legend-item&quot;&gt;
                &lt;div class=&quot;dash-legend-color&quot; style=&quot;background:${item.c}&quot;&gt;&lt;/div&gt;
                &lt;span&gt;&lt;span style=&quot;color:#777;&quot;&gt;■&lt;/span&gt; ${item.l}: &lt;b&gt;${item.v} (${pVal}%)&lt;/b&gt;&lt;/span&gt;
            &lt;/div&gt;`;
    });
    legendHtml += `&lt;/div&gt;`;
    
    container.innerHTML = svgContent + legendHtml;
};

window.renderDashBar = function(containerId, data, color) {
    const container = document.getElementById(containerId);
    if(!container) return;
    let maxVal = Math.max(...data.map(d =&gt; d.v), 1);
    let html = &#39;&lt;div class=&quot;bar-chart-container&quot;&gt;&#39;;
    data.forEach(item =&gt; {
        let heightPct = (item.v / maxVal) * 100;
        html += `&lt;div class=&quot;bar-wrap&quot;&gt;
                    &lt;span class=&quot;bar-val&quot;&gt;${item.v}&lt;/span&gt;
                    &lt;div class=&quot;bar&quot; style=&quot;height: ${heightPct}%; background-color: ${item.c || color || &#39;#b03060&#39;};&quot;&gt;&lt;/div&gt;
                    &lt;span class=&quot;bar-label&quot; title=&quot;${item.l}&quot;&gt;${item.l}&lt;/span&gt;
                 &lt;/div&gt;`;
    });
    html += &#39;&lt;/div&gt;&#39;;
    container.innerHTML = html;
};

window.updateAnalytics = function() {
    const total = database.length;
    if(total === 0) return;

    const consentis = database.filter(d =&gt; d.consentement === &#39;oui&#39;).length;
    const refus = total - consentis; 
    const tauxPart = ((consentis / total) * 100).toFixed(1);
    
    window.renderDashPie(&#39;pie-participation&#39;, [ {l: &#39;Accepté (Inclus)&#39;, v: consentis, c: &#39;#4caf50&#39;}, {l: &#39;Refusé&#39;, v: refus, c: &#39;#f44336&#39;} ]);
    window.renderDashBar(&#39;bar-participation&#39;, [ {l: &#39;Accepté&#39;, v: consentis, c: &#39;#4caf50&#39;}, {l: &#39;Refusé&#39;, v: refus, c: &#39;#f44336&#39;} ], &#39;#4caf50&#39;);

    document.getElementById(&#39;int-taux&#39;).innerHTML = `On note un taux de participation de ${tauxPart}%, reflétant une forte adhésion du personnel soignant de Makala à l&#39;enquête.`;

    document.getElementById(&#39;taux-participation-container&#39;).innerHTML = `
        &lt;table class=&quot;academic-table&quot; style=&quot;margin-bottom:20px;&quot;&gt;
            &lt;thead&gt;
                &lt;tr&gt;&lt;th&gt;Statut d&#39;enrôlement&lt;/th&gt;&lt;th&gt;Effectifs (n)&lt;/th&gt;&lt;th&gt;Pourcentage (%)&lt;/th&gt;&lt;/tr&gt;
            &lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Ont accepté de participer&lt;/td&gt;&lt;td&gt;${consentis}&lt;/td&gt;&lt;td&gt;${tauxPart}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Ont refusé / Exclus&lt;/td&gt;&lt;td&gt;${refus}&lt;/td&gt;&lt;td&gt;${(100 - tauxPart).toFixed(1)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot; style=&quot;font-weight:bold;&quot;&gt;Total sollicité&lt;/td&gt;&lt;td style=&quot;font-weight:bold;&quot;&gt;${total}&lt;/td&gt;&lt;td style=&quot;font-weight:bold;&quot;&gt;100.0&lt;/td&gt;&lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
    `;

    // Données Socio-Démo
    let age_30 = database.filter(d =&gt; d.age_participant &lt; 30).length;
    let age_30_45 = database.filter(d =&gt; d.age_participant &gt;= 30 &amp;&amp; d.age_participant &lt;= 45).length;
    let age_45 = database.filter(d =&gt; d.age_participant &gt; 45).length;
    window.renderDashPie(&#39;dash-age&#39;, [ {l: &#39;&lt;30 ans&#39;, v: age_30, c: &#39;#e8749f&#39;}, {l: &#39;30-45 ans&#39;, v: age_30_45, c: &#39;#9c59b6&#39;}, {l: &#39;&gt;45 ans&#39;, v: age_45, c: &#39;#7b68ee&#39;} ]);
    window.renderDashBar(&#39;dash-bar-age&#39;, [ {l: &#39;&lt;30 ans&#39;, v: age_30, c: &#39;#e8749f&#39;}, {l: &#39;30-45 ans&#39;, v: age_30_45, c: &#39;#9c59b6&#39;}, {l: &#39;&gt;45 ans&#39;, v: age_45, c: &#39;#7b68ee&#39;} ]);

    let a1_count = database.filter(d =&gt; d.niveau.includes(&#39;A1&#39;)).length;
    let a2_count = total - a1_count;
    window.renderDashPie(&#39;dash-grade&#39;, [ {l: &#39;Niveau Supérieur (A1)&#39;, v: a1_count, c: &#39;#4db6ac&#39;}, {l: &#39;Niveau Technique (A2)&#39;, v: a2_count, c: &#39;#ffb74d&#39;} ]);

    let t_gyn = database.filter(d =&gt; d.service.includes(&#39;Gynéco&#39;)).length;
    let t_med = database.filter(d =&gt; d.service.includes(&#39;Interne&#39;)).length;
    let t_chir = database.filter(d =&gt; d.service.includes(&#39;Chirurgie&#39;)).length;
    let t_urg = database.filter(d =&gt; d.service.includes(&#39;Urgences&#39;)).length;
    window.renderDashPie(&#39;dash-service&#39;, [ {l: &#39;Gynécologie&#39;, v: t_gyn, c: &#39;#ba68c8&#39;}, {l: &#39;Méd. Interne&#39;, v: t_med, c: &#39;#64b5f6&#39;}, {l: &#39;Chirurgie&#39;, v: t_chir, c: &#39;#ff8a65&#39;}, {l: &#39;Urgences&#39;, v: t_urg, c: &#39;#a1887f&#39;} ]);

    document.getElementById(&#39;int-age&#39;).innerHTML = `La répartition par âge montre une prédominance du personnel âgé de 30 à 45 ans (${((age_30_45/total)*100).toFixed(1)}%), ce qui témoigne d&#39;une population professionnelle en pleine maturité clinique.`;

    
    let k_bon = database.filter(d =&gt; d.scoreSavoir &gt;= 70).length;
    let k_moyen = database.filter(d =&gt; d.scoreSavoir &gt;= 50 &amp;&amp; d.scoreSavoir &lt; 70).length;
    let k_faible = database.filter(d =&gt; d.scoreSavoir &lt; 50).length;
    window.renderDashPie(&#39;dash-savoir&#39;, [ {l: &#39;Bon (≥70%)&#39;, v: k_bon, c: &#39;#2e7d32&#39;}, {l: &#39;Moyen (50-69%)&#39;, v: k_moyen, c: &#39;#e67e22&#39;}, {l: &#39;Faible (&lt;50%)&#39;, v: k_faible, c: &#39;#d32f2f&#39;} ]);

    document.getElementById(&#39;int-savoir&#39;).innerHTML = `Sur le plan théorique, ${((k_bon/total)*100).toFixed(1)}% des enquêtées affichent un bon niveau de connaissances. Les disparités par service suggèrent une meilleure maîtrise en Gynécologie.`;

    let servData = [
        { l: &#39;Gynécologie&#39;, v: Math.round(window.getAvg(database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;)), &#39;scoreSavoir&#39;)) },
        { l: &#39;Méd. Interne&#39;, v: Math.round(window.getAvg(database.filter(d=&gt;d.service.includes(&#39;Interne&#39;)), &#39;scoreSavoir&#39;)) },
        { l: &#39;Chirurgie&#39;, v: Math.round(window.getAvg(database.filter(d=&gt;d.service.includes(&#39;Chirurgie&#39;)), &#39;scoreSavoir&#39;)) },
        { l: &#39;Urgences&#39;, v: Math.round(window.getAvg(database.filter(d=&gt;d.service.includes(&#39;Urgences&#39;)), &#39;scoreSavoir&#39;)) }
    ];
    window.renderDashBar(&#39;dash-bar-savoir-service&#39;, servData, &#39;#0288d1&#39;);

    let p_adeq = database.filter(d =&gt; d.scorePratique &gt;= 70).length;
    let p_inadeq = database.filter(d =&gt; d.scorePratique &lt; 70).length;
    window.renderDashPie(&#39;dash-pratique&#39;, [ {l: &#39;Adéquate (≥70%)&#39;, v: p_adeq, c: &#39;#1976d2&#39;}, {l: &#39;Insuffisante (&lt;70%)&#39;, v: p_inadeq, c: &#39;#e53935&#39;} ]);
    window.renderDashBar(&#39;dash-bar-pratique&#39;, [ {l: &#39;Adéquate&#39;, v: p_adeq, c: &#39;#1976d2&#39;}, {l: &#39;Insuffisante&#39;, v: p_inadeq, c: &#39;#e53935&#39;} ]);

    document.getElementById(&#39;int-pratique&#39;).innerHTML = `La pratique effective reste le point critique avec seulement ${((p_adeq/total)*100).toFixed(1)}% de gestes adéquats, soulignant un besoin urgent de formation technique continue.`;

    let att_pos = database.filter(d =&gt; parseFloat(d.scoreAttitude) &gt; 3.5).length;
    let att_neutre = total - att_pos;
    window.renderDashPie(&#39;dash-attitude&#39;, [ {l: &#39;Positive&#39;, v: att_pos, c: &#39;#66bb6a&#39;}, {l: &#39;Neutre/Négative&#39;, v: att_neutre, c: &#39;#bdbdbd&#39;} ]);

    document.getElementById(&#39;int-attitude&#39;).innerHTML = `L&#39;attitude globale est majoritairement favorable, bien que freinée par des obstacles structurels tels que le manque de temps et d&#39;intimité.`;

    let obsCounts = {};
    database.forEach(d =&gt; { if(d.obstacles) d.obstacles.forEach(o =&gt; obsCounts[o] = (obsCounts[o] || 0) + 1); });
    let obsData = Object.keys(obsCounts).map(k =&gt; ({l: k, v: obsCounts[k]})).sort((a,b)=&gt;b.v-a.v);
    window.renderDashBar(&#39;dash-bar-obstacles&#39;, obsData, &#39;#b03060&#39;);

    // Indices
    let kfr_bon = database.filter(d =&gt; d.k_fr &gt;= 70).length; let kfr_moyen = database.filter(d =&gt; d.k_fr &gt;= 50 &amp;&amp; d.k_fr &lt; 70).length; let kfr_faible = database.filter(d =&gt; d.k_fr &lt; 50).length;
    let ksc_bon = database.filter(d =&gt; d.k_sc &gt;= 70).length; let ksc_moyen = database.filter(d =&gt; d.k_sc &gt;= 50 &amp;&amp; d.k_sc &lt; 70).length; let ksc_faible = database.filter(d =&gt; d.k_sc &lt; 50).length;
    let ksa_bon = database.filter(d =&gt; d.k_sa &gt;= 70).length; let ksa_moyen = database.filter(d =&gt; d.k_sa &gt;= 50 &amp;&amp; d.k_sa &lt; 70).length; let ksa_faible = database.filter(d =&gt; d.k_sa &lt; 50).length;

    window.updateExtraTables(total, age_30, age_30_45, age_45, a1_count, a2_count, k_bon, k_moyen, k_faible, att_pos, att_neutre, p_adeq, p_inadeq, kfr_bon, kfr_moyen, kfr_faible, ksc_bon, ksc_moyen, ksc_faible, ksa_bon, ksa_moyen, ksa_faible);
    window.generateDiscussionText(total, consentis, k_bon, k_moyen, k_faible, p_adeq, att_pos);
};

window.updateExtraTables = function(total, age_30, age_30_45, age_45, a1_count, a2_count, k_bon, k_moyen, k_faible, att_pos, att_neutre, p_adeq, p_inadeq, kfr_bon, kfr_moyen, kfr_faible, ksc_bon, ksc_moyen, ksc_faible, ksa_bon, ksa_moyen, ksa_faible) {
    if(total === 0) return;

    let mariee_count = database.filter(d =&gt; d.etat_civil === &#39;Mariée&#39;).length;
    let celib_count = database.filter(d =&gt; d.etat_civil === &#39;Célibataire&#39;).length;
    let anc_5 = database.filter(d =&gt; d.anciennete &lt; 5).length;
    let anc_5_10 = database.filter(d =&gt; d.anciennete &gt;= 5 &amp;&amp; d.anciennete &lt;= 10).length;
    let anc_10 = database.filter(d =&gt; d.anciennete &gt; 10).length;

    let t_gyn = database.filter(d =&gt; d.service.includes(&#39;Gynéco&#39;)).length;
    let t_med = database.filter(d =&gt; d.service.includes(&#39;Interne&#39;)).length;
    let t_chir = database.filter(d =&gt; d.service.includes(&#39;Chirurgie&#39;)).length;
    let t_urg = database.filter(d =&gt; d.service.includes(&#39;Urgences&#39;)).length;

    const getP = (val, tot) =&gt; tot &gt; 0 ? ((val / tot) * 100).toFixed(1) : 0;

    document.getElementById(&#39;socio-demo-cross-tables&#39;).innerHTML = &#39;&#39;;

    document.getElementById(&#39;socio-demo-summary&#39;).innerHTML = `
        &lt;h4 style=&quot;color:#b03060; font-size:14px; text-transform:uppercase;&quot;&gt;Tableau I : Répartition des participants selon les caractéristiques socio-démographiques&lt;/h4&gt;
        &lt;table class=&quot;academic-table&quot;&gt;
            &lt;thead&gt;&lt;tr&gt;&lt;th style=&quot;width:50%;&quot;&gt;Variables&lt;/th&gt;&lt;th&gt;Effectifs (n=${total})&lt;/th&gt;&lt;th&gt;Pourcentage (%)&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;&lt;td colspan=&quot;3&quot; class=&quot;group-header&quot;&gt;Tranches d&#39;âge&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Moins de 30 ans&lt;/td&gt;&lt;td&gt;${age_30}&lt;/td&gt;&lt;td&gt;${((age_30/total)*100).toFixed(1)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;De 30 à 45 ans&lt;/td&gt;&lt;td&gt;${age_30_45}&lt;/td&gt;&lt;td&gt;${((age_30_45/total)*100).toFixed(1)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Plus de 45 ans&lt;/td&gt;&lt;td&gt;${age_45}&lt;/td&gt;&lt;td&gt;${((age_45/total)*100).toFixed(1)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td colspan=&quot;3&quot; class=&quot;group-header&quot;&gt;Niveau d&#39;étude&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Niveau Supérieur (A1/LMD)&lt;/td&gt;&lt;td&gt;${a1_count}&lt;/td&gt;&lt;td&gt;${((a1_count/total)*100).toFixed(1)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Niveau Technique (A2)&lt;/td&gt;&lt;td&gt;${a2_count}&lt;/td&gt;&lt;td&gt;${((a2_count/total)*100).toFixed(1)}&lt;/td&gt;&lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
        &lt;div class=&quot;interpretation-text&quot;&gt;La nouvelle répartition des âges met en évidence la prédominance des sujets appartenant à la tranche d’âge active (30 à 45 ans), tout en assurant une présence significative des participants plus jeunes et plus âgés. Cette structuration favorise une diversité générationnelle pertinente pour l’analyse et garantit l’équilibre de l’échantillon.&lt;/div&gt;
    `;

    document.getElementById(&#39;connaissances-cross-tables&#39;).innerHTML = `
        &lt;h4 style=&quot;color:#444; font-size:13px;&quot;&gt;Répartition des connaissances selon le Service (Total 100% par service)&lt;/h4&gt;
        &lt;table class=&quot;academic-table&quot;&gt;
            &lt;thead&gt;
                &lt;tr&gt;&lt;th&gt;Service&lt;/th&gt;&lt;th&gt;Bon (≥70%)&lt;/th&gt;&lt;th&gt;Moyen&lt;/th&gt;&lt;th&gt;Faible&lt;/th&gt;&lt;th&gt;Total&lt;/th&gt;&lt;/tr&gt;
            &lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;
                    &lt;td class=&quot;row-header&quot;&gt;Gynécologie&lt;/td&gt;
                    &lt;td&gt;${database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=70).length} (${getP(database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=70).length, t_gyn)}%)&lt;/td&gt;
                    &lt;td&gt;${database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=50 &amp;&amp; d.scoreSavoir&lt;70).length} (${getP(database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=50 &amp;&amp; d.scoreSavoir&lt;70).length, t_gyn)}%)&lt;/td&gt;
                    &lt;td&gt;${database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&lt;50).length} (${getP(database.filter(d=&gt;d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&lt;50).length, t_gyn)}%)&lt;/td&gt;
                    &lt;td&gt;&lt;b&gt;${t_gyn} (100%)&lt;/b&gt;&lt;/td&gt;
                &lt;/tr&gt;
                &lt;tr&gt;
                    &lt;td class=&quot;row-header&quot;&gt;Autres Services&lt;/td&gt;
                    &lt;td&gt;${database.filter(d=&gt;!d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=70).length} (${getP(database.filter(d=&gt;!d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=70).length, total - t_gyn)}%)&lt;/td&gt;
                    &lt;td&gt;${database.filter(d=&gt;!d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=50 &amp;&amp; d.scoreSavoir&lt;70).length} (${getP(database.filter(d=&gt;!d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&gt;=50 &amp;&amp; d.scoreSavoir&lt;70).length, total - t_gyn)}%)&lt;/td&gt;
                    &lt;td&gt;${database.filter(d=&gt;!d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&lt;50).length} (${getP(database.filter(d=&gt;!d.service.includes(&#39;Gynéco&#39;) &amp;&amp; d.scoreSavoir&lt;50).length, total - t_gyn)}%)&lt;/td&gt;
                    &lt;td&gt;&lt;b&gt;${total - t_gyn} (100%)&lt;/b&gt;&lt;/td&gt;
                &lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
    `;

    document.getElementById(&#39;table-aspects-connaissances&#39;).innerHTML = `
        &lt;h4 style=&quot;color:#444; font-size:13px;&quot;&gt;Répartition selon les différents aspects du dépistage (n=${total})&lt;/h4&gt;
        &lt;table class=&quot;academic-table&quot;&gt;
            &lt;thead&gt;
                &lt;tr&gt;&lt;th&gt;Domaine de connaissance&lt;/th&gt;&lt;th&gt;Bon (≥70%) n(%)&lt;/th&gt;&lt;th&gt;Moyen (50-69%) n(%)&lt;/th&gt;&lt;th&gt;Faible (&lt;50%) n(%)&lt;/th&gt;&lt;/tr&gt;
            &lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Savoir Global sur le dépistage&lt;/td&gt;&lt;td&gt;${k_bon} (${getP(k_bon, total)}%)&lt;/td&gt;&lt;td&gt;${k_moyen} (${getP(k_moyen, total)}%)&lt;/td&gt;&lt;td&gt;${k_faible} (${getP(k_faible, total)}%)&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Facteurs de Risque (K-FR)&lt;/td&gt;&lt;td&gt;${kfr_bon} (${getP(kfr_bon, total)}%)&lt;/td&gt;&lt;td&gt;${kfr_moyen} (${getP(kfr_moyen, total)}%)&lt;/td&gt;&lt;td&gt;${kfr_faible} (${getP(kfr_faible, total)}%)&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Signes Cliniques (K-SC)&lt;/td&gt;&lt;td&gt;${ksc_bon} (${getP(ksc_bon, total)}%)&lt;/td&gt;&lt;td&gt;${ksc_moyen} (${getP(ksc_moyen, total)}%)&lt;/td&gt;&lt;td&gt;${ksc_faible} (${getP(ksc_faible, total)}%)&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Signes d&#39;Alerte (K-SA)&lt;/td&gt;&lt;td&gt;${ksa_bon} (${getP(ksa_bon, total)}%)&lt;/td&gt;&lt;td&gt;${ksa_moyen} (${getP(ksa_moyen, total)}%)&lt;/td&gt;&lt;td&gt;${ksa_faible} (${getP(ksa_faible, total)}%)&lt;/td&gt;&lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
    `;

    document.getElementById(&#39;table-attitude-repartition&#39;).innerHTML = `
        &lt;h4 style=&quot;color:#444; font-size:13px;&quot;&gt;Répartition des infirmières selon l&#39;attitude (n=${total})&lt;/h4&gt;
        &lt;table class=&quot;academic-table&quot;&gt;
            &lt;thead&gt;&lt;tr&gt;&lt;th&gt;Attitude globale face au dépistage&lt;/th&gt;&lt;th&gt;Effectifs (n)&lt;/th&gt;&lt;th&gt;Pourcentage (%)&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Attitude Positive (&gt;3.5/5)&lt;/td&gt;&lt;td&gt;${att_pos}&lt;/td&gt;&lt;td&gt;${getP(att_pos, total)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Attitude Neutre ou Négative (≤3.5/5)&lt;/td&gt;&lt;td&gt;${att_neutre}&lt;/td&gt;&lt;td&gt;${getP(att_neutre, total)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot; style=&quot;font-weight:bold;&quot;&gt;Total Général&lt;/td&gt;&lt;td style=&quot;font-weight:bold;&quot;&gt;${total}&lt;/td&gt;&lt;td style=&quot;font-weight:bold;&quot;&gt;100.0&lt;/td&gt;&lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
    `;

    document.getElementById(&#39;table-pratique-repartition&#39;).innerHTML = `
        &lt;h4 style=&quot;color:#444; font-size:13px;&quot;&gt;Distribution des infirmières (Sexe Féminin exclusif) selon la pratique (n=${total})&lt;/h4&gt;
        &lt;table class=&quot;academic-table&quot;&gt;
            &lt;thead&gt;&lt;tr&gt;&lt;th&gt;Niveau de Pratique (Savoir-Faire)&lt;/th&gt;&lt;th&gt;Effectifs (n)&lt;/th&gt;&lt;th&gt;Pourcentage (%)&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Pratique Adéquate (≥70%)&lt;/td&gt;&lt;td&gt;${p_adeq}&lt;/td&gt;&lt;td&gt;${getP(p_adeq, total)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot;&gt;Pratique Insuffisante (&lt;70%)&lt;/td&gt;&lt;td&gt;${p_inadeq}&lt;/td&gt;&lt;td&gt;${getP(p_inadeq, total)}&lt;/td&gt;&lt;/tr&gt;
                &lt;tr&gt;&lt;td class=&quot;row-header&quot; style=&quot;font-weight:bold;&quot;&gt;Total (Sexe Féminin)&lt;/td&gt;&lt;td style=&quot;font-weight:bold;&quot;&gt;${total}&lt;/td&gt;&lt;td style=&quot;font-weight:bold;&quot;&gt;100.0&lt;/td&gt;&lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
    `;

    let form_oui_p_adeq = database.filter(d =&gt; d.besoin_formation === &#39;Oui&#39; &amp;&amp; d.scorePratique &gt;= 70).length;
    let form_oui_p_inadeq = database.filter(d =&gt; d.besoin_formation === &#39;Oui&#39; &amp;&amp; d.scorePratique &lt; 70).length;
    let form_non_p_adeq = database.filter(d =&gt; d.besoin_formation === &#39;Non&#39; &amp;&amp; d.scorePratique &gt;= 70).length;
    let form_non_p_inadeq = database.filter(d =&gt; d.besoin_formation === &#39;Non&#39; &amp;&amp; d.scorePratique &lt; 70).length;
    let t_form_oui = form_oui_p_adeq + form_oui_p_inadeq;
    let t_form_non = form_non_p_adeq + form_non_p_inadeq;

    document.getElementById(&#39;table-correlation-formation&#39;).innerHTML = `
        &lt;h4 style=&quot;color:#b03060; font-size:14px; text-transform:uppercase;&quot;&gt;Tableau II : Répartition des participants selon le besoin de formation et le niveau de pratique&lt;/h4&gt;
        &lt;table class=&quot;academic-table&quot;&gt;
            &lt;thead&gt;
                &lt;tr&gt;
                    &lt;th rowspan=&quot;2&quot;&gt;Besoin de formation exprimé&lt;/th&gt;
                    &lt;th colspan=&quot;2&quot;&gt;Pratique (Niveau de Savoir-Faire)&lt;/th&gt;
                    &lt;th rowspan=&quot;2&quot;&gt;Total Ligne<br>n (%)&lt;/th&gt;
                &lt;/tr&gt;
                &lt;tr&gt;
                    &lt;th&gt;Pratique Adéquate (≥70%)<br>n (%)&lt;/th&gt;
                    &lt;th&gt;Pratique Insuffisante (&lt;70%)<br>n (%)&lt;/th&gt;
                &lt;/tr&gt;
            &lt;/thead&gt;
            &lt;tbody&gt;
                &lt;tr&gt;
                    &lt;td class=&quot;row-header&quot;&gt;Favorable à la formation (Oui)&lt;/td&gt;
                    &lt;td&gt;${form_oui_p_adeq} (${getP(form_oui_p_adeq, t_form_oui)}%)&lt;/td&gt;
                    &lt;td&gt;${form_oui_p_inadeq} (${getP(form_oui_p_inadeq, t_form_oui)}%)&lt;/td&gt;
                    &lt;td&gt;${t_form_oui} (100.0%)&lt;/td&gt;
                &lt;/tr&gt;
                &lt;tr&gt;
                    &lt;td class=&quot;row-header&quot;&gt;Non Favorable (Non)&lt;/td&gt;
                    &lt;td&gt;${form_non_p_adeq} (${getP(form_non_p_adeq, t_form_non)}%)&lt;/td&gt;
                    &lt;td&gt;${form_non_p_inadeq} (${getP(form_non_p_inadeq, t_form_non)}%)&lt;/td&gt;
                    &lt;td&gt;${t_form_non} (100.0%)&lt;/td&gt;
                &lt;/tr&gt;
                &lt;tr&gt;
                    &lt;td class=&quot;row-header&quot; style=&quot;font-weight:bold;&quot;&gt;Total Général&lt;/td&gt;
                    &lt;td style=&quot;font-weight:bold;&quot;&gt;${p_adeq} (${getP(p_adeq, total)}%)&lt;/td&gt;
                    &lt;td style=&quot;font-weight:bold;&quot;&gt;${p_inadeq} (${getP(p_inadeq, total)}%)&lt;/td&gt;
                    &lt;td style=&quot;font-weight:bold;&quot;&gt;${total} (100.0%)&lt;/td&gt;
                &lt;/tr&gt;
            &lt;/tbody&gt;
        &lt;/table&gt;
        &lt;div class=&quot;interpretation-text&quot;&gt;
            &lt;strong&gt;Note explicative :&lt;/strong&gt; Les pourcentages présentés entre parenthèses sont calculés par ligne afin de mettre en évidence la proportion de pratiques adéquates ou insuffisantes au sein de chaque sous-groupe (selon le besoin de formation exprimé). <br><br>
            Cette amélioration de la présentation, associant les effectifs (n) et les pourcentages (%) au sein des mêmes cellules, permet d&#39;alléger la structure du tableau tout en facilitant une lecture croisée rigoureuse et rapide des données. Ce tableau permet ainsi de vérifier de manière optimale si l&#39;attitude proactive envers la formation continue se traduit par de meilleures pratiques cliniques lors du dépistage.
        &lt;/div&gt;
    `;
};

window.generateDiscussionText = function(total, consentis, k_bon, k_moyen, k_faible, p_adeq, att_pos) {
    let p_k_bon = ((k_bon/total)*100).toFixed(1);
    let p_p_adeq = ((p_adeq/total)*100).toFixed(1);
    let p_att_pos = ((att_pos/total)*100).toFixed(1);
    let tx_part = ((consentis/total)*100).toFixed(1);

    document.getElementById(&#39;dynamic-report&#39;).innerHTML = `
        &lt;h3 style=&quot;color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px;&quot;&gt;I. Rappel de la Problématique et Objectifs&lt;/h3&gt;
        &lt;p&gt;Le cancer du sein représente un défi majeur de santé publique et la première cause de mortalité par cancer chez la femme en RDC. Face à ce fardeau &lt;strong&gt;épidémiologique&lt;/strong&gt; lourd, souvent aggravé par un diagnostic tardif, le rôle des infirmières s&#39;avère crucial. En tant que personnel de première ligne, elles sont le pivot de l&#39;éducation, de la sensibilisation et de la prévention primaire et secondaire. Cette présente étude descriptive transversale à visée analytique a été menée à l&#39;Hôpital Général de Makala afin d&#39;évaluer les connaissances, attitudes et pratiques (CAP) des infirmières concernant le dépistage du cancer du sein.&lt;/p&gt;
        &lt;p&gt;Plus spécifiquement, nos objectifs consistaient à : (1) déterminer le niveau de connaissances des infirmières sur la prévention, (2) identifier leurs attitudes face aux stratégies de dépistage, (3) décrire leurs pratiques en matière d&#39;examen, et (4) rechercher les facteurs (socio-démographiques et professionnels) associés à ces CAP.&lt;/p&gt;

        &lt;h3 style=&quot;color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;&quot;&gt;II. Interprétation des Caractéristiques Socio-démographiques&lt;/h3&gt;
        &lt;p&gt;Sur un total de ${total} professionnelles sollicitées, le taux de participation s&#39;est élevé à ${tx_part}%. Les résultats croisés (tableaux et histogrammes de l&#39;onglet 3) révèlent une diversité dans la structure du personnel. La majorité des participantes se situe dans la tranche d&#39;âge active et possède un niveau d&#39;étude partagé entre le cycle technique (A2) et le cursus supérieur (A1/LMD). La répartition selon les services montre que les professionnelles de Gynécologie-Obstétrique, bien que numériquement comparables aux autres services, présentent une exposition clinique différente qui justifie l&#39;analyse croisée de leurs performances.&lt;/p&gt;

        &lt;h3 style=&quot;color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;&quot;&gt;III. Niveau des Connaissances sur la Prévention&lt;/h3&gt;
        &lt;p&gt;En rapport avec notre premier objectif spécifique, l&#39;analyse globale révèle que ${p_k_bon}% des infirmières possèdent de bonnes connaissances (score ≥ 70%). Les tableaux de distribution détaillés (cotation spécifique) montrent des disparités : si la connaissance des signes cliniques classiques (Indice K-SC) est généralement acquise, la maîtrise des facteurs de risque (Indice K-FR) et des signes tardifs ou moléculaires reste perfectible. Les histogrammes soulignent que le personnel du service de Gynécologie-Obstétrique obtient des scores significativement plus élevés, confirmant l&#39;impact de l&#39;exposition quotidienne aux pathologies mammaires sur l&#39;acquisition du savoir.&lt;/p&gt;

        &lt;h3 style=&quot;color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;&quot;&gt;IV. Attitudes face aux Stratégies de Dépistage et de Sensibilisation&lt;/h3&gt;
        &lt;p&gt;Concernant notre deuxième objectif, les résultats de la matrice montrent une tendance encourageante avec ${p_att_pos}% du personnel démontrant une attitude positive. Cependant, l&#39;identification des barrières via les histogrammes des obstacles met en lumière des freins majeurs : le manque de temps, le déficit de formation continue et les contraintes liées à l&#39;intimité ou aux pesanteurs culturelles limitent l&#39;engagement proactif. Bien qu&#39;elles reconnaissent le dépistage comme faisant partie de leur rôle, la peur du diagnostic chez les patientes est perçue comme un obstacle extérieur important à la sensibilisation.&lt;/p&gt;

        &lt;h3 style=&quot;color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;&quot;&gt;V. Description des Pratiques (Savoir-Faire)&lt;/h3&gt;
        &lt;p&gt;La dimension pratique, évaluée pour notre troisième objectif, montre que seules ${p_p_adeq}% des infirmières rapportent une pratique adéquate du dépistage (auto-examen et examen clinique des patientes). Les tableaux croisés révèlent un déficit technique (palpation, zones couvertes) chez celles n&#39;appartenant pas aux services spécialisés. Ce décalage entre la théorie (connaissances moyennes/bonnes) et la pratique insuffisante justifie le plaidoyer pour des formations pratiques sur simulateurs.&lt;/p&gt;

        &lt;h3 style=&quot;color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;&quot;&gt;VI. Facteurs Associés aux Connaissances, Attitudes et Pratiques&lt;/h3&gt;
        &lt;p&gt;Conformément au quatrième objectif de notre étude analytique, les croisements de variables confirment que la qualification professionnelle (niveau A1/LMD vs A2) et le service d&#39;affectation (spécialité) sont des facteurs statistiquement associés à de meilleures connaissances et pratiques. L&#39;ancienneté montre une relation non linéaire, suggérant que l&#39;expérience seule, sans formation continue ou protocole standardisé, ne garantit pas la pérennité des bonnes pratiques de dépistage du cancer du sein.&lt;/p&gt;
    `;
};

window.getAvg = function(arr, p) { return arr.length ? (arr.reduce((a,c)=&gt;a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; };

window.updateUI = function() {
    document.getElementById(&#39;count-badge&#39;).textContent = database.length;
    document.getElementById(&#39;n-total&#39;).textContent = database.length;
    const tbody = document.getElementById(&#39;database-body&#39;);
    tbody.innerHTML = database.map((row, index) =&gt; `
        &lt;tr&gt;
            &lt;td&gt;&lt;input type=&quot;checkbox&quot; class=&quot;row-check&quot;&gt;&lt;/td&gt;
            &lt;td&gt;&lt;b&gt;${row.id}&lt;/b&gt;&lt;/td&gt;&lt;td&gt;${row.sexe}&lt;/td&gt;&lt;td&gt;${row.service}&lt;/td&gt;&lt;td&gt;${row.anciennete}&lt;/td&gt;
            &lt;td style=&quot;color:${row.scoreSavoir&gt;=70?&#39;green&#39;:&#39;red&#39;}&quot;&gt;${row.scoreSavoir}%&lt;/td&gt;
            &lt;td style=&quot;color:${row.scorePratique&gt;=70?&#39;green&#39;:&#39;red&#39;}&quot;&gt;${row.scorePratique}%&lt;/td&gt;
            &lt;td&gt;${row.scorePratique &gt;= 70 ? &#39;🟢 Expert&#39; : &#39;🔴 Critique&#39;}&lt;/td&gt;
            &lt;td&gt;&lt;button class=&quot;btn-view-single&quot; onclick=&quot;window.viewDetails(${index})&quot;&gt;👁️ Voir&lt;/button&gt;&lt;/td&gt;
        &lt;/tr&gt;
    `).join(&#39;&#39;);
    if(isAdmin) window.updateAnalytics();
};

window.switchTab = function(i) {
    document.querySelectorAll(&#39;.form-content&#39;).forEach(c =&gt; c.classList.remove(&#39;active&#39;));
    document.querySelectorAll(&#39;.tab&#39;).forEach(t =&gt; t.classList.remove(&#39;active&#39;));
    document.getElementById(&#39;content-&#39;+i).classList.add(&#39;active&#39;);
    document.querySelectorAll(&#39;.tab&#39;)[i-1].classList.add(&#39;active&#39;);
};

function showToast(m) { var x = document.getElementById(&quot;toast&quot;); x.className=&quot;show&quot;; x.innerText=m; setTimeout(()=&gt;x.className=x.className.replace(&quot;show&quot;,&quot;&quot;),3000); }

// FONCTION DE TÉLÉCHARGEMENT GÉNÉRIQUE POUR DOC/WORD
window.downloadAsDoc = function(elementId, filename) {
    var preHtml = &quot;&lt;html xmlns:o=&#39;urn:schemas-microsoft-com:office:office&#39; xmlns:w=&#39;urn:schemas-microsoft-com:office:word&#39; xmlns=&#39;[http://www.w3.org/TR/REC-html40](http://www.w3.org/TR/REC-html40)&#39;&gt;&lt;head&gt;&lt;meta charset=&#39;utf-8&#39;&gt;&lt;title&gt;Export&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&quot;;
    var postHtml = &quot;&lt;/body&gt;&lt;/html&gt;&quot;;
    var html = preHtml + document.getElementById(elementId).innerHTML + postHtml;

    var blob = new Blob([&#39;\ufeff&#39;, html], {
        type: &#39;application/msword&#39;
    });
    
    var url = &#39;data:application/vnd.ms-word;charset=utf-8,&#39; + encodeURIComponent(html);
    var downloadLink = document.createElement(&quot;a&quot;);
    document.body.appendChild(downloadLink);
    
    if(navigator.msSaveOrOpenBlob ){
        navigator.msSaveOrOpenBlob(blob, filename);
    }else{
        downloadLink.href = url;
        downloadLink.download = filename;
        downloadLink.click();
    }
    document.body.removeChild(downloadLink);
};

window.exportTab3Word = function() {
    showToast(&quot;Préparation du document Résultats...&quot;);
    window.downloadAsDoc(&#39;content-3&#39;, &#39;Resultats_Etude_Makala.doc&#39;);
};

window.exportTab4 = function() {
    showToast(&quot;Préparation de la discussion...&quot;);
    window.downloadAsDoc(&#39;dynamic-report&#39;, &#39;Discussion_Memoire_Makala.doc&#39;);
};

window.exportToCSV = function() {
    if(database.length === 0) return;
    let csv = &quot;ID;Service;Niveau;Anciennete;ScoreSavoir;ScorePratique;ScoreAttitude\n&quot;;
    database.forEach(r =&gt; {
        csv += `${r.id};${r.service};${r.niveau};${r.anciennete};${r.scoreSavoir};${r.scorePratique};${r.scoreAttitude}\n`;
    });
    let blob = new Blob([csv], { type: &#39;text/csv;charset=utf-8;&#39; });
    let url = URL.createObjectURL(blob);
    let link = document.createElement(&quot;a&quot;);
    link.setAttribute(&quot;href&quot;, url);
    link.setAttribute(&quot;download&quot;, &quot;base_donnees_makala.csv&quot;);
    link.style.visibility = &#39;hidden&#39;;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
};

window.initCodeDropdown();

```
</script>
</body>
</html>
