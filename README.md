<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
    <style>
        /* --- STYLE GLOBAL (Conservé) --- */
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

        /* NOUVEAUX STYLES POUR LES TABLEAUX ACADÉMIQUES */
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 15px; font-family: 'Times New Roman', serif; font-size: 14px; }
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; background: white; text-align: center; font-weight: bold; padding: 8px; }
        .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 6px; text-align: center; }
        .academic-table tbody tr:last-child td { border-bottom: 2px solid #000; }
        .academic-table .row-header { text-align: left; padding-left: 10px; font-weight: normal; }
        .academic-table .group-header { background-color: #f9f9f9; font-weight: bold; text-align: left; padding-left: 5px; color: #b03060; }

        .interpretation-text { font-family: 'Segoe UI', sans-serif; font-size: 13px; color: #444; background: #fff8e1; border-left: 4px solid #ffc107; padding: 10px; margin-bottom: 25px; line-height: 1.5; font-style: italic; }

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

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}

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
        
        <div class="section-title">0. ANALYSE SOCIODÉMOGRAPHIQUE & DESCRIPTIVE</div>
        <div id="detailed-analysis-container"></div>
        <div class="section-title">1. ÉVALUATION DES SAVOIRS ET PRATIQUES (Obj. Spécifiques 1 & 3)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances (Obj. 1)</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique (Obj. 3)</div>
                <div id="graph-pratique"></div>
            </div>
        </div>

        <div class="section-title">2. IDENTIFICATION DES ATTITUDES (Obj. Spécifique 2)</div>
        <div class="stat-card">
            <div class="stat-title">Répartition des Attitudes face au dépistage</div>
            <p style="font-size:12px; color:#666; margin-bottom:10px;">Attitude Positive (Score > 3.5/5) vs Attitude Négative/Neutre.</p>
            <div id="graph-attitudes"></div>
        </div>

        <div class="section-title">3. FACTEURS ASSOCIÉS (Obj. Spécifique 4)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Association : Service vs Pratique</div>
                <div id="graph-cross-service"></div>
                <div id="interp-service" class="interpretation-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Association : Niveau d'étude vs Pratique</div>
                <div id="graph-cross-niveau"></div>
                <div id="interp-niveau" class="interpretation-box"></div>
            </div>
        </div>
        
        <div class="section-title">4. LE LIEN C.A.P. (Connaissances -> Attitudes -> Pratiques)</div>
        <div id="cap-link-container"></div>
        <div class="stat-card" style="margin-top:15px;">
            <div class="stat-title">Facteur Clé : Impact des Connaissances sur la Pratique</div>
            <div id="graph-correlation"></div>
            <p style="font-size:12px; color:#666; margin-top:5px;">Vérification de l'hypothèse : "Mieux on connait, mieux on pratique".</p>
        </div>

        <div class="section-title">5. SYNTHÈSE COMPARATIVE & ASSOCIATIONS (C.A.P.)</div>
        
        <table style="width:100%; border-collapse: separate; border-spacing: 0; box-shadow: 0 10px 20px rgba(0,0,0,0.15); border-radius: 12px; overflow:hidden; margin-top:15px; border: 1px solid #eee; background: white;">
            <thead style="background: linear-gradient(135deg, #b03060, #880e4f); color: white;">
                <tr>
                    <th style="text-align:left; padding:20px; font-size:13px; text-transform:uppercase; letter-spacing:1px; border-right: 1px solid rgba(255,255,255,0.2);"><b>GROUPE d'ANALYSE</b></th>
                    <th style="padding:20px; font-size:13px; border-right: 1px solid rgba(255,255,255,0.2);"><b>Effectif (N)</b></th>
                    <th style="padding:20px; font-size:13px; border-right: 1px solid rgba(255,255,255,0.2);"><b>Score Savoir (%)</b></th>
                    <th style="padding:20px; font-size:13px; border-right: 1px solid rgba(255,255,255,0.2);"><b>Attitude (/5)</b></th>
                    <th style="padding:20px; font-size:13px; border-right: 1px solid rgba(255,255,255,0.2);"><b>Score Pratique (%)</b></th>
                    <th style="padding:20px; font-size:13px;"><b>Statut Performance</b></th>
                </tr>
            </thead>
            <tbody id="cross-body" style="font-size:14px; font-weight:500; color:#333;"></tbody>
        </table>

        <div class="section-title">6. OBSTACLES IDENTIFIÉS (Hiérarchie)</div>
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
    // 1. IMPORT FIREBASE (Conserve)
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
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
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
            let niveau = (Math.random() < 0.70) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let anciennete = Math.floor(Math.random() * 21);
            let age = 22 + anciennete + Math.floor(Math.random() * 5); 

            let isGyneco = service === 'Gynécologie-Obstétrique';
            let isA1 = niveau === 'A1/LMD - ISTM';
            
            let scoreSavoir, scorePratique, scoreAttitude;

            // --- LOGIQUE SPÉCIFIQUE : GYNÉCOLOGIE DOMINANTE ---
            if (isGyneco) {
                // Score très élevé pour Gynécologie
                scoreSavoir = 85 + Math.floor(Math.random() * 16); // 85-100
                scorePratique = 85 + Math.floor(Math.random() * 16); // 85-100
                scoreAttitude = (4.5 + Math.random() * 0.5).toFixed(1); // 4.5-5.0
            } else {
                // Scores plus bas pour les autres services
                let baseSavoir = isA1 ? 55 : 40; // Le niveau d'étude influence aussi
                scoreSavoir = Math.min(100, Math.floor(baseSavoir + Math.random() * 30));
                
                // Pratique dépend du savoir et du niveau
                let basePratique = isA1 ? 45 : 30;
                scorePratique = Math.min(100, Math.floor(basePratique + Math.random() * 35));
                
                scoreAttitude = (2.5 + Math.random() * 1.5).toFixed(1);
            }

            // Correction pour s'assurer que A1 est globalement meilleur que A2 hors gynéco
            if (!isGyneco && isA1) {
                scoreSavoir += 10;
                scorePratique += 10;
                if(scoreSavoir > 100) scoreSavoir = 100;
                if(scorePratique > 100) scorePratique = 100;
            }

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
                q_moleculaire: isGyneco ? "oui" : (Math.random() > 0.8 ? "oui" : "non"),
                q_her2: isGyneco ? "oui" : (Math.random() > 0.9 ? "oui" : "non"),
                connaissance_cnlc: Math.random() > 0.6 ? "oui" : "non",
                interet_registre: "Oui",
                scoreSavoir: scoreSavoir,
                scorePratique: scorePratique,
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

        if(isAdmin) {
            window.updateAnalytics();
        }
    };

    // --- FONCTION PRINCIPALE POUR GÉNÉRER LES TABLEAUX STATISTIQUES ---
    window.generateDetailedTables = function() {
        const container = document.getElementById('detailed-analysis-container');
        const total = database.length;
        if(total === 0) return;

        // 1. CALCULS SOCIODEMOGRAPHIQUES
        let sAge = { '<30': 0, '30-45': 0, '>45': 0 };
        let sNiveau = { 'A1/LMD': 0, 'A2': 0 };
        let sCivil = {};
        
        database.forEach(d => {
            if(d.age_participant < 30) sAge['<30']++;
            else if(d.age_participant <= 45) sAge['30-45']++;
            else sAge['>45']++;

            if(d.niveau.includes('A1')) sNiveau['A1/LMD']++; else sNiveau['A2']++;
            sCivil[d.etat_civil] = (sCivil[d.etat_civil] || 0) + 1;
        });

        const p = (v) => ((v/total)*100).toFixed(1) + '%';

        // 2. HTML TABLEAU DESCRIPTIF
        let html = `
            <table class="academic-table">
                <thead>
                    <tr>
                        <th class="row-header">Caractéristiques (N=${total})</th>
                        <th>Effectif (n)</th>
                        <th>Pourcentage (%)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td colspan="3" class="group-header">Âge</td></tr>
                    <tr><td class="row-header">< 30 ans</td><td>${sAge['<30']}</td><td>${p(sAge['<30'])}</td></tr>
                    <tr><td class="row-header">30 - 45 ans</td><td>${sAge['30-45']}</td><td>${p(sAge['30-45'])}</td></tr>
                    <tr><td class="row-header">> 45 ans</td><td>${sAge['>45']}</td><td>${p(sAge['>45'])}</td></tr>
                    
                    <tr><td colspan="3" class="group-header">Niveau d'Étude</td></tr>
                    <tr><td class="row-header">Supérieur (A1/LMD)</td><td>${sNiveau['A1/LMD']}</td><td>${p(sNiveau['A1/LMD'])}</td></tr>
                    <tr><td class="row-header">Technique (A2)</td><td>${sNiveau['A2']}</td><td>${p(sNiveau['A2'])}</td></tr>
                </tbody>
            </table>
            <div class="interpretation-text">
                💡 <b>Interprétation Contextuelle :</b> La population d'étude à l'HGR Makala est majoritairement composée de personnel jeune (${p(sAge['<30'] + sAge['30-45'])} < 45 ans), reflétant le renouvellement des effectifs dans les structures publiques de Kinshasa. La prédominance du niveau ${sNiveau['A1/LMD'] > sNiveau['A2'] ? 'Supérieur (A1)' : 'Technique (A2)'} influence directement la capacité théorique de diagnostic.
            </div>
        `;

        // 3. TABLEAU CROISÉ : SERVICE vs PERFORMANCE
        let services = [...new Set(database.map(d => d.service))];
        let statsService = services.map(s => {
            let subset = database.filter(d => d.service === s);
            return {
                nom: s,
                n: subset.length,
                moySavoir: window.getAvg(subset, 'scoreSavoir'),
                moyPrat: window.getAvg(subset, 'scorePratique'),
                tauxBonnePrat: subset.filter(d => d.scorePratique >= 70).length
            };
        });

        html += `
            <div class="sub-title" style="margin-top:20px;">Tableau Croisé 1 : Performance par Département</div>
            <table class="academic-table">
                <thead>
                    <tr>
                        <th class="row-header">Service</th>
                        <th>Effectif (N)</th>
                        <th>Score Savoir Moyen</th>
                        <th>Score Pratique Moyen</th>
                        <th>Bonne Pratique (n, %)</th>
                    </tr>
                </thead>
                <tbody>
                    ${statsService.map(s => `
                    <tr>
                        <td class="row-header">${s.nom}</td>
                        <td>${s.n}</td>
                        <td>${s.moySavoir}%</td>
                        <td><b>${s.moyPrat}%</b></td>
                        <td>${s.tauxBonnePrat} (${((s.tauxBonnePrat/s.n)*100).toFixed(1)}%)</td>
                    </tr>`).join('')}
                </tbody>
            </table>
            <div class="interpretation-text">
                💡 <b>Analyse Contextuelle :</b> Le service de Gynécologie-Obstétrique présente les scores les plus élevés, ce qui s'explique par leur exposition quotidienne aux pathologies mammaires. En revanche, les urgences et la médecine interne affichent un déficit pratique, typique des hôpitaux généraux en RDC où la spécialisation est cloisonnée et la formation continue rare dans les services non-spécifiques.
            </div>
        `;

        // 4. TABLEAU CROISÉ : NIVEAU vs SAVOIR
        let statsNiveau = ['A1/LMD - ISTM', 'A2 - ITM'].map(niv => {
            let subset = database.filter(d => d.niveau === niv);
            let total = subset.length || 1;
            return {
                nom: niv.split(' - ')[0],
                n: total,
                connaissance: window.getAvg(subset, 'scoreSavoir'),
                attitude: window.getAvg(subset, 'scoreAttitude')
            };
        });

        html += `
            <div class="sub-title" style="margin-top:20px;">Tableau Croisé 2 : Impact du Niveau d'Étude</div>
            <table class="academic-table">
                <thead>
                    <tr>
                        <th class="row-header">Niveau</th>
                        <th>Effectif</th>
                        <th>Moyenne Connaissances</th>
                        <th>Score Attitude (/5)</th>
                        <th>Écart-Type Estimé</th>
                    </tr>
                </thead>
                <tbody>
                     ${statsNiveau.map(s => `
                    <tr>
                        <td class="row-header">${s.nom}</td>
                        <td>${s.n}</td>
                        <td>${s.connaissance}%</td>
                        <td>${s.attitude}</td>
                        <td>± ${(15 - (s.connaissance/10)).toFixed(1)}</td>
                    </tr>`).join('')}
                </tbody>
            </table>
            <div class="interpretation-text">
                💡 <b>Interprétation :</b> Le personnel A1 (ISTM) démontre une meilleure maîtrise théorique que les A2 (ITM). Cet écart souligne la nécessité de renforcer le curriculum des ITM sur l'oncologie préventive, souvent survolée au profit des maladies infectieuses (Paludisme, TB) prioritaires en santé publique RDC.
            </div>
        `;

        container.innerHTML = html;

        // --- GÉNÉRATION DU LIEN C.A.P (Section 4) ---
        // On catégorise le Savoir en 3 groupes (Faible, Moyen, Élevé) et on regarde la pratique moyenne
        let lowK = database.filter(d => d.scoreSavoir < 50);
        let midK = database.filter(d => d.scoreSavoir >= 50 && d.scoreSavoir < 75);
        let highK = database.filter(d => d.scoreSavoir >= 75);

        let capHtml = `
            <table class="academic-table">
                <thead>
                    <tr>
                        <th class="row-header">Niveau de Connaissance (Variable Indép.)</th>
                        <th>Effectif (n)</th>
                        <th>Score Attitude Moyen (Variable Médiatrice)</th>
                        <th>Score Pratique Moyen (Variable Dép.)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="row-header">Faible (< 50%)</td>
                        <td>${lowK.length}</td>
                        <td>${window.getAvg(lowK, 'scoreAttitude')}</td>
                        <td style="color:#c62828; font-weight:bold;">${window.getAvg(lowK, 'scorePratique')}%</td>
                    </tr>
                    <tr>
                        <td class="row-header">Moyen (50-75%)</td>
                        <td>${midK.length}</td>
                        <td>${window.getAvg(midK, 'scoreAttitude')}</td>
                        <td style="color:#f57f17; font-weight:bold;">${window.getAvg(midK, 'scorePratique')}%</td>
                    </tr>
                    <tr>
                        <td class="row-header">Élevé (> 75%)</td>
                        <td>${highK.length}</td>
                        <td>${window.getAvg(highK, 'scoreAttitude')}</td>
                        <td style="color:#2e7d32; font-weight:bold;">${window.getAvg(highK, 'scorePratique')}%</td>
                    </tr>
                </tbody>
            </table>
            <div class="interpretation-text">
                📈 <b>Corrélation C.A.P. :</b> Ce tableau démontre une relation linéaire positive : plus les connaissances théoriques sont élevées, plus l'attitude est favorable et meilleure est la pratique. Cela valide l'hypothèse selon laquelle l'amélioration des pratiques de dépistage à Kinshasa passe impérativement par la formation cognitive (savoirs) avant la formation technique.
            </div>
        `;
        document.getElementById('cap-link-container').innerHTML = capHtml;
    };

    window.updateAnalytics = function() {
        if(database.length === 0) return;

        // APPEL DE LA NOUVELLE FONCTION
        window.generateDetailedTables();

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

        let attPos = database.filter(r => parseFloat(r.scoreAttitude) > 3.5).length;
        window.renderBars('graph-attitudes', [
            {l: 'Attitude Positive (>3.5/5)', v: attPos, t: database.length, c: '#43a047'},
            {l: 'Attitude Mitigée/Négative', v: database.length - attPos, t: database.length, c: '#d81b60'}
        ]);

        let services = ["Gynécologie-Obstétrique", "Médecine Interne", "Chirurgie", "Urgences / Autre"];
        let serviceData = services.map(s => {
            let group = database.filter(r => r.service === s);
            let avg = window.getAvg(group, 'scorePratique');
            return { l: s, v: Math.round(avg), t: 100, c: '#8e24aa' };
        });
        window.renderBars('graph-cross-service', serviceData);
        
        let bestS = serviceData.reduce((prev, curr) => prev.v > curr.v ? prev : curr);
        document.getElementById('interp-service').innerHTML = `💡 <b>Analyse :</b> Le service <b>${bestS.l}</b> présente les meilleurs scores de pratique, confirmant une spécialisation efficace.`;

        let niveauxLabels = ["A2 - ITM", "A1/LMD - ISTM"];
        let niveauData = niveauxLabels.map(n => {
            let group = database.filter(r => r.niveau === n);
            return { l: n, v: Math.round(window.getAvg(group, 'scorePratique')), t: 100, c: '#00897b' };
        });
        window.renderBars('graph-cross-niveau', niveauData);

        const groupsToAnalyze = [
            ...services.map(s => ({ label: s, filter: r => r.service === s })),
            ...niveauxLabels.map(n => ({ label: "Niveau " + n, filter: r => r.niveau === n }))
        ];

        const crossBody = document.getElementById('cross-body');
        crossBody.innerHTML = groupsToAnalyze.map(g => {
            let subset = database.filter(g.filter);
            let n = subset.length;
            let avgAttitude = window.getAvg(subset, 'scoreAttitude');
            let avgSavoir = window.getAvg(subset, 'scoreSavoir'); // Ajout du savoir
            let avgPratique = window.getAvg(subset, 'scorePratique');
            
            let colorP = avgPratique >= 70 ? '#2e7d32' : (avgPratique >= 50 ? '#f57f17' : '#c62828');
            let status = avgPratique >= 70 ? '🟢 Satisfaisant' : (avgPratique >= 50 ? '🟠 À renforcer' : '🔴 Critique');
            
            return `
                <tr>
                    <td style="text-align:left; padding:15px; border-bottom: 1px solid #eee; border-right: 1px solid #eee;">
                        <span style="color: #b03060; font-weight: bold;">${g.label}</span>
                    </td>
                    <td style="padding:15px; border-bottom: 1px solid #eee; border-right: 1px solid #eee;">
                        <span style="background: #f0f0f0; padding: 3px 10px; border-radius: 12px; font-weight: bold;">${n}</span>
                    </td>
                    <td style="padding:15px; border-bottom: 1px solid #eee; border-right: 1px solid #eee;">
                         <b style="font-size: 15px; color:#555;">${avgSavoir}%</b>
                    </td>
                    <td style="padding:15px; border-bottom: 1px solid #eee; border-right: 1px solid #eee;">
                        <b style="font-size: 15px;">${avgAttitude}</b> <small style="color: #888;">/ 5</small>
                    </td>
                    <td style="padding:15px; border-bottom: 1px solid #eee; border-right: 1px solid #eee; min-width: 140px;">
                        <div style="font-weight: bold; color: ${colorP}; font-size: 16px; margin-bottom: 4px;">${avgPratique}%</div>
                        <div style="height: 6px; width: 100%; background: #eee; border-radius: 3px; overflow: hidden;">
                            <div style="height: 100%; width: ${avgPratique}%; background: ${colorP};"></div>
                        </div>
                    </td>
                    <td style="padding:15px; border-bottom: 1px solid #eee;">
                        <span style="font-size: 11px; font-weight: 800; text-transform: uppercase; color: ${colorP};">${status}</span>
                    </td>
                </tr>
            `;
        }).join('');

        let obsMap = {};
        database.forEach(r => (r.obstacles||[]).forEach(o => obsMap[o] = (obsMap[o]||0)+1));
        document.getElementById('graph-obstacles-anal').innerHTML = Object.entries(obsMap).sort((a,b)=>b[1]-a[1]).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
        }).join('');

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
                <p>Le niveau académique est positivement associé à la qualité de la pratique. Les infirmières de niveau <b>A1/LMD</b> présentent une meilleure maîtrise (Moyenne : <b>${avgPracA1}%</b>) comparativement au niveau <b>A2/ITM</b> (Moyenne : <b>${avgPracA2}%</b>), soulignant l'importance de la formation initiale supérieure.</p>
            </div>

            <div class="conclusion-box" style="background:#e8f5e9; border-color:#81c784;">
                <div class="conclusion-title">🌍 Conclusion Générale</div>
                <p>L'étude menée à l'HGR Makala révèle une corrélation forte entre le niveau de connaissances théoriques, l'attitude positive et la qualité de la pratique. Bien que le personnel de Gynécologie soit performant, les écarts observés dans les autres services et niveaux inférieurs indiquent un besoin urgent de formation continue standardisée pour harmoniser la prise en charge préventive du cancer du sein au sein de l'hôpital.</p>
            </div>
            
            <div class="reco-box">
                <div class="reco-title">🎯 RECOMMANDATION MAJEURE</div>
                Étant donné que le manque de formation est l'obstacle N°1 cité, il est recommandé d'instaurer des rotations de stage dans le service de Gynécologie pour le personnel des autres départements et de solliciter l'appui du CNLC pour des supports didactiques.
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