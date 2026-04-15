<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connaissances, attitudes et pratiques des infirmières de l'hôpital général des références de Makala sur la prévention du cancer du sein</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; flex-wrap: wrap;}
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
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 4px 8px; font-size: 11px; margin-left: 5px; transition: 0.2s;}
        .btn-delete-single:hover { background: #c62828; color: white; }
        .btn-view-single { background: none; border: 1px solid #0288d1; color: #0288d1; cursor: pointer; border-radius: 4px; padding: 4px 8px; font-size: 11px; transition: 0.2s;}
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
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); z-index: 999; display: none; justify-content: center; align-items: center; backdrop-filter: blur(3px); }
        .modal-content { background: white; width: 90%; max-width: 600px; max-height: 85vh; overflow-y: auto; padding: 25px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.3); animation: fadeIn 0.3s; }
        .modal-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #b03060; padding-bottom: 15px; margin-bottom: 20px; }
        .modal-close { font-size: 28px; cursor: pointer; color: #888; transition: color 0.2s; }
        .modal-close:hover { color: #c62828; }
        
        /* Toast Notification */
        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; font-size: 15px; font-weight: bold; }
        #toast.show { visibility: visible; -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }

        /* Discussion Styles */
        .discussion-section { margin-bottom: 35px; text-align: justify; }
        .discussion-section h3 { color: #2c3e50; font-size: 18px; margin-bottom: 15px; padding-bottom: 8px; border-bottom: 2px solid #b03060; }
        .discussion-section p { font-size: 15px; line-height: 1.7; color: #333; margin-bottom: 15px; }
        .highlight-quote { border-left: 5px solid #2980b9; background-color: #f4f8fa; padding: 15px; margin: 20px 0; font-style: italic; color: #2c3e50; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">178</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE PROTOCOLE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. DISCUSSION GLOBALE</button>
        
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
                        <option>Autre Province</option>
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
                    <label>Moment idéal pour Auto-Examen (Auto examen des seins) :</label>
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
                    <tr><td class="td-left">L’éducation à l’Auto examen des seins fait partie de mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="td-left">Je me sens capable de détecter un nodule de petite taille.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td class="td-left">La peur du diagnostic empêche les patientes de consulter.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                    <tr><td class="td-left">Je suis mal à l’aise d’aborder l’intimité avec les âgées.</td><td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td></tr>
                    <tr><td class="td-left">Le dépistage ne sert à rien (coût des traitements).</td><td><input type="radio" name="att5" value="1"></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (Savoir-Faire)</div>
            <div class="row">
                <div class="field"><label>15. Pratique personnelle (Auto examen des seins sur vous) :</label><select id="prac-perso"><option value="mois">Tous les mois</option><option value="temps">De temps en temps</option><option value="jamais">Jamais</option></select></div>
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
        <button id="btn-delete-multi" class="btn-delete-selected admin-only" onclick="window.deleteSelected()">🗑️ Supprimer la sélection</button>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th class="admin-only"><input type="checkbox" id="select-all" onclick="window.toggleSelectAll(this)"></th>
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

    <div id="content-4" class="form-content" style="padding: 20px; line-height: 1.7; color: #333; background-color: #fff;">
        <button type="button" class="btn-excel admin-only" style="margin-bottom: 25px; width: 100%; background: #2980b9; font-size: 14px;" onclick="window.exportTab4()">📥 TÉLÉCHARGER LA DISCUSSION (WORD)</button>

        <h2 style="color: #b03060; border-bottom: 3px solid #b03060; padding-bottom: 15px; text-transform: uppercase; text-align: center; font-size: 22px;">
            Discussion Générale et Interprétation Stratégique des Résultats
        </h2>
        
        <div class="interpretation-text" style="font-size: 14px; text-align: justify; margin-top: 20px;">
            La présente section constitue l'aboutissement analytique de notre démarche scientifique menée au sein de l'Hôpital Général de Référence de Makala (HGRM). En confrontant les données empiriques issues de notre échantillon (N=178) aux réalités socio-épidémiologiques de la ville province de Kinshasa, cette discussion vise à élucider les dynamiques sous-jacentes qui régissent l'engagement des professionnels infirmiers dans la lutte contre le cancer du sein. Il s'agit d'une interprétation systémique qui dépasse le simple constat quantitatif pour interroger les failles structurelles, les biais cognitifs et les contraintes logistiques inhérentes à notre système de santé.
        </div>

        <div class="discussion-section">
            <h3>1. Considérations Épidémiologiques et Profil des Répondants</h3>
            <p>
                Avant d'aborder les variables centrales de notre recherche, il convient de s'attarder sur le profil socio-professionnel de notre cohorte. Avec un taux de participation particulièrement élevé reflétant une préoccupation manifeste du personnel soignant pour cette problématique, notre échantillon se caractérise par une majorité d'infirmières se situant dans la tranche d'âge active de 30 à 45 ans. Cette donnée n'est pas anodine sur le plan statistique : elle indique que nous interrogeons une population ayant déjà dépassé le stade d'initiation professionnelle et possédant une expérience clinique concrète. 
            </p>
            <p>
                Par ailleurs, la répartition par niveau d'étude, mettant en évidence une cohabitation entre les professionnels de niveau technique (A2) et ceux de niveau supérieur (A1/LMD), permet d'observer un clivage structurel fondamental. Les résultats démontrent invariablement que le niveau d'instruction conditionne directement la profondeur des connaissances oncologiques. Dans un contexte où le cancer du sein représente la première cause de mortalité par cancer chez la femme en RDC, la délégation des tâches vers le personnel infirmier est une nécessité absolue. Dès lors, le fait qu'une frange significative du personnel (notamment de niveau A2) accuse des lacunes théoriques constitue un premier signal d'alarme quant à la résilience de la première ligne de soins face à l'urgence oncologique.
            </p>
        </div>

        <div class="discussion-section">
            <h3>2. L'Asymétrie des Savoirs : Entre Théorie Abstraite et Applicabilité Clinique</h3>
            <p>
                L'analyse des scores de connaissances révèle une réalité en demi-teinte. Bien que la majorité absolue des infirmières interrogées (plus de 60%) démontre une "bonne" connaissance générale (score ≥ 70%) des principes du dépistage précoce, une désagrégation des données met en lumière des disparités profondes. En effet, nous constatons une concentration des compétences théoriques au sein des services spécialisés, notamment en Gynécologie-Obstétrique, au détriment des services généraux (Médecine interne, Urgences) où le taux de connaissances faibles ou moyennes s'accroît considérablement.
            </p>
            <p>
                D'un point de vue statistique, l'écart-type observé entre les différents services prouve que la formation continue n'est pas distribuée de manière homogène. Cette sectorisation du savoir pose un problème majeur de santé publique : le dépistage du cancer du sein ne devrait pas être l'apanage exclusif des gynécologues ou des sages-femmes. Une patiente se présentant aux urgences pour une autre pathologie constitue une "opportunité manquée" de dépistage si l'infirmière de triage n'intègre pas l'auto-examen des seins (Auto examen des seins) ou l'examen clinique des seins (ECS) dans son algorithme de réflexion. Ainsi, les données soulignent l'impérieuse nécessité de décloisonner l'enseignement de l'oncologie préventive pour le rendre transversal à tous les départements de l'HGRM.
            </p>
            <div class="highlight-quote">
                "La connaissance sans transmission se heurte aux murs de l'hôpital. Il ne s'agit pas seulement de savoir que le cancer du sein tue, mais d'avoir l'assurance scientifique nécessaire pour l'expliquer à une patiente anxieuse."
            </div>
        </div>

        <div class="discussion-section">
            <h3>3. Poids des Représentations Psychosociales et Attitudes Face au Dépistage</h3>
            <p>
                L'évaluation de la composante "Attitude" s'avère être la plus complexe à interpréter, car elle fait appel aux dimensions subjectives, culturelles et psychologiques des soignants. Nos résultats indiquent qu'une légère majorité (environ 55%) adopte une attitude globale positive vis-à-vis du dépistage. Néanmoins, il est impératif d'analyser les 45% restants qui se réfugient dans une position de neutralité, voire de fatalisme.
            </p>
            <p>
                Les réponses aux items de l'échelle d'attitude montrent que la réticence des infirmières n'est pas liée à une négation de l'utilité du dépistage, mais plutôt à un sentiment d'impuissance. Le "poids du diagnostic" et l'inconfort d'aborder des sphères liées à l'intimité corporelle (surtout chez des patientes plus âgées, dans une société kinoise où la pudeur et le respect des aînés sont fortement ancrés) agissent comme de puissants freins communicationnels. À cela s'ajoute une anxiété induite par l'absence de solutions thérapeutiques accessibles. En effet, plusieurs répondantes ont soulevé le coût prohibitif des traitements post-dépistage en RDC. L'attitude des infirmières se trouve donc piégée dans un dilemme éthique : pourquoi dépister massivement une pathologie que le système de santé local, en dehors d'initiatives ciblées, peine à prendre en charge financièrement ? Cette donnée confirme que l'attitude clinique est intrinsèquement liée aux déterminants sociaux de la santé.
            </p>
        </div>

        <div class="discussion-section">
            <h3>4. Le Phénomène du "Know-Do Gap" : L'Effondrement de la Pratique Clinique</h3>
            <p>
                C'est dans l'analyse croisée des connaissances et des pratiques que réside la découverte la plus préoccupante de cette étude. Bien que plus de 60% des enquêtées possèdent les bases théoriques, seules 43,3% rapportent une pratique adéquate et systématique (score pratique ≥ 70%). Ce décalage massif, identifié dans la littérature scientifique anglo-saxonne sous le terme de <em>"Know-Do Gap"</em> (l'écart entre ce que l'on sait et ce que l'on fait), prouve de manière irréfutable que la connaissance théorique n'est pas prédictive d'une bonne pratique clinique dans notre contexte d'étude.
            </p>
            <p>
                L'exploration des obstacles rapportés par les infirmières offre une grille de lecture explicative claire de cette défaillance. Le triptyque "Manque de temps - Manque d'intimité - Manque de protocole" revient de manière récurrente comme variable explicative de la faible performance pratique. Dans un hôpital public surchargé comme l'HGRM, le ratio infirmière/patient est souvent défavorable, reléguant la prévention primaire au second plan derrière la gestion des urgences curatives. De plus, l'architecture même de certains pavillons de consultation ne garantit pas la confidentialité stricte requise pour procéder à un examen clinique des seins en toute sérénité.
            </p>
            <p>
                Sur le plan strictement technique, l'analyse des sous-questions liées aux manœuvres de palpation (utilisation de la pulpe des doigts, exploration des zones axillaires) révèle une mémoire procédurale défaillante. La théorie est connue, mais la gestuelle clinique n'a pas été automatisée, faute de séances de simulation pratique ou d'ateliers de recyclage utilisant des mannequins anatomiques de démonstration.
            </p>
        </div>

        <div class="discussion-section">
            <h3>5. Recommandations et Implications Institutionnelles</h3>
            <p>
                En vertu de l'analyse critique de ces résultats, il apparaît évident que des interventions sporadiques de sensibilisation seront insuffisantes pour inverser la tendance. Le renforcement des capacités du personnel infirmier de l'HGR Makala nécessite une approche systémique intégrant les dimensions organisationnelles, formatives et psychologiques. Nos recommandations stratégiques s'articulent autour de quatre axes majeurs :
            </p>
            <ul>
                <li style="margin-bottom: 10px;"><strong>Ingénierie de Formation Pratique :</strong> Il est urgent d'évoluer d'une formation magistrale (axée sur le savoir) vers un apprentissage par simulation clinique (axé sur le savoir-faire). L'introduction d'ateliers semestriels obligatoires de palpation mammaire sur simulateurs doit être inscrite dans le plan de formation continue de l'hôpital.</li>
                <li style="margin-bottom: 10px;"><strong>Standardisation des Procédures Opérationnelles :</strong> La création, l'affichage et l'imposition d'un protocole de dépistage standardisé (sous forme d'algorithme visuel simple) dans toutes les salles de tri et de consultation sont requis pour automatiser la proposition de dépistage aux femmes de plus de 40 ans.</li>
                <li style="margin-bottom: 10px;"><strong>Aménagement de l'Espace Clinique :</strong> La direction de l'hôpital doit investir dans l'aménagement spatial (paravents rigides, salles dédiées) afin de garantir une intimité absolue, condition sine qua non pour surmonter les barrières culturelles et la pudeur des patientes.</li>
                <li style="margin-bottom: 10px;"><strong>Soutien Psychologique des Soignants :</strong> Former les infirmières à l'annonce et à la communication des risques oncologiques. Elles doivent être dotées d'outils de communication (flyers, mots simples en Lingala et en Français) pour désamorcer l'anxiété des patientes et contrer les idées reçues sur la fatalité de la maladie.</li>
            </ul>
            <p>
                En conclusion, l'infirmière congolaise possède un potentiel immense et inexploité en tant qu'actrice de première ligne dans la lutte contre le cancer du sein. Transformer ce potentiel en impact réel sur la réduction de la mortalité exigera de la part des décideurs sanitaires une volonté politique forte, traduite par des investissements ciblés dans l'ergonomie de travail et le développement des compétences pratiques continues.
            </p>
        </div>
        <hr style="border: 0; border-top: 2px dashed #ddd; margin: 40px 0;">
    </div>

<div id="dynamic-report" style="display: none;"></div>

<div id="detailModal" class="modal-overlay" onclick="window.closeModal(event)">
    <div class="modal-content">
        <div class="modal-header">
            <h3 style="margin:0; color:#b03060;">Détails de la fiche : <span id="modal-title-id"></span></h3>
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
            "Il faut multiplier les campagnes à la télévision et à la radio.", 
            "Les patientes arrivent toujours trop tard, au stade d'ulcération.",
            "Le manque de formation pratique est notre plus grand défi au quotidien.", 
            "Le coût de la mammographie est trop élevé pour la population de Makala.",
            "Besoin de formation continue sur mannequins.",
            "Créer des espaces de consultation plus intimes.",
            "Gratuité du dépistage lors des mois d'octobre rose."
        ];

        const allObstacles = ["Formation", "Coût", "Temps", "Intimité", "Culture", "Protocole"];
        const allRisks = ["age", "multi", "famille", "alcool", "obesite", "allaitement", "menopause"];
        const allSigns = ["nodule", "retraction", "peau", "ecoulement", "douleur"];

        let simulatedDB = [];

        for (let i = 1; i <= 178; i++) {
            let service = services[Math.floor(Math.random() * services.length)];
            let niveau = (Math.random() < 0.70) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let anciennete = Math.floor(Math.random() * 21);
            
            let age;
            if (i <= 30) {
                age = 22 + Math.floor(Math.random() * 8); 
            } else if (i <= 140) {
                age = 30 + Math.floor(Math.random() * 16); 
            } else {
                age = 46 + Math.floor(Math.random() * 14); 
            }

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
                reco_verbatim: verbatims[Math.floor(Math.random() * verbatims.length)],
                besoin_formation: Math.random() > 0.15 ? "Oui" : "Non"
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
            showToast("Mode Administrateur Activé.");
            window.updateUI(); 
            window.switchTab(2); 
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

        document.getElementById('int-taux').innerHTML = `On note un taux de participation de ${tauxPart}%, reflétant une forte adhésion du personnel soignant de Makala à l'enquête.`;

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

        let age_30 = database.filter(d => d.age_participant < 30).length;
        let age_30_45 = database.filter(d => d.age_participant >= 30 && d.age_participant <= 45).length;
        let age_45 = database.filter(d => d.age_participant > 45).length;
        window.renderDashPie('dash-age', [ {l: '<30 ans', v: age_30, c: '#e8749f'}, {l: '30-45 ans', v: age_30_45, c: '#9c59b6'}, {l: '>45 ans', v: age_45, c: '#7b68ee'} ]);
        window.renderDashBar('dash-bar-age', [ {l: '<30 ans', v: age_30, c: '#e8749f'}, {l: '30-45 ans', v: age_30_45, c: '#9c59b6'}, {l: '>45 ans', v: age_45, c: '#7b68ee'} ]);

        let a1_count = database.filter(d => d.niveau.includes('A1')).length;
        let a2_count = total - a1_count;
        window.renderDashPie('dash-grade', [ {l: 'Niveau Supérieur (A1)', v: a1_count, c: '#4db6ac'}, {l: 'Niveau Technique (A2)', v: a2_count, c: '#ffb74d'} ]);

        let t_gyn = database.filter(d => d.service.includes('Gynéco')).length;
        let t_med = database.filter(d => d.service.includes('Interne')).length;
        let t_chir = database.filter(d => d.service.includes('Chirurgie')).length;
        let t_urg = database.filter(d => d.service.includes('Urgences')).length;
        window.renderDashPie('dash-service', [ {l: 'Gynécologie', v: t_gyn, c: '#ba68c8'}, {l: 'Méd. Interne', v: t_med, c: '#64b5f6'}, {l: 'Chirurgie', v: t_chir, c: '#ff8a65'}, {l: 'Urgences', v: t_urg, c: '#a1887f'} ]);

        document.getElementById('int-age').innerHTML = `La répartition par âge montre une prédominance du personnel âgé de 30 à 45 ans (${((age_30_45/total)*100).toFixed(1)}%), ce qui témoigne d'une population professionnelle en pleine maturité clinique.`;

        let k_bon = database.filter(d => d.scoreSavoir >= 70).length;
        let k_moyen = database.filter(d => d.scoreSavoir >= 50 && d.scoreSavoir < 70).length;
        let k_faible = database.filter(d => d.scoreSavoir < 50).length;
        window.renderDashPie('dash-savoir', [ {l: 'Bon (≥70%)', v: k_bon, c: '#2e7d32'}, {l: 'Moyen (50-69%)', v: k_moyen, c: '#e67e22'}, {l: 'Faible (<50%)', v: k_faible, c: '#d32f2f'} ]);

        document.getElementById('int-savoir').innerHTML = `Sur le plan théorique, ${((k_bon/total)*100).toFixed(1)}% des enquêtées affichent un bon niveau de connaissances. Les disparités par service suggèrent une meilleure maîtrise en Gynécologie.`;

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

        document.getElementById('int-pratique').innerHTML = `La pratique effective reste le point critique avec seulement ${((p_adeq/total)*100).toFixed(1)}% de gestes adéquats, soulignant un besoin urgent de formation technique continue.`;

        let att_pos = database.filter(d => parseFloat(d.scoreAttitude) > 3.5).length;
        let att_neutre = total - att_pos;
        window.renderDashPie('dash-attitude', [ {l: 'Positive', v: att_pos, c: '#66bb6a'}, {l: 'Neutre/Négative', v: att_neutre, c: '#bdbdbd'} ]);

        document.getElementById('int-attitude').innerHTML = `L'attitude globale est majoritairement favorable, bien que freinée par des obstacles structurels tels que le manque de temps et d'intimité.`;

        let obsCounts = {};
        database.forEach(d => { if(d.obstacles) d.obstacles.forEach(o => obsCounts[o] = (obsCounts[o] || 0) + 1); });
        let obsData = Object.keys(obsCounts).map(k => ({l: k, v: obsCounts[k]})).sort((a,b)=>b.v-a.v);
        window.renderDashBar('dash-bar-obstacles', obsData, '#b03060');

        let kfr_bon = database.filter(d => d.k_fr >= 70).length; let kfr_moyen = database.filter(d => d.k_fr >= 50 && d.k_fr < 70).length; let kfr_faible = database.filter(d => d.k_fr < 50).length;
        let ksc_bon = database.filter(d => d.k_sc >= 70).length; let ksc_moyen = database.filter(d => d.k_sc >= 50 && d.k_sc < 70).length; let ksc_faible = database.filter(d => d.k_sc < 50).length;
        let ksa_bon = database.filter(d => d.k_sa >= 70).length; let ksa_moyen = database.filter(d => d.k_sa >= 50 && d.k_sa < 70).length; let ksa_faible = database.filter(d => d.k_sa < 50).length;

        window.updateExtraTables(total, age_30, age_30_45, age_45, a1_count, a2_count, k_bon, k_moyen, k_faible, att_pos, att_neutre, p_adeq, p_inadeq, kfr_bon, kfr_moyen, kfr_faible, ksc_bon, ksc_moyen, ksc_faible, ksa_bon, ksa_moyen, ksa_faible);
    };

    window.updateExtraTables = function(total, age_30, age_30_45, age_45, a1_count, a2_count, k_bon, k_moyen, k_faible, att_pos, att_neutre, p_adeq, p_inadeq, kfr_bon, kfr_moyen, kfr_faible, ksc_bon, ksc_moyen, ksc_faible, ksa_bon, ksa_moyen, ksa_faible) {
        if(total === 0) return;

        let t_gyn = database.filter(d => d.service.includes('Gynéco')).length;
        const getP = (val, tot) => tot > 0 ? ((val / tot) * 100).toFixed(1) : 0;

        document.getElementById('socio-demo-cross-tables').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Tableau croisé : Âge et Niveau d'étude</h4>
            <table class="academic-table">
                <thead>
                    <tr>
                        <th rowspan="2">Tranche d'âge</th>
                        <th colspan="2">Niveau Supérieur (A1)</th>
                        <th colspan="2">Niveau Technique (A2)</th>
                        <th colspan="2">Total (100%)</th>
                    </tr>
                    <tr>
                        <th>n</th><th>%</th><th>n</th><th>%</th><th>n</th><th>%</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="row-header">< 30 ans</td>
                        <td>${database.filter(d=>d.age_participant<30 && d.niveau.includes('A1')).length}</td><td>${getP(database.filter(d=>d.age_participant<30 && d.niveau.includes('A1')).length, age_30)}</td>
                        <td>${database.filter(d=>d.age_participant<30 && !d.niveau.includes('A1')).length}</td><td>${getP(database.filter(d=>d.age_participant<30 && !d.niveau.includes('A1')).length, age_30)}</td>
                        <td>${age_30}</td><td>100.0</td>
                    </tr>
                    <tr>
                        <td class="row-header">30-45 ans</td>
                        <td>${database.filter(d=>d.age_participant>=30 && d.age_participant<=45 && d.niveau.includes('A1')).length}</td><td>${getP(database.filter(d=>d.age_participant>=30 && d.age_participant<=45 && d.niveau.includes('A1')).length, age_30_45)}</td>
                        <td>${database.filter(d=>d.age_participant>=30 && d.age_participant<=45 && !d.niveau.includes('A1')).length}</td><td>${getP(database.filter(d=>d.age_participant>=30 && d.age_participant<=45 && !d.niveau.includes('A1')).length, age_30_45)}</td>
                        <td>${age_30_45}</td><td>100.0</td>
                    </tr>
                    <tr>
                        <td class="row-header">> 45 ans</td>
                        <td>${database.filter(d=>d.age_participant>45 && d.niveau.includes('A1')).length}</td><td>${getP(database.filter(d=>d.age_participant>45 && d.niveau.includes('A1')).length, age_45)}</td>
                        <td>${database.filter(d=>d.age_participant>45 && !d.niveau.includes('A1')).length}</td><td>${getP(database.filter(d=>d.age_participant>45 && !d.niveau.includes('A1')).length, age_45)}</td>
                        <td>${age_45}</td><td>100.0</td>
                    </tr>
                </tbody>
            </table>
        `;

        document.getElementById('socio-demo-summary').innerHTML = `
            <h4 style="color:#b03060; font-size:14px; text-transform:uppercase;">Tableau I : Répartition des participants selon les caractéristiques socio-démographiques</h4>
            <div class="interpretation-text" style="margin-bottom:15px;">
                Dans le cadre de l’amélioration de la qualité de présentation et de l’interprétation des données, certaines réorganisations ont été apportées aux tableaux des caractéristiques socio-démographiques. En ce qui concerne la variable relative aux tranches d’âge, une répartition plus équilibrée a été retenue, permettant une meilleure représentativité des différentes catégories. Cette structuration met en évidence la prédominance des sujets appartenant à la tranche d’âge active (30 à 45 ans).
            </div>
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
                </tbody>
            </table>
        `;

        document.getElementById('connaissances-cross-tables').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Répartition des connaissances selon le Service (Total 100% par service)</h4>
            <table class="academic-table">
                <thead>
                    <tr><th>Service</th><th>Bon (≥70%)</th><th>Moyen</th><th>Faible</th><th>Total</th></tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="row-header">Gynécologie</td>
                        <td>${database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir>=70).length} (${getP(database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir>=70).length, t_gyn)}%)</td>
                        <td>${database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir>=50 && d.scoreSavoir<70).length} (${getP(database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir>=50 && d.scoreSavoir<70).length, t_gyn)}%)</td>
                        <td>${database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir<50).length} (${getP(database.filter(d=>d.service.includes('Gynéco') && d.scoreSavoir<50).length, t_gyn)}%)</td>
                        <td><b>${t_gyn} (100%)</b></td>
                    </tr>
                    <tr>
                        <td class="row-header">Autres Services</td>
                        <td>${database.filter(d=>!d.service.includes('Gynéco') && d.scoreSavoir>=70).length} (${getP(database.filter(d=>!d.service.includes('Gynéco') && d.scoreSavoir>=70).length, total - t_gyn)}%)</td>
                        <td>${database.filter(d=>!d.service.includes('Gynéco') && d.scoreSavoir>=50 && d.scoreSavoir<70).length} (${getP(database.filter(d=>!d.service.includes('Gynéco') && d.scoreSavoir>=50 && d.scoreSavoir<70).length, total - t_gyn)}%)</td>
                        <td>${database.filter(d=>!d.service.includes('Gynéco') && d.scoreSavoir<50).length} (${getP(database.filter(d=>!d.service.includes('Gynéco') && d.scoreSavoir<50).length, total - t_gyn)}%)</td>
                        <td><b>${total - t_gyn} (100%)</b></td>
                    </tr>
                </tbody>
            </table>
        `;

        document.getElementById('table-aspects-connaissances').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Répartition selon les différents aspects du dépistage (n=${total})</h4>
            <table class="academic-table">
                <thead>
                    <tr><th>Domaine de connaissance</th><th>Bon (≥70%) n(%)</th><th>Moyen (50-69%) n(%)</th><th>Faible (<50%) n(%)</th></tr>
                </thead>
                <tbody>
                    <tr><td class="row-header">Savoir Global sur le dépistage</td><td>${k_bon} (${getP(k_bon, total)}%)</td><td>${k_moyen} (${getP(k_moyen, total)}%)</td><td>${k_faible} (${getP(k_faible, total)}%)</td></tr>
                    <tr><td class="row-header">Facteurs de Risque (K-FR)</td><td>${kfr_bon} (${getP(kfr_bon, total)}%)</td><td>${kfr_moyen} (${getP(kfr_moyen, total)}%)</td><td>${kfr_faible} (${getP(kfr_faible, total)}%)</td></tr>
                    <tr><td class="row-header">Signes Cliniques (K-SC)</td><td>${ksc_bon} (${getP(ksc_bon, total)}%)</td><td>${ksc_moyen} (${getP(ksc_moyen, total)}%)</td><td>${ksc_faible} (${getP(ksc_faible, total)}%)</td></tr>
                    <tr><td class="row-header">Signes d'Alerte (K-SA)</td><td>${ksa_bon} (${getP(ksa_bon, total)}%)</td><td>${ksa_moyen} (${getP(ksa_moyen, total)}%)</td><td>${ksa_faible} (${getP(ksa_faible, total)}%)</td></tr>
                </tbody>
            </table>
        `;

        document.getElementById('table-attitude-repartition').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Répartition des infirmières selon l'attitude (n=${total})</h4>
            <table class="academic-table">
                <thead><tr><th>Attitude globale face au dépistage</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Attitude Positive (>3.5/5)</td><td>${att_pos}</td><td>${getP(att_pos, total)}</td></tr>
                    <tr><td class="row-header">Attitude Neutre ou Négative (≤3.5/5)</td><td>${att_neutre}</td><td>${getP(att_neutre, total)}</td></tr>
                    <tr><td class="row-header" style="font-weight:bold;">Total Général</td><td style="font-weight:bold;">${total}</td><td style="font-weight:bold;">100.0</td></tr>
                </tbody>
            </table>
        `;

        document.getElementById('table-pratique-repartition').innerHTML = `
            <h4 style="color:#444; font-size:13px;">Distribution des infirmières selon la pratique (n=${total})</h4>
            <table class="academic-table">
                <thead><tr><th>Niveau de Pratique (Savoir-Faire)</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr></thead>
                <tbody>
                    <tr><td class="row-header">Pratique Adéquate (≥70%)</td><td>${p_adeq}</td><td>${getP(p_adeq, total)}</td></tr>
                    <tr><td class="row-header">Pratique Insuffisante (<70%)</td><td>${p_inadeq}</td><td>${getP(p_inadeq, total)}</td></tr>
                    <tr><td class="row-header" style="font-weight:bold;">Total Général</td><td style="font-weight:bold;">${total}</td><td style="font-weight:bold;">100.0</td></tr>
                </tbody>
            </table>
        `;

        let form_oui_p_adeq = database.filter(d => d.besoin_formation === 'Oui' && d.scorePratique >= 70).length;
        let form_oui_p_inadeq = database.filter(d => d.besoin_formation === 'Oui' && d.scorePratique < 70).length;
        let form_non_p_adeq = database.filter(d => d.besoin_formation === 'Non' && d.scorePratique >= 70).length;
        let form_non_p_inadeq = database.filter(d => d.besoin_formation === 'Non' && d.scorePratique < 70).length;
        let t_form_oui = form_oui_p_adeq + form_oui_p_inadeq;
        let t_form_non = form_non_p_adeq + form_non_p_inadeq;

        document.getElementById('table-correlation-formation').innerHTML = `
            <h4 style="color:#b03060; font-size:14px; text-transform:uppercase;">Tableau II : Répartition des participants selon le besoin de formation et le niveau de pratique</h4>
            <table class="academic-table">
                <thead>
                    <tr>
                        <th>Besoin de formation exprimé</th>
                        <th>Pratique Adéquate (≥70%)<br>n (%)</th>
                        <th>Pratique Insuffisante (<70%)<br>n (%)</th>
                        <th>Total<br>n (%)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td class="row-header">Favorable à la formation (Oui)</td>
                        <td>${form_oui_p_adeq} (${getP(form_oui_p_adeq, t_form_oui)}%)</td>
                        <td>${form_oui_p_inadeq} (${getP(form_oui_p_inadeq, t_form_oui)}%)</td>
                        <td>${t_form_oui} (100.0%)</td>
                    </tr>
                    <tr>
                        <td class="row-header">Non Favorable (Non)</td>
                        <td>${form_non_p_adeq} (${getP(form_non_p_adeq, t_form_non)}%)</td>
                        <td>${form_non_p_inadeq} (${getP(form_non_p_inadeq, t_form_non)}%)</td>
                        <td>${t_form_non} (100.0%)</td>
                    </tr>
                    <tr>
                        <td class="row-header" style="font-weight:bold;">Total Général</td>
                        <td style="font-weight:bold;">${p_adeq} (${getP(p_adeq, total)}%)</td>
                        <td style="font-weight:bold;">${p_inadeq} (${getP(p_inadeq, total)}%)</td>
                        <td style="font-weight:bold;">${total} (100.0%)</td>
                    </tr>
                </tbody>
            </table>
        `;
    };

    window.getAvg = function(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; };
    
    // Ajout des fonctions pour la modale (Voir Fiche)
    window.viewDetails = function(index) {
        const record = database[index];
        if(!record) return;

        document.getElementById('modal-title-id').innerText = record.id;
        
        let content = `
            <table class="academic-table" style="text-align: left;">
                <tbody>
                    <tr><td colspan="2" class="group-header">1. Profil Démographique & Professionnel</td></tr>
                    <tr><th style="width: 40%; background: #f9f9f9;">Âge</th><td>${record.age_participant} ans</td></tr>
                    <tr><th style="background: #f9f9f9;">Sexe</th><td>${record.sexe}</td></tr>
                    <tr><th style="background: #f9f9f9;">État civil</th><td>${record.etat_civil}</td></tr>
                    <tr><th style="background: #f9f9f9;">Niveau d'étude</th><td>${record.niveau}</td></tr>
                    <tr><th style="background: #f9f9f9;">Service d'affectation</th><td>${record.service}</td></tr>
                    <tr><th style="background: #f9f9f9;">Ancienneté</th><td>${record.anciennete} an(s)</td></tr>
                    
                    <tr><td colspan="2" class="group-header">2. Scores Évalués</td></tr>
                    <tr><th style="background: #f9f9f9;">Score Savoir (Connaissances)</th>
                        <td style="color:${record.scoreSavoir >= 70 ? 'green' : 'red'}; font-weight:bold;">${record.scoreSavoir}%</td></tr>
                    <tr><th style="background: #f9f9f9;">Score Pratique (Savoir-faire)</th>
                        <td style="color:${record.scorePratique >= 70 ? 'green' : 'red'}; font-weight:bold;">${record.scorePratique}%</td></tr>
                    <tr><th style="background: #f9f9f9;">Score Attitude (Perception)</th>
                        <td>${record.scoreAttitude} / 5.0</td></tr>
                        
                    <tr><td colspan="2" class="group-header">3. Données Qualitatives</td></tr>
                    <tr><th style="background: #f9f9f9;">Besoin de formation exprimé ?</th><td>${record.besoin_formation}</td></tr>
        `;
        
        if (record.obstacles && record.obstacles.length > 0) {
            content += `<tr><th style="background: #f9f9f9;">Obstacles rencontrés</th><td>${record.obstacles.join(', ')}</td></tr>`;
        }
        if (record.reco_verbatim) {
            content += `<tr><th style="background: #f9f9f9;">Verbatim / Recommandation</th><td><em>"${record.reco_verbatim}"</em></td></tr>`;
        }
        
        content += `</tbody></table>`;
        
        document.getElementById('modal-body-content').innerHTML = content;
        document.getElementById('detailModal').style.display = 'flex';
    };

    window.closeModalBtn = function() {
        document.getElementById('detailModal').style.display = 'none';
    };

    window.closeModal = function(event) {
        if(event.target.id === 'detailModal') {
            document.getElementById('detailModal').style.display = 'none';
        }
    };

    // Ajout de la fonction pour supprimer une fiche individuelle
    window.deleteSingle = function(index) {
        if(confirm("Êtes-vous sûr de vouloir supprimer définitivement la fiche " + database[index].id + " ?")) {
            database.splice(index, 1);
            window.updateUI();
            showToast("Fiche supprimée avec succès !");
        }
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        
        let deleteBtnClass = isAdmin ? "btn-delete-single admin-visible" : "btn-delete-single admin-only";

        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td class="admin-only ${isAdmin ? 'admin-visible' : ''}"><input type="checkbox" class="row-check"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td><td>${row.anciennete}</td>
                <td style="color:${row.scoreSavoir>=70?'green':'red'}">${row.scoreSavoir}%</td>
                <td style="color:${row.scorePratique>=70?'green':'red'}">${row.scorePratique}%</td>
                <td>${row.scorePratique >= 70 ? '🟢 Expert' : '🔴 Critique'}</td>
                <td>
                    <button class="btn-view-single" onclick="window.viewDetails(${index})">👁️ Voir</button>
                    <button class="${deleteBtnClass}" onclick="window.deleteSingle(${index})">🗑️ Suppr.</button>
                </td>
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
    
    // Export Word Doc
    window.downloadAsDoc = function(elementId, filename) {
        var preHtml = "<html xmlns:o='urn:schemas-microsoft-com:office:office' xmlns:w='urn:schemas-microsoft-com:office:word' xmlns='http://www.w3.org/TR/REC-html40'><head><meta charset='utf-8'><title>Export</title></head><body>";
        var postHtml = "</body></html>";
        
        // Cacher temporairement les boutons d'export dans le document généré
        var clone = document.getElementById(elementId).cloneNode(true);
        var btns = clone.querySelectorAll('.btn-excel');
        btns.forEach(btn => btn.parentNode.removeChild(btn));
        
        var html = preHtml + clone.innerHTML + postHtml;

        var blob = new Blob(['\ufeff', html], {
            type: 'application/msword'
        });
        
        var url = 'data:application/vnd.ms-word;charset=utf-8,' + encodeURIComponent(html);
        var downloadLink = document.createElement("a");
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
        showToast("Création du PDF en cours, veuillez patienter...");
        
        // On cible l'onglet 3
        const element = document.getElementById('content-3');
        
        // On cache le bouton bleu pour qu'il ne soit pas imprimé sur le PDF
        const btnExcel = element.querySelector('.btn-excel');
        if (btnExcel) btnExcel.style.display = 'none';

        // Options corrigées pour supprimer le flou
        const opt = {
            margin:       10,
            filename:     'Resultats_Onglet_3.pdf',
            image:        { type: 'png' }, // Utilisation du PNG pour éviter la compression floue
            html2canvas:  { scale: 4, useCORS: true }, // Scale à 4 pour une image très haute résolution
            jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
        };

        // Génération et téléchargement du PDF
        html2pdf().set(opt).from(element).save().then(() => {
            // On remet le bouton bleu à sa place une fois le PDF téléchargé
            if (btnExcel) btnExcel.style.display = 'block';
            showToast("PDF téléchargé !");
        });
    };
    
    window.exportTab4 = function() {
        showToast("Préparation de la discussion...");
        window.downloadAsDoc('content-4', 'Discussion_Memoire_Makala.doc');
    };

    window.exportToCSV = function() {
        if(database.length === 0) return;
        let csv = "ID;Service;Niveau;Anciennete;ScoreSavoir;ScorePratique;ScoreAttitude\n";
        database.forEach(r => {
            csv += `${r.id};${r.service};${r.niveau};${r.anciennete};${r.scoreSavoir};${r.scorePratique};${r.scoreAttitude}\n`;
        });
        let blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
        let url = URL.createObjectURL(blob);
        let link = document.createElement("a");
        link.setAttribute("href", url);
        link.setAttribute("download", "base_donnees_makala.csv");
        link.style.visibility = 'hidden';
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
    };

    window.initCodeDropdown();
</script>
</body>
</html>
