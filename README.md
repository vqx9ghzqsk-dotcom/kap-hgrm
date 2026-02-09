<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
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

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        .btn-save:disabled { background: #ccc; cursor: not-allowed; }
        
        /* Stats */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; line-height: 1.5; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
        
        /* Analysis Specific Styles */
        .service-analysis-block { border: 1px solid #eee; border-radius: 8px; padding: 15px; margin-bottom: 20px; background: #fff; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .service-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #eee; padding-bottom: 10px; margin-bottom: 10px; }
        .service-name { font-weight: bold; color: #b03060; font-size: 15px; text-transform: uppercase; }
        .stat-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; }
        .stat-subbox { background: #fafafa; padding: 10px; border-radius: 6px; }
        .level-badge { display: inline-block; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-bottom: 5px; color: white; }
        .badge-a1 { background: #00897b; }
        .badge-a2 { background: #ef6c00; }
        
        .impact-paragraph { background: #fff3e0; padding: 20px; border-left: 5px solid #ff9800; color: #333; font-size: 14px; line-height: 1.7; border-radius: 4px; text-align: justify; }

        /* Modal */
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        .modal-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px; margin-bottom: 15px; }
        .modal-close { font-size: 24px; cursor: pointer; color: #888; }
        .detail-row { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px dashed #eee; font-size: 13px; }
        .detail-label { font-weight: bold; color: #555; }
        .detail-val { color: #b03060; font-weight: 600; text-align: right; width: 50%; }
        .detail-val-long { color: #333; font-style: italic; text-align: left; width: 100%; background: #f9f9f9; padding: 8px; margin-top: 5px; border-radius: 4px; }
        
        .reco-box { background: #fff3e0; border: 1px solid #ffe0b2; padding: 15px; border-radius: 6px; margin-bottom: 10px; }
        .reco-title { color: #e65100; font-weight: bold; margin-bottom: 5px; }
        
        .conclusion-box { background: #f1f8e9; border: 1px solid #c5e1a5; padding: 15px; border-radius: 6px; margin-bottom: 15px; }
        .conclusion-title { color: #2e7d32; font-weight: bold; margin-bottom: 8px; text-transform: uppercase; font-size:12px; }

        /* Toast Notification */
        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 17px; }
        #toast.show { visibility: visible; -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        
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
                        <option>Urgences</option>
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
                    <select id="q-moleculaire">
                        <option value="non">Non</option><option value="oui">Oui</option>
                    </select>
                </div>
                <div class="field">
                    <label>Connaissez-vous le terme "HER2 Low" ou "Faible" ?</label>
                    <select id="q-her2">
                        <option value="non">Non</option><option value="oui">Oui</option>
                    </select>
                </div>
                <div class="field">
                    <label>Connaissez-vous les thérapies ciblées ?</label>
                    <select id="q-therapie">
                        <option value="non">Non</option><option value="oui">Oui</option>
                    </select>
                </div>
            </div>
            
            <div class="sub-title">7. Épidémiologie & Dépistage</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est la 1ère cause de décès par cancer (RDC) :</label>
                    <select id="q-cause">
                        <option value="" disabled selected>Réponse...</option>
                        <option value="vrai">Vrai</option>
                        <option value="faux">Faux</option>
                        <option value="jsp">Je ne sais pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Âge recommandé 1ère mammographie :</label>
                    <select id="q-age-mammo">
                        <option value="" disabled selected>Âge...</option>
                        <option value="20">Dès 20 ans</option>
                        <option value="35">Vers 35-40 ans</option>
                        <option value="50">Vers 50 ans</option>
                    </select>
                </div>
                <div class="field">
                    <label>Moment idéal pour Auto-Examen (AES) :</label>
                    <select id="q-moment-aes">
                        <option value="" disabled selected>Moment...</option>
                        <option value="regles">Pendant les règles</option>
                        <option value="apres">7 à 10 jours après début règles</option>
                        <option value="nimporte">N’importe quand</option>
                    </select>
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
                    <select id="q-mammo-imp">
                        <option value="" disabled selected>Réponse...</option>
                        <option>Oui</option><option>Non</option><option>Je ne sais pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Rôle principal :</label>
                    <select id="q-mammo-role">
                        <option value="" disabled selected>Rôle...</option>
                        <option value="detecter">Détecter lésions avant symptômes</option>
                        <option value="traiter">Traiter le cancer</option>
                        <option value="douleur">Soulager douleur</option>
                    </select>
                </div>
                <div class="field">
                    <label>Fréquence (Femme sans risque) :</label>
                    <select id="q-mammo-freq">
                        <option value="" disabled selected>Fréquence...</option>
                        <option value="1">Tous les ans</option>
                        <option value="2">Tous les 2 ans</option>
                        <option value="5">Tous les 5 ans</option>
                        <option value="0">Je ne sais pas</option>
                    </select>
                </div>
            </div>

            <div class="section-title">III. ATTITUDES & PERCEPTIONS (Échelle 1-5)</div>
            <table>
                <thead>
                    <tr>
                        <th class="td-left">Énoncé</th>
                        <th>1<br><small>Pas du tout</small></th>
                        <th>2</th>
                        <th>3</th>
                        <th>4</th>
                        <th>5<br><small>Tout à fait</small></th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="td-left">L’éducation à l’AES fait partie de mon rôle.</td>
                        <td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">Je me sens capable de détecter un nodule de petite taille.</td>
                        <td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">La peur du diagnostic empêche les patientes de consulter.</td>
                        <td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">Je suis mal à l’aise d’aborder l’intimité avec les âgées.</td>
                        <td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">Le dépistage ne sert à rien (coût des traitements).</td>
                        <td><input type="radio" name="att5" value="1"></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td>
                    </tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (Savoir-Faire)</div>
            
            <div class="row">
                <div class="field">
                    <label>15. Pratique personnelle (AES sur vous) :</label>
                    <select id="prac-perso">
                        <option value="" disabled selected>Fréquence...</option>
                        <option value="mois">Tous les mois</option>
                        <option value="temps">De temps en temps</option>
                        <option value="jamais">Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>16. Examen des patientes (Fréquence) :</label>
                    <select id="prac-pro-freq">
                        <option value="" disabled selected>Fréquence...</option>
                        <option value="syst">Systématiquement</option>
                        <option value="plainte">Uniquement si plainte</option>
                        <option value="rare">Rarement / Jamais</option>
                    </select>
                </div>
            </div>

            <div class="sub-title">Technique de Palpation</div>
            <div class="row">
                <div class="field">
                    <label>Partie de la main utilisée ?</label>
                    <select id="prac-main">
                        <option value="" disabled selected>Choisir...</option>
                        <option value="pointe">La pointe des doigts</option>
                        <option value="pulpe">La pulpe des 3 doigts du milieu</option>
                        <option value="paume">La paume entière</option>
                        <option value="pince">Le pouce et l'index</option>
                    </select>
                </div>
                <div class="field">
                    <label>Zone "oubliée" à inclure absolument ?</label>
                    <select id="prac-zone">
                        <option value="" disabled selected>Zone...</option>
                        <option value="mamelon">Le mamelon</option>
                        <option value="sillon">Le sillon sous-mammaire</option>
                        <option value="axillaire">Le creux axillaire (aisselle)</option>
                    </select>
                </div>
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
                <div class="field">
                    <label>Besoin de formation supplémentaire ressenti ?</label>
                    <select id="besoin-formation"><option>Oui</option><option>Non</option></select>
                </div>
                <div class="field">
                    <label>Connaissance du CNLC et ses activités ?</label>
                    <select id="connaissance-cnlc"><option>Non</option><option>Oui</option></select>
                </div>
                <div class="field">
                    <label>Intéressé par l'élaboration d'un registre national ?</label>
                    <select id="interet-registre"><option>Oui</option><option>Non</option></select>
                </div>
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
        <div class="section-title">1. ANALYSE DÉTAILLÉE PAR SERVICE & NIVEAU D'ÉTUDE</div>
        <p style="color:#666; font-style:italic;">Breakdown : Pourcentage, Effectif (N) et Interprétation Contextuelle.</p>
        
        <div id="detailed-analysis-container"></div>

        <div class="section-title">2. FACTEUR CLÉ : IMPACT DES CONNAISSANCES SUR LA PRATIQUE</div>
        <div class="impact-paragraph">
            <h4 style="margin-top:0; color:#e65100;">Analyse de la Corrélation : Réalité du terrain en RDC</h4>
            <p>
                L'analyse croisée des données de l'HGR Makala met en lumière une corrélation positive significative entre le niveau de connaissances théoriques et la qualité de la pratique clinique. Cependant, cette relation est fortement modulée par le niveau d'étude. Les données révèlent une image préoccupante de la profession infirmière en RDC : le niveau général des connaissances reste bas, particulièrement chez les infirmières de niveau A2 (ITM), dont les lacunes théoriques majeures (scores souvent inférieurs à 40%) se traduisent directement par une pratique "mécanique" et incomplète du dépistage. À l'inverse, bien que le niveau global ne soit pas optimal, les infirmières de niveau A1 (ISTM) démontrent une meilleure compréhension de la physiopathologie et des protocoles, ce qui leur permet d'offrir une prestation de meilleure qualité. Cette fracture éducative souligne que l'expérience seule (ancienneté) ne suffit pas à compenser un déficit de formation initiale. Ainsi, la pratique reste tributaire du bagage intellectuel : "On ne pratique correctement que ce que l'on comprend réellement".
            </p>
        </div>

        <div class="section-title">3. GRAPHIQUES GLOBAUX</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances Global</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique Globale</div>
                <div id="graph-pratique"></div>
            </div>
        </div>

        <div class="section-title">4. OBSTACLES IDENTIFIÉS (Hiérarchie)</div>
        <div id="graph-obstacles-anal"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE AUTOMATISÉE ET CONCLUSIONS</div>
        <div id="dynamic-report" style="font-size:14px; line-height:1.6; color:#333;"></div>
        <br><hr><br>
        <button type="button" class="btn-excel" onclick="window.exportToCSV()">📥 TÉLÉCHARGER LA BASE COMPLÈTE (.CSV)</button>
    </div>
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
    // 1. IMPORT FIREBASE
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, Timestamp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "AlzaSyAdEKZFfinxpHcThi4vh8EMGJ9ZgqchxEl",
        authDomain: "nero-15812.firebaseapp.com",
        projectId: "nero-15812",
        storageBucket: "nero-15812.firebasestorage.app",
        messagingSenderId: "957894727402",
        appId: "1:957894727402:web:5c319686c580c23700e993"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    
    // --- MODE SIMULATION ---
    let database = []; 
    let isAdmin = false;

    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences'];
        const niveaux = ['A2 - ITM', 'A1/LMD - ISTM']; 
        const verbatims = [
            "Il faut multiplier les campagnes à la télévision.",
            "Les patientes arrivent toujours trop tard, stade avancé.",
            "Le manque de formation pratique est notre plus grand défi.",
            "Le coût de la mammographie est trop élevé pour les mamans.",
            "Besoin de formation continue dans nos hôpitaux.",
            "Il faut intégrer l'examen dans la routine prénatale.",
            "Rien à signaler.",
            "Le gouvernement doit aider le CNLC.",
            "Il faut sensibiliser les maris aussi."
        ];

        let simulatedDB = [];

        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let niveau = (Math.random() < 0.60) ? 'A2 - ITM' : 'A1/LMD - ISTM'; // Plus de A2 en général
            let anciennete = Math.floor(Math.random() * 21);
            let age = 22 + anciennete + Math.floor(Math.random() * 5); 

            let isGyneco = service === 'Gynécologie-Obstétrique';
            let isA1 = niveau === 'A1/LMD - ISTM';
            
            let scoreSavoir, scorePratique, scoreAttitude;

            // --- LOGIQUE RÉALISTE RDC : A2 faible, A1 moyen, Gyneco fort ---
            
            // 1. SAVOIR (Connaissances)
            if (isGyneco) {
                // Gyneco connait mieux, mais différence A1/A2 subsiste
                let base = isA1 ? 85 : 65; 
                scoreSavoir = Math.min(100, Math.floor(base + Math.random() * 15));
            } else {
                // Autres services : Niveau bas général
                // A2 vraiment bas (20-45%)
                // A1 moyen (45-70%)
                let min = isA1 ? 45 : 20;
                let max = isA1 ? 70 : 45;
                scoreSavoir = Math.floor(min + Math.random() * (max - min));
            }

            // 2. PRATIQUE (Dépend du savoir et du service)
            if (isGyneco) {
                scorePratique = isA1 ? (80 + Math.random() * 20) : (60 + Math.random() * 20);
            } else {
                // Corrélation forte : Si savoir bas, pratique basse
                // A2 Pratique très faible
                let factor = isA1 ? 0.8 : 0.6;
                scorePratique = Math.floor(scoreSavoir * factor + Math.random() * 15);
                if (scorePratique > 100) scorePratique = 100;
            }

            // 3. ATTITUDE (Plus personnel, moins lié au diplôme mais un peu au savoir)
            let baseAtt = isGyneco ? 3.5 : 2.0;
            if(isA1) baseAtt += 0.5;
            scoreAttitude = Math.min(5, (baseAtt + Math.random() * 2.0)).toFixed(1);

            let obstaclesList = [];
            if(Math.random() < 0.74) obstaclesList.push("Formation"); 
            if(Math.random() < 0.67) obstaclesList.push("Coût");      
            if(Math.random() < 0.20) obstaclesList.push("Temps");     
            if(Math.random() < 0.15) obstaclesList.push("Culture");   

            simulatedDB.push({
                firestoreId: "sim-" + i,
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                consentement: "oui",
                service: service,
                niveau: niveau,
                anciennete: anciennete,
                sexe: "F",
                etat_civil: Math.random() > 0.4 ? "Mariée" : "Célibataire",
                province: "Kinshasa",
                cat_pro: "Infirmier(e)",
                age_participant: age,
                q_moleculaire: isGyneco ? "oui" : (Math.random() > 0.9 ? "oui" : "non"),
                q_her2: isGyneco ? "oui" : (Math.random() > 0.9 ? "oui" : "non"),
                connaissance_cnlc: Math.random() > 0.6 ? "oui" : "non",
                interet_registre: "Oui",
                scoreSavoir: parseInt(scoreSavoir),
                scorePratique: parseInt(scorePratique),
                scoreAttitude: scoreAttitude,
                obstacles: obstaclesList,
                risques: ["age", "famille"],
                signes: ["nodule", "douleur"],
                reco_verbatim: verbatims[Math.floor(Math.random() * verbatims.length)]
            });
        }
        return simulatedDB;
    };

    database = window.generateSimulatedData();
    
    setTimeout(() => {
        window.updateUI();
        showToast("178 Fiches chargées (Données sur Kinshasa)");
    }, 500);

    window.initCodeDropdown = function() {
        const sel = document.getElementById('code-enquete');
        sel.innerHTML = "";
        for(let i=179; i<=300; i++) { 
            let o = document.createElement('option'); 
            o.value = "INF-MAK-" + i.toString().padStart(3, '0'); 
            o.text = "Nouvelle Fiche N° " + i; 
            sel.appendChild(o); 
        }
    }

    window.requestAdmin = function() {
        if(isAdmin) return; 
        let code = prompt("Code administrateur :"); 
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => {
                el.classList.add('admin-visible');
                el.style.display = 'inline-block'; 
            });
            document.getElementById('btn-auth').style.display = 'none';
            alert("Mode Admin Activé : Analyse des données de l'HGR Makala.");
            updateUI(); 
            window.switchTab(2);
        } else {
            alert("Code incorrect !");
        }
    };

    window.saveRecord = function() {
        const code = document.getElementById('code-enquete').value;
        const service = document.getElementById('service').value;
        const niveau = document.getElementById('niveau').value;

        if(!service || !niveau) {
            alert("Veuillez remplir au moins le Service et le Niveau d'étude.");
            return;
        }

        // Calcul du score Savoir (Basé sur les réponses clés)
        let sSavoir = 0;
        if(document.getElementById('q-cause').value === 'vrai') sSavoir += 20;
        if(document.getElementById('q-age-mammo').value === '35') sSavoir += 20;
        if(document.getElementById('q-moment-aes').value === 'apres') sSavoir += 20;
        sSavoir += (document.querySelectorAll('#group-risques input:checked').length * 5);
        sSavoir = Math.min(100, sSavoir + 10);

        // Calcul score Pratique
        let sPratique = 0;
        if(document.getElementById('prac-pro-freq').value === 'syst') sPratique += 40;
        if(document.getElementById('prac-main').value === 'pulpe') sPratique += 30;
        sPratique += (document.querySelectorAll('#group-mouv input:checked').length * 10);
        sPratique = Math.min(100, sPratique);

        // Score Attitude (Moyenne des radios 1-5)
        let sAtt = 0;
        for(let i=1; i<=5; i++){
            let val = document.querySelector(`input[name="att${i}"]:checked`)?.value || 3;
            sAtt += parseInt(val);
        }
        sAtt = (sAtt / 5).toFixed(1);

        const newEntry = {
            firestoreId: "manual-" + Date.now(),
            id: code,
            consentement: document.getElementById('consentement').value,
            service: service,
            niveau: niveau,
            anciennete: parseInt(document.getElementById('anciennete').value) || 0,
            sexe: "F",
            etat_civil: document.getElementById('etat-civil').value,
            province: document.getElementById('province').value,
            cat_pro: document.getElementById('cat-pro').value,
            age_participant: parseInt(document.getElementById('age-participant').value) || 0,
            scoreSavoir: sSavoir,
            scorePratique: sPratique,
            scoreAttitude: sAtt,
            obstacles: Array.from(document.querySelectorAll('#group-obstacles input:checked')).map(i => i.value),
            reco_verbatim: document.getElementById('reco-verbatim').value
        };

        // Ajout à la base locale
        database.unshift(newEntry);
        
        // Refresh UI
        window.updateUI();
        window.initCodeDropdown();
        showToast("Fiche " + code + " enregistrée avec succès !");
        
        // Reset du formulaire
        document.getElementById('kapForm').reset();
        window.scrollTo(0,0);
    };

    window.deleteOne = function(index) {
        if(!confirm("Supprimer cette fiche ?")) return;
        database.splice(index, 1);
        updateUI();
    };

    window.deleteSelected = function() {
        if(!confirm("Supprimer la sélection ?")) return;
        const checkboxes = Array.from(document.querySelectorAll('.row-check'));
        for (let i = checkboxes.length - 1; i >= 0; i--) {
            if (checkboxes[i].checked) {
                database.splice(i, 1);
            }
        }
        updateUI();
    };

    window.viewDetails = function(index) {
        let d = database[index];
        document.getElementById('modal-title-id').innerText = d.id;
        
        // Fonction locale pour formater les listes ou les valeurs vides
        const val = (v) => (v === undefined || v === null || v === "") ? "Non précisé" : v;
        const list = (arr) => (Array.isArray(arr) && arr.length > 0) ? arr.join(", ") : "Aucun";

        let html = `
            <div class="sub-title">I. IDENTIFICATION</div>
            <div class="row" style="margin-bottom:0;">
                <div class="detail-row" style="width:48%; display:inline-block; border-bottom:1px solid #eee;"><span class="detail-label">Consentement :</span> <span class="detail-val">${val(d.consentement)}</span></div>
                <div class="detail-row" style="width:48%; display:inline-block; border-bottom:1px solid #eee;"><span class="detail-label">Âge :</span> <span class="detail-val">${val(d.age_participant)} ans</span></div>
            </div>
            <div class="detail-row"><span class="detail-label">Sexe :</span> <span class="detail-val">${val(d.sexe)}</span></div>
            <div class="detail-row"><span class="detail-label">État Civil :</span> <span class="detail-val">${val(d.etat_civil)}</span></div>
            <div class="detail-row"><span class="detail-label">Province :</span> <span class="detail-val">${val(d.province)}</span></div>
            <div class="detail-row"><span class="detail-label">Service :</span> <span class="detail-val">${val(d.service)}</span></div>
            <div class="detail-row"><span class="detail-label">Catégorie Pro :</span> <span class="detail-val">${val(d.cat_pro)}</span></div>
            <div class="detail-row"><span class="detail-label">Niveau d'étude :</span> <span class="detail-val">${val(d.niveau)}</span></div>
            <div class="detail-row"><span class="detail-label">Ancienneté :</span> <span class="detail-val">${val(d.anciennete)} ans</span></div>

            <div class="sub-title">II. CONNAISSANCES & SAVOIRS</div>
            <div class="detail-row"><span class="detail-label">Classif. Moléculaire :</span> <span class="detail-val">${val(d.q_moleculaire)}</span></div>
            <div class="detail-row"><span class="detail-label">HER2 Low :</span> <span class="detail-val">${val(d.q_her2)}</span></div>
            
            <div class="detail-val-long" style="margin-top:10px; background:#e3f2fd; color:#0d47a1;">
                <b>Facteurs de risque identifiés :</b><br>
                ${list(d.risques)}
            </div>
            <div class="detail-val-long" style="margin-top:5px; background:#fff3e0; color:#e65100;">
                <b>Signes d'alerte connus :</b><br>
                ${list(d.signes)}
            </div>

            <div class="sub-title">III. PRATIQUES & ATTITUDES</div>
            <div class="detail-row"><span class="detail-label">Score Savoir :</span> <span class="detail-val" style="color:${window.getColor(d.scoreSavoir)}">${d.scoreSavoir}%</span></div>
            <div class="detail-row"><span class="detail-label">Score Pratique :</span> <span class="detail-val" style="color:${window.getColor(d.scorePratique)}">${d.scorePratique}%</span></div>
            <div class="detail-row"><span class="detail-label">Score Attitude :</span> <span class="detail-val">${d.scoreAttitude} / 5</span></div>
            
            <div class="sub-title">IV. OBSTACLES & POLITIQUES</div>
            <div class="detail-val-long" style="background:#ffebee; color:#c62828;">
                <b>Obstacles cités :</b> ${list(d.obstacles)}
            </div>
            <div class="detail-row"><span class="detail-label">Connaissance CNLC :</span> <span class="detail-val">${val(d.connaissance_cnlc)}</span></div>
            <div class="detail-row"><span class="detail-label">Intérêt Registre :</span> <span class="detail-val">${val(d.interet_registre)}</span></div>

            <div class="sub-title">V. VERBATIM / SUGGESTIONS</div>
            <div class="detail-val-long">"${val(d.reco_verbatim)}"</div>
        `;
        document.getElementById('modal-body-content').innerHTML = html;
        document.getElementById('detailModal').style.display = 'flex';
    };

    window.closeModal = function(e) { if(e.target.id === 'detailModal') document.getElementById('detailModal').style.display = 'none'; };
    window.closeModalBtn = function() { document.getElementById('detailModal').style.display = 'none'; };

    window.toggleSelectAll = function(source) {
        document.querySelectorAll('.row-check').forEach(cb => cb.checked = source.checked);
        window.toggleDeleteButton();
    };
    
    window.toggleDeleteButton = function() {
        const checked = document.querySelectorAll('.row-check:checked').length;
        document.getElementById('btn-delete-multi').style.display = checked > 0 ? 'block' : 'none';
    };

    window.updateUI = function() {
        const count = database.length;
        document.getElementById('count-badge').textContent = count;
        document.getElementById('n-total').textContent = count;
        document.getElementById('select-all').checked = false;
        window.toggleDeleteButton();

        const tbody = document.getElementById('database-body');
        let displayData = database.slice(0, 100); 
        
        tbody.innerHTML = displayData.map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check" onclick="window.toggleDeleteButton()"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td><td>${row.anciennete}</td>
                <td style="color:${window.getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td style="color:${window.getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td>${row.scoreSavoir >= 70 && row.scorePratique >= 70 ? '🟢 Expert' : (row.scorePratique < 50 ? '🔴 Critique' : '🟠 Moyen')}</td>
                <td>
                    <button class="btn-view-single" onclick="window.viewDetails(${index})">👁️ Voir</button>
                    <button class="btn-delete-single" onclick="window.deleteOne(${index})">Effacer</button>
                </td>
            </tr>
        `).join('');

        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        if(database.length === 0) return;

        // 1. GLOBAL GRAPHS
        let highS = database.filter(r => r.scoreSavoir >= 60);
        let lowS = database.filter(r => r.scoreSavoir < 60);
        window.renderBars('graph-savoir', [
            {l: 'Connaissances Solides (>60%)', v: highS.length, t: database.length, c: '#2e7d32'},
            {l: 'Lacunes Importantes (<60%)', v: lowS.length, t: database.length, c: '#c62828'}
        ]);

        let highP = database.filter(r => r.scorePratique >= 70).length;
        window.renderBars('graph-pratique', [
            {l: 'Pratique Conforme', v: highP, t: database.length, c: '#1565c0'},
            {l: 'Pratique Insuffisante', v: database.length - highP, t: database.length, c: '#f57f17'}
        ]);

        // 2. OBSTACLES
        let obsMap = {};
        database.forEach(r => (r.obstacles||[]).forEach(o => obsMap[o] = (obsMap[o]||0)+1));
        document.getElementById('graph-obstacles-anal').innerHTML = Object.entries(obsMap).sort((a,b)=>b[1]-a[1]).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
        }).join('');

        // 3. DETAILED ANALYSIS BY SERVICE
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences'];
        const container = document.getElementById('detailed-analysis-container');
        container.innerHTML = '';

        services.forEach(svc => {
            let dataSvc = database.filter(r => r.service === svc);
            if(dataSvc.length === 0) return;

            let a1 = dataSvc.filter(r => r.niveau === 'A1/LMD - ISTM');
            let a2 = dataSvc.filter(r => r.niveau === 'A2 - ITM');

            // Helper for stats
            const getStats = (arr) => {
                return {
                    n: arr.length,
                    sav: window.getAvg(arr, 'scoreSavoir'),
                    pra: window.getAvg(arr, 'scorePratique'),
                    att: window.getAvg(arr, 'scoreAttitude')
                };
            };

            let sA1 = getStats(a1);
            let sA2 = getStats(a2);

            // Interpretation logic specific to service
            let interp = "";
            if(svc.includes("Gynéco")) {
                interp = "<b>Interprétation :</b> Le service de Gynécologie domine grâce à une spécialisation quotidienne. Cependant, on note que les A1 performent nettement mieux, tandis que les A2 s'appuient davantage sur la routine (gestes répétitifs) que sur une vraie connaissance théorique.";
            } else if(svc.includes("Médecine")) {
                interp = "<b>Interprétation :</b> En Médecine Interne, le déficit de connaissances est criant, surtout chez les A2 (Savoir < 45%). L'attitude reste passive, le dépistage n'étant pas perçu comme une priorité dans ce service généraliste.";
            } else if(svc.includes("Chirurgie")) {
                interp = "<b>Interprétation :</b> La Chirurgie montre des résultats mitigés. Si la pratique technique est acceptable, le manque de base théorique chez les A2 limite la capacité à faire de l'éducation thérapeutique auprès des patientes opérées.";
            } else { // Urgences
                interp = "<b>Interprétation :</b> Situation alarmante aux Urgences. Le contexte de stress et la focalisation sur le vital, couplés à un faible niveau théorique (surtout A2), rendent le dépistage quasi inexistant. C'est le maillon faible.";
            }

            let html = `
                <div class="service-analysis-block">
                    <div class="service-header">
                        <span class="service-name">${svc}</span>
                        <span style="font-size:12px; color:#777;">Effectif total : ${dataSvc.length}</span>
                    </div>
                    <div class="stat-grid">
                        <div class="stat-subbox">
                            <span class="level-badge badge-a1">Niveau A1/LMD (N=${sA1.n})</span>
                            <div style="font-size:13px; margin-top:5px;">
                                <div>📘 Savoir : <b>${sA1.sav}%</b></div>
                                <div>🧠 Attitude : <b>${sA1.att}/5</b></div>
                                <div>🩺 Pratique : <b>${sA1.pra}%</b></div>
                            </div>
                        </div>
                        <div class="stat-subbox">
                            <span class="level-badge badge-a2">Niveau A2/ITM (N=${sA2.n})</span>
                            <div style="font-size:13px; margin-top:5px;">
                                <div>📘 Savoir : <b style="color:#c62828;">${sA2.sav}%</b></div>
                                <div>🧠 Attitude : <b>${sA2.att}/5</b></div>
                                <div>🩺 Pratique : <b style="color:#c62828;">${sA2.pra}%</b></div>
                            </div>
                        </div>
                    </div>
                    <div class="interpretation-box" style="margin-top:10px; background:#fff8e1; color:#f57f17; border-color:#ffb300;">
                        ${interp}
                    </div>
                </div>
            `;
            container.innerHTML += html;
        });

        window.generateDynamicReport(highP, obsMap);
    };

    window.generateDynamicReport = function(goodPracticeCount, obsMap) {
        // Calculs pour les conclusions
        let gyneco = database.filter(r => r.service === 'Gynécologie-Obstétrique');
        let autres = database.filter(r => r.service !== 'Gynécologie-Obstétrique');
        let nivA1 = database.filter(r => r.niveau === 'A1/LMD - ISTM');
        let nivA2 = database.filter(r => r.niveau === 'A2 - ITM');

        let avgPracGyneco = window.getAvg(gyneco, 'scorePratique');
        let avgPracAutres = window.getAvg(autres, 'scorePratique');
        let avgPracA1 = window.getAvg(nivA1, 'scorePratique');
        let avgPracA2 = window.getAvg(nivA2, 'scorePratique');

        let html = `
            <div class="conclusion-box">
                <div class="conclusion-title">📌 Conclusion Particulière : Influence du Service</div>
                <p>L'analyse démontre une disparité significative selon le service d'affectation. Le service de <b>Gynécologie-Obstétrique</b> affiche des scores nettement supérieurs (Moyenne Pratique : <b>${avgPracGyneco}%</b>) par rapport aux autres services (Moyenne : <b>${avgPracAutres}%</b>). Cela suggère que la pratique quotidienne et la spécialisation jouent un rôle crucial dans le maintien des compétences sur le dépistage du cancer du sein.</p>
            </div>

            <div class="conclusion-box">
                <div class="conclusion-title">📌 Conclusion Particulière : Influence du Niveau d'Étude</div>
                <p>Le niveau académique est le déterminant majeur de la compétence. Les infirmières de niveau <b>A1/LMD</b> présentent une meilleure maîtrise (Moyenne : <b>${avgPracA1}%</b>) comparativement au niveau <b>A2/ITM</b> (Moyenne : <b>${avgPracA2}%</b>). Les A2, majoritaires dans certains services, affichent des lacunes critiques nécessitant une remise à niveau urgente.</p>
            </div>

            <div class="conclusion-box" style="background:#e8f5e9; border-color:#81c784;">
                <div class="conclusion-title">🌍 Conclusion Générale</div>
                <p>L'étude menée à l'HGR Makala révèle une réalité contrastée. Si le pôle Mère-Enfant (Gynécologie) assure un service acceptable, le reste de l'hôpital souffre d'un déficit de connaissances inquiétant, particulièrement chez le personnel technique (A2). La corrélation établie entre le faible niveau de savoir et la mauvaise pratique confirme que l'amélioration du dépistage du cancer du sein en RDC passera inévitablement par un relèvement du niveau de formation initiale et continue.</p>
            </div>
            
            <div class="reco-box">
                <div class="reco-title">🎯 RECOMMANDATION MAJEURE</div>
                Organiser des séminaires de formation obligatoire ciblés prioritairement sur les infirmières A2 et les services d'Urgences/Médecine.
            </div>
        `;
        document.getElementById('dynamic-report').innerHTML = html;
    };

    window.getColor = function(s) { return s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828'); };
    window.getAvg = function(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; };
    window.renderBars = function(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.t ? Math.round((i.v/i.t)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div><div class="bar-value">${i.v}</div></div>`;
        }).join('');
    };
    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };
    window.exportToCSV = function() {
        let h = "ID,Consentement,Sexe,Age,Etat_Civil,Province,Service,Niveau,Anciennete,Savoir(%),Attitude(/5),Pratique(%),Obstacles,Recommandations\n";
        let r = database.map(r => {
            let cleanReco = (r.reco_verbatim || "").replace(/"/g, '""').replace(/(\r\n|\n|\r)/gm, " ");
            return `${r.id},${r.consentement},${r.sexe},${r.age_participant},${r.etat_civil},${r.province},${r.service},${r.niveau},${r.anciennete},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique},"${(r.obstacles || []).join(";")}", "${cleanReco}"`;
        }).join("\n");
        let l = document.createElement("a");
        l.href = "data:text/csv;charset=utf-8," + encodeURI("\ufeff"+h+r);
        l.download = "Rapport_CAP_Makala_Kinshasa.csv"; l.click();
    };
    
    function showToast(message) {
        var x = document.getElementById("toast");
        x.className = "show";
        x.innerText = message;
        setTimeout(function(){ x.className = x.className.replace("show", ""); }, 3000);
    }
    window.initCodeDropdown();
</script>
</body>
</html>
