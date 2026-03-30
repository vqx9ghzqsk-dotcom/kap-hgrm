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
            --bg-body: #f0f4f8;
            --bg-card: #ffffff;
            --text-title: #263238;
            --text-body: #455a64;
            --border: #e0e6ed;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

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
            <button class="tab" onclick="switchTab(1)">1. Collecte 📋 <span class="badge-count" id="badge-1">150</span></button>
            <button class="tab" onclick="switchTab(2)">2. Matrice de Dépouillement 📊</button>
            <button class="tab active" onclick="switchTab(3)">3. Résultats & Analyse 📈</button>
            <button class="tab" onclick="switchTab(4)">4. Synthèse finale 📄</button>
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
        <h2 style="font-weight: 800;">BASE DE DONNÉES EN LIGNE (N=150)</h2>
        <div class="matrix-container">
            <table>
                <thead>
                    <tr>
                        <th>N° FICHE</th><th>SERVICE</th><th>ÂGE</th><th>CONNAISSANCE</th><th>ATTITUDE</th><th>PRATIQUE</th><th>ACTION</th>
                    </tr>
                </thead>
                <tbody id="matrixBody">
                    <tr><td>F-MAK-001</td><td>Gynécologie</td><td>34 ans</td><td>Bonne</td><td>Favorable</td><td>Oui</td><td><button style="font-size:10px; padding:5px 10px; border-radius:5px; border:1px solid #ccc; cursor:pointer;">Éditer</button></td></tr>
                    <tr><td>F-MAK-002</td><td>Pédiatrie</td><td>42 ans</td><td>Médiocre</td><td>Favorable</td><td>Non</td><td><button style="font-size:10px; padding:5px 10px; border-radius:5px; border:1px solid #ccc; cursor:pointer;">Éditer</button></td></tr>
                    <tr><td>F-MAK-003</td><td>Urgences</td><td>29 ans</td><td>Passable</td><td>Défavorable</td><td>Non</td><td><button style="font-size:10px; padding:5px 10px; border-radius:5px; border:1px solid #ccc; cursor:pointer;">Éditer</button></td></tr>
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
                <div class="stat-value">93.7%</div>
                <div class="stat-label">1. Taux de participation</div>
                <div style="font-size: 11px; margin-top: 10px; color: #999;">(150 répondants sur 160 sollicités)</div>
            </div>
            <div class="stat-card" style="border-bottom: 5px solid var(--accent);">
                <div class="stat-value">58%</div>
                <div class="stat-label">Connaissance Satisfaisante</div>
                <div style="font-size: 11px; margin-top: 10px; color: #999;">Moyenne globale du personnel</div>
            </div>
            <div class="stat-card" style="border-bottom: 5px solid #ff7043;">
                <div class="stat-value">24.5%</div>
                <div class="stat-label">Taux de pratique effective</div>
                <div style="font-size: 11px; margin-top: 10px; color: #999;">Chez le personnel féminin</div>
            </div>
        </div>

        <!-- 2. CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES -->
        <div class="section-header">2. CARACTÉRISTIQUES SOCIO-DÉMOGRAPHIQUES DES ENQUÊTÉS</div>
        <div class="matrix-container" style="margin-bottom: 40px;">
            <table>
                <thead>
                    <tr>
                        <th>Variables Socio-démographiques</th>
                        <th>Fréquence (n=150)</th>
                        <th>Pourcentage (%)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr style="background:#fcfcfc;"><td colspan="3"><strong>Tranches d'âge</strong></td></tr>
                    <tr><td>20 - 29 ans</td><td>42</td><td>28.0%</td></tr>
                    <tr><td>30 - 39 ans</td><td>58</td><td>38.7%</td></tr>
                    <tr><td>40 - 49 ans</td><td>35</td><td>23.3%</td></tr>
                    <tr><td>50 ans et plus</td><td>15</td><td>10.0%</td></tr>
                    <tr style="background:#fcfcfc;"><td colspan="3"><strong>Ancienneté professionnelle</strong></td></tr>
                    <tr><td>< 5 ans</td><td>38</td><td>25.3%</td></tr>
                    <tr><td>5 - 10 ans</td><td>72</td><td>48.0%</td></tr>
                    <tr><td>> 10 ans</td><td>40</td><td>26.7%</td></tr>
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

    <!-- TAB 4: SYNTHÈSE -->
    <div id="content-4" class="tab-content">
        <h2 style="font-weight: 800;">RAPPORT FINAL DE SYNTHÈSE</h2>
        <div style="background: #fff; border: 1px solid var(--border); padding: 30px; border-radius: 15px; border-left: 10px solid var(--primary);">
            <p><strong>Conclusion Intérimaire :</strong> Bien que la majorité du personnel infirmier possède une attitude favorable (84%) vis-à-vis du dépistage, la pratique effective reste très faible (24.5% au global), particulièrement chez le personnel féminin exposé au risque. Un renforcement des capacités sur la mammographie et l'examen clinique est préconisé au sein de l'HGR Makala.</p>
        </div>
        <button class="btn-primary" style="background: var(--secondary); max-width: 300px;">📥 Télécharger le rapport (.CSV)</button>
    </div>
</div>

<script>
    function switchTab(idx) {
        document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        
        document.getElementById('content-' + idx).classList.add('active');
        document.querySelectorAll('.tab')[idx-1].classList.add('active');
        window.scrollTo(0,0);
        
        // Re-init charts if switching to tab 3
        if(idx === 3) initCharts();
    }

    function initCharts() {
        // Chart 3: Répartition par service
        const ctxService = document.getElementById('serviceChart').getContext('2d');
        new Chart(ctxService, {
            type: 'bar',
            data: {
                labels: ['Urgences', 'Chirurgie', 'Médecine', 'Gynéco', 'Pédiatrie'],
                datasets: [{
                    label: 'Nombre de personnel',
                    data: [25, 35, 40, 30, 20],
                    backgroundColor: '#26a69a',
                    borderRadius: 8
                }]
            },
            options: {
                responsive: true,
                plugins: { legend: { display: false } },
                scales: { y: { beginAtZero: true, grid: { display: false } }, x: { grid: { display: false } } }
            }
        });

        // Chart 5: Attitude
        const ctxAttitude = document.getElementById('attitudeChart').getContext('2d');
        new Chart(ctxAttitude, {
            type: 'doughnut',
            data: {
                labels: ['Favorable', 'Défavorable', 'Indifférent'],
                datasets: [{
                    data: [84, 11, 5],
                    backgroundColor: ['#00796b', '#ff7043', '#cfd8dc'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                cutout: '70%',
                plugins: { legend: { position: 'bottom' } }
            }
        });

        // Chart 6: Pratique (Féminin)
        const ctxPractice = document.getElementById('practiceChart').getContext('2d');
        new Chart(ctxPractice, {
            type: 'pie',
            data: {
                labels: ['Pratiquantes', 'Non-pratiquantes'],
                datasets: [{
                    data: [36, 76], // Sur 112 femmes
                    backgroundColor: ['#00796b', '#e0e0e0'],
                    borderWidth: 2,
                    borderColor: '#fff'
                }]
            },
            options: {
                responsive: true,
                plugins: { legend: { position: 'bottom' } }
            }
        });
    }

    // Initialize charts on load since tab 3 is active by default in the mockup
    window.onload = initCharts;
</script>

</body>
</html>
