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
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel:hover { background: #1b5e20; }

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

        /* Tableaux Likert */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; vertical-align: middle; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        /* Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        /* Bouton Action */
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        
        /* Elements Analyse */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .interpretation-box { background: #e8f5e9; border-left: 5px solid #2e7d32; padding: 20px; font-style: italic; color: #1b5e20; margin-top: 20px; border-radius: 0 8px 8px 0; }
        .alert-box { background: #ffebee; border-left: 5px solid #c62828; padding: 20px; font-style: italic; color: #b71c1c; margin-top: 20px; border-radius: 0 8px 8px 0; }
        
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE CROISÉE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION & SYNTHÈSE</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
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
                        <option>A2 (Secondaire)</option>
                        <option selected>A1 (Gradué)</option>
                        <option>A0 (Licencié/Master)</option>
                    </select>
                </div>
                <div class="field">
                    <label>4. Ancienneté (années)</label>
                    <input type="number" id="anciennete" min="0" value="5">
                </div>
                <div class="field">
                    <label>5. Sexe</label>
                    <select id="sexe">
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
                        <option value="vrai">Vrai</option>
                        <option value="faux">Faux</option>
                        <option value="jsp">Je ne sais pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Âge recommandé 1ère mammographie :</label>
                    <select id="q-age-mammo">
                        <option value="20">Dès 20 ans</option>
                        <option value="35">Vers 35-40 ans</option>
                        <option value="50">Vers 50 ans</option>
                    </select>
                </div>
                <div class="field">
                    <label>Moment idéal pour Auto-Examen (AES) :</label>
                    <select id="q-moment-aes">
                        <option value="regles">Pendant les règles</option>
                        <option value="apres" selected>7 à 10 jours après début règles</option>
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
                    <select id="q-mammo-imp"><option>Oui</option><option>Non</option><option>Je ne sais pas</option></select>
                </div>
                <div class="field">
                    <label>Rôle principal :</label>
                    <select id="q-mammo-role">
                        <option value="detecter">Détecter lésions avant symptômes</option>
                        <option value="traiter">Traiter le cancer</option>
                        <option value="douleur">Soulager douleur</option>
                    </select>
                </div>
                <div class="field">
                    <label>Fréquence (Femme sans risque) :</label>
                    <select id="q-mammo-freq">
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
                        <td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5" checked></td>
                    </tr>
                    <tr>
                        <td class="td-left">Je me sens capable de détecter un nodule de petite taille.</td>
                        <td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4" checked></td><td><input type="radio" name="att2" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">La peur du diagnostic empêche les patientes de consulter.</td>
                        <td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3" checked></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">Je suis mal à l’aise d’aborder l’intimité avec les âgées.</td>
                        <td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2" checked></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td>
                    </tr>
                    <tr>
                        <td class="td-left">Le dépistage ne sert à rien (coût des traitements).</td>
                        <td><input type="radio" name="att5" value="1" checked></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td>
                    </tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (Savoir-Faire)</div>
            
            <div class="row">
                <div class="field">
                    <label>9. Pratique personnelle (AES sur vous) :</label>
                    <select id="prac-perso">
                        <option value="mois">Tous les mois</option>
                        <option value="temps">De temps en temps</option>
                        <option value="jamais">Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>10. Examen des patientes (Fréquence) :</label>
                    <select id="prac-pro-freq">
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
                        <option value="pointe">La pointe des doigts</option>
                        <option value="pulpe" selected>La pulpe des 3 doigts du milieu</option>
                        <option value="paume">La paume entière</option>
                        <option value="pince">Le pouce et l'index</option>
                    </select>
                </div>
                <div class="field">
                    <label>Zone "oubliée" à inclure absolument ?</label>
                    <select id="prac-zone">
                        <option value="mamelon">Le mamelon</option>
                        <option value="sillon">Le sillon sous-mammaire</option>
                        <option value="axillaire" selected>Le creux axillaire (aisselle)</option>
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
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th>Code</th><th>Sexe</th><th>Service</th><th>Exp (ans)</th>
                        <th>Score Savoir (%)</th><th>Score Attitude (/5)</th><th>Score Pratique (%)</th>
                        <th>Diagnostic Compétence</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. RÉPARTITION DES NIVEAUX DE COMPÉTENCE</div>
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

        <div class="section-title">2. ANALYSE CROISÉE : IMPACT DU SAVOIR SUR L'ACTION</div>
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

        <div id="interpretation-cross"></div>

        <div class="section-title">3. ANALYSE DES BARRIÈRES À LA PRÉVENTION</div>
        <div id="graph-obstacles"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
        <div id="final-conclusion" style="font-size:15px; line-height:1.8; color:#333;"></div>
        <br><hr><br>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📥 TÉLÉCHARGER LA BASE COMPLÈTE (.CSV)</button>
    </div>
</div>

<script>
    let database = [];

    // --- INITIALISATION DES LISTES DÉROULANTES ---
    const codeSel = document.getElementById('code-enquete');
    for(let i=1; i<=200; i++) { 
        let o=document.createElement('option'); 
        o.value="INF-"+i.toString().padStart(3, '0'); 
        o.text="Fiche N° "+i; 
        codeSel.appendChild(o); 
    }

    // --- FONCTION PRINCIPALE D'ENREGISTREMENT ---
    function saveRecord() {
        // 1. Récupération des données brutes du nouveau formulaire
        let r = {
            id: document.getElementById('code-enquete').value,
            service: document.getElementById('service').value,
            niveau: document.getElementById('niveau').value,
            anciennete: document.getElementById('anciennete').value,
            sexe: document.getElementById('sexe').value,
            
            // Connaissances
            q_cause: document.getElementById('q-cause').value,
            q_age: document.getElementById('q-age-mammo').value,
            q_aes: document.getElementById('q-moment-aes').value,
            risques: getCheckedValues('group-risques'),
            signes: getCheckedValues('group-signes'),
            mammo_role: document.getElementById('q-mammo-role').value,
            mammo_freq: document.getElementById('q-mammo-freq').value,

            // Attitudes (Likert)
            att1: parseInt(getRadioValue('att1')),
            att2: parseInt(getRadioValue('att2')),
            att3: parseInt(getRadioValue('att3')),
            att4: parseInt(getRadioValue('att4')), 
            att5: parseInt(getRadioValue('att5')), 

            // Pratiques
            prac_perso: document.getElementById('prac-perso').value,
            prac_freq: document.getElementById('prac-pro-freq').value,
            prac_main: document.getElementById('prac-main').value,
            prac_zone: document.getElementById('prac-zone').value,
            prac_mouv: getCheckedValues('group-mouv'),

            // Obstacles
            obstacles: getCheckedValues('group-obstacles')
        };

        // 2. CALCUL DES SCORES
        let ptsSavoir = 0;
        let maxSavoir = 15; 
        if(r.q_cause === "vrai") ptsSavoir += 1;
        if(r.q_age === "50" || r.q_age === "35") ptsSavoir += 1; 
        if(r.q_aes === "apres") ptsSavoir += 1;
        let riskPoints = 0;
        ['age', 'famille', 'alcool', 'obesite', 'menopause'].forEach(k => { if(r.risques.includes(k)) riskPoints++; });
        ptsSavoir += riskPoints;
        let signPoints = 0;
        ['nodule', 'retraction', 'peau', 'ecoulement'].forEach(k => { if(r.signes.includes(k)) signPoints++; });
        ptsSavoir += signPoints;
        if(r.mammo_role === "detecter") ptsSavoir += 2;
        if(r.mammo_freq === "2") ptsSavoir += 1;
        r.scoreSavoir = Math.round((ptsSavoir / maxSavoir) * 100);

        let invAtt4 = 6 - r.att4;
        let invAtt5 = 6 - r.att5;
        let sumAtt = r.att1 + r.att2 + r.att3 + invAtt4 + invAtt5;
        r.scoreAttitude = (sumAtt / 5).toFixed(1);

        let ptsPrac = 0;
        let maxPrac = 20;
        if(r.prac_perso === "mois") ptsPrac += 3; 
        if(r.prac_freq === "syst") ptsPrac += 5; 
        else if(r.prac_freq === "plainte") ptsPrac += 1;
        if(r.prac_main === "pulpe") ptsPrac += 4; 
        if(r.prac_zone === "axillaire") ptsPrac += 4; 
        let validMoves = ['circulaire', 'vertical', 'radial'];
        let movesCount = 0;
        r.prac_mouv.forEach(m => { if(validMoves.includes(m)) movesCount++; });
        if(r.prac_mouv.includes('aleatoire')) movesCount = 0; 
        if(movesCount >= 2) ptsPrac += 4;
        else if(movesCount === 1) ptsPrac += 2;
        r.scorePratique = Math.round((ptsPrac / maxPrac) * 100);

        // AJOUT DE L'ENVOI VERS GOOGLE SHEETS
        const webAppUrl = https://script.google.com/macros/s/AKfycbyDsuYQ8DMEpHkTxQorlVHKf5T63O9_QRHdXQhO0X4SAMsmhfUMPtMiNN6YjQKTCuWQ/exec;

        fetch(webAppUrl, {
            method: "POST",
            mode: "no-cors", 
            cache: "no-cache",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(r)
        })
        .then(() => {
            alert("Données synchronisées avec Google Sheets !");
        })
        .catch(err => {
            console.error("Erreur d'envoi :", err);
            alert("Erreur lors de la synchronisation.");
        });

        // 3. Stockage local et Mise à jour interface
        database.push(r);
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        
        alert(`Fiche ${r.id} enregistrée !\n\n📊 Savoir: ${r.scoreSavoir}%\n🧠 Attitude: ${r.scoreAttitude}/5\n🩺 Pratique: ${r.scorePratique}%`);
        
        codeSel.selectedIndex = (codeSel.selectedIndex + 1) % codeSel.options.length;
        updateAnalysis();
    }

    // --- FONCTIONS D'ANALYSE (ONGLETS 2, 3, 4) ---
    function updateAnalysis() {
        if(database.length === 0) return;

        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(row => `
            <tr>
                <td><b>${row.id}</b></td>
                <td>${row.sexe}</td>
                <td>${row.service}</td>
                <td>${row.anciennete}</td>
                <td style="color:${getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td>${row.scoreAttitude}</td>
                <td style="color:${getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td>${row.scoreSavoir >= 70 && row.scorePratique >= 70 ? '🟢 Expert' : (row.scoreSavoir >= 50 ? '🟠 Moyen' : '🔴 À Former')}</td>
            </tr>
        `).join('');

        let high = database.filter(r => r.scoreSavoir >= 60);
        let low = database.filter(r => r.scoreSavoir < 60);

        let avgAttH = getAvg(high, 'scoreAttitude'), avgPracH = getAvg(high, 'scorePratique');
        let avgAttL = getAvg(low, 'scoreAttitude'), avgPracL = getAvg(low, 'scorePratique');

        document.getElementById('cross-body').innerHTML = `
            <tr><td style="padding:15px;"><b>Bonnes Connaissances (>=60%)</b></td><td>${high.length}</td><td>${avgAttH}/5</td><td style="font-weight:bold; font-size:14px;">${avgPracH}%</td></tr>
            <tr><td style="padding:15px;"><b>Connaissances Faibles (<60%)</b></td><td>${low.length}</td><td>${avgAttL}/5</td><td style="font-weight:bold; font-size:14px;">${avgPracL}%</td></tr>
        `;

        renderBarChart('graph-savoir', [
            {label: 'Connaissances Solides', val: high.length, total: database.length, color: '#2e7d32'},
            {label: 'Lacunes Théoriques', val: low.length, total: database.length, color: '#c62828'}
        ]);
        
        let goodPrac = database.filter(r => r.scorePratique >= 70).length;
        renderBarChart('graph-pratique', [
            {label: 'Pratique Conforme', val: goodPrac, total: database.length, color: '#1565c0'},
            {label: 'Pratique Insuffisante', val: database.length - goodPrac, total: database.length, color: '#f57f17'}
        ]);

        let gap = avgPracH - avgPracL;
        let interpDiv = document.getElementById('interpretation-cross');
        if(gap > 15) {
            interpDiv.className = 'interpretation-box';
            interpDiv.innerHTML = `<b>Corrélation Positive Forte :</b> L'analyse montre que le personnel ayant de bonnes connaissances théoriques performe mieux en pratique (+${Math.round(gap)} pts).`;
        } else {
            interpDiv.className = 'alert-box';
            interpDiv.innerHTML = `<b>Dissociation Savoir/Agir :</b> Le problème semble structurel plutôt que théorique.`;
        }

        let obsCounts = {};
        database.forEach(r => r.obstacles.forEach(o => obsCounts[o] = (obsCounts[o]||0)+1));
        let sortedObs = Object.entries(obsCounts).sort((a,b)=>b[1]-a[1]);
        
        document.getElementById('graph-obstacles').innerHTML = sortedObs.map(([k,v]) => {
            let p = Math.round((v/database.length)*100);
            return `<div class="bar-container"><div class="bar-label">${k}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:#b03060;">${p}%</div></div><div class="bar-value">${v}</div></div>`;
        }).join('');

        let mainObstacle = sortedObs.length > 0 ? sortedObs[0][0] : "Aucun";
        document.getElementById('final-conclusion').innerHTML = `
            <h3>Synthèse pour la Direction de l'Hôpital</h3>
            <p>L'enquête réalisée auprès de <b>${database.length} agents</b> met en évidence :</p>
            <ul>
                <li><b>Niveau Global :</b> ${Math.round((goodPrac/database.length)*100)}% de pratique conforme.</li>
                <li><b>Frein Majeur :</b> ${mainObstacle}.</li>
            </ul>
        `;
    }

    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); }
    function getRadioValue(n) { let e = document.querySelector(`input[name="${n}"]:checked`); return e ? e.value : 0; }
    function getColor(s) { return s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828'); }
    function getAvg(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0; }
    function renderBarChart(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.total ? Math.round((i.val/i.total)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.label}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.color}">${p}%</div></div><div class="bar-value">${i.val}</div></div>`;
        }).join('');
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }

    function exportToCSV() {
        if(database.length === 0) { alert("Aucune donnée à exporter."); return; }
        let headers = "ID,Sexe,Service,Niveau,Exp,Savoir(%),Attitude(/5),Pratique(%),Obstacles\n";
        let rows = database.map(r => `${r.id},${r.sexe},${r.service},${r.niveau},${r.anciennete},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique},"${r.obstacles.join('|')}"`).join("\n");
        let link = document.createElement("a"); 
        link.href = "data:text/csv;charset=utf-8," + encodeURI("\ufeff"+headers+rows);
        link.download = "Donnees_CAP_CancerSein.csv"; 
        link.click();
    }
</script>

</body>
</html>
