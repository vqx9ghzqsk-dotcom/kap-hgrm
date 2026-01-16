<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR RDC)</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; flex-wrap: wrap;}
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* Boutons Actions */
        .actions-group { margin-left: auto; display: flex; gap: 5px; }
        .btn-excel { background: #2e7d32; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 11px; }
        .btn-backup { background: #1976d2; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 11px; }
        .btn-import { background: #f57f17; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 11px; }
        
        /* Suppression */
        .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }
        .btn-delete-single:hover { background: #c62828; color: white; }

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
        select, input[type="text"], input[type="number"] { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        /* Tableaux */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        /* Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        /* Bouton Enregistrer */
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        
        /* Analyse & Graphiques Avancés */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #333; margin-bottom: 15px; font-size: 15px; border-bottom: 2px solid #b03060; display: inline-block; padding-bottom: 5px; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 15px; font-size: 12px; }
        .bar-label { width: 200px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #eee; height: 24px; border-radius: 4px; margin: 0 15px; overflow: hidden; position: relative; box-shadow: inset 0 1px 3px rgba(0,0,0,0.1); }
        .bar-fill { height: 100%; display: flex; align-items: center; padding-left: 10px; color: white; font-size: 11px; font-weight: bold; transition: width 1s ease-in-out; text-shadow: 0 1px 2px rgba(0,0,0,0.3); }
        .bar-value { width: 50px; text-align: right; font-weight: bold; color: #b03060; font-size: 14px; }

        /* Statistique Chi-2 */
        .chi2-box { background: #f3e5f5; border: 1px solid #ba68c8; border-radius: 8px; padding: 20px; margin-top: 20px; }
        .chi2-result { font-size: 18px; font-weight: bold; color: #6a1b9a; margin-bottom: 10px; }
        .chi2-explain { font-size: 13px; color: #4a148c; line-height: 1.5; }
        .signif { color: #2e7d32; font-weight: bold; }
        .not-signif { color: #c62828; font-weight: bold; }

        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. ANALYSE & CHI-CARRÉ</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
        
        <div class="actions-group">
            <input type="file" id="fileImport" style="display: none;" onchange="importData(this)">
            <button type="button" class="btn-import" onclick="document.getElementById('fileImport').click()">📂 IMPORTER</button>
            <button type="button" class="btn-backup" onclick="exportFullBackup()">💾 SAUVEGARDE COMPLÈTE</button>
            <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
        </div>
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
                    <label>2. Service d'affectation</label>
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
                    <label>3. Niveau d'étude</label>
                    <select id="niveau">
                        <option value="" disabled selected>Niveau...</option>
                        <option>A2 (Secondaire)</option>
                        <option>A1 (Gradué)</option>
                        <option>A0 (Licencié/Master)</option>
                    </select>
                </div>
                <div class="field">
                    <label>4. Ancienneté (années)</label>
                    <input type="number" id="anciennete" min="0" placeholder="Ex: 5">
                </div>
                <div class="field">
                    <label>5. Sexe</label>
                    <select id="sexe">
                        <option value="" disabled selected>Sexe...</option>
                        <option>F (Féminin)</option>
                        <option>M (Masculin)</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES (SAVOIRS THÉORIQUES)</div>
            
            <div class="sub-title">6. Épidémiologie & Dépistage</div>
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

            <div class="sub-title">7. Facteurs de risque (Cochez ceux prouvés scientifiquement)</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="multi"> Multiparité (NB: Risque faible/Protecteur)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité et sédentarité</label>
                <label class="check-item"><input type="checkbox" value="allaitement"> Allaitement prolongé (NB: Protecteur)</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive (>55 ans)</label>
            </div>

            <div class="sub-title">8. Signes d’alerte</div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur et indolore</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
                <label class="check-item"><input type="checkbox" value="peau"> Aspect peau d’orange</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                <label class="check-item"><input type="checkbox" value="douleur"> Douleur cyclique (Souvent bénin)</label>
            </div>

            <div class="sub-title">9-13. Connaissance Mammographie</div>
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
                    <label>9. Pratique personnelle (AES sur vous) :</label>
                    <select id="prac-perso">
                        <option value="" disabled selected>Fréquence...</option>
                        <option value="mois">Tous les mois</option>
                        <option value="temps">De temps en temps</option>
                        <option value="jamais">Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>10. Examen des patientes (Fréquence) :</label>
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
                        <th>Score Savoir (%)</th><th>Score Attitude (/5)</th><th>Score Pratique (%)</th>
                        <th>Diagnostic</th><th>Action</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. RÉPARTITION DES NIVEAUX (GRAPHIQUES)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique</div>
                <div id="graph-pratique"></div>
            </div>
        </div>

        <div class="section-title">2. ASSOCIATION STATISTIQUE (TEST DU CHI-CARRÉ)</div>
        <div class="stat-card">
            <p style="font-size:13px; color:#555;">Nous testons l'hypothèse d'une association entre <b>Avoir de bonnes connaissances (>=60%)</b> et <b>Avoir une bonne pratique (>=60%)</b>.</p>
            <div id="chi-square-results"></div>
        </div>

        <div class="section-title">3. TABLEAU DE CONTINGENCE 2x2</div>
        <table style="background:#444; color:white; border-radius:8px; overflow:hidden;">
            <thead>
                <tr>
                    <th style="text-align:left; padding:15px;">Croisement</th>
                    <th>Bonnes Pratiques</th>
                    <th>Mauvaises Pratiques</th>
                    <th>Total</th>
                </tr>
            </thead>
            <tbody id="contingency-body" style="background:white; color:#333;"></tbody>
        </table>

        <div class="section-title">4. ANALYSE DES BARRIÈRES</div>
        <div id="graph-obstacles-anal"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
        <div id="final-conclusion" style="font-size:15px; line-height:1.8; color:#333;"></div>
        <br><hr><br>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 TÉLÉCHARGER LA BASE COMPLÈTE (.CSV)</button>
    </div>
</div>

<script>
    // --- 1. INITIALISATION ---
    let database = JSON.parse(localStorage.getItem('survey_database')) || [];

    window.onload = function() {
        initCodeDropdown();
        updateUI();
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

    // --- 2. FONCTIONS IMPORT / EXPORT (NOUVEAU) ---
    function importData(input) {
        let file = input.files[0];
        if (!file) return;
        let reader = new FileReader();
        reader.onload = function(e) {
            try {
                // Essai d'import JSON (Format complet)
                let importedData = JSON.parse(e.target.result);
                if (Array.isArray(importedData)) {
                    if(confirm("Vous allez importer " + importedData.length + " fiches. Cela ajoutera aux données existantes.")) {
                        database = database.concat(importedData);
                        saveAndRefresh();
                        alert("Importation réussie !");
                    }
                } else {
                    alert("Format JSON invalide. Essayez d'importer le fichier de sauvegarde (.json).");
                }
            } catch (error) {
                // Si échec JSON, tentative CSV (Mode dégradé)
                alert("Tentative d'import CSV (Mode partiel)...");
                parseCSVImport(e.target.result);
            }
        };
        reader.readAsText(file);
        input.value = ''; // Reset
    }

    function parseCSVImport(csvText) {
        // Import simple pour restaurer les scores si l'utilisateur n'a que le CSV
        let lines = csvText.split('\n');
        let importedCount = 0;
        for(let i=1; i<lines.length; i++) { // Sauter header
            let cols = lines[i].split(',');
            if(cols.length >= 6) { // Vérif minimale
                let r = {
                    id: cols[0], sexe: cols[1], service: cols[2], 
                    scoreSavoir: parseFloat(cols[3]), scoreAttitude: parseFloat(cols[4]), scorePratique: parseFloat(cols[5]),
                    risques: [], signes: [], obstacles: [] // Données perdues en CSV simple
                };
                database.push(r);
                importedCount++;
            }
        }
        if(importedCount > 0) {
            saveAndRefresh();
            alert(importedCount + " fiches récupérées depuis le CSV ! (Note: Les détails des cases cochées sont absents du CSV simple)");
        } else {
            alert("Impossible de lire le fichier. Assurez-vous d'utiliser un fichier généré par cette application.");
        }
    }

    function exportFullBackup() {
        // Exporte TOUT (JSON) pour une restauration parfaite
        let dataStr = JSON.stringify(database, null, 2);
        let link = document.createElement("a");
        link.href = "data:text/json;charset=utf-8," + encodeURIComponent(dataStr);
        link.download = "SAUVEGARDE_COMPLETE_CAP_" + new Date().toISOString().slice(0,10) + ".json";
        link.click();
    }

    // --- 3. ENREGISTREMENT ---
    function saveRecord() {
        let r = {
            id: document.getElementById('code-enquete').value,
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
            obstacles: getCheckedValues('group-obstacles')
        };

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

        // Synchro Google (Silencieuse)
        const url = "https://script.google.com/macros/s/AKfycbwQPk3CAUYV75xr-JdLk-NqgwRyIlcqnZCvTL_OdH0bO5fCoza_U4qtapwsr_UZc11ENQ/exec";
        fetch(url, { method: "POST", mode: "no-cors", cache: "no-cache", body: JSON.stringify(r) }).catch(e=>console.log(e));

        database.push(r);
        saveAndRefresh();
        
        alert(`Fiche ${r.id} enregistrée avec succès !`);
        // Reset manuel pour que l'utilisateur saisisse à nouveau
        document.getElementById('kapForm').reset();
        document.getElementById('code-enquete').selectedIndex = (database.length) % 200;
        // On remet les selects à la valeur par défaut
        document.querySelectorAll('select').forEach(s => s.selectedIndex = 0);
    }

    // --- 4. GESTION DONNÉES ---
    function deleteOne(index) {
        if(confirm("Supprimer cette fiche ?")) {
            database.splice(index, 1);
            saveAndRefresh();
        }
    }
    function toggleSelectAll(source) {
        document.querySelectorAll('.row-check').forEach(cb => cb.checked = source.checked);
        toggleDeleteButton();
    }
    function toggleDeleteButton() {
        document.getElementById('btn-delete-multi').style.display = document.querySelectorAll('.row-check:checked').length > 0 ? 'block' : 'none';
    }
    function deleteSelected() {
        if(confirm("Confirmer la suppression ?")) {
            const checkboxes = Array.from(document.querySelectorAll('.row-check'));
            database = database.filter((_, index) => !checkboxes[index].checked);
            saveAndRefresh();
        }
    }
    function saveAndRefresh() {
        localStorage.setItem('survey_database', JSON.stringify(database));
        updateUI();
    }

    // --- 5. INTERFACE & GRAPHIQUES ---
    function updateUI() {
        const count = database.length;
        document.getElementById('count-badge').textContent = count;
        document.getElementById('n-total').textContent = count;
        document.getElementById('select-all').checked = false;
        toggleDeleteButton();

        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check" onclick="toggleDeleteButton()"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td><td>${row.anciennete}</td>
                <td style="color:${getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td>${row.scoreAttitude}</td>
                <td style="color:${getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td>${row.scoreSavoir >= 70 && row.scorePratique >= 70 ? '🟢 Expert' : '🟠 Moyen'}</td>
                <td><button class="btn-delete-single" onclick="deleteOne(${index})">Effacer</button></td>
            </tr>
        `).join('');

        updateAnalytics();
    }

    function updateAnalytics() {
        if(database.length === 0) {
            document.getElementById('graph-savoir').innerHTML = "<p>Aucune donnée.</p>";
            document.getElementById('chi-square-results').innerHTML = "";
            return;
        }

        // Groupes
        let highS = database.filter(r => r.scoreSavoir >= 60);
        let lowS = database.filter(r => r.scoreSavoir < 60);
        
        // Graphiques
        renderBars('graph-savoir', [
            {l: 'Connaissances Solides (>=60%)', v: highS.length, t: database.length, c: '#2e7d32'},
            {l: 'Connaissances Faibles (<60%)', v: lowS.length, t: database.length, c: '#c62828'}
        ]);

        let highP = database.filter(r => r.scorePratique >= 60).length;
        renderBars('graph-pratique', [
            {l: 'Pratique Correcte (>=60%)', v: highP, t: database.length, c: '#1565c0'},
            {l: 'Pratique Insuffisante (<60%)', v: database.length - highP, t: database.length, c: '#f57f17'}
        ]);

        // STATISTIQUES CHI-CARRÉ (2x2)
        // Table:
        //          | Bon Prat | Mauv Prat | Total
        // Bon Sav  |    a     |     b     | a+b
        // Mauv Sav |    c     |     d     | c+d
        
        let a = highS.filter(r => r.scorePratique >= 60).length;
        let b = highS.filter(r => r.scorePratique < 60).length;
        let c = lowS.filter(r => r.scorePratique >= 60).length;
        let d = lowS.filter(r => r.scorePratique < 60).length;
        let total = database.length;

        // Affichage Tableau Contingence
        document.getElementById('contingency-body').innerHTML = `
            <tr><td><b>Bonnes Connaissances</b></td><td>${a}</td><td>${b}</td><td>${a+b}</td></tr>
            <tr><td><b>Mauvaises Connaissances</b></td><td>${c}</td><td>${d}</td><td>${c+d}</td></tr>
            <tr style="background:#eee; font-weight:bold;"><td>Total</td><td>${a+c}</td><td>${b+d}</td><td>${total}</td></tr>
        `;

        // Calcul Chi2
        // Formule simplifiée (sans correction Yates pour l'instant pour lisibilité)
        // Chi2 = N * (ad - bc)^2 / [(a+b)(c+d)(a+c)(b+d)]
        let numerator = total * Math.pow(Math.abs(a*d - b*c), 2);
        let denominator = (a+b) * (c+d) * (a+c) * (b+d);
        let chi2 = denominator > 0 ? (numerator / denominator) : 0;
        let significant = chi2 > 3.841; // Pour ddl=1, alpha=0.05

        let msg = significant 
            ? `<span class="signif">OUI, l'association est significative (p < 0.05).</span><br>Cela signifie que le niveau de connaissances influence statistiquement la qualité de la pratique.` 
            : `<span class="not-signif">NON, pas de lien significatif (p > 0.05).</span><br>Les connaissances théoriques ne semblent pas garantir une meilleure pratique dans cet échantillon.`;

        document.getElementById('chi-square-results').innerHTML = `
            <div class="chi2-box">
                <div class="chi2-result">Chi² = ${chi2.toFixed(3)}</div>
                <div class="chi2-explain">${msg}</div>
            </div>
        `;

        // Obstacles
        let obsMap = {};
        if(database.length > 0 && database[0].obstacles) {
             database.forEach(r => { if(r.obstacles) r.obstacles.forEach(o => obsMap[o] = (obsMap[o]||0)+1) });
             document.getElementById('graph-obstacles-anal').innerHTML = Object.entries(obsMap).sort((a,b)=>b[1]-a[1]).map(([k,v]) => {
                let p = Math.round((v/database.length)*100);
                return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
            }).join('');
        }
    }

    // --- UTILITAIRES ---
    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); }
    function getRadioValue(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e ? e.value : 0; }
    function getColor(s) { return s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828'); }
    function renderBars(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.t ? Math.round((i.v/i.t)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${i.v} (${p}%)</div></div></div>`;
        }).join('');
    }
    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }
    function exportToCSV() {
        if(database.length === 0) { alert("Rien à exporter"); return; }
        let h = "ID,Sexe,Service,Savoir(%),Attitude(/5),Pratique(%)\n";
        let r = database.map(r => `${r.id},${r.sexe},${r.service},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let l = document.createElement("a");
        l.href = "data:text/csv;charset=utf-8," + encodeURI("\ufeff"+h+r);
        l.download = "Rapport_CAP_Cancer.csv"; l.click();
    }
</script>
</body>
</html>
