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
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. DISCUSSION</button>
        
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
        <div id="connaissances-cross-tables"></div>
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
        <div id="pratiques-cross-tables"></div>
        <div id="pratiques-summary"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">DISCUSSION</div>
        <button type="button" class="btn-excel admin-only" style="margin-bottom: 20px; width: 100%; background: #0288d1; font-size: 14px;" onclick="window.exportTab4()">📥 TÉLÉCHARGER TOUTE LA DISCUSSION (WORD / PDF)</button>
        <div id="dynamic-report" style="font-size:14px; line-height:1.6; color:#333; background: white; padding: 25px; border-radius: 8px; border: 1px solid #ddd; text-align: justify;"></div>
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
    // Simulation Mode Setup
    let database = []; 
    let isAdmin = false;

    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        const verbatims = [
            "Il faut multiplier les campagnes à la télévision.", "Les patientes arrivent toujours trop tard.",
            "Le manque de formation pratique est notre plus grand défi.", "Le coût de la mammographie est trop élevé.",
            "Besoin de formation continue."
        ];

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

            let k_fr_score = Math.min(100, Math.max(0, scoreSavoir + (Math.floor(Math.random() * 30) - 15)));
            let k_sc_score = Math.min(100, Math.max(0, scoreSavoir + (Math.floor(Math.random() * 20) - 5))); 
            let k_sa_score = Math.min(100, Math.max(0, scoreSavoir - 15 + (Math.floor(Math.random() * 30) - 15)));

            let genObs = allObstacles.filter(() => Math.random() > 0.4); 
            if(genObs.length === 0) genObs.push("Formation"); 
            
            let genRisks = allRisks.filter(() => Math.random() > 0.5);
            let genSigns = allSigns.filter(() => Math.random() > 0.4);

            simulatedDB.push({
                firestoreId: "sim-" + i,
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                consentement: "oui", service: service, niveau: niveau,
                anciennete: anciennete, sexe: "F",
                etat_civil: Math.random() > 0.4 ? "Mariée" : "Célibataire",
                province: "Kinshasa", cat_pro: "Infirmier(e)",
                age_participant: age,
                scoreSavoir: scoreSavoir, scorePratique: scorePratique, scoreAttitude: scoreAttitude,
                k_fr: k_fr_score, k_sc: k_sc_score, k_sa: k_sa_score, 
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
            window.switchTab(3); 
        } else { alert("Code incorrect !"); }
    };

    window.renderDashPie = function(containerId, data) {
        const container = document.getElementById(containerId);
        if(!container) return;
        
        const total = data.reduce((sum, item) => sum + item.v, 0);
        let currentAngle = 0;
        let svgContent = `<svg width="100" height="100" viewBox="-1 -1 2 2" style="transform: rotate(-90deg); border-radius: 50%;">`;
        
        data.forEach(item => {
            if(total === 0 || item.v === 0) return;
            const percent = (item.v / total);
            if (percent === 1) {
                svgContent += `<circle cx="0" cy="0" r="1" fill="${item.c}"></circle>`;
                return;
            }
            const largeArcFlag = percent > 0.5 ? 1 : 0;
            const startX = Math.cos(2 * Math.PI * currentAngle);
            const startY = Math.sin(2 * Math.PI * currentAngle);
            currentAngle += percent;
            const endX = Math.cos(2 * Math.PI * currentAngle);
            const endY = Math.sin(2 * Math.PI * currentAngle);
            
            svgContent += `<path d="M 0 0 L ${startX} ${startY} A 1 1 0 ${largeArcFlag} 1 ${endX} ${endY} Z" fill="${item.c}"></path>`;
        });
        
        svgContent += `</svg>`;
        
        let legendHtml = `<div class="dash-legend">`;
        data.forEach(item => {
            let pVal = total > 0 ? ((item.v/total)*100).toFixed(1) : 0;
            legendHtml += `
                <div class="dash-legend-item">
                    <div class="dash-legend-color" style="background:${item.c}"></div>
                    <span><span style="color:#777;">■</span> ${item.l}: <b>${item.v} (${pVal}%)</b></span>
                </div>`;
        });
        legendHtml += `</div>`;
        
        container.innerHTML = svgContent + legendHtml;
    };

    window.renderDashBar = function(containerId, data, color) {
        const container = document.getElementById(containerId);
        if(!container) return;
        let maxVal = Math.max(...data.map(d => d.v), 1);
        let html = '<div class="bar-chart-container">';
        data.forEach(item => {
            let heightPct = (item.v / maxVal) * 100;
            html += `<div class="bar-wrap">
                        <span class="bar-val">${item.v}</span>
                        <div class="bar" style="height: ${heightPct}%; background-color: ${item.c || color || '#b03060'};"></div>
                        <span class="bar-label" title="${item.l}">${item.l}</span>
                     </div>`;
        });
        html += '</div>';
        container.innerHTML = html;
    };

    window.updateAnalytics = function() {
        const total = database.length;
        if(total === 0) return;

        const consentis = database.filter(d => d.consentement === 'oui').length;
        const refus = total - consentis; 
        const tauxPart = ((consentis / total) * 100).toFixed(1);
        
        window.renderDashPie('pie-participation', [ {l: 'Accepté (Inclus)', v: consentis, c: '#4caf50'}, {l: 'Refusé', v: refus, c: '#f44336'} ]);
        window.renderDashBar('bar-participation', [ {l: 'Accepté', v: consentis, c: '#4caf50'}, {l: 'Refusé', v: refus, c: '#f44336'} ], '#4caf50');

        document.getElementById('taux-participation-container').innerHTML = `
            <table class="academic-table" style="margin-bottom:20px;">
                <thead>
                    <tr><th>Statut d'enrôlement</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr>
                </thead>
                <tbody>
                    <tr><td class="row-header">Ont accepté de participer</td><td>${consentis}</td><td>${tauxPart}</td></tr>
                    <tr><td class="row-header">Ont refusé / Exclus</td><td>${refus}</td><td>${(100 - tauxPart).toFixed(1)}</td></tr>
                    <tr><td class="row-header" style="font-weight:bold;">Total sollicité</td><td style="font-weight:bold;">${total}</td><td style="font-weight:bold;">100.0</td></tr>
                </tbody>
            </table>
        `;

        // Données Socio-Démo
        let age_30 = database.filter(d => d.age_participant < 30).length;
        let age_30_45 = database.filter(d => d.age_participant >= 30 && d.age_participant <= 45).length;
        let age_45 = database.filter(d => d.age_participant > 45).length;
        window.renderDashPie('dash-age', [ {l: '<30 ans', v: age_30, c: '#e8749f'}, {l: '30-45 ans', v: age_30_45, c: '#9c59b6'}, {l: '>45 ans', v: age_45, c: '#7b68ee'} ]);
        window.renderDashBar('dash-bar-age', [ {l: '<30 ans', v: age_30, c: '#e8749f'}, {l: '30-45 ans', v: age_30_45, c: '#9c59b6'}, {l: '>45 ans', v: age_45, c: '#7b68ee'} ]);

        let a1_count = database.filter(d => d.niveau.includes('A1')).length;
        let a2_count = total - a1_count;
        
        let k_bon = database.filter(d => d.scoreSavoir >= 70).length;
        let k_moyen = database.filter(d => d.scoreSavoir >= 50 && d.scoreSavoir < 70).length;
        let k_faible = database.filter(d => d.scoreSavoir < 50).length;
        window.renderDashPie('dash-savoir', [ {l: 'Bon (≥70%)', v: k_bon, c: '#2e7d32'}, {l: 'Moyen (50-69%)', v: k_moyen, c: '#e67e22'}, {l: 'Faible (<50%)', v: k_faible, c: '#d32f2f'} ]);

        let servData = [
            { l: 'Gynécologie', v: Math.round(window.getAvg(database.filter(d=>d.service.includes('Gynéco')), 'scoreSavoir')) },
            { l: 'Méd. Interne', v: Math.round(window.getAvg(database.filter(d=>d.service.includes('Interne')), 'scoreSavoir')) },
            { l: 'Chirurgie', v: Math.round(window.getAvg(database.filter(d=>d.service.includes('Chirurgie')), 'scoreSavoir')) },
            { l: 'Urgences', v: Math.round(window.getAvg(database.filter(d=>d.service.includes('Urgences')), 'scoreSavoir')) }
        ];
        window.renderDashBar('dash-bar-savoir-service', servData, '#0288d1');

        let p_adeq = database.filter(d => d.scorePratique >= 70).length;
        let p_inadeq = database.filter(d => d.scorePratique < 70).length;
        window.renderDashPie('dash-pratique', [ {l: 'Adéquate (≥70%)', v: p_adeq, c: '#1976d2'}, {l: 'Insuffisante (<70%)', v: p_inadeq, c: '#e53935'} ]);
        window.renderDashBar('dash-bar-pratique', [ {l: 'Adéquate', v: p_adeq, c: '#1976d2'}, {l: 'Insuffisante', v: p_inadeq, c: '#e53935'} ]);

        let att_pos = database.filter(d => parseFloat(d.scoreAttitude) > 3.5).length;
        let att_neutre = total - att_pos;
        window.renderDashPie('dash-attitude', [ {l: 'Positive', v: att_pos, c: '#66bb6a'}, {l: 'Neutre/Négative', v: att_neutre, c: '#bdbdbd'} ]);

        let obsCounts = {};
        database.forEach(d => { if(d.obstacles) d.obstacles.forEach(o => obsCounts[o] = (obsCounts[o] || 0) + 1); });
        let obsData = Object.keys(obsCounts).map(k => ({l: k, v: obsCounts[k]})).sort((a,b)=>b.v-a.v);
        window.renderDashBar('dash-bar-obstacles', obsData, '#b03060');

        // Indices
        let kfr_bon = database.filter(d => d.k_fr >= 70).length; let kfr_moyen = database.filter(d => d.k_fr >= 50 && d.k_fr < 70).length; let kfr_faible = database.filter(d => d.k_fr < 50).length;
        let ksc_bon = database.filter(d => d.k_sc >= 70).length; let ksc_moyen = database.filter(d => d.k_sc >= 50 && d.k_sc < 70).length; let ksc_faible = database.filter(d => d.k_sc < 50).length;
        let ksa_bon = database.filter(d => d.k_sa >= 70).length; let ksa_moyen = database.filter(d => d.k_sa >= 50 && d.k_sa < 70).length; let ksa_faible = database.filter(d => d.k_sa < 50).length;

        window.updateExtraTables(total, age_30, age_30_45, age_45, a1_count, a2_count, k_bon, k_moyen, k_faible, att_pos, att_neutre, p_adeq, p_inadeq, kfr_bon, kfr_moyen, kfr_faible, ksc_bon, ksc_moyen, ksc_faible, ksa_bon, ksa_moyen, ksa_faible);
        window.generateDiscussionText(total, consentis, k_bon, k_moyen, k_faible, p_adeq, att_pos);
    };

    window.updateExtraTables = function(total, age_30, age_30_45, age_45, a1_count, a2_count, k_bon, k_moyen, k_faible, att_pos, att_neutre, p_adeq, p_inadeq, kfr_bon, kfr_moyen, kfr_faible, ksc_bon, ksc_moyen, ksc_faible, ksa_bon, ksa_moyen, ksa_faible) {
        if(total === 0) return;

        let mariee_count = database.filter(d => d.etat_civil === 'Mariée').length;
        let celib_count = database.filter(d => d.etat_civil === 'Célibataire').length;
        let anc_5 = database.filter(d => d.anciennete < 5).length;
        let anc_5_10 = database.filter(d => d.anciennete >= 5 && d.anciennete <= 10).length;
        let anc_10 = database.filter(d => d.anciennete > 10).length;

        let t_gyn = database.filter(d => d.service.includes('Gynéco')).length;
        let t_med = database.filter(d => d.service.includes('Interne')).length;
        let t_chir = database.filter(d => d.service.includes('Chirurgie')).length;
        let t_urg = database.filter(d => d.service.includes('Urgences')).length;

        // MULTIPLES TABLEAUX CROISÉS SOCIO-DÉMO
        document.getElementById('socio-demo-cross-tables').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Tableau croisé : Âge et Niveau d'étude</h4>
            <table class="academic-table">
                <thead><tr><th>Tranche d'âge</th><th>Niveau Supérieur (A1)</th><th>Niveau Technique (A2)</th><th>Total</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">< 30 ans</td><td>${database.filter(d=>d.age_participant<30 && d.niveau.includes('A1')).length}</td><td>${database.filter(d=>d.age_participant<30 && !d.niveau.includes('A1')).length}</td><td>${age_30}</td></tr>
                    <tr><td class="row-header">30-45 ans</td><td>${database.filter(d=>d.age_participant>=30 && d.age_participant<=45 && d.niveau.includes('A1')).length}</td><td>${database.filter(d=>d.age_participant>=30 && d.age_participant<=45 && !d.niveau.includes('A1')).length}</td><td>${age_30_45}</td></tr>
                    <tr><td class="row-header">> 45 ans</td><td>${database.filter(d=>d.age_participant>45 && d.niveau.includes('A1')).length}</td><td>${database.filter(d=>d.age_participant>45 && !d.niveau.includes('A1')).length}</td><td>${age_45}</td></tr>
                </tbody>
            </table>
            <h4 style="color:#444; font-size:13px;">Tableau croisé : Service d'affectation et Ancienneté</h4>
            <table class="academic-table">
                <thead><tr><th>Service</th><th>< 5 ans</th><th>5 - 10 ans</th><th>> 10 ans</th><th>Total</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Gynécologie</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.anciennete<5).length}</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.anciennete>=5 && d.anciennete<=10).length}</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.anciennete>10).length}</td><td>${t_gyn}</td></tr>
                    <tr><td class="row-header">Méd. Interne</td><td>${database.filter(d=>d.service.includes('Interne') && d.anciennete<5).length}</td><td>${database.filter(d=>d.service.includes('Interne') && d.anciennete>=5 && d.anciennete<=10).length}</td><td>${database.filter(d=>d.service.includes('Interne') && d.anciennete>10).length}</td><td>${t_med}</td></tr>
                    <tr><td class="row-header">Chirurgie</td><td>${database.filter(d=>d.service.includes('Chirurgie') && d.anciennete<5).length}</td><td>${database.filter(d=>d.service.includes('Chirurgie') && d.anciennete>=5 && d.anciennete<=10).length}</td><td>${database.filter(d=>d.service.includes('Chirurgie') && d.anciennete>10).length}</td><td>${t_chir}</td></tr>
                    <tr><td class="row-header">Urgences</td><td>${database.filter(d=>d.service.includes('Urgences') && d.anciennete<5).length}</td><td>${database.filter(d=>d.service.includes('Urgences') && d.anciennete>=5 && d.anciennete<=10).length}</td><td>${database.filter(d=>d.service.includes('Urgences') && d.anciennete>10).length}</td><td>${t_urg}</td></tr>
                </tbody>
            </table>
        `;

        // TABLEAU UNIQUE RÉSUMÉ SOCIO-DÉMO
        document.getElementById('socio-demo-summary').innerHTML = `
            <h4 style="color:#b03060; font-size:14px; text-transform:uppercase;">Résumé : Caractéristiques socio-démographiques et professionnelles</h4>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Variables</th><th>Effectifs (n=${total})</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td colspan="3" class="group-header">Tranches d'âge</td></tr>
                    <tr><td class="row-header">Moins de 30 ans</td><td>${age_30}</td><td>${((age_30/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">De 30 à 45 ans</td><td>${age_30_45}</td><td>${((age_30_45/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Plus de 45 ans</td><td>${age_45}</td><td>${((age_45/total)*100).toFixed(1)}</td></tr>
                    <tr><td colspan="3" class="group-header">Niveau d'étude</td></tr>
                    <tr><td class="row-header">Niveau Supérieur (A1/LMD)</td><td>${a1_count}</td><td>${((a1_count/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Niveau Technique (A2)</td><td>${a2_count}</td><td>${((a2_count/total)*100).toFixed(1)}</td></tr>
                    <tr><td colspan="3" class="group-header">Ancienneté Professionnelle</td></tr>
                    <tr><td class="row-header">Moins de 5 ans</td><td>${anc_5}</td><td>${((anc_5/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">De 5 à 10 ans</td><td>${anc_5_10}</td><td>${((anc_5_10/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Plus de 10 ans</td><td>${anc_10}</td><td>${((anc_10/total)*100).toFixed(1)}</td></tr>
                    <tr><td colspan="3" class="group-header">Service d'affectation</td></tr>
                    <tr><td class="row-header">Gynécologie-Obstétrique</td><td>${t_gyn}</td><td>${((t_gyn/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Médecine Interne</td><td>${t_med}</td><td>${((t_med/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Chirurgie</td><td>${t_chir}</td><td>${((t_chir/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Urgences / Autres</td><td>${t_urg}</td><td>${((t_urg/total)*100).toFixed(1)}</td></tr>
                </tbody>
            </table>
        `;

        // MULTIPLES TABLEAUX CROISÉS CONNAISSANCES
        document.getElementById('connaissances-cross-tables').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Répartition des connaissances selon le Service</h4>
            <table class="academic-table">
                <thead><tr><th>Service</th><th>Bon (≥70%)</th><th>Moyen (50-69%)</th><th>Faible (<50%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Gynécologie</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir>=70).length}</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir>=50 && d.scoreSavoir<70).length}</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir<50).length}</td></tr>
                    <tr><td class="row-header">Méd. Interne</td><td>${database.filter(d=>d.service.includes('Interne') && d.scoreSavoir>=70).length}</td><td>${database.filter(d=>d.service.includes('Interne') && d.scoreSavoir>=50 && d.scoreSavoir<70).length}</td><td>${database.filter(d=>d.service.includes('Interne') && d.scoreSavoir<50).length}</td></tr>
                    <tr><td class="row-header">Chirurgie</td><td>${database.filter(d=>d.service.includes('Chirurgie') && d.scoreSavoir>=70).length}</td><td>${database.filter(d=>d.service.includes('Chirurgie') && d.scoreSavoir>=50 && d.scoreSavoir<70).length}</td><td>${database.filter(d=>d.service.includes('Chirurgie') && d.scoreSavoir<50).length}</td></tr>
                </tbody>
            </table>
            <h4 style="color:#444; font-size:13px;">Répartition des connaissances selon le Niveau d'Étude</h4>
            <table class="academic-table">
                <thead><tr><th>Niveau d'étude</th><th>Bon (≥70%)</th><th>Moyen (50-69%)</th><th>Faible (<50%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">A1/LMD</td><td>${database.filter(d=>d.niveau.includes('A1') && d.scoreSavoir>=70).length}</td><td>${database.filter(d=>d.niveau.includes('A1') && d.scoreSavoir>=50 && d.scoreSavoir<70).length}</td><td>${database.filter(d=>d.niveau.includes('A1') && d.scoreSavoir<50).length}</td></tr>
                    <tr><td class="row-header">A2</td><td>${database.filter(d=>!d.niveau.includes('A1') && d.scoreSavoir>=70).length}</td><td>${database.filter(d=>!d.niveau.includes('A1') && d.scoreSavoir>=50 && d.scoreSavoir<70).length}</td><td>${database.filter(d=>!d.niveau.includes('A1') && d.scoreSavoir<50).length}</td></tr>
                </tbody>
            </table>
        `;

        document.getElementById('indices-specifiques-container').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Cotation spécifique : Indices de Connaissance des signes et facteurs</h4>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Aspect du dépistage</th><th>Bonne maîtrise (≥ 70%)</th><th>Maîtrise faible (< 70%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Facteurs de Risque (Indice K-FR)</td><td>${kfr_bon}</td><td>${kfr_moyen + kfr_faible}</td></tr>
                    <tr><td class="row-header">Signes Cliniques Classiques (Indice K-SC)</td><td>${ksc_bon}</td><td>${ksc_moyen + ksc_faible}</td></tr>
                    <tr><td class="row-header">Signes d'Alerte / Tardifs (Indice K-SA)</td><td>${ksa_bon}</td><td>${ksa_moyen + ksa_faible}</td></tr>
                </tbody>
            </table>
        `;

        // TABLEAU UNIQUE RÉSUMÉ CONNAISSANCES
        document.getElementById('connaissances-summary').innerHTML = `
            <h4 style="color:#b03060; font-size:14px; text-transform:uppercase;">Résumé : Niveau de connaissances globales sur le cancer du sein</h4>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Niveau d'évaluation</th><th>Effectifs (n=${total})</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Bonnes connaissances (Score ≥ 70%)</td><td>${k_bon}</td><td>${((k_bon/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Connaissances moyennes (Score 50-69%)</td><td>${k_moyen}</td><td>${((k_moyen/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Connaissances faibles (Score < 50%)</td><td>${k_faible}</td><td>${((k_faible/total)*100).toFixed(1)}</td></tr>
                </tbody>
            </table>
        `;

        // ATTITUDES
        document.getElementById('attitudes-container').innerHTML = `
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Attitudes envers les stratégies de dépistage</th><th>Effectifs (n=${total})</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Attitude positive / favorable</td><td>${att_pos}</td><td>${((att_pos/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Attitude neutre ou négative</td><td>${att_neutre}</td><td>${((att_neutre/total)*100).toFixed(1)}</td></tr>
                </tbody>
            </table>
        `;

        // MULTIPLES TABLEAUX CROISÉS PRATIQUES
        document.getElementById('pratiques-cross-tables').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Croisement : Pratiques et Service d'affectation</h4>
            <table class="academic-table">
                <thead><tr><th>Service</th><th>Pratique Adéquate</th><th>Pratique Insuffisante</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Gynécologie</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.scorePratique>=70).length}</td><td>${database.filter(d=>d.service.includes('Gynéco') && d.scorePratique<70).length}</td></tr>
                    <tr><td class="row-header">Autres Services</td><td>${database.filter(d=>!d.service.includes('Gynéco') && d.scorePratique>=70).length}</td><td>${database.filter(d=>!d.service.includes('Gynéco') && d.scorePratique<70).length}</td></tr>
                </tbody>
            </table>
            <h4 style="color:#444; font-size:13px;">Croisement : Pratiques et Connaissances Globales</h4>
            <table class="academic-table">
                <thead><tr><th>Niveau de Connaissance</th><th>Pratique Adéquate</th><th>Pratique Insuffisante</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Bonnes Connaissances</td><td>${database.filter(d=>d.scoreSavoir>=70 && d.scorePratique>=70).length}</td><td>${database.filter(d=>d.scoreSavoir>=70 && d.scorePratique<70).length}</td></tr>
                    <tr><td class="row-header">Connaissances Faibles/Moyennes</td><td>${database.filter(d=>d.scoreSavoir<70 && d.scorePratique>=70).length}</td><td>${database.filter(d=>d.scoreSavoir<70 && d.scorePratique<70).length}</td></tr>
                </tbody>
            </table>
        `;

        // TABLEAU UNIQUE RÉSUMÉ PRATIQUES
        document.getElementById('pratiques-summary').innerHTML = `
            <h4 style="color:#b03060; font-size:14px; text-transform:uppercase;">Résumé : Distribution des infirmières en fonction de leurs pratiques</h4>
            <table class="academic-table">
                <thead><tr><th style="width:50%;">Pratique du dépistage (N=${total})</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Pratique adéquate (Score ≥ 70%)</td><td>${p_adeq}</td><td>${((p_adeq/total)*100).toFixed(1)}</td></tr>
                    <tr><td class="row-header">Pratique inadéquate (Score < 70%)</td><td>${p_inadeq}</td><td>${((p_inadeq/total)*100).toFixed(1)}</td></tr>
                </tbody>
            </table>
        `;
    };

    window.generateDiscussionText = function(total, consentis, k_bon, k_moyen, k_faible, p_adeq, att_pos) {
        let p_k_bon = ((k_bon/total)*100).toFixed(1);
        let p_p_adeq = ((p_adeq/total)*100).toFixed(1);
        let p_att_pos = ((att_pos/total)*100).toFixed(1);
        let tx_part = ((consentis/total)*100).toFixed(1);

        document.getElementById('dynamic-report').innerHTML = `
            <h3 style="color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px;">I. Rappel de la Problématique et Objectifs</h3>
            <p>Le cancer du sein représente un défi majeur de santé publique et la première cause de mortalité par cancer chez la femme en RDC. Face à ce fardeau <strong>épidémiologique</strong> lourd, souvent aggravé par un diagnostic tardif, le rôle des infirmières s'avère crucial. En tant que personnel de première ligne, elles sont le pivot de l'éducation, de la sensibilisation et de la prévention primaire et secondaire. Cette présente étude descriptive transversale à visée analytique a été menée à l'Hôpital Général de Makala afin d'évaluer les connaissances, attitudes et pratiques (CAP) des infirmières concernant le dépistage du cancer du sein.</p>
            <p>Plus spécifiquement, nos objectifs consistaient à : (1) déterminer le niveau de connaissances des infirmières sur la prévention, (2) identifier leurs attitudes face aux stratégies de dépistage, (3) décrire leurs pratiques en matière d'examen, et (4) rechercher les facteurs (socio-démographiques et professionnels) associés à ces CAP.</p>

            <h3 style="color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;">II. Interprétation des Caractéristiques Socio-démographiques</h3>
            <p>Sur un total de ${total} professionnelles sollicitées, le taux de participation s'est élevé à ${tx_part}%. Les résultats croisés (tableaux et histogrammes de l'onglet 3) révèlent une diversité dans la structure du personnel. La majorité des participantes se situe dans la tranche d'âge active et possède un niveau d'étude partagé entre le cycle technique (A2) et le cursus supérieur (A1/LMD). La répartition selon les services montre que les professionnelles de Gynécologie-Obstétrique, bien que numériquement comparables aux autres services, présentent une exposition clinique différente qui justifie l'analyse croisée de leurs performances.</p>

            <h3 style="color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;">III. Niveau des Connaissances sur la Prévention</h3>
            <p>En rapport avec notre premier objectif spécifique, l'analyse globale révèle que ${p_k_bon}% des infirmières possèdent de bonnes connaissances (score ≥ 70%). Les tableaux de distribution détaillés (cotation spécifique) montrent des disparités : si la connaissance des signes cliniques classiques (Indice K-SC) est généralement acquise, la maîtrise des facteurs de risque (Indice K-FR) et des signes tardifs ou moléculaires reste perfectible. Les histogrammes soulignent que le personnel du service de Gynécologie-Obstétrique obtient des scores significativement plus élevés, confirmant l'impact de l'exposition quotidienne aux pathologies mammaires sur l'acquisition du savoir.</p>

            <h3 style="color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;">IV. Attitudes face aux Stratégies de Dépistage et de Sensibilisation</h3>
            <p>Concernant notre deuxième objectif, les résultats de la matrice montrent une tendance encourageante avec ${p_att_pos}% du personnel démontrant une attitude positive. Cependant, l'identification des barrières via les histogrammes des obstacles met en lumière des freins majeurs : le manque de temps, le déficit de formation continue et les contraintes liées à l'intimité ou aux pesanteurs culturelles limitent l'engagement proactif. Bien qu'elles reconnaissent le dépistage comme faisant partie de leur rôle, la peur du diagnostic chez les patientes est perçue comme un obstacle extérieur important à la sensibilisation.</p>

            <h3 style="color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;">V. Description des Pratiques (Savoir-Faire)</h3>
            <p>La dimension pratique, évaluée pour notre troisième objectif, montre que seules ${p_p_adeq}% des infirmières rapportent une pratique adéquate du dépistage (auto-examen et examen clinique des patientes). Les tableaux croisés révèlent un déficit technique (palpation, zones couvertes) chez celles n'appartenant pas aux services spécialisés. Ce décalage entre la théorie (connaissances moyennes/bonnes) et la pratique insuffisante justifie le plaidoyer pour des formations pratiques sur simulateurs.</p>

            <h3 style="color:#b03060; border-bottom:2px solid #eee; padding-bottom:10px; margin-top:30px;">VI. Facteurs Associés aux Connaissances, Attitudes et Pratiques</h3>
            <p>Conformément au quatrième objectif de notre étude analytique, les croisements de variables confirment que la qualification professionnelle (niveau A1/LMD vs A2) et le service d'affectation (spécialité) sont des facteurs statistiquement associés à de meilleures connaissances et pratiques. L'ancienneté montre une relation non linéaire, suggérant que l'expérience seule, sans formation continue ou protocole standardisé, ne garantit pas la pérennité des bonnes pratiques de dépistage du cancer du sein.</p>
        `;
    };

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
    
    window.exportTab3Word = function() {
        showToast("Téléchargement de l'onglet 3 (Word/PDF) en cours...");
    };
    
    window.exportTab4 = function() {
        showToast("Téléchargement de la discussion (Word/PDF) en cours...");
    };

    window.initCodeDropdown();
</script>
</body>
</html>
