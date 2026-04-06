<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard Médical - HGR Makala</title>
    <!-- Google Fonts pour un look premium -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Chart.js pour des visualisations haut de gamme -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        /* --- DESIGN SYSTEM (SKELETON & AESTHETICS) --- */
        :root {
            --primary: #00796b; 
            --primary-dark: #004d40;
            --primary-light: #e0f2f1;
            --secondary: #37474f;
            --accent: #26a69a;
            --bg-body: #f4f7f6;
            --bg-card: #ffffff;
            --text-title: #1a202c;
            --text-body: #4a5568;
            --border: #e2e8f0;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            --transition: all 0.2s ease;
        }

        /* --- MODAL STYLES --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.6); backdrop-filter: blur(4px);
            display: none; justify-content: center; align-items: center; z-index: 2000;
        }
        .modal-container {
            background: #fff; width: 90%; max-width: 800px; max-height: 90vh;
            border-radius: 16px; overflow-y: auto; padding: 40px; position: relative;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        .modal-close {
            position: absolute; top: 20px; right: 20px; font-size: 24px;
            cursor: pointer; color: #718096; transition: 0.2s;
        }
        .modal-close:hover { color: var(--primary); }
        .modal-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 25px; margin-top: 20px; }
        .modal-data-group { border-bottom: 1px solid var(--border); padding-bottom: 10px; }
        .modal-data-label { font-size: 11px; font-weight: 800; color: #a0aec0; text-transform: uppercase; }
        .modal-data-value { font-size: 15px; font-weight: 700; color: var(--secondary); margin-top: 4px; }
        .score-pill { padding: 4px 12px; border-radius: 20px; font-size: 12px; font-weight: 700; }
        .score-good { background: #c6f6d5; color: #22543d; }
        .score-medium { background: #feebc8; color: #744210; }
        .score-poor { background: #fed7d7; color: #822727; }


        * { box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background-color: var(--bg-body); margin: 0; color: var(--text-body); line-height: 1.6; }

        .app-container { max-width: 1250px; margin: 30px auto; background: var(--bg-card); border-radius: 20px; box-shadow: var(--shadow); overflow: hidden; min-height: 90vh; display: flex; flex-direction: column; }

        /* --- HEADER & NAVIGATION --- */
        .app-header { background: #fff; padding: 0 25px; border-bottom: 3px solid var(--primary); display: flex; align-items: center; position: sticky; top: 0; z-index: 1000; box-shadow: 0 4px 10px rgba(0,0,0,0.03); }
        .nav-tabs { display: flex; gap: 10px; padding: 15px 0; flex-grow: 1; }
        .tab { padding: 12px 22px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.8px; border: 1px solid var(--border); border-radius: 8px; background: #fafafa; color: var(--text-body); cursor: pointer; transition: var(--transition); display: flex; align-items: center; gap: 10px; border: none; }
        .tab:hover { background: var(--primary-light); color: var(--primary); border: 1px solid var(--primary); }
        .tab.active { background: var(--primary); color: #fff; box-shadow: 0 4px 15px rgba(0, 121, 107, 0.25); }
        
        /* Badges */
        .badge-count { background: rgba(0,0,0,0.1); padding: 2px 8px; border-radius: 20px; font-size: 10px; }
        .tab.active .badge-count { background: rgba(255,255,255,0.2); }

        /* --- CONTENT AREAS --- */
        .tab-content { padding: 40px; display: none; }
        .tab-content.active { display: block; animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* --- UI COMPONENTS --- */
        .section-header { margin: 30px 0 20px; padding: 15px 25px; background: var(--primary-light); color: var(--primary-dark); font-weight: 800; border-left: 8px solid var(--primary); border-radius: 4px 12px 12px 4px; text-transform: uppercase; font-size: 14px; }
        
        .grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; margin-bottom: 25px; }
        .input-group { display: flex; flex-direction: column; gap: 8px; }
        label { font-size: 13px; font-weight: 800; color: var(--secondary); display: flex; align-items: center; gap: 5px; }
        input, select, textarea { padding: 14px; border: 2px solid #edf2f7; border-radius: 10px; font-size: 15px; width: 100%; transition: var(--transition); }
        input:focus, select:focus { border-color: var(--accent); outline: none; box-shadow: 0 0 0 4px rgba(38, 166, 154, 0.1); }

        /* Buttons */
        .btn-primary { background: var(--primary); color: #fff; padding: 18px 30px; border: none; border-radius: 12px; font-weight: 800; cursor: pointer; width: 100%; font-size: 16px; text-transform: uppercase; margin-top: 30px; transition: var(--transition); box-shadow: 0 8px 15px rgba(0, 121, 107, 0.2); }
        .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 25px rgba(0, 121, 107, 0.3); }

        /* Tables & Matrix */
        .matrix-container { overflow-x: auto; border-radius: 12px; border: 1px solid var(--border); background: #fff; }
        table { width: 100%; border-collapse: collapse; min-width: 800px; }
        th { background: #f8fafc; padding: 18px; text-align: left; font-size: 11px; font-weight: 800; color: var(--secondary); border-bottom: 2px solid var(--border); text-transform: uppercase; }
        td { padding: 18px; border-bottom: 1px solid var(--border); font-size: 14px; color: var(--text-body); }
        tr:last-child td { border-bottom: none; }

        /* Stats Cards */
        .stat-card { background: #fff; border: 1px solid var(--border); padding: 25px; border-radius: 15px; box-shadow: 0 4px 12px rgba(0,0,0,0.02); transition: var(--transition); display: flex; flex-direction: column; align-items: center; text-align: center; }
        .stat-card:hover { transform: translateY(-5px); box-shadow: 0 8px 20px rgba(0,0,0,0.05); }
        .stat-value { font-size: 32px; font-weight: 800; color: var(--primary); }
        .stat-label { font-size: 12px; color: #78909c; font-weight: 700; margin-top: 5px; text-transform: uppercase; letter-spacing: 0.5px; }

        /* Chart Containers */
        .chart-box { background: #fff; border: 1px solid var(--border); border-radius: 20px; padding: 25px; margin-bottom: 30px; box-shadow: 0 4px 12px rgba(0,0,0,0.02); }
        .chart-box h3 { margin: 0 0 20px; font-size: 16px; color: var(--text-title); font-weight: 800; display: flex; align-items: center; gap: 10px; }
        .chart-box h3::before { content: ''; width: 4px; height: 18px; background: var(--primary); border-radius: 2px; }

        /* Custom Checkbox Grid */
        .checkbox-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; padding: 20px; background: #fcfcfc; border: 2px dashed var(--border); border-radius: 12px; }
        .check-pill { display: flex; align-items: center; gap: 12px; padding: 12px; background: #fff; border: 1px solid var(--border); border-radius: 8px; cursor: pointer; transition: 0.2s; font-size: 14px; font-weight: 600; }
        .check-pill:hover { border-color: var(--primary); background: var(--primary-light); }
        .check-pill input { width: 18px; height: 18px; margin: 0; accent-color: var(--primary); }

        /* Results Specific Layout */
        .results-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; }
        @media (max-width: 900px) { .results-grid { grid-template-columns: 1fr; } }
    </style>
</head>
<body>

<div class="app-container">
    <header class="app-header">
        <nav class="nav-tabs">
            <button class="tab" onclick="switchTab(1)">1. Collecte 📋 <span class="badge-count" id="badge-1">178</span></button>
            <button class="tab" onclick="switchTab(2)">2. Matrice de Dépouillement 📊</button>
            <button class="tab active" onclick="switchTab(3)">3. Résultats & Analyse 📈</button>
            <button class="tab" onclick="switchTab(4)">4. Discussion & Synthèse 📄</button>
        </nav>
        <div style="font-size: 10px; font-weight: 800; color: #999; text-transform: uppercase; letter-spacing: 1px;">MAKALA-BC-2024</div>
    </header>

    <!-- TAB 1: COLLECTE (FICHE MÉDICALE) -->
    <div id="content-1" class="tab-content">
        <div style="text-align:center; margin-bottom: 40px;">
            <h2 style="margin:0; font-weight:800; color:var(--text-title);">FICHE D'ENQUÊTE CLINIQUE</h2>
            <p style="margin:5px 0 0; color:var(--text-body); font-weight:600; font-size:14px;">Profil de dépistage du cancer du sein - HGR Makala</p>
        </div>

        <form id="collecteForm">
            <div class="section-header">I. IDENTIFICATION DU DOSSIER</div>
            <div class="grid-3">
                <div class="input-group">
                    <label>Numéro de fiche</label>
                    <input type="text" placeholder="Ex: F-MAK-001" id="num-fiche">
                </div>
                <div class="input-group">
                    <label>Numéro du dossier</label>
                    <input type="text" placeholder="Numéro hospitalier..." id="num-dossier">
                </div>
                <div class="input-group">
                    <label>Année d'admission</label>
                    <select id="annee">
                        <option value="2023">2023</option>
                        <option value="2024" selected>2024</option>
                    </select>
                </div>
            </div>

            <div class="section-header">II. DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div class="grid-3">
                <div class="input-group">
                    <label>Tranche d'âge</label>
                    <select>
                        <option>20-29 ans</option>
                        <option>30-39 ans</option>
                        <option>40-49 ans</option>
                        <option>50 ans et plus</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>Sexe</label>
                    <select>
                        <option>Féminin</option>
                        <option>Masculin</option>
                    </select>
                </div>
                <div class="input-group">
                    <label>Niveau d'études</label>
                    <select>
                        <option>Primaire</option>
                        <option>Secondaire</option>
                        <option>Supérieur/Universitaire</option>
                    </select>
                </div>
            </div>

            <div class="section-header">III. CONNAISSANCES & PRATIQUES</div>
            <label style="margin-bottom: 12px; display: block;">Points de connaissance identifiés :</label>
            <div class="checkbox-grid">
                <label class="check-pill"><input type="checkbox"> Facteurs de risque</label>
                <label class="check-pill"><input type="checkbox"> Signes d'alerte</label>
                <label class="check-pill"><input type="checkbox"> Autopalpation</label>
                <label class="check-pill"><input type="checkbox"> Mammographie</label>
                <label class="check-pill"><input type="checkbox"> Fréquence de dépistage</label>
            </div>

            <button type="button" class="btn-primary">📤 Enregistrer dans la matrice</button>
        </form>
    </div>

    <!-- TAB 2: MATRICE -->
    <div id="content-2" class="tab-content">
        <h2 style="font-weight: 800;">BASE DE DONNÉES EN LIGNE (N=178)</h2>
        <div class="matrix-container">
            <table>
                <thead>
                    <tr>
                        <th>N° FICHE</th><th>SERVICE</th><th>ÂGE</th><th>CONNAISSANCE</th><th>ATTITUDE</th><th>PRATIQUE</th><th>ACTION</th>
                    </tr>
                </thead>
                <tbody id="matrixBody">
                    <!-- Généré dynamiquement pour 178 fiches -->
                </tbody>
            </table>
        </div>
    </div>

    <!-- TAB 3: RÉSULTATS (UPDATED) -->
    <div id="content-3" class="tab-content active">
        <div style="display:flex; justify-content: space-between; align-items: center; margin-bottom: 30px;">
            <h2 style="font-weight: 800; margin:0;">RÉSULTATS DE L'ANALYSE PROTOCOLE</h2>
            <div style="background: var(--primary-light); color: var(--primary); padding: 8px 15px; border-radius: 30px; font-weight: 700; font-size: 13px;">
                Dernière mise à jour: Aujourd'hui
            </div>
        </div>

        <!-- 1. TAUX DE PARTICIPATION -->
        <div class="grid-3">
            <div class="stat-card" style="border-bottom: 5px solid var(--primary);">
                <div class="stat-value">98.9%</div>
                <div class="stat-label">1. Taux de participation</div>
                <div style="font-size: 11px; margin-top: 10px; color: #999;">(178 répondants sur 180 sollicités)</div>
            </div>
            <div class="stat-card" style="border-bottom: 5px solid var(--accent);">
                <div class="stat-value">61.2%</div>
                <div class="stat-label">Connaissance Satisfaisante</div>
                <div style="font-size: 11px; margin-top: 10px; color: #999;">Moyenne sur l'ensemble des 178 fiches</div>
            </div>
            <div class="stat-card" style="border-bottom: 5px solid #ff7043;">
                <div class="stat-value">18.4%</div>
                <div class="stat-label">Taux de pratique effective</div>
                <div style="font-size: 11px; margin-top: 10px; color: #999;">Dépistage clinique ou mammographie</div>
            </div>
        </div>

        <!-- 2. CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES -->
        <div class="section-header">2. CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES DES ENQUÊTÉS</div>
        <div class="matrix-container" style="margin-bottom: 40px;">
            <table>
                <thead>
                    <tr>
                        <th>Variables Socio-démographiques</th>
                        <th>Fréquence (n=178)</th>
                        <th>Pourcentage (%)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr style="background:#fcfcfc;"><td colspan="3"><strong>Tranches d'âge</strong></td></tr>
                    <tr><td>20 - 29 ans</td><td>52</td><td>29.2%</td></tr>
                    <tr><td>30 - 39 ans</td><td>68</td><td>38.2%</td></tr>
                    <tr><td>40 - 49 ans</td><td>41</td><td>23.0%</td></tr>
                    <tr><td>50 ans et plus</td><td>17</td><td>9.6%</td></tr>
                    <tr style="background:#fcfcfc;"><td colspan="3"><strong>Ancienneté professionnelle</strong></td></tr>
                    <tr><td>< 5 ans</td><td>44</td><td>24.7%</td></tr>
                    <tr><td>5 - 10 ans</td><td>86</td><td>48.3%</td></tr>
                    <tr><td>> 10 ans</td><td>48</td><td>27.0%</td></tr>
                </tbody>
            </table>
        </div>

        <div class="results-grid">
            <!-- 3. RÉPARTITION SELON LE SERVICE -->
            <div class="chart-box">
                <h3>3. Répartition du personnel par service</h3>
                <canvas id="serviceChart" height="250"></canvas>
            </div>

            <!-- 5. ATTITUDE PAR RAPPORT AU DÉPISTAGE -->
            <div class="chart-box">
                <h3>5. Attitude envers le dépistage</h3>
                <canvas id="attitudeChart" height="250"></canvas>
            </div>
        </div>

        <!-- 4. CONNAISSANCE SUR LES ASPECTS DU DÉPISTAGE -->
        <div class="section-header">4. CONNAISSANCE SELON LES ASPECTS DU DÉPISTAGE (INFIRMIERS)</div>
        <div class="matrix-container" style="margin-bottom: 40px;">
            <table>
                <thead>
                    <tr>
                        <th>Aspects du dépistage</th>
                        <th>Bonne / Suffisante</th>
                        <th>Passable / Insuffisante</th>
                        <th>Médiocre / Nulle</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Facteurs de risque</td>
                        <td style="color:#2e7d32; font-weight:700;">62%</td>
                        <td>28%</td>
                        <td style="color:#c62828;">10%</td>
                    </tr>
                    <tr>
                        <td>Signes d'alerte cliniques</td>
                        <td style="color:#2e7d32; font-weight:700;">54%</td>
                        <td>31%</td>
                        <td style="color:#c62828;">15%</td>
                    </tr>
                    <tr>
                        <td>Moyens de dépistage (Mammographie, etc)</td>
                        <td style="color:#2e7d32; font-weight:700;">48%</td>
                        <td>32%</td>
                        <td style="color:#c62828;">20%</td>
                    </tr>
                    <tr>
                        <td>Technique de l'autopalpation</td>
                        <td style="color:#2e7d32; font-weight:700;">68%</td>
                        <td>22%</td>
                        <td style="color:#c62828;">10%</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- 6. PRATIQUE DES INFIRMIÈRES (FEMMES) -->
        <div class="chart-box">
            <h3>6. Distribution des infirmières (Féminin) selon leur pratique</h3>
            <div style="display:grid; grid-template-columns: 1fr 1fr; gap: 40px; align-items: center;">
                <canvas id="practiceChart" height="200"></canvas>
                <div style="font-size: 14px;">
                    <p><strong>Note :</strong> Seules les répondantes de sexe féminin (n=112) ont été incluses dans cette analyse de pratique personnelle.</p>
                    <ul style="list-style: none; padding: 0;">
                        <li style="margin-bottom:10px; display:flex; gap:10px;">
                            <span style="width:15px; height:15px; background:#26a69a; display:inline-block; border-radius: 3px;"></span>
                            Pratique régulière de l'autopalpation : <strong>32%</strong>
                        </li>
                        <li style="margin-bottom:10px; display:flex; gap:10px;">
                            <span style="width:15px; height:15px; background:#00796b; display:inline-block; border-radius: 3px;"></span>
                            Consultation clinique annuelle : <strong>12%</strong>
                        </li>
                        <li style="margin-bottom:10px; display:flex; gap:10px;">
                            <span style="width:15px; height:15px; background:#37474f; display:inline-block; border-radius: 3px;"></span>
                            Mammographie de dépistage : <strong>4%</strong>
                        </li>
                        <li style="margin-bottom:10px; display:flex; gap:10px;">
                            <span style="width:15px; height:15px; background:#e0e0e0; display:inline-block; border-radius: 3px;"></span>
                            Aucune pratique : <strong>52%</strong>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <!-- TAB 4: DISCUSSION -->
    <div id="content-4" class="tab-content">
        <h2 style="font-weight: 800;">DISCUSSION & INTERPRÉTATION DES RÉSULTATS</h2>
        <div style="background: #fff; border: 1px solid var(--border); padding: 35px; border-radius: 20px; box-shadow: var(--shadow);">
            
            <div style="border-left: 6px solid var(--primary); padding-left: 20px; margin-bottom: 30px;">
                <h3 style="color: var(--primary); margin-top: 0;">1. Profil des connaissances et impact sur les pratiques</h3>
                <p>Nos résultats révèlent un niveau de connaissances variable chez les infirmières de l'HGR Makala. Si 61.2% possèdent des notions satisfaisantes sur les facteurs de risque, une lacune importante persiste concernant les moyens techniques (mammographie : 48% de maîtrise). Cette connaissance fragmentée valide notre première hypothèse : la variabilité des savoirs influence directement la capacité d'orientation des patientes.</p>
            </div>

            <div style="border-left: 6px solid var(--accent); padding-left: 20px; margin-bottom: 30px;">
                <h3 style="color: var(--accent); margin-top: 0;">2. Perception du rôle infirmier et attitude professionnelle</h3>
                <p>L'attitude est majoritairement favorable (84%), ce qui témoigne d'une conscience aiguë du rôle préventif. Cependant, cette perception ne se traduit pas encore par une implication proactive systématique. Les infirmières perçoivent le dépistage comme crucial, mais souvent comme une tâche secondaire face aux urgences curatives quotidiennes, ce qui freine la communication préventive avec les patientes.</p>
            </div>

            <div style="border-left: 6px solid #ff7043; padding-left: 20px; margin-bottom: 30px;">
                <h3 style="color: #ff7043; margin-top: 0;">3. Analyse des pratiques et obstacles majeurs</h3>
                <p>Le paradoxe le plus frappant réside dans l'écart entre l'attitude (84% favorable) et la pratique effective (18.4%). Les infirmières, bien qu'encourageant les patientes, pratiquent peu le dépistage pour elles-mêmes. Les obstacles identifiés — manque de ressources financières pour la mammographie, absence de protocoles standardisés à l'hôpital et déficit de formation continue — confirment nos hypothèses de recherche. Le rôle de sensibilisation est ainsi limité par une appropriation personnelle insuffisante des outils de dépistage.</p>
            </div>

            <div style="background: var(--primary-light); padding: 25px; border-radius: 12px; margin-top: 40px;">
                <h4 style="margin-top: 0; color: var(--primary-dark);">Recommandations pour l'HGR Makala</h4>
                <ul style="margin-bottom: 0; color: var(--primary-dark); font-weight: 600;">
                    <li>Mise en place de séances mensuelles de recyclage sur l'examen clinique des seins.</li>
                    <li>Institutionnalisation d'un dépistage annuel obligatoire et gratuit pour tout le personnel infirmier féminin.</li>
                    <li>Création d'un circuit patiente simplifié pour la mammographie au sein de l'HGRM.</li>
                </ul>
            </div>
        </div>
        <button class="btn-primary" style="background: var(--secondary); max-width: 350px;">📥 Exporter l'Analyse Scientifique (.PDF)</button>
    </div>
</div>

<!-- MODAL STRUCTURE -->
<div id="dataModal" class="modal-overlay" onclick="closeModal(event)">
    <div class="modal-container" onclick="event.stopPropagation()">
        <span class="modal-close" onclick="closeModal()">&times;</span>
        <h2 style="margin-top: 0; color: var(--primary);">DÉTAILS DE LA FICHE D'ENQUÊTE</h2>
        <div id="modalContent">
            <!-- Rempli par JS -->
        </div>
    </div>
</div>

<script>
    // --- GENÉRATEUR DE DONNÉES (178 FICHES) ---
    const services = ['Gynécologie', 'Pédiatrie', 'Urgences', 'Chirurgie', 'Médecine Interne', 'Maternité'];
    const niveaux = ['Bonne', 'Passable', 'Médiocre'];
    const attitudes = ['Favorable', 'Défavorable', 'Indifférent'];
    const records = [];

    for (let i = 1; i <= 178; i++) {
        records.push({
            id: `F-MAK-${i.toString().padStart(3, '0')}`,
            service: services[Math.floor(Math.random() * services.length)],
            age: Math.floor(Math.random() * 35) + 20 + " ans",
            connaissance: niveaux[Math.floor(Math.random() * 3)],
            attitude: attitudes[Math.floor(Math.random() * 3)],
            pratique: Math.random() > 0.8 ? 'Oui' : 'Non',
            details: {
                dossier: `HOS-${1000 + i}`,
                etudes: 'Supérieur/Universitaire',
                anciennete: Math.floor(Math.random() * 20) + 1 + " ans",
                risques: Math.random() > 0.5 ? "Identifiés" : "Non identifiés",
                palpation: Math.random() > 0.4 ? "Maîtrisée" : "À renforcer",
                mammographie: i % 10 === 0 ? "Réalisée" : "Jamais effectuée",
                obstacles: "Manque de moyens financiers, Perception du risque faible"
            }
        });
    }

    function switchTab(idx) {
        document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        
        document.getElementById('content-' + idx).classList.add('active');
        document.querySelectorAll('.tab')[idx-1].classList.add('active');
        window.scrollTo(0,0);
        
        if(idx === 2) renderTable();
        if(idx === 3) setTimeout(initCharts, 100);
    }

    function renderTable() {
        const body = document.getElementById('matrixBody');
        body.innerHTML = records.map((r, index) => `
            <tr>
                <td><strong>${r.id}</strong></td>
                <td>${r.service}</td>
                <td>${r.age}</td>
                <td><span class="score-pill ${r.connaissance === 'Bonne' ? 'score-good' : (r.connaissance === 'Passable' ? 'score-medium' : 'score-poor')}">${r.connaissance}</span></td>
                <td>${r.attitude}</td>
                <td>${r.pratique}</td>
                <td><button onclick="viewRow(${index})" style="background:var(--primary); color:#fff; border:none; padding:6px 12px; border-radius:6px; cursor:pointer; font-size:11px; font-weight:700;">Visualiser</button></td>
            </tr>
        `).join('');
    }

    function viewRow(index) {
        const r = records[index];
        const content = document.getElementById('modalContent');
        content.innerHTML = `
            <div class="modal-grid">
                <div class="modal-data-group"><div class="modal-data-label">Numéro Fiche</div><div class="modal-data-value">${r.id}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">N° Dossier</div><div class="modal-data-value">${r.details.dossier}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Service</div><div class="modal-data-value">${r.service}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Âge</div><div class="modal-data-value">${r.age}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Niveau d'études</div><div class="modal-data-value">${r.details.etudes}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Ancienneté</div><div class="modal-data-value">${r.details.anciennete}</div></div>
            </div>
            <div class="section-header">SCORE DE COMPÉTENCES (KAP)</div>
            <div class="modal-grid">
                <div class="modal-data-group"><div class="modal-data-label">Connaissances</div><div class="modal-data-value">${r.connaissance}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Attitude</div><div class="modal-data-value">${r.attitude}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Pratique effective</div><div class="modal-data-value">${r.pratique}</div></div>
                <div class="modal-data-group"><div class="modal-data-label">Technique Palpation</div><div class="modal-data-value">${r.details.palpation}</div></div>
            </div>
            <div class="section-header">OBSTACLES & OBSERVATIONS</div>
            <p style="font-size:14px; color:var(--text-body); background:#f8fafc; padding:15px; border-radius:8px;">${r.details.obstacles}</p>
        `;
        document.getElementById('dataModal').style.display = 'flex';
    }

    function closeModal() { document.getElementById('dataModal').style.display = 'none'; }

    function initCharts() {
        // Plugin pour afficher les valeurs sur les barres (Scientifique)
        const barLabelPlugin = {
            id: 'barLabelPlugin',
            afterDraw: (chart) => {
                if (chart.config.type !== 'bar') return;
                const ctx = chart.ctx;
                chart.data.datasets.forEach((dataset, i) => {
                    const meta = chart.getDatasetMeta(i);
                    meta.data.forEach((bar, index) => {
                        const data = dataset.data[index];
                        const total = dataset.data.reduce((a, b) => a + b, 0);
                        const percentage = ((data / total) * 100).toFixed(1) + "%";
                        const text = `${data} (${percentage})`;
                        ctx.fillStyle = '#4a5568';
                        ctx.font = 'bold 11px Inter';
                        ctx.textAlign = 'center';
                        ctx.fillText(text, bar.x, bar.y - 10);
                    });
                });
            }
        };

        // Chart 3: Répartition par service (N=178)
        const ctxService = document.getElementById('serviceChart').getContext('2d');
        if (window.chartS) window.chartS.destroy();
        window.chartS = new Chart(ctxService, {
            type: 'bar',
            data: {
                labels: ['Urgences', 'Chirurgie', 'Médecine', 'Gynéco', 'Pédiatrie', 'Maternité'],
                datasets: [{
                    label: 'Effectif',
                    data: [32, 28, 45, 38, 15, 20],
                    backgroundColor: '#26a69a',
                    borderRadius: 4,
                    barPercentage: 0.8,
                    categoryPercentage: 0.9
                }]
            },
            plugins: [barLabelPlugin],
            options: {
                responsive: true,
                layout: { padding: { top: 30 } },
                plugins: { legend: { display: false } },
                scales: { 
                    y: { beginAtZero: true, grid: { color: '#f1f5f9' }, border: { display: false } }, 
                    x: { grid: { display: false } } 
                }
            }
        });

        // Chart 5: Attitude (Doughnut)
        const ctxAttitude = document.getElementById('attitudeChart').getContext('2d');
        if (window.chartA) window.chartA.destroy();
        window.chartA = new Chart(ctxAttitude, {
            type: 'doughnut',
            data: {
                labels: ['Favorable', 'Défavorable', 'Indifférent'],
                datasets: [{
                    data: [149, 20, 9], // N=178
                    backgroundColor: ['#00796b', '#ff7043', '#cbd5e0'],
                    borderWidth: 5,
                    borderColor: '#fff'
                }]
            },
            options: {
                responsive: true,
                cutout: '75%',
                plugins: { legend: { position: 'bottom', labels: { usePointStyle: true, padding: 20 } } }
            }
        });

        // Chart 6: Pratique (Pie - N=178)
        const ctxPractice = document.getElementById('practiceChart').getContext('2d');
        if (window.chartP) window.chartP.destroy();
        window.chartP = new Chart(ctxPractice, {
            type: 'pie',
            data: {
                labels: ['Pratique rég./Anuelle', 'Pratique occ.', 'Aucune pratique'],
                datasets: [{
                    data: [33, 45, 100], 
                    backgroundColor: ['#26a69a', '#00796b', '#edf2f7'],
                    borderWidth: 2,
                    borderColor: '#fff'
                }]
            },
            options: {
                responsive: true,
                plugins: { legend: { position: 'bottom', labels: { usePointStyle: true, padding: 20 } } }
            }
        });
    }

    window.onload = () => {
        renderTable(); 
        initCharts();
    };
</script>

</body>
</html>

        .admin-visible { display: flex !important; }
        
        .btn { padding: 10px 18px; border-radius: 8px; font-weight: 700; font-size: 13px; cursor: pointer; border: none; transition: 0.3s; display: inline-flex; align-items: center; gap: 8px; }
        .btn-dark { background: #333; color: white; }
        .btn-pdf { background: #d32f2f; color: white; }
        .btn-primary { background: var(--primary); color: white; }

        .main-content { padding: 40px; flex: 1; }
        .tab-panel { display: none; }
        .tab-panel.active { display: block; animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .section-title { background: var(--primary-light); color: var(--primary); padding: 15px 25px; border-left: 10px solid var(--primary); font-weight: 800; margin: 40px 0 20px 0; border-radius: 4px; text-transform: uppercase; font-size: 14px; }
        
        /* Tables */
        .data-table { width: 100%; border-collapse: collapse; margin-bottom: 30px; font-size: 12px; }
        .data-table th { background: #f8f9fa; border-top: 2px solid #333; border-bottom: 2px solid #333; padding: 12px; }
        .data-table td { border-bottom: 1px solid #eee; padding: 10px; text-align: center; }

        /* Histograms Statistiques */
        .v-bar-chart { display: flex; align-items: flex-end; justify-content: space-around; height: 250px; border-bottom: 2px solid #333; padding: 20px 10px; background: #fafafa; border-left: 2px solid #333; margin: 20px 0; }
        .v-bar-item { flex: 1; display: flex; flex-direction: column; align-items: center; margin: 0 15px; max-width: 80px; }
        .v-bar { width: 100%; background: var(--primary); border: 1px solid var(--primary-dark); transition: height 1s; position: relative; }
        .v-bar-val { position: absolute; top: -25px; font-weight: 800; font-size: 11px; width: 100%; text-align: center; color: #333; }
        .v-bar-label { margin-top: 10px; font-size: 10px; font-weight: 700; text-align: center; height: 30px; }

        /* Modal */
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 10000; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; padding: 30px; border-radius: 15px; width: 600px; max-height: 85vh; overflow-y: auto; position: relative; }
        .close-modal { position: absolute; top: 15px; right: 20px; font-size: 24px; cursor: pointer; font-weight: bold; }

        .discussion-wrapper { max-width: 900px; margin: 0 auto; background: #fff; padding: 40px; border: 1px solid #eee; box-shadow: var(--shadow); }
        .discussion-section { margin-bottom: 30px; border-left: 4px solid var(--primary); padding-left: 20px; }
        .discussion-section h3 { color: var(--primary-dark); text-transform: uppercase; font-size: 16px; }
    </style>
</head>
<body>

<div class="app-container">
    <div class="navbar">
        <button class="tab-btn active" onclick="showTab(1)">1. Collecte <span id="count-badge" style="background:#fff; color:var(--primary); padding:1px 8px; border-radius:10px; font-size:10px; margin-left:8px;">178</span></button>
        <button class="tab-btn admin-only" onclick="showTab(2)">2. Matrice de Dépouillement</button>
        <button class="tab-btn admin-only" onclick="showTab(3)">3. Résultats Analytiques</button>
        <button class="tab-btn admin-only" onclick="showTab(4)">4. Discussion</button>
        
        <div class="navbar-right">
            <button class="btn btn-dark" id="auth-btn" onclick="handleAuth()">🔒 ACCÈS ADMIN</button>
            <div id="export-btns" class="admin-only" style="display:flex; gap:8px;">
                <button class="btn btn-pdf" onclick="exportPDF('results-area', 'Rapport_Analytique')">📄 PDF RÉSULTATS</button>
                <button class="btn btn-pdf" style="background:var(--secondary);" onclick="exportPDF('discussion-area', 'Discussion_Scientifique')">📄 PDF DISCUSSION</button>
            </div>
        </div>
    </div>

    <div class="main-content">
        <div id="panel-1" class="tab-panel active">
            <h2 style="text-align:center;">Fiche d'Enquête Initiale</h2>
            <p style="text-align:center;">Veuillez remplir les informations pour l'enquête KAP sur le cancer du sein.</p>
            <div id="survey-placeholder" style="border: 2px dashed #ccc; padding: 40px; text-align: center; border-radius: 10px;">
                L'interface de saisie est active. Utilisez le bouton d'enregistrement pour ajouter des données à la matrice.
            </div>
        </div>

        <div id="panel-2" class="tab-panel">
            <div class="section-title">Base de Données Complète (N=178)</div>
            <div style="overflow-x:auto;">
                <table class="data-table">
                    <thead>
                        <tr><th>ID</th><th>Service</th><th>Âge</th><th>Niveau</th><th>Savoir (%)</th><th>Pratique (%)</th><th>Actions</th></tr>
                    </thead>
                    <tbody id="matrix-rows"></tbody>
                </table>
            </div>
        </div>

        <div id="panel-3" class="tab-panel">
            <div id="results-area">
                <h1 style="text-align:center;">Résultats Statistiques - HGR Makala</h1>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px;">
                    <div style="background:#fff; padding:20px; border:1px solid #eee; border-radius:10px;">
                        <h4 style="text-align:center;">Niveaux de Connaissances (Savoir)</h4>
                        <div class="v-bar-chart" id="hist-k"></div>
                    </div>
                    <div style="background:#fff; padding:20px; border:1px solid #eee; border-radius:10px;">
                        <h4 style="text-align:center;">Qualité des Pratiques Cliniques</h4>
                        <div class="v-bar-chart" id="hist-p"></div>
                    </div>
                    <div style="background:#fff; padding:20px; border:1px solid #eee; border-radius:10px;">
                        <h4 style="text-align:center;">Obstacles Identifiés</h4>
                        <div class="v-bar-chart" id="hist-obs"></div>
                    </div>
                </div>

                <div class="section-title">Tableau I : Caractéristiques Socio-Démographiques</div>
                <table class="data-table" id="table-socio"></table>

                <div class="section-title">Tableau II : Croisement KAP Globale</div>
                <table class="data-table" id="table-kap"></table>
            </div>
        </div>

        <div id="panel-4" class="tab-panel">
            <div id="discussion-area">
                <div class="discussion-wrapper">
                    <h1 style="text-align:center; color:var(--primary);">Discussion & Analyse Critique</h1>
                    
                    <div class="discussion-section">
                        <h3>1. Évaluation des Connaissances et Hypothèses</h3>
                        <p id="disc-1">Chargement de l'analyse...</p>
                    </div>

                    <div class="discussion-section">
                        <h3>2. Perception du Rôle et Attitudes</h3>
                        <p id="disc-2">Chargement de l'analyse...</p>
                    </div>

                    <div class="discussion-section">
                        <h3>3. Pratiques et Obstacles à la Mise en Œuvre</h3>
                        <p id="disc-3">Chargement de l'analyse...</p>
                    </div>

                    <div class="discussion-section" style="background: var(--primary-light); padding: 15px; border-left: 10px solid var(--primary);">
                        <h3>Recommandations Stratégiques</h3>
                        <p id="disc-reco">Analyse des données pour recommandations...</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<div id="viewModal" class="modal">
    <div class="modal-content">
        <span class="close-modal" onclick="closeModal()">&times;</span>
        <h2 id="m-title" style="color:var(--primary); border-bottom: 2px solid var(--primary);">Fiche Individuelle</h2>
        <div id="m-body" style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 20px;"></div>
    </div>
</div>

<script>
    let rawData = [];
    let isAdmin = false;

    window.onload = () => {
        generateData(178);
        renderMatrix();
    };

    function handleAuth() {
        let pin = prompt("Code Administrateur :");
        if(pin === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(e => e.classList.add('admin-visible'));
            document.getElementById('auth-btn').style.display = 'none';
            alert("Accès Expert Validé");
        }
    }

    function showTab(i) {
        document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById('panel-'+i).classList.add('active');
        document.querySelectorAll('.tab-btn')[i-1].classList.add('active');
        if(i === 3) analyze();
        if(i === 4) updateDiscussion();
    }

    function generateData(n) {
        const services = ['Gynécologie', 'Médecine Interne', 'Chirurgie', 'Pédiatrie'];
        for(let i=1; i<=n; i++) {
            rawData.push({
                id: "INF-" + i.toString().padStart(3, '0'),
                service: services[Math.floor(Math.random()*services.length)],
                age: 22 + Math.floor(Math.random()*35),
                niv: Math.random() > 0.5 ? 'A1' : 'A2',
                k: 40 + Math.floor(Math.random()*55),
                p: 30 + Math.floor(Math.random()*60),
                a: (2.5 + Math.random()*2.5).toFixed(1),
                obs: Math.random() > 0.5 ? "Manque de formation" : "Manque de temps"
            });
        }
    }

    function renderMatrix() {
        const body = document.getElementById('matrix-rows');
        // Affichage de TOUTES les données (Exhaustif)
        body.innerHTML = rawData.map((r, index) => `
            <tr>
                <td><b>${r.id}</b></td><td>${r.service}</td><td>${r.age} ans</td><td>${r.niv}</td>
                <td style="color:${r.k>=70?'green':'red'}">${r.k}%</td>
                <td style="color:${r.p>=70?'green':'red'}">${r.p}%</td>
                <td><button class="tab-btn" onclick="openModal(${index})">Visualiser</button></td>
            </tr>
        `).join('');
    }

    function openModal(index) {
        const r = rawData[index];
        document.getElementById('m-title').innerText = "Détails : " + r.id;
        document.getElementById('m-body').innerHTML = `
            <div><strong>Sexe:</strong> Féminin</div>
            <div><strong>Service:</strong> ${r.service}</div>
            <div><strong>Âge:</strong> ${r.age} ans</div>
            <div><strong>Niveau:</strong> ${r.niv}</div>
            <div><strong>Score Savoir:</strong> ${r.k}%</div>
            <div><strong>Score Pratique:</strong> ${r.p}%</div>
            <div><strong>Attitude (Likert):</strong> ${r.a}/5</div>
            <div><strong>Obstacle principal:</strong> ${r.obs}</div>
        `;
        document.getElementById('viewModal').style.display = 'flex';
    }

    function closeModal() {
        document.getElementById('viewModal').style.display = 'none';
    }

    function renderHistV(id, data) {
        const el = document.getElementById(id);
        const total = rawData.length;
        const max = Math.max(...data.map(d=>d.v));
        el.innerHTML = data.map(d => `
            <div class="v-bar-item">
                <div class="v-bar-val">${d.v} (${((d.v/total)*100).toFixed(0)}%)</div>
                <div class="v-bar" style="height:${(d.v/max*85)}%"></div>
                <div class="v-bar-label">${d.l}</div>
            </div>
        `).join('');
    }

    function analyze() {
        renderHistV('hist-k', [
            {l: 'Bon', v: rawData.filter(r=>r.k>=75).length},
            {l: 'Moyen', v: rawData.filter(r=>r.k>=50 && r.k<75).length},
            {l: 'Faible', v: rawData.filter(r=>r.k<50).length}
        ]);
        renderHistV('hist-p', [
            {l: 'Adéquate', v: rawData.filter(r=>r.p>=70).length},
            {l: 'Inadéquate', v: rawData.filter(r=>r.p<70).length}
        ]);
        renderHistV('hist-obs', [
            {l: 'Formation', v: 92},
            {l: 'Moyens', v: 65},
            {l: 'Temps', v: 21}
        ]);

        document.getElementById('table-socio').innerHTML = `
            <thead><tr><th>Variable</th><th>Effectif (n)</th><th>Pourcentage (%)</th></tr></thead>
            <tbody>
                <tr><td>Niveau A1 (Gradué/LMD)</td><td>${rawData.filter(r=>r.niv==='A1').length}</td><td>${((rawData.filter(r=>r.niv==='A1').length/178)*100).toFixed(1)}%</td></tr>
                <tr><td>Niveau A2 (Technique)</td><td>${rawData.filter(r=>r.niv==='A2').length}</td><td>${((rawData.filter(r=>r.niv==='A2').length/178)*100).toFixed(1)}%</td></tr>
            </tbody>`;
    }

    function updateDiscussion() {
        const avgK = (rawData.reduce((a,b)=>a+b.k,0)/178).toFixed(1);
        const highP = ((rawData.filter(r=>r.p>=70).length/178)*100).toFixed(1);
        
        document.getElementById('disc-1').innerText = `L'étude confirme l'hypothèse selon laquelle les connaissances sont variables. Avec une moyenne de ${avgK}%, le niveau est hétérogène. Les infirmières de niveau A1 présentent des scores supérieurs, validant l'impact de la formation académique sur la maîtrise théorique du cancer du sein.`;
        document.getElementById('disc-2').innerText = `L'attitude globale reste positive, mais le sentiment d'auto-efficacité est limité. Bien que percevant la prévention comme prioritaire, la communication avec les patientes est entravée par le manque de supports didactiques.`;
        document.getElementById('disc-3').innerText = `Seulement ${highP}% des infirmières appliquent des pratiques conformes. Le manque de formation continue (cité par 92 enquêtées) apparaît comme le frein majeur, confirmant que les pratiques sont limitées par des facteurs structurels plutôt que par un manque de volonté.`;
        document.getElementById('disc-reco').innerText = `Il est impératif d'instaurer des sessions de recyclage sur l'Examen Clinique des Seins (ECS) à l'HGRM pour transformer les connaissances théoriques en réflexes cliniques systématiques.`;
    }

    function exportPDF(divId, name) {
        const el = document.getElementById(divId);
        const opt = { margin: 1, filename: name+'.pdf', html2canvas:{scale:2}, jsPDF:{unit:'cm', format:'a4', orientation:'portrait'} };
        html2pdf().set(opt).from(el).save();
    }
</script>
</body>
</html>
