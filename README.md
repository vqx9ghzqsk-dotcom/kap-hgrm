<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        
        /* Header & Tabs */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel:hover { background: #1b5e20; }

        .form-content { padding: 30px; display: none; /* Caché par défaut, géré par JS */ }
        .form-content.active { display: block; animation: fadeIn 0.5s; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input[type="text"], input[type="number"] { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        /* Tables Likert & Results */
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

        /* Styles Spécifiques aux Résultats (Nouveau) */
        .score-box { background: #fff; border: 1px solid #ddd; padding: 20px; border-radius: 8px; margin-bottom: 20px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .score-title { font-size: 16px; font-weight: bold; color: #444; margin-bottom: 10px; }
        .progress-bg { background: #eee; height: 20px; border-radius: 10px; overflow: hidden; }
        .progress-bar { height: 100%; text-align: center; color: white; font-size: 12px; line-height: 20px; transition: width 1s ease-in-out; }
        .bg-success { background-color: #2e7d32; }
        .bg-warning { background-color: #f57f17; }
        .bg-danger { background-color: #c62828; }
        
        .reco-card { background: #e3f2fd; border-left: 5px solid #2196f3; padding: 15px; margin-bottom: 10px; }
        .reco-card h4 { margin: 0 0 5px 0; color: #1565c0; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE</button>
        <button class="tab" onclick="switchTab(2)">2. DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTAT ET ANALYSE</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT EXCEL (CSV)</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field">
                    <label>Code Enquêté(e)</label>
                    <select id="code-enquete"></select>
                </div>
                <div class="field">
                    <label>Service / Département</label>
                    <select id="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie (si existant)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select id="statut">
                        <option selected>Titulaire du service</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire (Fin de cycle)</option>
                        <option>Sous-statutaire (Bénévole)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge de l'infirmier(e)</label><select id="age-select"></select></div>
                <div class="field"><label>Années d'expérience professionnelle</label><select id="exp-select"></select></div>
                <div class="field">
                    <label>Niveau d'étude le plus élevé</label>
                    <select id="niveau">
                        <option>A2 (Diplômée d'État)</option>
                        <option selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option>L0/L1 (Licenciée nouveau système)</option>
                        <option>Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select id="q1"><option selected>Vrai (Oui)</option><option>Faux (Non)</option><option>Ne sait pas</option></select>
                </div>
                <div class="field">
                    <label>À quel âge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                    <select id="q2"><option>Dès 12 ans</option><option selected>Dès 20 ans</option><option>Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select id="q3"><option selected>7 jours après les règles</option><option>Pendant les règles</option><option>N'importe quand</option></select>
                </div>
            </div>

            <label style="margin: 15px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Facteurs de risque connus (Cochez les propositions valides) :</label>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="nulliparite" checked> Nulliparité (n'avoir jamais accouché)</label>
                <label class="check-item"><input type="checkbox" value="tardive" checked> Première grossesse tardive (> 30 ans)</label>
                <label class="check-item"><input type="checkbox" value="menopause" checked> Ménopause tardive (> 55 ans)</label>
                <label class="check-item"><input type="checkbox" value="alcool" checked> Consommation d'alcool et tabac</label>
                <label class="check-item"><input type="checkbox" value="contraceptif"> Usage prolongé de contraceptifs oraux</label>
                <label class="check-item"><input type="checkbox" value="famille" checked> Antécédents familiaux (Mère, Sœur)</label>
            </div>

            <label style="margin: 20px 0 10px 0; display:block; font-weight: bold; color: #b03060;">Signes cliniques d'alerte (Signes à rechercher) :</label>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule" checked> Nodule dur, fixe et indolore</label>
                <label class="check-item"><input type="checkbox" value="ecoulement" checked> Écoulement séro-sanguinolent unilatéral</label>
                <label class="check-item"><input type="checkbox" value="retraction" checked> Rétraction ou ombilication du mamelon</label>
                <label class="check-item"><input type="checkbox" value="adenopathie" checked> Adénopathie axillaire (boule sous l'aisselle)</label>
                <label class="check-item"><input type="checkbox" value="peauorange" checked> Aspect de "peau d'orange" sur le tégument</label>
                <label class="check-item"><input type="checkbox" value="douleur"> Douleur mammaire isolée (Mastodynie)</label>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (SAVOIR-ÊTRE : 1 À 5)</div>
            <table id="table-attitude">
                <thead>
                    <tr>
                        <th class="text-left">Énoncés (Perception de l'infirmier/e)</th>
                        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule suspect lors d'une palpation.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">L'influence culturelle (pudeur) empêche mes patientes de se déshabiller.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                    <tr><td class="text-left">Le diagnostic de cancer est une sentence de mort en RDC.</td><td><input type="radio" name="p3" value="1"></td><td><input type="radio" name="p3" value="2" checked></td><td><input type="radio" name="p3" value="3"></td><td><input type="radio" name="p3" value="4"></td><td><input type="radio" name="p3" value="5"></td></tr>
                    <tr><td class="text-left">Je pense que chaque femme en consultation doit être sensibilisée au cancer.</td><td><input type="radio" name="p4" value="1"></td><td><input type="radio" name="p4" value="2"></td><td><input type="radio" name="p4" value="3"></td><td><input type="radio" name="p4" value="4"></td><td><input type="radio" name="p4" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES (SAVOIR-FAIRE)</div>
            <div class="row">
                <div class="field">
                    <label>Fréquence de la palpation clinique des seins (ECS) en consultation :</label>
                    <select id="pratique-freq">
                        <option selected>Systématique pour chaque patiente</option>
                        <option>Uniquement si la patiente se plaint</option>
                        <option>Rarement par manque de temps</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignement de la technique d'autopalpation (AES) :</label>
                    <select id="pratique-enseigne">
                        <option selected>Je démontre la technique physiquement</option>
                        <option>J'explique verbalement seulement</option>
                        <option>Je ne l'enseigne pas</option>
                    </select>
                </div>
                <div class="field">
                    <label>Référence des cas suspects :</label>
                    <select id="pratique-ref">
                        <option selected>Vers l'imagerie (Mammographie/Echo)</option>
                        <option>Vers la Chirurgie directement</option>
                        <option>Observation (Attendre le prochain RDV)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field">
                    <label>Utilisation de supports visuels (Affiches, Boites à images) :</label>
                    <select id="pratique-visuel"><option selected>Jamais (Pas de matériel disponible)</option><option>Parfois</option><option>Toujours</option></select>
                </div>
                <div class="field">
                    <label>Avez-vous déjà palpé un sein ce matin ?</label>
                    <select id="pratique-matin"><option selected>Oui</option><option>Non</option></select>
                </div>
                <div class="field">
                    <label>Nombre de cas de cancer suspectés ce mois-ci :</label>
                    <select id="pratique-cas"><option>0</option><option selected>1 à 5 cas</option><option>Plus de 5 cas</option></select>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES ET SOLUTIONS (RDC CONTEXT)</div>
            <label style="margin-bottom: 10px; display:block; font-weight: bold;">Quelles sont les barrières à l'HGRM ? (Cochez tout ce qui est vrai):</label>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="intimite" checked> Absence de salle isolée respectant l'intimité</label>
                <label class="check-item"><input type="checkbox" value="cout" checked> Coût exorbitant de la mammographie (> 50$)</label>
                <label class="check-item"><input type="checkbox" value="formation" checked> Manque de formation continue sur le cancer</label>
                <label class="check-item"><input type="checkbox" value="culture" checked> Préférence des patientes pour la prière/tradition</label>
                <label class="check-item"><input type="checkbox" value="surcharge"> Surcharge de travail (Ratio infirmière/patient)</label>
            </div>

            <div class="field" style="margin-top: 20px;">
                <label>Votre recommandation principale pour l'HGRM :</label>
                <select id="recommandation-user">
                    <option selected>Installation d'une unité de dépistage permanent</option>
                    <option>Formation certifiante pour tout le personnel infirmier</option>
                    <option>Subvention des examens d'imagerie pour les indigents</option>
                    <option>Campagnes de masse dans les églises et marchés</option>
                </select>
            </div>

            <button type="button" class="btn-save" onclick="switchTab(2)">VALIDER ET PASSER AU DÉPOUILLEMENT</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">DÉPOUILLEMENT DES DONNÉES BRUTES</div>
        <p>Ce tableau résume la transformation des réponses textuelles en scores numériques exploitables.</p>
        
        <table>
            <thead>
                <tr>
                    <th class="text-left">Variable / Domaine</th>
                    <th>Réponse Enregistrée</th>
                    <th>Score / Codage</th>
                </tr>
            </thead>
            <tbody id="table-depouillement">
                </tbody>
        </table>
        <div style="text-align: right;">
            <button type="button" class="btn-excel" onclick="switchTab(3)">VOIR L'ANALYSE &gt;</button>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE DES PERFORMANCES (K.A.P)</div>
        
        <div class="score-box">
            <div class="score-title">1. SAVOIRS (CONNAISSANCES THÉORIQUES)</div>
            <div id="res-savoir-text" style="margin-bottom:5px;">Analyse en cours...</div>
            <div class="progress-bg">
                <div id="bar-savoir" class="progress-bar bg-success" style="width: 0%">0%</div>
            </div>
        </div>

        <div class="score-box">
            <div class="score-title">2. ATTITUDES (PERCEPTION & PSYCHOLOGIE)</div>
            <div id="res-attitude-text" style="margin-bottom:5px;">Analyse en cours...</div>
            <div class="progress-bg">
                <div id="bar-attitude" class="progress-bar bg-warning" style="width: 0%">0%</div>
            </div>
            <small>Score basé sur l'échelle de Likert (Moyenne sur 5)</small>
        </div>

        <div class="score-box">
            <div class="score-title">3. PRATIQUES (ACTION TERRAIN)</div>
            <div id="res-pratique-text" style="margin-bottom:5px;">Analyse en cours...</div>
            <div class="progress-bg">
                <div id="bar-pratique" class="progress-bar bg-danger" style="width: 0%">0%</div>
            </div>
            <small>Basé sur la fréquence de palpation et la technique d'enseignement</small>
        </div>

        <div class="section-title">BARRIÈRES IDENTIFIÉES</div>
        <ul id="list-barrieres" style="list-style-type: square; padding-left: 20px;">
            </ul>
        <br>
        <button type="button" class="btn-save" onclick="switchTab(4)">VOIR LES CONCLUSIONS</button>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSION GÉNÉRALE & RECOMMANDATIONS</div>
        
        <div id="conclusion-text" style="margin-bottom: 20px; font-style: italic;">
            </div>

        <h3>RECOMMANDATIONS PRIORITAIRES POUR L'HGRM</h3>
        <div id="recommendations-container">
            </div>

        <div style="margin-top: 40px; padding: 20px; background: #eee; text-align: center;">
            <p><strong>Prochaine étape :</strong> Exporter ces données pour la base centrale.</p>
            <button type="button" class="btn-excel" onclick="exportToCSV()" style="font-size: 16px; padding: 15px 30px;">📥 TÉLÉCHARGER LE RAPPORT (CSV)</button>
        </div>
    </div>

</div>

<script>
    // --- 1. INITIALISATION (Code original +) ---
    const codeSelect = document.getElementById('code-enquete');
    for (let i = 0; i <= 200; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = "Code: " + i;
        codeSelect.appendChild(opt);
    }
    const ageSelect = document.getElementById('age-select');
    for (let i = 18; i <= 60; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = i + " ans";
        if(i === 35) opt.selected = true;
        ageSelect.appendChild(opt);
    }
    const expSelect = document.getElementById('exp-select');
    let m = document.createElement('option'); m.text = "Stagiaire / Moins d'un an"; expSelect.appendChild(m);
    for (let i = 1; i <= 30; i++) {
        let opt = document.createElement('option');
        opt.value = i; opt.text = i + (i === 1 ? " an" : " ans") + " d'expérience";
        if(i === 10) opt.selected = true;
        expSelect.appendChild(opt);
    }

    // --- 2. GESTION DES ONGLETS ---
    function switchTab(tabIndex) {
        // Masquer tous les contenus
        document.querySelectorAll('.form-content').forEach(div => div.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(btn => btn.classList.remove('active'));

        // Afficher le contenu désiré
        document.getElementById('content-' + tabIndex).classList.add('active');
        
        // Activer le bouton correspondant (utilisation de nth-child)
        document.querySelector(`.header-tabs button:nth-child(${tabIndex})`).classList.add('active');

        // Si on quitte l'onglet 1, on lance les calculs
        if (tabIndex > 1) {
            calculateAndDisplay();
        }
    }

    // --- 3. MOTEUR DE CALCUL ET ANALYSE ---
    function calculateAndDisplay() {
        // A. RECUPERATION DES VALEURS
        const q1 = document.getElementById('q1').value;
        const q2 = document.getElementById('q2').value;
        const q3 = document.getElementById('q3').value;
        
        // Checkboxes Risques
        let scoreRisque = 0;
        document.querySelectorAll('#group-risques input:checked').forEach(() => scoreRisque++);
        
        // Checkboxes Signes
        let scoreSignes = 0;
        document.querySelectorAll('#group-signes input:checked').forEach(() => scoreSignes++);

        // Likert Attitudes (Moyenne)
        let totalLikert = 0;
        let countLikert = 0;
        ['p1', 'p2', 'p3', 'p4'].forEach(name => {
            const el = document.querySelector(`input[name="${name}"]:checked`);
            if(el) {
                totalLikert += parseInt(el.value);
                countLikert++;
            }
        });
        const moyAttitude = countLikert > 0 ? (totalLikert / countLikert).toFixed(1) : 0;

        // Pratiques
        const freq = document.getElementById('pratique-freq').value;
        const enseigne = document.getElementById('pratique-enseigne').value;
        const matin = document.getElementById('pratique-matin').value;

        // B. CALCUL DES SCORES (Logique simple)
        // Score Savoir (Sur 20 pts fictifs ramenés en %)
        // Q1=1pt, Q2=1pt, Q3=1pt, Risques=1pt chaque, Signes=1pt chaque
        let rawSavoir = 0;
        if(q1.includes("Vrai")) rawSavoir++;
        if(q2.includes("20 ans")) rawSavoir++;
        if(q3.includes("7 jours")) rawSavoir++;
        rawSavoir += scoreRisque + scoreSignes;
        // Max théorique environ 15 (3 questions + 6 risques + 6 signes)
        let pctSavoir = Math.min(100, Math.round((rawSavoir / 15) * 100));

        // Score Pratique (Algorithme qualitatif)
        let pctPratique = 0;
        if (freq.includes("Systématique")) pctPratique += 40;
        if (freq.includes("plaint")) pctPratique += 10;
        if (enseigne.includes("démontre")) pctPratique += 40;
        if (enseigne.includes("verbalement")) pctPratique += 10;
        if (matin === "Oui") pctPratique += 20;

        // C. REMPLISSAGE ONGLET 2 (DÉPOUILLEMENT)
        const tbody = document.getElementById('table-depouillement');
        tbody.innerHTML = `
            <tr><td class="text-left">Connaissance Cause/Age/Moment</td><td>${q1} / ${q2}</td><td>${q1.includes('Vrai') && q2.includes('20') ? 'Correct (2pts)' : 'Incomplet'}</td></tr>
            <tr><td class="text-left">Facteurs de Risque identifiés</td><td>${scoreRisque} facteurs cochés</td><td>${scoreRisque}/6</td></tr>
            <tr><td class="text-left">Signes d'alerte connus</td><td>${scoreSignes} signes cochés</td><td>${scoreSignes}/6</td></tr>
            <tr><td class="text-left"><strong>TOTAL SAVOIR</strong></td><td>-</td><td><strong>${pctSavoir}%</strong></td></tr>
            <tr><td class="text-left">Attitude Moyenne (Likert)</td><td>Moyenne sur 4 items</td><td>${moyAttitude} / 5</td></tr>
            <tr><td class="text-left">Qualité de la Pratique</td><td>Freq: ${freq.substring(0,10)}...</td><td>${pctPratique}%</td></tr>
        `;

        // D. REMPLISSAGE ONGLET 3 (RÉSULTAT)
        updateBar('bar-savoir', pctSavoir, 'res-savoir-text');
        updateBar('bar-attitude', (moyAttitude/5)*100, 'res-attitude-text', moyAttitude + "/5");
        updateBar('bar-pratique', pctPratique, 'res-pratique-text');

        // Liste des barrières
        const ulBar = document.getElementById('list-barrieres');
        ulBar.innerHTML = "";
        document.querySelectorAll('#group-obstacles input:checked').forEach(chk => {
            let li = document.createElement('li');
            li.textContent = chk.parentNode.textContent;
            ulBar.appendChild(li);
        });

        // E. REMPLISSAGE ONGLET 4 (CONCLUSION)
        generateConclusion(pctSavoir, moyAttitude, pctPratique);
    }

    function updateBar(id, pct, textId, customVal) {
        const bar = document.getElementById(id);
        const txt = document.getElementById(textId);
        bar.style.width = pct + "%";
        bar.textContent = (customVal ? customVal : pct + "%");
        
        // Couleur dynamique
        bar.className = "progress-bar " + (pct > 70 ? "bg-success" : (pct > 40 ? "bg-warning" : "bg-danger"));
        
        let appreciation = pct > 70 ? "Excellent niveau" : (pct > 40 ? "Niveau Moyen" : "Niveau Critique");
        txt.innerHTML = `Score calculé : <strong>${pct}%</strong> - ${appreciation}`;
    }

    function generateConclusion(savoir, attitude, pratique) {
        const divConcl = document.getElementById('conclusion-text');
        const divReco = document.getElementById('recommendations-container');
        
        divConcl.innerHTML = `L'analyse des données de l'infirmier(e) montre un niveau de connaissances théoriques de <strong>${savoir}%</strong>, couplé à une attitude de ${attitude}/5. Cependant, la pratique réelle sur le terrain est évaluée à <strong>${pratique}%</strong>. Le décalage entre le savoir et le faire semble lié aux obstacles structurels.`;

        let recos = "";
        // Logique conditionnelle pour les recommandations
        if(savoir < 50) {
            recos += `<div class="reco-card"><h4>🚑 Formation Urgente Requise</h4><p>Le personnel a des lacunes sur les signes cliniques. Programmer une session de mise à niveau sur l'anatomie et la palpation.</p></div>`;
        }
        if(pratique < 50) {
            recos += `<div class="reco-card"><h4>📋 Protocole de Soins</h4><p>La palpation n'est pas systématique. Instaurer une fiche de contrôle obligatoire dans chaque dossier patient.</p></div>`;
        }
        // Obstacles
        const obstacles = document.querySelectorAll('#group-obstacles input:checked');
        let hasCout = false;
        obstacles.forEach(o => { if(o.value === 'cout') hasCout = true; });
        
        if(hasCout) {
            recos += `<div class="reco-card"><h4>💰 Plaidoyer Financier</h4><p>Le coût est un frein majeur identifié. Proposer à la direction de l'HGRM un forfait "Octobre Rose" ou des subventions.</p></div>`;
        } else {
             recos += `<div class="reco-card"><h4>🏥 Aménagement</h4><p>Vérifier la disponibilité des paravents pour garantir l'intimité et encourager l'examen.</p></div>`;
        }

        divReco.innerHTML = recos;
    }

    // --- 4. EXPORT EXCEL (CSV) ---
    function exportToCSV() {
        const code = document.getElementById('code-enquete').value;
        const niveau = document.getElementById('niveau').value;
        const q1 = document.getElementById('q1').value;
        
        // Calcul rapide pour l'export
        let score = 0; 
        if(q1.includes("Vrai")) score++;

        // Construction du CSV (En-têtes + Données)
        // \ufeff est le BOM pour forcer Excel à lire l'UTF-8 (accents)
        let csvContent = "data:text/csv;charset=utf-8,\ufeff";
        csvContent += "Code,Niveau Etude,Connaissance Cause,Pratique Matin,Recommandation\n";
        csvContent += `${code},${niveau},${q1},${document.getElementById('pratique-matin').value},${document.getElementById('recommandation-user').value}\n`;

        // Création du lien de téléchargement
        var encodedUri = encodeURI(csvContent);
        var link = document.createElement("a");
        link.setAttribute("href", encodedUri);
        link.setAttribute("download", "KAP_HGRM_Resultats.csv");
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
    }
</script>

</body>
</html>
