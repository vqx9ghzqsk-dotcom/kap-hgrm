<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR RDC) - Version Admin</title>
    <style>
        /* --- STYLE GLOBAL (INTACT) --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* --- CLASSES POUR LA SÉCURITÉ --- */
        .admin-only { display: none; } 
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}

        /* --- STYLE BOUTONS ACTIONS --- */
        .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; margin-left: 5px; }
        .btn-view-single { background: none; border: 1px solid #0288d1; color: #0288d1; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }
        .btn-delete-single:hover { background: #c62828; color: white; }
        .btn-view-single:hover { background: #0288d1; color: white; }

        /* Contenu */
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections Formulaire */
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }
        textarea { resize: vertical; font-family: inherit; }

        /* Tableaux & Checkboxes */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        
        /* Elements Analyse & Graphiques */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; font-size: 13px; color: #0d47a1; margin-top: 15px; border-radius: 4px; }
        
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}

        /* --- MODAL DÉTAILS --- */
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
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE CROISÉE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. CONCLUSION & RECOMMANDATIONS</button>
        
        <button type="button" class="btn-auth" id="btn-auth" onclick="requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
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
                        <option>A2 (Secondaire)</option>
                        <option>A1 (Gradué)</option>
                        <option>A0 (Licencié/Master)</option>
                    </select>
                </div>
                <div class="field">
                    <label>5. Ancienneté (années)</label>
                    <input type="number" id="anciennete" min="0" placeholder="Ex: 5">
                </div>
                <div class="field">
                    <label>6. Sexe</label>
                    <select id="sexe">
                        <option value="F" selected>F (Féminin)</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS THÉORIQUES)</div>
            
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

            <div class="sub-title">8. Facteurs de risque (Cochez ceux prouvés scientifiquement)</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="multi"> Multiparité (NB: Risque faible/Protecteur)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité et sédentarité</label>
                <label class="check-item"><input type="checkbox" value="allaitement"> Allaitement prolongé (NB: Protecteur)</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive (>55 ans)</label>
            </div>

            <div class="sub-title">9. Signes d’alerte</div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur et indolore</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
                <label class="check-item"><input type="checkbox" value="peau"> Aspect peau d’orange</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                <label class="check-item"><input type="checkbox" value="douleur"> Douleur cyclique (Souvent bénin)</label>
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

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES BRUTE (N = <span id="n-total">0</span>)</div>
        <button id="btn-delete-multi" class="btn-delete-selected" onclick="deleteSelected()">🗑️ Supprimer la sélection</button>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th><input type="checkbox" id="select-all" onclick="toggleSelectAll(this)"></th>
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
        <div class="section-title">1. VUE D'ENSEMBLE DES COMPÉTENCES</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances (Savoir Théorique)</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique Clinique (Savoir-Faire)</div>
                <div id="graph-pratique"></div>
            </div>
        </div>

        <div class="section-title">2. ANALYSE CROISÉE & DIAGRAMMES COMPARATIFS</div>
        <p style="font-size:12px; color:#666;">Comparaison des scores moyens par Service et Niveau d'étude.</p>
        
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Score Moyen Pratique par SERVICE</div>
                <div id="graph-cross-service"></div>
                <div id="interp-service" class="interpretation-box"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Score Moyen Pratique par NIVEAU D'ÉTUDE</div>
                <div id="graph-cross-niveau"></div>
                <div id="interp-niveau" class="interpretation-box"></div>
            </div>
        </div>

        <div class="section-title">3. TABLEAU SYNTHÉTIQUE</div>
        <table style="background:#444; color:white; border-radius:8px; overflow:hidden;">
            <thead>
                <tr>
                    <th style="text-align:left; padding:15px;">Groupe d'analyse</th>
                    <th>Effectif (N)</th>
                    <th>Attitude Moyenne (/5)</th>
                    <th>Score Pratique Moyen (%)</th>
                </tr>
            </thead>
            <tbody id="cross-body" style="background:white; color:#333;"></tbody>
        </table>

        <div class="section-title">4. ANALYSE DES BARRIÈRES À LA PRÉVENTION</div>
        <div id="graph-obstacles-anal"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE AUTOMATISÉE ET RECOMMANDATIONS</div>
        
        <div id="dynamic-report" style="font-size:14px; line-height:1.6; color:#333;">
            </div>

        <br><hr><br>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 TÉLÉCHARGER LA BASE COMPLÈTE (.CSV)</button>
    </div>
</div>

<div id="detailModal" class="modal-overlay" onclick="closeModal(event)">
    <div class="modal-content">
        <div class="modal-header">
            <h3 style="margin:0; color:#b03060;">Détails de la fiche <span id="modal-title-id"></span></h3>
            <span class="modal-close" onclick="closeModalBtn()">&times;</span>
        </div>
        <div id="modal-body-content"></div>
    </div>
</div>

<script>
    // --- 1. INITIALISATION & DONNÉES ---
    let database = JSON.parse(localStorage.getItem('survey_database')) || [];
    let isAdmin = false;

    window.onload = function() {
        initCodeDropdown();
        updateUI(); // Met à jour l'UI mais cache les onglets admin
    };

    function initCodeDropdown() {
        const sel = document.getElementById('code-enquete');
        for(let i=1; i<=200; i++) { 
            let o = document.createElement('option'); 
            o.value = "INF-" + i.toString().padStart(3, '0'); 
            o.text = "Fiche N° " + i; 
            sel.appendChild(o); 
        }
    }

    // --- 2. SÉCURITÉ (Code 1398) ---
    function requestAdmin() {
        if(isAdmin) return; // Déjà connecté
        let code = prompt("Veuillez entrer le code d'accès administrateur :");
        if(code === "1398") {
            isAdmin = true;
            // Affiche les onglets cachés
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            document.getElementById('btn-auth').style.display = 'none'; // Cache le bouton login
            alert("Accès autorisé. Les onglets d'analyse sont maintenant visibles.");
            updateUI();
        } else {
            alert("Code incorrect !");
        }
    }

    // --- 3. ENREGISTREMENT ---
    function saveRecord() {
        let r = {
            id: document.getElementById('code-enquete').value,
            consentement: document.getElementById('consentement').value, // Ajout Consentement
            service: document.getElementById('service').value,
            niveau: document.getElementById('niveau').value,
            anciennete: document.getElementById('anciennete').value,
            sexe: document.getElementById('sexe').value,
            q_cause: document.getElementById('q-cause').value,
            q_age: document.getElementById('q-age-mammo').value,
            q_aes: document.getElementById('q-moment-aes').value,
            risques: getCheckedValues('group-risques'),
            signes: getCheckedValues('group-signes'),
            mammo_role: document.getElementById('q-mammo-role').value,
            mammo_freq: document.getElementById('q-mammo-freq').value,
            att1: parseInt(getRadioValue('att1')),
            att2: parseInt(getRadioValue('att2')),
            att3: parseInt(getRadioValue('att3')),
            att4: parseInt(getRadioValue('att4')), 
            att5: parseInt(getRadioValue('att5')), 
            prac_perso: document.getElementById('prac-perso').value,
            prac_freq: document.getElementById('prac-pro-freq').value,
            prac_main: document.getElementById('prac-main').value,
            prac_zone: document.getElementById('prac-zone').value,
            prac_mouv: getCheckedValues('group-mouv'),
            obstacles: getCheckedValues('group-obstacles'),
            reco_verbatim: document.getElementById('reco-verbatim').value // Ajout Recommandations
        };

        // Calculs Scores (Intacts)
        let ptsS = (r.q_cause === "vrai" ? 1 : 0) + (r.q_age !== "20" ? 1 : 0) + (r.q_aes === "apres" ? 1 : 0);
        ['age', 'famille', 'alcool', 'obesite', 'menopause'].forEach(k => { if(r.risques.includes(k)) ptsS++; });
        ['nodule', 'retraction', 'peau', 'ecoulement'].forEach(k => { if(r.signes.includes(k)) ptsS++; });
        if(r.mammo_role === "detecter") ptsS += 2;
        if(r.mammo_freq === "2") ptsS += 1;
        r.scoreSavoir = Math.round((ptsS / 15) * 100);

        let sumAtt = r.att1 + r.att2 + r.att3 + (6-r.att4) + (6-r.att5);
        r.scoreAttitude = (sumAtt / 5).toFixed(1);

        let ptsP = (r.prac_perso === "mois" ? 3 : 0) + (r.prac_freq === "syst" ? 5 : 0);
        if(r.prac_main === "pulpe") ptsP += 4;
        if(r.prac_zone === "axillaire") ptsP += 4;
        let mv = r.prac_mouv.filter(m => ['circulaire', 'vertical', 'radial'].includes(m)).length;
        ptsP += (mv >= 2 ? 4 : (mv === 1 ? 2 : 0));
        r.scorePratique = Math.round((ptsP / 20) * 100);

        database.push(r);
        localStorage.setItem('survey_database', JSON.stringify(database));
        
        alert(`Fiche ${r.id} enregistrée avec succès !`);
        document.getElementById('kapForm').reset();
        document.getElementById('code-enquete').selectedIndex = (database.length) % 200;
        // Reset manuel du sexe à F
        document.getElementById('sexe').value = "F";
        updateUI();
    }

    // --- 4. GESTION SUPPRESSION & VUE DÉTAILS ---
    function deleteOne(index) {
        if(confirm("Supprimer cette fiche ?")) {
            database.splice(index, 1);
            saveAndRefresh();
        }
    }

    function viewDetails(index) {
        let d = database[index];
        document.getElementById('modal-title-id').innerText = d.id;
        
        // Construction du HTML des détails
        let html = `
            <div class="sub-title">IDENTITÉ</div>
            <div class="detail-row"><span class="detail-label">Consentement</span><span class="detail-val">${d.consentement}</span></div>
            <div class="detail-row"><span class="detail-label">Service</span><span class="detail-val">${d.service}</span></div>
            <div class="detail-row"><span class="detail-label">Niveau</span><span class="detail-val">${d.niveau}</span></div>
            <div class="detail-row"><span class="detail-label">Ancienneté</span><span class="detail-val">${d.anciennete} ans</span></div>

            <div class="sub-title">SCORES</div>
            <div class="detail-row"><span class="detail-label">Score Savoir</span><span class="detail-val">${d.scoreSavoir}%</span></div>
            <div class="detail-row"><span class="detail-label">Score Pratique</span><span class="detail-val">${d.scorePratique}%</span></div>

            <div class="sub-title">RÉPONSES DÉTAILLÉES</div>
            <div class="detail-row"><span class="detail-label">Facteurs Risque Cochés</span><span class="detail-val">${d.risques.join(', ') || 'Aucun'}</span></div>
            <div class="detail-row"><span class="detail-label">Signes Alerte Cochés</span><span class="detail-val">${d.signes.join(', ') || 'Aucun'}</span></div>
            <div class="detail-row"><span class="detail-label">Obstacles Cités</span><span class="detail-val">${d.obstacles.join(', ') || 'Aucun'}</span></div>
            
            <div class="sub-title">RECOMMANDATIONS DE L'ENQUÊTÉE</div>
            <div class="detail-val-long">${d.reco_verbatim || "Aucune suggestion."}</div>
        `;
        
        document.getElementById('modal-body-content').innerHTML = html;
        document.getElementById('detailModal').style.display = 'flex';
    }

    function closeModal(e) { if(e.target.id === 'detailModal') document.getElementById('detailModal').style.display = 'none'; }
    function closeModalBtn() { document.getElementById('detailModal').style.display = 'none'; }

    function toggleSelectAll(source) {
        document.querySelectorAll('.row-check').forEach(cb => cb.checked = source.checked);
        toggleDeleteButton();
    }
    function toggleDeleteButton() {
        const checked = document.querySelectorAll('.row-check:checked').length;
        document.getElementById('btn-delete-multi').style.display = checked > 0 ? 'block' : 'none';
    }
    function deleteSelected() {
        if(confirm("Supprimer les fiches sélectionnées ?")) {
            const checkboxes = Array.from(document.querySelectorAll('.row-check'));
            database = database.filter((_, index) => !checkboxes[index].checked);
            saveAndRefresh();
        }
    }
    function saveAndRefresh() {
        localStorage.setItem('survey_database', JSON.stringify(database));
        updateUI();
    }

    // --- 5. UI & ANALYTIQUES AVANCÉES ---
    function updateUI() {
        const count = database.length;
        document.getElementById('count-badge').textContent = count;
        document.getElementById('n-total').textContent = count;
        document.getElementById('select-all').checked = false;
        toggleDeleteButton();

        // MATRICE
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check" onclick="toggleDeleteButton()"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td><td>${row.anciennete}</td>
                <td style="color:${getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td style="color:${getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td>${row.scoreSavoir >= 70 && row.scorePratique >= 70 ? '🟢 Expert' : '🟠 Moyen'}</td>
                <td>
                    <button class="btn-view-single" onclick="viewDetails(${index})">👁️ Voir</button>
                    <button class="btn-delete-single" onclick="deleteOne(${index})">Effacer</button>
                </td>
            </tr>
        `).join('');

        if(isAdmin) updateAnalytics();
    }

    function updateAnalytics() {
        if(database.length === 0) return;

        // --- A. Graphiques Simples ---
        let highS = database.filter(r => r.scoreSavoir >= 60);
        let lowS = database.filter(r => r.scoreSavoir < 60);
        renderBars('graph-savoir', [
            {l: 'Connaissances Solides', v: highS.length, t: database.length, c: '#2e7d32'},
            {l: 'Lacunes Importantes', v: lowS.length, t: database.length, c: '#c62828'}
        ]);

        let highP = database.filter(r => r.scorePratique >= 70).length;
        renderBars('graph-pratique', [
            {l: 'Pratique Conforme', v: highP, t: database.length, c: '#1565c0'},
            {l: 'Pratique Insuffisante', v: database.length - highP, t: database.length, c: '#f57f17'}
        ]);

        // --- B. Analyses Croisées (Nouveaux Graphiques) ---
        // Par Service
        let services = ["Gynécologie-Obstétrique", "Médecine Interne", "Chirurgie", "Urgences / Autre"];
        let serviceData = services.map(s => {
            let group = database.filter(r => r.service === s);
            return { l: s, v: Math.round(getAvg(group, 'scorePratique')), t: 100, c: '#8e24aa' };
        });
        renderBars('graph-cross-service', serviceData);
        // Interprétation dynamique Service
        let bestS = serviceData.reduce((prev, curr) => prev.v > curr.v ? prev : curr);
        document.getElementById('interp-service').innerHTML = `💡 <b>Analyse :</b> Le service <b>${bestS.l}</b> présente la meilleure performance pratique avec une moyenne de ${bestS.v}%.`;

        // Par Niveau
        let niveaux = ["A2 (Secondaire)", "A1 (Gradué)", "A0 (Licencié/Master)"];
        let niveauData = niveaux.map(n => {
            let group = database.filter(r => r.niveau === n);
            return { l: n, v: Math.round(getAvg(group, 'scorePratique')), t: 100, c: '#00897b' };
        });
        renderBars('graph-cross-niveau', niveauData);

        // --- C. Obstacles ---
        let obsMap = {};
        database.forEach(r => r.obstacles.forEach(o => obsMap[o] = (obsMap[o]||0)+1));
        document.getElementById('graph-obstacles-anal').innerHTML = Object.entries(obsMap).sort((a,b)=>b[1]-a[1]).map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
        }).join('');

        // --- D. Tableau Croisé Global ---
        let avgAttH = getAvg(highS, 'scoreAttitude'), avgPracH = getAvg(highS, 'scorePratique');
        let avgAttL = getAvg(lowS, 'scoreAttitude'), avgPracL = getAvg(lowS, 'scorePratique');
        document.getElementById('cross-body').innerHTML = `
            <tr><td style="padding:15px;">Bonnes Connaissances</td><td>${highS.length}</td><td>${avgAttH}</td><td>${avgPracH}%</td></tr>
            <tr><td style="padding:15px;">Connaissances Faibles</td><td>${lowS.length}</td><td>${avgAttL}</td><td>${avgPracL}%</td></tr>
        `;

        generateDynamicReport(highP, obsMap);
    }

    // --- 6. GÉNÉRATEUR DE CONCLUSION AUTOMATIQUE ---
    function generateDynamicReport(goodPracticeCount, obsMap) {
        let total = database.length;
        let pPractice = Math.round((goodPracticeCount/total)*100);
        let topObstacle = Object.keys(obsMap).sort((a,b) => obsMap[b]-obsMap[a])[0] || "Aucun";

        let report = `<p>Sur un total de <b>${total} participants</b>, l'analyse en temps réel révèle que <b>${pPractice}%</b> du personnel possède une maîtrise pratique satisfaisante de l'examen clinique des seins.</p>`;
        
        // Recommandations dynamiques
        let recs = "";
        if(pPractice < 50) {
            recs += `<div class="reco-box"><div class="reco-title">🔴 PRIORITÉ : FORMATION PRATIQUE</div>Le niveau de compétence pratique est critique (< 50%). Il est urgent d'organiser des ateliers de simulation sur mannequins.</div>`;
        } else {
            recs += `<div class="reco-box"><div class="reco-title">🟢 MAINTIEN DES ACQUIS</div>Le niveau pratique est encourageant. Instaurer un mentorat par les pairs pour maintenir ces acquis.</div>`;
        }

        if(topObstacle === "Temps") {
            recs += `<div class="reco-box"><div class="reco-title">🟠 ORGANISATION DU TRAVAIL</div>Le manque de temps est l'obstacle majeur. Recommandation : Intégrer le dépistage dans la fiche de prise de paramètres vitaux systématiques.</div>`;
        } else if (topObstacle === "Formation") {
             recs += `<div class="reco-box"><div class="reco-title">🔵 BESOIN COGNITIF</div>Le personnel réclame plus de formation. Distribuer des aides-mémoires visuels dans les services.</div>`;
        }

        document.getElementById('dynamic-report').innerHTML = report + recs;
    }

    // --- UTILITAIRES (Intacts) ---
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); }
    function getRadioValue(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e ? e.value : 0; }
    function getColor(s) { return s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828'); }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; }
    function renderBars(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.t ? Math.round((i.v/i.t)*100) : 0; // Si t=100 alors v est déjà %
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div><div class="bar-value">${i.v}</div></div>`;
        }).join('');
    }
    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }
    function exportToCSV() {
        // Mise à jour de l'export pour inclure Consentement et Recommandations
        let h = "ID,Consentement,Sexe,Service,Savoir(%),Attitude(/5),Pratique(%),Recommandations\n";
        let r = database.map(r => {
            // Échapper les guillemets et sauts de ligne dans le verbatim
            let cleanReco = (r.reco_verbatim || "").replace(/"/g, '""').replace(/(\r\n|\n|\r)/gm, " ");
            return `${r.id},${r.consentement},${r.sexe},${r.service},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique},"${cleanReco}"`;
        }).join("\n");
        let l = document.createElement("a");
        l.href = "data:text/csv;charset=utf-8," + encodeURI("\ufeff"+h+r);
        l.download = "Rapport_CAP_Cancer_RDC.csv"; l.click();
    }
</script>
</body>
</html>
