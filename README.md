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
        .academic-table { width: 100%; border-collapse: collapse; margin-bottom: 25px; font-family: 'Times New Roman', serif; font-size: 14px; background: white;}
        .academic-table thead th { border-bottom: 2px solid #000; border-top: 2px solid #000; background: #fdfdfd; text-align: center; font-weight: bold; padding: 10px; }
        .academic-table tbody td { border-bottom: 1px solid #ddd; padding: 8px; text-align: center; }
        .academic-table tbody tr:last-child td { border-bottom: 2px solid #000; }
        .academic-table .row-header { text-align: left; padding-left: 15px; font-weight: normal; }
        .academic-table .group-header { background-color: #f0f8ff; font-weight: bold; text-align: left; padding-left: 10px; color: #0d47a1; }
        .table-caption { font-weight: bold; color: #333; margin-bottom: 8px; font-size: 15px; text-align: left; font-family: 'Segoe UI', sans-serif;}

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
        .pie-legend { font-size: 12px; display: flex; flex-direction: column; gap: 5px; }
        .legend-item { display: flex; align-items: center; gap: 8px; }
        .legend-color { width: 12px; height: 12px; border-radius: 2px; }

        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; width: 100%; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; width: 100%; }
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
        
        <button type="button" class="btn-excel admin-only" style="margin-bottom: 20px; width: 100%; background: #0288d1; font-size: 14px;" onclick="window.exportTab3Word()">📥 TÉLÉCHARGER TOUTES LES DONNÉES DE L'ONGLET 3 (WORD)</button>

        <div class="section-title">0. ANALYSE SOCIODÉMOGRAPHIQUE (CAMEMBERTS)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Répartition par Âge</div>
                <div id="pie-age" class="pie-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Répartition par Niveau d'Étude</div>
                <div id="pie-niveau" class="pie-box"></div>
            </div>
        </div>

        <div class="section-title">1. ÉVALUATION GÉNÉRALE DES C.A.P. (CAMEMBERTS)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Savoir (Théorique)</div>
                <div id="pie-savoir" class="pie-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique</div>
                <div id="pie-pratique" class="pie-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Type d'Attitude</div>
                <div id="pie-attitude" class="pie-box"></div>
            </div>
        </div>

        <div class="section-title">2. ANALYSES CROISÉES : CONNAISSANCES PAR CATÉGORIE</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Savoir vs Département (Service)</div>
                <div id="pie-cross-service" class="pie-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Savoir vs Niveau d'Étude</div>
                <div id="pie-cross-niveau" class="pie-box"></div>
            </div>
        </div>

        <div class="section-title">3. CROISEMENT DES PERFORMANCES (LE LIEN C.A.P.)</div>
        <div class="row">
             <div class="stat-card">
                <div class="stat-title">Pratique vs Niveau de Savoir</div>
                <div id="pie-cross-kp" class="pie-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Attitude vs Niveau de Savoir</div>
                <div id="pie-cross-ka" class="pie-box"></div>
            </div>
        </div>
        
        <div class="section-title">4. TABLEAUX RÉCAPITULATIFS & SYNTHÈSE</div>
        <div id="detailed-analysis-container">
            </div>

        <div class="section-title">5. SYNTHÈSE COMPARATIVE (C.A.P. GROUPE)</div>
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

        <div class="section-title">6. ANALYSES CROISÉES DÉTAILLÉES (TABLEAUX SUPPLÉMENTAIRES)</div>
        <div id="extra-tables-container">
            </div>
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
        const verbatims = [
            "Il faut multiplier les campagnes à la télévision.", "Les patientes arrivent toujours trop tard.",
            "Le manque de formation pratique est notre plus grand défi.", "Le coût de la mammographie est trop élevé.",
            "Besoin de formation continue.", "Rien à signaler."
        ];

        // Listes pour simuler des sélections multiples réalistes
        const allObstacles = ["Formation", "Coût", "Temps", "Intimité", "Culture", "Protocole"];
        const allRisks = ["age", "multi", "famille", "alcool", "obesite", "allaitement", "menopause"];
        const allSigns = ["nodule", "retraction", "peau", "ecoulement", "douleur"];

        let simulatedDB = [];

        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let niveau = (Math.random() < 0.70) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let anciennete = Math.floor(Math.random() * 21);
            let age = 22 + anciennete + Math.floor(Math.random() * 5); 

            let isGyneco = service === 'Gynécologie-Obstétrique';
            let isA1 = niveau === 'A1/LMD - ISTM';
            
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

            // Sélection aléatoire de multiples items pour les tableaux croisés
            let genObs = allObstacles.filter(() => Math.random() > 0.6);
            if(genObs.length === 0) genObs.push("Formation"); // Au moins 1
            
            let genRisks = allRisks.filter(() => Math.random() > 0.5);
            if(genRisks.length === 0) genRisks.push("age");

            let genSigns = allSigns.filter(() => Math.random() > 0.4);
            if(genSigns.length === 0) genSigns.push("nodule");

            simulatedDB.push({
                firestoreId: "sim-" + i,
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                consentement: "oui", service: service, niveau: niveau,
                anciennete: anciennete, sexe: "F",
                etat_civil: Math.random() > 0.4 ? "Mariée" : "Célibataire",
                province: "Kinshasa", cat_pro: "Infirmier(e)",
                age_participant: age,
                q_moleculaire: isGyneco ? "oui" : (Math.random() > 0.8 ? "oui" : "non"),
                q_her2: isGyneco ? "oui" : (Math.random() > 0.9 ? "oui" : "non"),
                connaissance_cnlc: Math.random() > 0.6 ? "oui" : "non",
                interet_registre: "Oui",
                scoreSavoir: scoreSavoir, scorePratique: scorePratique, scoreAttitude: scoreAttitude,
                obstacles: genObs, 
                risks: genRisks, 
                signs: genSigns,
                reco_verbatim: verbatims[Math.floor(Math.random() * verbatims.length)]
            });
        }
        return simulatedDB;
    };

    database = window.generateSimulatedData();
    
    setTimeout(() => {
        window.updateUI();
        showToast("178 Fiches chargées (Données Kinshasa)");
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
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            alert("Mode Admin Activé.");
            updateUI(); 
            window.switchTab(3); // On bascule vers l'onglet 3 pour voir les résultats
        } else { alert("Code incorrect !"); }
    };

    // --- FONCTION DE RENDU CAMEMBERT (SVG) ---
    window.renderPie = function(containerId, data) {
        const container = document.getElementById(containerId);
        if(!container) return;
        
        const total = data.reduce((sum, item) => sum + item.v, 0);
        let currentAngle = 0;
        let svgContent = `<svg width="150" height="150" viewBox="-1 -1 2 2" style="transform: rotate(-90deg); border-radius: 50%;">`;
        
        data.forEach(item => {
            if(total === 0) return;
            const percent = (item.v / total);
            const largeArcFlag = percent > 0.5 ? 1 : 0;
            const startX = Math.cos(2 * Math.PI * currentAngle);
            const startY = Math.sin(2 * Math.PI * currentAngle);
            currentAngle += percent;
            const endX = Math.cos(2 * Math.PI * currentAngle);
            const endY = Math.sin(2 * Math.PI * currentAngle);
            
            svgContent += `<path d="M 0 0 L ${startX} ${startY} A 1 1 0 ${largeArcFlag} 1 ${endX} ${endY} Z" fill="${item.c}"></path>`;
        });
        
        svgContent += `</svg>`;
        
        let legendHtml = `<div class="pie-legend">`;
        data.forEach(item => {
            let pVal = total > 0 ? ((item.v/total)*100).toFixed(1) : 0;
            legendHtml += `
                <div class="legend-item">
                    <div class="legend-color" style="background:${item.c}"></div>
                    <span>${item.l}: <b>${item.v} (${pVal}%)</b></span>
                </div>`;
        });
        legendHtml += `</div>`;
        
        container.innerHTML = svgContent + legendHtml;
    };

    window.updateAnalytics = function() {
        const total = database.length;
        if(total === 0) return;

        // 0. SOCIODEMO
        let sAge = [{l:'<30', v:0, c:'#f06292'}, {l:'30-45', v:0, c:'#ba68c8'}, {l:'>45', v:0, c:'#9575cd'}];
        let sNiveau = [{l:'A1/LMD', v:0, c:'#4db6ac'}, {l:'A2', v:0, c:'#81c784'}];
        
        database.forEach(d => {
            if(d.age_participant < 30) sAge[0].v++; else if(d.age_participant <= 45) sAge[1].v++; else sAge[2].v++;
            if(d.niveau.includes('A1')) sNiveau[0].v++; else sNiveau[1].v++;
        });
        window.renderPie('pie-age', sAge);
        window.renderPie('pie-niveau', sNiveau);

        // 1. EVALUATION GENERALE
        let sK = [{l:'Bon (≥70%)', v:0, c:'#2e7d32'}, {l:'Moyen (50-69%)', v:0, c:'#f57f17'}, {l:'Faible (<50%)', v:0, c:'#c62828'}];
        let sP = [{l:'Adéquate (≥70%)', v:0, c:'#1565c0'}, {l:'Insuffisante', v:0, c:'#ef5350'}];
        let sA = [{l:'Positive (>3.5)', v:0, c:'#66bb6a'}, {l:'Neutre/Nég.', v:0, c:'#bdbdbd'}];

        database.forEach(d => {
            if(d.scoreSavoir >= 70) sK[0].v++; else if(d.scoreSavoir >= 50) sK[1].v++; else sK[2].v++;
            if(d.scorePratique >= 70) sP[0].v++; else sP[1].v++;
            if(parseFloat(d.scoreAttitude) > 3.5) sA[0].v++; else sA[1].v++;
        });
        window.renderPie('pie-savoir', sK);
        window.renderPie('pie-pratique', sP);
        window.renderPie('pie-attitude', sA);

        // 2. ANALYSES CROISÉES
        let servicesList = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let colors = ['#e91e63', '#9c27b0', '#673ab7', '#3f51b5'];
        let crossService = servicesList.map((s, idx) => ({
            l: s,
            v: database.filter(d => d.service === s && d.scoreSavoir >= 70).length,
            c: colors[idx]
        }));
        window.renderPie('pie-cross-service', crossService);

        let crossNiv = [
            {l: 'A1 - Bon Savoir', v: database.filter(d => d.niveau.includes('A1') && d.scoreSavoir >= 70).length, c: '#00acc1'},
            {l: 'A2 - Bon Savoir', v: database.filter(d => d.niveau.includes('A2') && d.scoreSavoir >= 70).length, c: '#ffa000'}
        ];
        window.renderPie('pie-cross-niveau', crossNiv);

        // 3. LIEN C.A.P.
        let crossKP = [
            {l: 'Savoir Haut -> Prat. Bon', v: database.filter(d => d.scoreSavoir >= 70 && d.scorePratique >= 70).length, c: '#43a047'},
            {l: 'Savoir Bas -> Prat. Bon', v: database.filter(d => d.scoreSavoir < 70 && d.scorePratique >= 70).length, c: '#fb8c00'}
        ];
        window.renderPie('pie-cross-kp', crossKP);

        let crossKA = [
            {l: 'Savoir Haut -> Att. Pos', v: database.filter(d => d.scoreSavoir >= 70 && parseFloat(d.scoreAttitude) > 3.5).length, c: '#1e88e5'},
            {l: 'Savoir Bas -> Att. Pos', v: database.filter(d => d.scoreSavoir < 70 && parseFloat(d.scoreAttitude) > 3.5).length, c: '#e53935'}
        ];
        window.renderPie('pie-cross-ka', crossKA);

        // Mise à jour des Tableaux
        window.updateExtraTables();
    };

    window.updateExtraTables = function() {
        const total = database.length;
        if(total === 0) return;

        // --- GÉNÉRATION DU TABLEAU 5 (Synthèse Comparative) ---
        const crossBody = document.getElementById('cross-body');
        const services = ["Gynécologie-Obstétrique", "Médecine Interne", "Chirurgie", "Urgences / Autre"];
        
        crossBody.innerHTML = services.map(s => {
            let subset = database.filter(d => d.service === s);
            let n = subset.length;
            let avgS = window.getAvg(subset, 'scoreSavoir');
            let avgA = window.getAvg(subset, 'scoreAttitude');
            let avgP = window.getAvg(subset, 'scorePratique');
            let colorP = avgP >= 70 ? '#2e7d32' : (avgP >= 50 ? '#f57f17' : '#c62828');
            return `
                <tr>
                    <td style="text-align:left; padding:15px; border-right: 1px solid #eee;"><b>${s}</b></td>
                    <td style="padding:15px; border-right: 1px solid #eee;">${n}</td>
                    <td style="padding:15px; border-right: 1px solid #eee;">${avgS}%</td>
                    <td style="padding:15px; border-right: 1px solid #eee;">${avgA}</td>
                    <td style="padding:15px; color:${colorP}; font-weight:bold;">${avgP}%</td>
                    <td>${avgP >= 70 ? '🟢 Expert' : '🟠 À renforcer'}</td>
                </tr>`;
        }).join('');

        // --- GÉNÉRATION DES TABLEAUX DÉTAILLÉS (Section 4) ---
        const detailedContainer = document.getElementById('detailed-analysis-container');
        
        // 1. Calculs Socio-Démo
        let a1_count = database.filter(d => d.niveau.includes('A1')).length;
        let a2_count = total - a1_count;
        let mariee_count = database.filter(d => d.etat_civil === 'Mariée').length;
        let celib_count = database.filter(d => d.etat_civil === 'Célibataire').length;
        let autres_civ = total - mariee_count - celib_count;

        let table4HTML = `
            <div class="table-caption">Tableau I : Caractéristiques sociodémographiques des enquêtées (N=${total})</div>
            <table class="academic-table">
                <thead>
                    <tr><th style="width:50%;">Variables</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr>
                </thead>
                <tbody>
                    <tr><td colspan="3" class="group-header">Niveau d'étude</td></tr>
                    <tr><td class="row-header">A1/LMD (Niveau Supérieur)</td><td>${a1_count}</td><td>${((a1_count/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">A2 (Niveau Technique)</td><td>${a2_count}</td><td>${((a2_count/total)*100).toFixed(1)}</td></tr>
                    
                    <tr><td colspan="3" class="group-header">État Civil</td></tr>
                    <tr><td class="row-header">Mariée</td><td>${mariee_count}</td><td>${((mariee_count/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Célibataire</td><td>${celib_count}</td><td>${((celib_count/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Autre (Veuve/Divorcée)</td><td>${autres_civ}</td><td>${((autres_civ/total)*100).toFixed(1)}</td></tr>
                </tbody>
            </table>
        `;
        detailedContainer.innerHTML = table4HTML;


        // --- GÉNÉRATION DES TABLEAUX SUPPLÉMENTAIRES (Section 6) ---
        const extraContainer = document.getElementById('extra-tables-container');
        
        // Helper pour compter les éléments dans des tableaux imbriqués (ex: obstacles)
        const countOccurrences = (key) => {
            let counts = {};
            database.forEach(d => {
                if(d[key] && Array.isArray(d[key])) {
                    d[key].forEach(val => {
                        counts[val] = (counts[val] || 0) + 1;
                    });
                }
            });
            return counts;
        };

        const obsCounts = countOccurrences('obstacles');
        const riskCounts = countOccurrences('risks');
        const signCounts = countOccurrences('signs');

        // Générer les lignes HTML pour les objets comptés
        const generateRows = (dict) => {
            return Object.entries(dict).sort((a,b) => b[1] - a[1]).map(([label, count]) => {
                let perc = ((count / total) * 100).toFixed(1);
                // Rendre les labels plus lisibles
                let displayLabel = label.charAt(0).toUpperCase() + label.slice(1);
                if(label==='age') displayLabel = 'Âge avancé (>50 ans)';
                if(label==='multi') displayLabel = 'Multiparité';
                if(label==='famille') displayLabel = 'Antécédents familiaux';
                
                return `<tr><td class="row-header">${displayLabel}</td><td>${count}</td><td>${perc}</td></tr>`;
            }).join('');
        };

        let table6_1 = `
            <div class="table-caption">Tableau II : Connaissance des facteurs de risque identifiés</div>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Facteurs de risque cités</th><th>Fréquence (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>${generateRows(riskCounts)}</tbody>
            </table>
        `;

        let table6_2 = `
            <div class="table-caption">Tableau III : Connaissance des signes d'alerte cliniques</div>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Signes d'alerte identifiés</th><th>Fréquence (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>${generateRows(signCounts)}</tbody>
            </table>
        `;

        let table6_3 = `
            <div class="table-caption">Tableau IV : Principaux obstacles rapportés liés à la pratique de dépistage</div>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Obstacles</th><th>Fréquence (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>${generateRows(obsCounts)}</tbody>
            </table>
        `;

        extraContainer.innerHTML = table6_1 + table6_2 + table6_3;
    };

    // Fonctions utilitaires
    window.getAvg = function(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; };
    
    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td><td>${row.anciennete}</td>
                <td style="color:${row.scoreSavoir>=70?'green':'red'}">${row.scoreSavoir}%</td>
                <td style="color:${row.scorePratique>=70?'green':'red'}">${row.scorePratique}%</td>
                <td>${row.scorePratique >= 70 ? '🟢 Expert' : '🔴 Critique'}</td>
                <td><button class="btn-view-single" onclick="window.viewDetails(${index})">👁️ Voir</button></td>
            </tr>
        `).join('');
        if(isAdmin) window.updateAnalytics();
    };

    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    function showToast(m) { var x = document.getElementById("toast"); x.className="show"; x.innerText=m; setTimeout(()=>x.className=x.className.replace("show",""),3000); }
    window.initCodeDropdown();
</script>
</body>
</html>
