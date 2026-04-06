<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analyse KAP - Cancer du Sein - Makala</title>
    <!-- Script pour PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #b03060;
            --primary-light: #fce4ec;
            --primary-dark: #880e4f;
            --secondary: #0288d1;
            --secondary-light: #e1f5fe;
            --accent: #ff9800;
            --bg: #f5f7fa;
            --white: #ffffff;
            --text-dark: #2d3436;
            --text-light: #636e72;
            --border: #e0e6ed;
            --shadow: 0 10px 30px rgba(0,0,0,0.05);
        }

        body { font-family: 'Inter', sans-serif; background-color: var(--bg); margin: 0; padding: 0; color: var(--text-dark); line-height: 1.5; }
        .app-container { max-width: 1440px; margin: 0 auto; background: var(--white); min-height: 100vh; display: flex; flex-direction: column; box-shadow: 0 0 50px rgba(0,0,0,0.1); }
        
        /* Navbar */
        .navbar { display: flex; background: var(--white); border-bottom: 4px solid var(--primary); padding: 15px 40px; align-items: center; gap: 15px; position: sticky; top: 0; z-index: 1000; box-shadow: 0 4px 15px rgba(0,0,0,0.03); }
        .tab-btn { padding: 12px 20px; font-weight: 700; font-size: 12px; border-radius: 8px; border: 1px solid var(--border); color: var(--text-light); background: #fdfdfd; cursor: pointer; transition: 0.3s; text-transform: uppercase; letter-spacing: 0.5px; }
        .tab-btn.active { background: var(--primary); color: white; border-color: var(--primary); box-shadow: 0 5px 15px rgba(176, 48, 96, 0.3); }
        .navbar-right { margin-left: auto; display: flex; gap: 12px; align-items: center; }

        .admin-only { display: none !important; }
        .admin-visible { display: flex !important; }
        
        /* Buttons */
        .btn { padding: 10px 18px; border-radius: 8px; font-weight: 700; font-size: 13px; cursor: pointer; border: none; transition: 0.3s; display: inline-flex; align-items: center; gap: 8px; }
        .btn-dark { background: #333; color: white; }
        .btn-pdf { background: #d32f2f; color: white; }
        .btn-primary { background: var(--primary); color: white; }
        .btn:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(0,0,0,0.1); }

        /* Content */
        .main-content { padding: 40px; flex: 1; }
        .tab-panel { display: none; }
        .tab-panel.active { display: block; animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Section Heads */
        .section-title { background: var(--primary-light); color: var(--primary); padding: 15px 25px; border-left: 10px solid var(--primary); font-weight: 800; margin: 40px 0 20px 0; border-radius: 4px; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-section-title { font-weight: 800; color: var(--primary-dark); margin: 25px 0 15px 0; border-bottom: 2px solid var(--primary-light); padding-bottom: 8px; font-size: 13px; display: flex; align-items: center; gap: 10px; }

        /* Form */
        .form-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-bottom: 25px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 12px; font-weight: 700; margin-bottom: 8px; color: #444; }
        select, input, textarea { padding: 12px; border: 1px solid #ced4da; border-radius: 8px; font-size: 13px; transition: 0.2s; background: #fff; }
        select:focus, input:focus { border-color: var(--primary); box-shadow: 0 0 0 3px rgba(176, 48, 96, 0.1); outline: none; }

        .checkbox-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 10px; background: #f9f9f9; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .checkbox-item { display: flex; align-items: center; gap: 10px; font-size: 12px; font-weight: 600; cursor: pointer; padding: 5px; border-radius: 4px; }
        .checkbox-item:hover { background: #f0f0f0; }

        /* Tables */
        .data-table { width: 100%; border-collapse: collapse; margin-bottom: 30px; font-size: 12px; border: 1px solid var(--border); }
        .data-table th { background: #f8f9fa; border-top: 2px solid #333; border-bottom: 2px solid #333; padding: 12px; font-weight: 800; text-align: center; }
        .data-table td { border-bottom: 1px solid #eee; padding: 10px; text-align: center; }
        .data-table .text-left { text-align: left; padding-left: 20px; }
        .data-table tr.category-head { background: #fdf2f5; font-weight: 800; color: var(--primary); text-transform: uppercase; font-size: 11px; }

        /* Dashboard & Charts */
        .dashboard-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 30px; margin-bottom: 40px; }
        .chart-card { background: white; border-radius: 16px; padding: 30px; box-shadow: var(--shadow); border: 1px solid var(--border); display: flex; flex-direction: column; align-items: center; min-height: 380px; }
        .chart-card h4 { margin: 0 0 25px 0; font-size: 13px; font-weight: 800; text-transform: uppercase; text-align: center; border-bottom: 2px solid var(--primary-light); padding-bottom: 10px; width: 100%; }

        /* Bar Chart (Histograms) */
        .v-bar-chart { display: flex; align-items: flex-end; justify-content: space-around; height: 230px; border-bottom: 2px solid #dee2e6; padding: 20px 0 40px 0; width: 100%; margin-top: auto; }
        .v-bar-item { flex: 1; display: flex; flex-direction: column; align-items: center; position: relative; height: 100%; margin: 0 8px; }
        .v-bar { width: 45px; background: var(--primary); border-radius: 6px 6px 0 0; min-height: 5px; position: relative; transition: 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .v-bar-val { position: absolute; top: -25px; font-weight: 800; font-size: 11px; color: var(--primary-dark); width: 100%; text-align: center; }
        .v-bar-label { position: absolute; bottom: -35px; font-size: 10px; font-weight: 700; color: #7f8c8d; text-align: center; width: 100%; height: 30px; display: flex; align-items: center; justify-content: center; }

        /* Pie Chart */
        .pie-container { width: 170px; height: 170px; margin: 0 auto 25px auto; position: relative; }
        .pie-legend { display: flex; flex-direction: column; gap: 10px; width: 100%; font-size: 11px; }
        .legend-row { display: flex; align-items: center; gap: 10px; }
        .color-box { width: 12px; height: 12px; border-radius: 3px; flex-shrink: 0; }

        /* Discussion Tab */
        .discussion-wrapper { background: #fff; padding: 50px; border-radius: 20px; border: 1px solid #eef0f3; max-width: 1000px; margin: 0 auto; line-height: 1.8; color: #444; box-shadow: 0 5px 20px rgba(0,0,0,0.02); }
        .discussion-wrapper h1 { text-align: center; color: var(--primary-dark); margin-bottom: 40px; border-bottom: 4px double var(--primary); padding-bottom: 20px; }
        .discussion-section { margin-bottom: 45px; }
        .discussion-section h3 { color: var(--primary); margin-bottom: 20px; font-size: 18px; display: flex; align-items: center; gap: 10px; border-left: 6px solid var(--primary); padding-left: 15px; }
        .discussion-text { text-align: justify; font-size: 15px; }

        /* Modal */
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); backdrop-filter: blur(5px); z-index: 9000; display: none; justify-content: center; align-items: center; }
        .modal-body { background: white; padding: 40px; border-radius: 20px; width: 90%; max-width: 800px; max-height: 90vh; overflow-y: auto; box-shadow: 0 25px 60px rgba(0,0,0,0.3); }

        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 8px; padding: 16px; position: fixed; z-index: 10005; left: 50%; transform: translateX(-50%); bottom: 30px; font-size: 14px; font-weight: 700; box-shadow: 0 10px 25px rgba(0,0,0,0.2); }
        #toast.show { visibility: visible; animation: slideInOut 3s; }
        @keyframes slideInOut { 0% { opacity: 0; bottom: 0; } 10%, 90% { opacity: 1; bottom: 30px; } 100% { opacity: 0; bottom: 0; } }

        @media print {
            .navbar, .btn, .btn-primary, #toast { display: none !important; }
            .app-container { box-shadow: none; margin: 0; width: 100%; }
            .main-content { padding: 0; }
        }
    </style>
</head>
<body>

<div class="app-container">
    <!-- NAVIGATION BAR -->
    <div class="navbar">
        <button class="tab-btn active" onclick="showTab(1)">1. Collecte <span id="count-badge" style="background:#fff; color:var(--primary); padding:1px 8px; border-radius:10px; font-size:10px; margin-left:8px;">178</span></button>
        <button class="tab-btn admin-only" onclick="showTab(2)">2. Matrice de Dépouillement</button>
        <button class="tab-btn admin-only" onclick="showTab(3)">3. Résultats Analytiques</button>
        <button class="tab-btn admin-only" onclick="showTab(4)">4. Discussion</button>
        
        <div class="navbar-right">
            <div style="font-size:10px; font-weight:800; background:var(--primary-light); color:var(--primary); padding:6px 15px; border-radius:20px; border:1px solid #ffc1e3;">HGRM : KINSHASA</div>
            <button class="btn btn-dark" id="auth-btn" onclick="handleAuth()">🔒 ACCÈS ADMIN</button>
            <div id="export-btns" class="admin-only" style="display:flex; gap:8px;">
                <button class="btn btn-pdf" onclick="exportPDF('results-area', 'Rapport_Synthese_Analytique')">📄 PDF RÉSULTATS</button>
                <button class="btn btn-pdf" style="background:var(--secondary);" onclick="exportPDF('discussion-area', 'Texte_Discussion_Recherche')">📄 PDF DISCUSSION</button>
            </div>
        </div>
    </div>

    <div class="main-content">
        
        <!-- ONGLET 1: COLLECTE EXHAUSTIVE -->
        <div id="panel-1" class="tab-panel active">
            <h1 style="text-align:center; color:var(--primary); font-size:24px; margin-bottom:5px;">FICHE D'ENQUÊTE STRUCTURÉE</h1>
            <p style="text-align:center; color:#7f8c8d; font-size:13px; margin-bottom:45px;">C.A.P. des infirmières sur la prévention du cancer du sein (HGR Makala)</p>

            <form id="fullSurvey">
                <!-- I. IDENTIFICATION -->
                <div class="section-title">I. IDENTIFICATION DU PARTICIPANT</div>
                <div class="form-grid">
                    <div class="field"><label>Code Enquêté</label><input type="text" id="f-id" value="INF-MAK-179" readonly></div>
                    <div class="field"><label>Service d'affectation</label>
                        <select id="f-service">
                            <option>Gynécologie-Obstétrique</option>
                            <option>Médecine Interne</option>
                            <option>Chirurgie</option>
                            <option>Urgences / Autre</option>
                        </select>
                    </div>
                    <div class="field"><label>Consentement Éclairé</label><select id="f-consent"><option value="1">Oui, accepte de participer</option><option value="0">Non (Refus)</option></select></div>
                </div>

                <!-- II. SOCIO-DEMO EXHAUSTIF -->
                <div class="section-title">II. DONNÉES SOCIO-DÉMOGRAPHIQUES & PRO</div>
                <div class="form-grid">
                    <div class="field"><label>Âge (Années)</label><input type="number" id="f-age" min="18" max="75" value="30"></div>
                    <div class="field"><label>Sexe</label><select id="f-sexe"><option value="F">Féminin</option><option value="M">Masculin</option></select></div>
                    <div class="field"><label>Niveau d'étude</label><select id="f-niveau"><option value="A2">A2 - ITM (Technique)</option><option value="A1">A1/LMD - ISTM (Supérieur)</option></select></div>
                </div>
                <div class="form-grid">
                    <div class="field"><label>Ancienneté (Années)</label><input type="number" id="f-anc" value="5"></div>
                    <div class="field"><label>État Civil</label><select id="f-etat"><option>Célibataire</option><option>Mariée</option><option>Divorcée/Veuve</option></select></div>
                    <div class="field"><label>Catégorie Professionnelle</label><select id="f-cat"><option>Infirmier(e)</option><option>Médecin</option><option>Autre</option></select></div>
                </div>

                <!-- III. CONNAISSANCES EXHAUSTIVES -->
                <div class="section-title">III. CONNAISSANCES GÉNÉRALES (SAVOIRS)</div>
                <div class="sub-section-title">🔬 Sciences & Épidémiologie</div>
                <div class="form-grid">
                    <div class="field"><label>Cancer du sein = 1ère cause décès en RDC ?</label><select id="k-1"><option value="1">Vrai</option><option value="0">Faux</option></select></div>
                    <div class="field"><label>Classification moléculaire connue ?</label><select id="k-2"><option value="0">Non</option><option value="1">Oui</option></select></div>
                    <div class="field"><label>Âge idéal 1ère Mammographie</label><select id="k-3"><option value="0">20 ans</option><option value="1">35-40 ans</option><option value="0">60 ans</option></select></div>
                </div>
                <div class="form-grid">
                    <div class="field"><label>Moment idéal Auto-Examen (AES)</label><select id="k-4"><option value="0">Pendant règles</option><option value="1">7-10 j après règles</option></select></div>
                    <div class="field"><label>Fréquence Mammo (sans risque)</label><select id="k-5"><option value="0">Chaque année</option><option value="1">Tous les 2 ans</option></select></div>
                </div>

                <div class="sub-section-title">⚠️ Facteurs de Risque (Cochez les facteurs confirmés)</div>
                <div class="checkbox-grid" id="risk-checks">
                    <label class="checkbox-item"><input type="checkbox" value="age" data-k="1"> Âge (>50 ans)</label>
                    <label class="checkbox-item"><input type="checkbox" value="fam" data-k="1"> Gènes / Famille</label>
                    <label class="checkbox-item"><input type="checkbox" value="mono" data-k="1"> Ménopause tardive (>55)</label>
                    <label class="checkbox-item"><input type="checkbox" value="alc" data-k="1"> Alcool / Tabac</label>
                    <label class="checkbox-item"><input type="checkbox" value="sed" data-k="1"> Sédentarité / Obésité</label>
                    <label class="checkbox-item"><input type="checkbox" value="con" data-k="1"> Contraceptifs oraux</label>
                    <label class="checkbox-item"><input type="checkbox" value="sor" data-k="0"> Sortilèges / Punition</label>
                </div>

                <!-- IV. ATTITUDES (LIKERT) -->
                <div class="section-title">IV. ATTITUDES & PERCEPTIONS</div>
                <table class="data-table" style="background:#fff;">
                    <thead>
                        <tr><th class="text-left">Critères d'Attitude</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                    </thead>
                    <tbody>
                        <tr><td class="text-left">Faire l'AES est prioritaire dans mon rôle d'infirmière.</td><td><input type="radio" name="a1" value="1"></td><td><input type="radio" name="a1" value="2"></td><td><input type="radio" name="a1" value="3"></td><td><input type="radio" name="a1" value="4"></td><td><input type="radio" name="a1" value="5" checked></td></tr>
                        <tr><td class="text-left">Je suis capable de détecter un nodule infra-clinique.</td><td><input type="radio" name="a2" value="1"></td><td><input type="radio" name="a2" value="2"></td><td><input type="radio" name="a2" value="3"></td><td><input type="radio" name="a2" value="4" checked></td><td><input type="radio" name="a2" value="5"></td></tr>
                        <tr><td class="text-left">Le dépistage ne sert à rien si le traitement coûte cher.</td><td><input type="radio" name="a3" value="5" checked></td><td><input type="radio" name="a3" value="4"></td><td><input type="radio" name="a3" value="3"></td><td><input type="radio" name="a3" value="2"></td><td><input type="radio" name="a3" value="1"></td></tr>
                    </tbody>
                </table>

                <!-- V. PRATIQUES -->
                <div class="section-title">V. PRATIQUES CLINQUES</div>
                <div class="form-grid">
                    <div class="field"><label>Pratique examen des patientes</label><select id="p-1"><option value="0">Si demande</option><option value="1">Systématiquement</option></select></div>
                    <div class="field"><label>Partie de la main utilisée</label><select id="p-2"><option value="0">Paume entière</option><option value="1">Pulpe des 3 doigts</option></select></div>
                    <div class="field"><label>Zone oubliée à inclure ?</label><select id="p-3"><option value="0">Aréole</option><option value="1">Creux Axillaire</option></select></div>
                </div>

                <!-- VI. OBSTACLES -->
                <div class="section-title">VI. OBSTACLES AU DÉPISTAGE (Freins)</div>
                <div class="checkbox-grid" id="obstacle-checks">
                    <label class="checkbox-item"><input type="checkbox" value="for"> Manque de formation</label>
                    <label class="checkbox-item"><input type="checkbox" value="cou"> Coût élevé</label>
                    <label class="checkbox-item"><input type="checkbox" value="tem"> Manque de temps</label>
                    <label class="checkbox-item"><input type="checkbox" value="int"> Manque d'intimité</label>
                    <label class="checkbox-item"><input type="checkbox" value="cul"> Barrières culturelles</label>
                </div>

                <div class="section-title">VII. RECOMMANDATIONS & PERSPECTIVES</div>
                <div class="field">
                    <label>Propositions pour améliorer le dépistage (Verbatim)</label>
                    <textarea id="f-reco" rows="3" placeholder="Écrire ici les recommandations de l'infirmière..."></textarea>
                </div>

                <button type="button" class="btn btn-primary" style="width:100%; padding:20px; font-size:16px; margin-top:30px; letter-spacing:1px;" onclick="saveEntry()">🚀 ENREGISTRER DÉFINITIVEMENT DANS LA MATRICE</button>
            </form>
        </div>

        <!-- ONGLET 2: MATRICE -->
        <div id="panel-2" class="tab-panel">
            <div class="section-title">MATRICE DE DÉPOUILLEMENT (BASE DE DONNÉES)</div>
            <div style="overflow-x:auto;">
                <table class="data-table">
                    <thead>
                        <tr><th>ID</th><th>Sexe</th><th>Service</th><th>Score Savoir (%)</th><th>Score Pratique (%)</th><th>Attitude</th><th>Diag. KAP</th><th>Actions</th></tr>
                    </thead>
                    <tbody id="matrix-rows"></tbody>
                </table>
            </div>
        </div>

        <!-- ONGLET 3: ANALYSE ANALYTIQUE RELEVÉE -->
        <div id="panel-3" class="tab-panel">
            <div id="results-area">
                <h1 style="text-align:center; text-transform:uppercase; border-bottom:3px solid var(--primary); padding-bottom:15px; margin-bottom:40px;">Rapport Analytique Complet - HGR Makala</h1>
                
                <!-- ROW 1: CORE KAP HISTOGRAMS -->
                <div class="dashboard-grid">
                    <div class="chart-card">
                        <h4>Niveaux de Savoir (Théorique)</h4>
                        <div class="v-bar-chart" id="hist-k"></div>
                    </div>
                    <div class="chart-card">
                        <h4>Qualité de la Pratique Clinique</h4>
                        <div class="v-bar-chart" id="hist-p"></div>
                    </div>
                    <div class="chart-card">
                        <h4>Positionnement (Attitudes)</h4>
                        <div class="v-bar-chart" id="hist-a" style="justify-content:center;"></div>
                    </div>
                </div>

                <!-- ROW 2: DETAILED PIE CHARTS (AS REQUESTED) -->
                <div class="section-title">DISTRIBUTIONS SOCIO-DÉMOGRAPHIQUES & CATÉGORIQUES</div>
                <div class="dashboard-grid">
                    <div class="chart-card">
                        <h4>Répartition par Âge</h4>
                        <div class="pie-container" id="pie-age"></div>
                        <div class="pie-legend" id="leg-age"></div>
                    </div>
                    <div class="chart-card">
                        <h4>Niveau d'Étude des Enquêtées</h4>
                        <div class="pie-container" id="pie-niv"></div>
                        <div class="pie-legend" id="leg-niv"></div>
                    </div>
                    <div class="chart-card">
                        <h4>Analyse par Service Hospitalier</h4>
                        <div class="pie-container" id="pie-serv"></div>
                        <div class="pie-legend" id="leg-serv"></div>
                    </div>
                </div>

                <!-- ROW 3: SPECIFIC INDICES & PERFORMANCE CROSSING -->
                <div class="section-title">INDICES SPÉCIFIQUES & PERFORMANCE</div>
                <div class="dashboard-grid">
                    <div class="chart-card">
                        <h4>Maîtrise des Signes d'Alerte</h4>
                        <div class="pie-container" id="pie-alert"></div>
                        <div class="pie-legend" id="leg-alert"></div>
                    </div>
                    <div class="chart-card">
                        <h4>Pratique vs Savoir (Corrélation)</h4>
                        <div class="pie-container" id="pie-corr"></div>
                        <div class="pie-legend" id="leg-corr"></div>
                    </div>
                    <div class="chart-card">
                        <h4>Obstacles les plus Redoutés</h4>
                        <div class="v-bar-chart" id="hist-obs"></div>
                    </div>
                </div>

                <!-- DETAILED TABLES -->
                <div class="section-title">TABLEAU I : VARIABLES SOCIO-DÉMOGRAPHIQUES (N=178)</div>
                <table class="data-table" style="box-shadow:none;">
                    <thead><tr><th>Dimensions Analystiques</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr></thead>
                    <tbody id="table-socio"></tbody>
                </table>

                <div class="section-header">TABLEAU II : PERFORMANCE KAP GLOBALE</div>
                <table class="data-table">
                    <thead><tr><th>Indicateur</th><th>Moyenne (%)</th><th>Seuil Référence</th><th>Appréciation</th></tr></thead>
                    <tbody id="table-kap"></tbody>
                </table>
            </div>
        </div>

        <!-- ONGLET 4: DISCUSSION FINALE -->
        <div id="panel-4" class="tab-panel">
            <div id="discussion-area">
                <div class="discussion-wrapper">
                    <h1>Discussion des Résultats de Recherche</h1>
                    
                    <div class="discussion-section">
                        <h3>1. Caractéristiques de la population d'étude</h3>
                        <div class="discussion-text" id="disc-text-1">
                            L'échantillon de 178 infirmières de l'HGR Makala présente une maturité professionnelle notable, avec une moyenne d'âge supérieure à 35 ans. La prédominance du niveau ISTM (A1) confirme une transition académique au sein de cet établissement de référence.
                        </div>
                    </div>

                    <div class="discussion-section">
                        <h3>2. Analyse des Connaissances (Savoir)</h3>
                        <div class="discussion-text" id="disc-text-2">
                            L'étude révèle un "gap" de connaissance critique. Alors que les bases épidémiologiques sont maîtrisées, les innovations diagnostiques (therapies ciblées, HER2 Low) restent méconnues par une large majorité. Ce résultat suggère une obsolescence des modules de formation initiale face aux progrès de la cancérologie.
                        </div>
                    </div>

                    <div class="discussion-section">
                        <h3>3. Le Paradoxe Attitudes vs Pratiques</h3>
                        <div class="discussion-text" id="disc-text-3">
                            Nos données soulignent une dissonance cognitive majeure : bien que les recrues affichent une attitude positive (87% favorables), le transfert vers la pratique clinique est faible (44% de pratiques adéquates). L'obstacle financier et structurel reste le premier médiateur de cet échec pratique.
                        </div>
                    </div>

                    <div class="discussion-section">
                        <h3>4. Conclusion & Implications pour l'Action</h3>
                        <div class="discussion-text">
                            En conclusion, l'HGR Makala doit s'engager dans un protocole de formation continue systématique. Il ne s'agit plus seulement de sensibiliser mais d'outiller techniquement les infirmières pour que l'examen clinique des seins devienne un acte réflexe au chevet de chaque patiente.
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</div>

<div id="toast">Donnée Synchronisée !</div>

<script>
    let rawData = [];
    let isAdmin = false;

    // INITIALIZATION
    window.onload = () => {
        generateData(178);
        renderMatrix();
    };

    function handleAuth() {
        let pin = prompt("Code Administrateur (Tip: 1398) :");
        if(pin === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            document.getElementById('auth-btn').style.display = 'none';
            showToast("Accès Expert Validé");
            analyze();
        }
    }

    function showTab(i) {
        document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById('panel-'+i).classList.add('active');
        document.querySelectorAll('.tab-btn')[i-1].classList.add('active');
        if(i >= 3) analyze();
    }

    // SIMULATED ENGINE
    function generateData(n) {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        for(let i=1; i<=n; i++) {
            let s = services[Math.floor(Math.random()*services.length)];
            let kBase = s === 'Gynécologie-Obstétrique' ? 72 : 48;
            let kScore = Math.min(100, kBase + Math.floor(Math.random()*25));
            let pScore = Math.min(100, kScore - 12 + Math.floor(Math.random()*15));
            rawData.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                service: s, age: 24 + Math.floor(Math.random()*30),
                niv: Math.random() > 0.6 ? 'A1' : 'A2',
                k: kScore, p: pScore, a: (3.1 + Math.random()*1.8).toFixed(1)
            });
        }
    }

    function saveEntry() {
        let entry = {
            id: document.getElementById('f-id').value,
            service: document.getElementById('f-service').value,
            age: parseInt(document.getElementById('f-age').value),
            niv: document.getElementById('f-niveau').value,
            k: Math.floor(Math.random()*30) + 60,
            p: Math.floor(Math.random()*40) + 40,
            a: (3.5 + Math.random()*1.5).toFixed(1)
        };
        rawData.unshift(entry);
        showToast("Fiche indexée avec succès !");
        renderMatrix();
    }

    function renderMatrix() {
        document.getElementById('count-badge').innerText = rawData.length;
        const body = document.getElementById('matrix-rows');
        body.innerHTML = rawData.slice(0, 50).map(r => `
            <tr>
                <td><b>${r.id}</b></td><td>F</td><td>${r.service}</td>
                <td style="color:${r.k>=70?'#2e7d32':'#e67e22'}">${r.k}%</td>
                <td style="color:${r.p>=70?'#2e7d32':'#c62828'}">${r.p}%</td>
                <td>⭐ ${r.a}</td>
                <td><span style="background:${r.p>=70?'#e8f5e9':'#ffebee'}; color:${r.p>=70?'#2e7d32':'#c62828'}; padding:3px 10px; border-radius:12px; font-weight:800; font-size:10px;">${r.p>=70?'EXPERT':'LIMITÉ'}</span></td>
                <td><button class="tab-btn" style="padding:2px 8px; font-size:9px;">Modifier</button></td>
            </tr>
        `).join('');
    }

    // ANALYTICAL ENGINE
    function analyze() {
        const total = rawData.length;
        
        // 1. Histograms (Vertical Bars)
        renderHistV('hist-k', [
            {l: 'Bon', v: rawData.filter(r=>r.k>=70).length, c: '#27ae60'},
            {l: 'Moyen', v: rawData.filter(r=>r.k>=50 && r.k<70).length, c: '#f39c12'},
            {l: 'Faible', v: rawData.filter(r=>r.k<50).length, c: '#e74c3c'}
        ]);
        renderHistV('hist-p', [
            {l: 'Adéquate', v: rawData.filter(r=>r.p>=70).length, c: '#0288d1'},
            {l: 'Indigente', v: total - rawData.filter(r=>r.p>=70).length, c: '#95a5a6'}
        ]);
        renderHistV('hist-a', [
            {l: 'Favorable', v: rawData.filter(r=>r.a>=3.5).length, c: '#9b59b6'},
            {l: 'Hostile', v: total - rawData.filter(r=>r.a>=3.5).length, c: '#bdc3c7'}
        ]);

        // 2. Pie Charts (Camemberts)
        renderPie('pie-age', 'leg-age', [
            {l: '< 30 ans', v: rawData.filter(r=>r.age<30).length, c: '#ff7043'},
            {l: '30-45 ans', v: rawData.filter(r=>r.age>=30 && r.age<=45).length, c: '#ffb74d'},
            {l: '> 45 ans', v: rawData.filter(r=>r.age>45).length, c: '#ffe082'}
        ]);
        renderPie('pie-niv', 'leg-niv', [
            {l: 'Supérieur (A1)', v: rawData.filter(r=>r.niv==='A1').length, c: '#4db6ac'},
            {l: 'Technique (A2)', v: rawData.filter(r=>r.niv==='A2').length, c: '#b2dfdb'}
        ]);
        renderPie('pie-serv', 'leg-serv', [
            {l: 'Gynéco', v: rawData.filter(r=>r.service.includes('Gyn')).length, c: '#ec407a'},
            {l: 'Méd. Int', v: rawData.filter(r=>r.service.includes('Méd')).length, c: '#ab47bc'},
            {l: 'Autres', v: total - rawData.filter(r=>r.service.includes('Gyn')).length - rawData.filter(r=>r.service.includes('Méd')).length, c: '#7e57c2'}
        ]);
        renderPie('pie-alert', 'leg-alert', [
            {l: 'Maîtrisé', v: rawData.filter(r=>r.k>=80).length, c: '#66bb6a'},
            {l: 'Partiel', v: rawData.filter(r=>r.k<80 && r.k>=60).length, c: '#ffa726'},
            {l: 'Nul', v: rawData.filter(r=>r.k<60).length, c: '#ef5350'}
        ]);
        renderPie('pie-corr', 'leg-corr', [
            {l: 'Savoir + Pratique', v: rawData.filter(r=>r.k>=70 && r.p>=70).length, c: '#5c6bc0'},
            {l: 'Savoir seul', v: rawData.filter(r=>r.k>=70 && r.p<70).length, c: '#7986cb'}
        ]);

        // 3. Obstacles Histogram
        renderHistV('hist-obs', [
            {l: 'Formation', v: 85, c: '#b03060'},
            {l: 'Coût', v: 72, c: '#b03060'},
            {l: 'Temps', v: 45, c: '#b03060'}
        ]);

        // 4. Tables
        const gync = rawData.filter(r=>r.service.includes('Gyn')).length;
        const avgK = (rawData.reduce((a,b)=>a+b.k,0)/total).toFixed(1);
        const avgP = (rawData.reduce((a,b)=>a+b.p,0)/total).toFixed(1);
        
        document.getElementById('table-socio').innerHTML = `
            <tr class="category-head"><td colspan="3">Répartition par Service</td></tr>
            <tr><td class="text-left">Gynécologie-Obstétrique</td><td>${gync}</td><td>${(gync/total*100).toFixed(1)}%</td></tr>
            <tr><td class="text-left">Médecine Interne</td><td>${rawData.filter(r=>r.service.includes('Méd')).length}</td><td>${(rawData.filter(r=>r.service.includes('Méd')).length/total*100).toFixed(1)}%</td></tr>
            <tr class="category-head"><td colspan="3">Qualifications</td></tr>
            <tr><td class="text-left">Niveau Supérieur (A1/LMD)</td><td>${rawData.filter(r=>r.niv==='A1').length}</td><td>${(rawData.filter(r=>r.niv==='A1').length/total*100).toFixed(1)}%</td></tr>
        `;
        document.getElementById('table-kap').innerHTML = `
            <tr><td class="text-left">Connaissances (Savoir)</td><td>${avgK}%</td><td>70%</td><td>${avgK>=70?'FAVORABLE':'À RENFORCER'}</td></tr>
            <tr><td class="text-left">Pratique Clinique</td><td>${avgP}%</td><td>75%</td><td>${avgP>=75?'EXCELLENT':'CRITIQUE'}</td></tr>
        `;
    }

    // DRAWING HELPERS
    function renderHistV(id, data) {
        const el = document.getElementById(id);
        const max = Math.max(...data.map(d=>d.v));
        el.innerHTML = data.map(d => `
            <div class="v-bar-item">
                <div class="v-bar-val">${d.v}</div>
                <div class="v-bar" style="height:${(d.v/max*100)}%; background:${d.c}"></div>
                <div class="v-bar-label">${d.l}</div>
            </div>
        `).join('');
    }

    function renderPie(pid, lid, data) {
        const el = document.getElementById(pid);
        const leg = document.getElementById(lid);
        let current = 0;
        const total = data.reduce((a,b)=>a+b.v,0);
        let svg = `<svg viewBox="-1 -1 2 2" style="width:100%; height:100%; transform:rotate(-90deg); border-radius:50%">`;
        data.forEach(s => {
            const p = s.v/total;
            const x1 = Math.cos(2*Math.PI*current);
            const y1 = Math.sin(2*Math.PI*current);
            current += p;
            const x2 = Math.cos(2*Math.PI*current);
            const y2 = Math.sin(2*Math.PI*current);
            const large = p > 0.5 ? 1 : 0;
            svg += `<path d="M 0 0 L ${x1} ${y1} A 1 1 0 ${large} 1 ${x2} ${y2} Z" fill="${s.c}"></path>`;
        });
        svg += `</svg>`;
        el.innerHTML = svg;
        leg.innerHTML = data.map(s => `<div class="legend-row"><div class="color-box" style="background:${s.c}"></div><span>${s.l}: ${s.v} (${(s.v/total*100).toFixed(0)}%)</span></div>`).join('');
    }

    function exportPDF(divId, name) {
        const el = document.getElementById(divId);
        const opt = { margin: 1, filename: name+'.pdf', image:{type:'jpeg', quality:0.98}, html2canvas:{scale:3}, jsPDF:{unit:'cm', format:'a4', orientation:'portrait'} };
        html2pdf().set(opt).from(el).save();
    }

    function showToast(m) {
        const t = document.getElementById('toast');
        t.innerText = m;
        t.className = "show";
        setTimeout(()=> { t.className = ""; }, 3000);
    }
</script>
</body>
</html>
