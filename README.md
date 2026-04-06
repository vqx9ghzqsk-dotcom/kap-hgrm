<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard Recherche | Cancer du Sein HGR Makala</title>
    <!-- Google Fonts: Inter for UI, Merriweather for Reports -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Merriweather:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
    <style>
        /* --- DESIGN SYSTEM --- */
        :root {
            --primary: #b03060; /* Deep Pink */
            --primary-dark: #880e4f;
            --primary-light: #fce4ec;
            --secondary: #0d47a1; /* Clinical Blue */
            --bg-body: #f8fafc;
            --bg-card: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --border-color: #e2e8f0;
            --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);
            --shadow-md: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0,0.06);
            --shadow-lg: 0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05);
            --radius: 12px;
            --radius-sm: 6px;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { 
            font-family: 'Inter', sans-serif; 
            background-color: var(--bg-body); 
            color: var(--text-main); 
            line-height: 1.6;
            padding: 20px;
        }

        .container { 
            max-width: 1400px; 
            margin: auto; 
            background: var(--bg-card); 
            border-radius: var(--radius); 
            box-shadow: var(--shadow-lg); 
            min-height: 90vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        /* --- HEADER & NAVIGATION --- */
        .app-header {
            background: white;
            border-bottom: 2px solid var(--primary-light);
            padding: 20px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .app-title {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .app-title h1 {
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--primary);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        .ribbon-icon {
            width: 40px;
            height: 40px;
            background: var(--primary);
            mask-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M12,2C10.34,2,9,3.34,9,5c0,1.21,0.72,2.26,1.75,2.75L6.5,15.5C5.5,17.5,6.5,20,9,20c1.5,0,2.5-0.5,3-1.5c0.5,1,1.5,1.5,3,1.5c2.5,0,3.5-2.5,2.5-4.5l-4.25-7.75C14.28,7.26,15,6.21,15,5C15,3.34,13.66,2,12,2z M12,4c0.55,0,1,0.45,1,1s-0.45,1-1,1s-1-0.45-1-1S11.45,4,12,4z"/></svg>');
            -webkit-mask-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M12,2C10.34,2,9,3.34,9,5c0,1.21,0.72,2.26,1.75,2.75L6.5,15.5C5.5,17.5,6.5,20,9,20c1.5,0,2.5-0.5,3-1.5c0.5,1,1.5,1.5,3,1.5c2.5,0,3.5-2.5,2.5-4.5l-4.25-7.75C14.28,7.26,15,6.21,15,5C15,3.34,13.66,2,12,2z M12,4c0.55,0,1,0.45,1,1s-0.45,1-1,1s-1-0.45-1-1S11.45,4,12,4z"/></svg>');
            mask-size: cover;
            -webkit-mask-size: cover;
        }

        .header-tabs { 
            display: flex; 
            background: #f1f5f9; 
            padding: 6px; 
            gap: 4px;
            border-bottom: 1px solid var(--border-color);
        }
        .tab { 
            padding: 10px 18px; 
            font-weight: 600; 
            font-size: 13px; 
            border: none; 
            border-radius: var(--radius-sm); 
            color: var(--text-muted); 
            background: transparent; 
            cursor: pointer; 
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .tab:hover { background: rgba(0,0,0,0.05); color: var(--text-main); }
        .tab.active { 
            background: white; 
            color: var(--primary); 
            box-shadow: var(--shadow-sm); 
        }
        
        .header-actions {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 30px;
            background: #f8fafc;
            border-bottom: 1px solid var(--border-color);
        }

        /* --- SYSTEM BADGES --- */
        .sim-badge { background: #ff9800; color: white; padding: 4px 10px; border-radius: 20px; font-size: 11px; font-weight: 700; }
        .admin-only { display: none !important; }
        .admin-visible { display: flex !important; }

        .btn-premium {
            padding: 10px 16px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 13px;
            cursor: pointer;
            border: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: 0.2s;
        }
        .btn-primary { background: var(--primary); color: white; }
        .btn-primary:hover { background: var(--primary-dark); transform: translateY(-1px); }
        .btn-secondary { background: #334155; color: white; }
        .btn-success { background: #10b981; color: white; }

        /* --- CONTENT AREAS --- */
        .form-content { 
            padding: 40px; 
            display: none; 
            max-height: calc(90vh - 150px);
            overflow-y: auto;
            scrollbar-width: thin;
        }
        .form-content.active { display: block; animation: slideIn 0.4s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* --- FORMS AND FIELDS --- */
        .section-title { 
            background: var(--primary-light); 
            color: var(--primary-dark); 
            padding: 16px 20px; 
            font-weight: 700; 
            border-radius: var(--radius-sm);
            margin: 30px 0 20px 0; 
            text-transform: uppercase; 
            font-size: 14px; 
            display: flex; 
            align-items: center; 
            justify-content: space-between; 
            border-left: 4px solid var(--primary);
        }
        .sub-title { font-weight: 700; color: var(--primary); margin: 25px 0 10px 0; font-size: 15px; border-bottom: 2px solid var(--primary-light); display: inline-block; padding-bottom: 4px; }
        
        .grid-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 24px; margin-bottom: 20px; }
        .field { display: flex; flex-direction: column; gap: 8px; }
        label { font-size: 13px; font-weight: 600; color: var(--text-main); }
        select, input, textarea { 
            padding: 12px; 
            border: 1px solid var(--border-color); 
            border-radius: 8px; 
            font-size: 14px; 
            background: #fff; 
            width: 100%; 
            transition: 0.2s;
        }
        select:focus, input:focus { border-color: var(--primary); outline: none; box-shadow: 0 0 0 3px var(--primary-light); }

        .check-group { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); 
            gap: 12px; 
            background: #fbfcfe; 
            padding: 20px; 
            border: 1px solid var(--border-color); 
            border-radius: var(--radius); 
        }
        .check-item { 
            display: flex; 
            align-items: center; 
            gap: 10px;
            font-size: 13px; 
            cursor: pointer; 
            padding: 8px;
            border-radius: 6px;
            transition: 0.2s;
        }
        .check-item:hover { background: white; box-shadow: var(--shadow-sm); }
        .check-item input { width: auto; transform: scale(1.1); }

        /* --- DASHBOARD ELEMENTS --- */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 30px; }
        .card { 
            background: white; 
            border: 1px solid var(--border-color); 
            border-radius: var(--radius); 
            padding: 24px; 
            box-shadow: var(--shadow-sm);
        }
        .card-header { 
            font-weight: 700; 
            font-size: 14px; 
            color: var(--text-muted); 
            margin-bottom: 20px; 
            text-transform: uppercase;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* --- GRAPHS --- */
        .chart-box { display: flex; align-items: center; gap: 20px; }
        .chart-svg { min-width: 120px; flex-shrink: 0; }
        .legend { font-size: 12px; display: flex; flex-direction: column; gap: 6px; flex-grow: 1; }
        .legend-item { display: flex; align-items: center; gap: 10px; }
        .color-dot { width: 10px; height: 10px; border-radius: 2px; }

        .bar-container { 
            display: flex; 
            align-items: flex-end; 
            justify-content: space-between; 
            height: 200px; 
            padding: 20px 10px;
            border-bottom: 2px solid #e2e8f0;
            margin-top: 10px;
        }
        .bar-wrap { flex: 1; display: flex; flex-direction: column; align-items: center; height: 100%; position: relative; }
        .bar-fill { width: 60%; background: var(--primary); border-radius: 4px 4px 0 0; min-height: 2px; transition: height 0.6s ease; position: relative; }
        .bar-fill:hover { opacity: 0.8; }
        .bar-abs { font-size: 11px; font-weight: 700; margin-bottom: 5px; }
        .bar-label { position: absolute; bottom: -30px; font-size: 10px; font-weight: 600; text-align: center; white-space: nowrap; max-width: 80px; overflow: hidden; text-overflow: ellipsis; color: var(--text-muted); }

        /* --- TABLES --- */
        .table-container { width: 100%; overflow-x: auto; margin: 20px 0; border: 1px solid var(--border-color); border-radius: var(--radius-sm); }
        table { width: 100%; border-collapse: collapse; background: white; font-size: 13px; }
        th { background: #f8fafc; padding: 14px 16px; text-align: left; border-bottom: 1px solid var(--border-color); color: var(--text-muted); font-weight: 600; }
        td { padding: 12px 16px; border-bottom: 1px solid #f1f5f9; vertical-align: middle; }
        .score-pill { padding: 4px 10px; border-radius: 20px; font-weight: 700; font-size: 11px; }
        .score-high { background: #dcfce7; color: #166534; }
        .score-mid { background: #fef9c3; color: #854d0e; }
        .score-low { background: #fee2e2; color: #991b1b; }

        /* --- ACADEMIC TABLE STYLE (TAB 3) --- */
        .academic-table { 
            font-family: 'Merriweather', serif; 
            width: 100%; 
            border-top: 2px solid #000; 
            border-bottom: 2px solid #000; 
            margin: 30px 0;
            background: white;
        }
        .academic-table th { border-bottom: 1px solid #000; background: #fff; color: #000; font-weight: 700; text-align: center; padding: 12px; }
        .academic-table td { border-bottom: 1px solid #eee; padding: 10px; text-align: center; color: #333; }
        .row-head { text-align: left !important; font-weight: 600; padding-left: 20px !important; background: #fafafa; }
        .group-head { background: #f0f7ff; text-align: left !important; font-weight: 800; text-transform: uppercase; font-size: 12px; color: var(--secondary); }

        /* --- MODAL --- */
        .modal-overlay { position: fixed; inset: 0; background: rgba(15, 23, 42, 0.75); backdrop-filter: blur(4px); z-index: 1000; display: none; place-items: center; padding: 20px; }
        .modal-content { background: white; width: 100%; max-width: 850px; max-height: 90vh; border-radius: var(--radius); box-shadow: var(--shadow-lg); overflow: hidden; display: flex; flex-direction: column; }
        .modal-header { padding: 20px 30px; border-bottom: 1px solid var(--border-color); display: flex; justify-content: space-between; align-items: center; background: var(--bg-body); }
        .modal-body { padding: 30px; overflow-y: auto; flex-grow: 1; }
        .close-modal { font-size: 24px; cursor: pointer; color: var(--text-muted); }

        /* --- NOTIFICATION --- */
        #toast { visibility: hidden; min-width: 250px; background-color: #1e293b; color: #fff; text-align: center; border-radius: 8px; padding: 16px; position: fixed; z-index: 2000; left: 50%; transform: translateX(-50%); bottom: 40px; font-size: 14px; font-weight: 600; box-shadow: var(--shadow-lg); transition: 0.3s; }
        #toast.show { visibility: visible; bottom: 60px; }

        @media (max-width: 1024px) {
            .stats-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

<div class="container">
    <!-- Header -->
    <header class="app-header">
        <div class="app-title">
            <div class="ribbon-icon"></div>
            <div>
                <h1>Étude Hospitalière : Cancer du Sein</h1>
                <p style="font-size: 11px; color: var(--text-muted); font-weight: 600;">HGR MAKALA - KINSHASA (2024)</p>
            </div>
        </div>
        <div style="display: flex; gap: 10px;">
            <div class="sim-badge" id="data-status">SIMULATED MODE (N=178)</div>
            <button class="btn-premium btn-secondary" id="btn-lock" onclick="window.requestAdmin()">
                <span>🔒 ACCÈS ADMIN</span>
            </button>
        </div>
    </header>

    <!-- Navigation -->
    <nav class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">📂 COLLECTE <span id="badge-n" style="background:var(--primary); color:white; padding:1px 6px; border-radius:10px; font-size:10px;">178</span></button>
        <button class="tab admin-only" onclick="switchTab(2)">📝 MATRICE </button>
        <button class="tab admin-only" onclick="switchTab(3)">📊 ANALYSE SCIENTIFIQUE</button>
        <button class="tab admin-only" onclick="switchTab(4)">📜 DISCOURS & PERSPECTIVES</button>
    </nav>

    <!-- Context Actions -->
    <div class="header-actions admin-only">
        <button class="btn-premium btn-success" onclick="window.exportToCSV()">📄 EXPORTER CSV (FULL)</button>
        <button class="btn-premium btn-primary" onclick="window.printReport()">🖨️ IMPRIMER RAPPORT TOTAL</button>
        <div style="margin-left: auto; color: var(--text-muted); font-size: 12px; font-weight: 600;">
            Dernière mise à jour : <span id="last-update">--:--</span>
        </div>
    </div>

    <!-- TAB 1: COLLECTION -->
    <div id="content-1" class="form-content active">
        <div style="max-width: 900px; margin: auto;">
            <h2 style="text-align: center; margin-bottom: 40px; color: var(--primary);">Formulaire de Recherche (KAP)</h2>
            
            <form id="kapForm">
                <!-- Section I -->
                <div class="section-title">I. IDENTIFICATION & PROFIL <span style="font-size: 11px;">(Socio-démographique)</span></div>
                <div class="grid-row">
                    <div class="field">
                        <label>Code Enquêté(e)</label>
                        <select id="f-code" required></select>
                    </div>
                    <div class="field">
                        <label>Service d'affectation</label>
                        <select id="f-service" required>
                            <option value="">Choisir...</option>
                            <option>Gynécologie-Obstétrique</option>
                            <option>Médecine Interne</option>
                            <option>Chirurgie</option>
                            <option>Urgences / Autre</option>
                        </select>
                    </div>
                </div>
                <div class="grid-row">
                    <div class="field">
                        <label>Niveau d'étude</label>
                        <select id="f-niveau">
                            <option value="A1/LMD - ISTM">A1/LMD - Niveau Supérieur</option>
                            <option value="A2 - ITM">A2 - Niveau Technique</option>
                        </select>
                    </div>
                    <div class="field">
                        <label>Ancienneté (Années)</label>
                        <input type="number" id="f-exp" min="0" max="40" placeholder="Ex: 5">
                    </div>
                    <div class="field">
                        <label>Âge du participant</label>
                        <input type="number" id="f-age" min="18" max="70" placeholder="Ex: 32">
                    </div>
                </div>

                <!-- Section II -->
                <div class="section-title">II. CONNAISSANCES THÉORIQUES <span style="font-size: 11px;">(Savoir)</span></div>
                <div class="sub-title">Classification & Épidémiologie</div>
                <div class="grid-row">
                    <div class="field">
                        <label>Connaissance "HER2 Low" / Classification Moléculaire</label>
                        <select id="f-k1"><option value="0">Non</option><option value="1">Oui</option></select>
                    </div>
                    <div class="field">
                        <label>1ère cause de décès par cancer (Femme RDC) ?</label>
                        <select id="f-k2"><option value="1">Vrai (Cancer du Sein)</option><option value="0">Faux</option></select>
                    </div>
                </div>
                
                <div class="sub-title">Dépistage & Signes</div>
                <div class="grid-row">
                    <div class="field">
                        <label>Âge recommandé 1ère Mammographie (Standard)</label>
                        <select id="f-k3"><option value="0">20 ans</option><option value="1">35-40 ans</option><option value="0">50 ans</option></select>
                    </div>
                    <div class="field">
                        <label>Moment idéal pour l'Auto-Examen (AES)</label>
                        <select id="f-k4"><option value="0">Pendant les règles</option><option value="1">7-10 jours après</option><option value="0">N'importe quand</option></select>
                    </div>
                </div>

                <label style="display: block; margin-top: 20px; font-weight: 700; font-size: 13px;">Facteurs de Risque (Sélectionnez les items identifiés)</label>
                <div class="check-group" id="f-risques">
                    <label class="check-item"><input type="checkbox" value="age"> Âge (>50 ans)</label>
                    <label class="check-item"><input type="checkbox" value="famille"> Hérédité (Gènes BRCA)</label>
                    <label class="check-item"><input type="checkbox" value="sedent"> Obésité / Sédentarité</label>
                    <label class="check-item"><input type="checkbox" value="tabac"> Tabac / Alcool</label>
                    <label class="check-item"><input type="checkbox" value="menop"> Ménopause tardive (>55 ans)</label>
                    <label class="check-item"><input type="checkbox" value="nulle"> Nulliparité</label>
                    <label class="check-item"><input type="checkbox" value="gros"> Gros Seins (Faux facteur)</label>
                </div>

                <!-- Section III -->
                <div class="section-title">III. ATTITUDES & PRATIQUES <span style="font-size: 11px;">(Savoir-Être & Savoir-Faire)</span></div>
                <div class="grid-row">
                    <div class="field">
                        <label>Réalisation AES personnelle (Fréquence)</label>
                        <select id="f-p1"><option value="1">Chaque mois</option><option value="0.5">Irrégulier</option><option value="0">Jamais</option></select>
                    </div>
                    <div class="field">
                        <label>Examen clinique systématique des patientes ?</label>
                        <select id="f-p2"><option value="1">Oui (Systématique)</option><option value="0.5">Si plainte uniquement</option><option value="0">Rarement</option></select>
                    </div>
                </div>

                <div class="sub-title">Technique Clinique</div>
                <div class="grid-row">
                    <div class="field">
                        <label>Zone indispensable à ne pas oublier ?</label>
                        <select id="f-p3"><option value="1">Creux Axillaire</option><option value="0.5">Mamelon uniquement</option></select>
                    </div>
                    <div class="field">
                        <label>Mouvement de palpation recommandé</label>
                        <select id="f-p4"><option value="1">Circulaire / Vertical</option><option value="0">Aléatoire</option></select>
                    </div>
                </div>

                <div class="section-title">IV. VERBATIM & SUGGESTIONS</div>
                <div class="field">
                    <textarea id="f-reco" rows="4" placeholder="Suggestions de l'infirmière pour améliorer le dépistage localement..."></textarea>
                </div>

                <button type="button" class="btn-premium btn-primary" style="width: 100%; margin-top: 30px; padding: 20px;" onclick="window.saveCurrentForm()">
                    🚀 ENREGISTRER LA FICHE DE DONNÉES
                </button>
            </form>
        </div>
    </div>

    <!-- TAB 2: DATABASE MATRIX -->
    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT <span id="n-display-2" style="font-size: 11px;">N = 178</span></div>
        
        <div style="margin-bottom: 20px; display: flex; gap: 10px;">
            <input type="text" id="db-search" placeholder="Rechercher par Code ou Service..." style="max-width: 300px;" onkeyup="window.filterMatrix()">
            <button class="btn-premium btn-secondary" onclick="window.deleteSelected()" id="btn-del" style="display: none;">🗑️ SUPPRIMER LA SÉLECTION</button>
        </div>

        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th style="width: 40px;"><input type="checkbox" id="chk-all" onclick="window.toggleAllChecks(this)"></th>
                        <th>CODE</th>
                        <th>SERVICE</th>
                        <th>NIVEAU</th>
                        <th>SAVOIR (K)</th>
                        <th>PRATIQUE (P)</th>
                        <th>STATUT</th>
                        <th style="text-align: center;">ACTIONS</th>
                    </tr>
                </thead>
                <tbody id="matrix-body">
                    <!-- JS Generated -->
                </tbody>
            </table>
        </div>
    </div>

    <!-- TAB 3: STATISTICAL ANALYSIS -->
    <div id="content-3" class="form-content">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 30px; border-bottom: 3px solid var(--secondary); padding-bottom: 10px;">
            <h2 style="color: var(--secondary); font-family: 'Merriweather', serif;">PRÉSENTATION DES RÉSULTATS SCIENTIFIQUES</h2>
            <button class="btn-premium btn-secondary" onclick="window.exportToWord()">📥 EXPORTER RAPPORT (.doc)</button>
        </div>

        <!-- 1. Taux de participation -->
        <div class="section-title">1. Taux de participation</div>
        <div class="card" style="max-width: 500px; margin: auto; margin-bottom: 30px;">
            <div class="card-header">Participation globale Inclusion/Exclusion</div>
            <div class="chart-box">
                <div id="svg-participation" class="chart-svg"></div>
                <div class="legend" id="legend-participation"></div>
            </div>
        </div>

        <!-- 2. Caractéristiques socio-démographiques -->
        <div class="section-title" id="point-2">2. Caractéristiques socio-démographiques (Tableau)</div>
        <div id="academic-table-1">
            <!-- Tableau I: Socio-démo -->
        </div>

        <!-- 3. Répartition du personnel selon leur grade ou service -->
        <div class="section-title">3. Répartition du personnel selon leur grade ou service (Figure)</div>
        <div class="stats-grid" style="margin-bottom: 30px;">
            <div class="card">
                <div class="card-header">Répartition par Niveau d'Étude (Grade)</div>
                <div class="chart-box">
                    <div id="svg-grade-dist" class="chart-svg"></div>
                    <div class="legend" id="legend-grade"></div>
                </div>
            </div>
            <div class="card">
                <div class="card-header">Répartition par Service d'Affectation</div>
                <div class="chart-box">
                    <div id="svg-service-dist" class="chart-svg"></div>
                    <div class="legend" id="legend-service"></div>
                </div>
            </div>
        </div>

        <!-- 4. Connaissance sur les différents aspects -->
        <div class="section-title">4. Connaissance sur les différents aspects du dépistage (Tableau)</div>
        <div id="academic-table-2">
            <!-- Tableau II: Connaissances détaillées -->
        </div>

        <!-- 5. Attitude par rapport au dépistage -->
        <div class="section-title">5. Attitude par rapport au dépistage (Figure/Distribution)</div>
        <div class="card" style="max-width: 500px; margin: auto; margin-bottom: 30px;">
            <div class="card-header">Orientation de l'Attitude Interrogée</div>
            <div class="chart-box">
                <div id="svg-attitude-dist" class="chart-svg"></div>
                <div class="legend" id="legend-attitude"></div>
            </div>
        </div>

        <!-- 6. Pratique par rapport au dépistage (Infirmières) -->
        <div class="section-title">6. Pratique par rapport au dépistage (Distribution)</div>
        <div class="card" style="max-width: 500px; margin: auto;">
            <div class="card-header">Adéquation de la Pratique Clinique (N=Femmes)</div>
            <div class="chart-box">
                <div id="svg-practice-dist" class="chart-svg"></div>
                <div class="legend" id="legend-practice"></div>
            </div>
        </div>
    </div>

    <!-- TAB 4: DISCUSSION & CONCLUSIONS -->
    <div id="content-4" class="form-content">
        <div style="max-width: 1000px; margin: auto; font-family: 'Merriweather', serif;">
            <h1 style="color: var(--primary); text-align: center; border-bottom: 3px solid var(--primary-light); padding-bottom: 20px;">DISCUSSION DES RÉSULTATS</h1>
            
            <div id="dynamic-discussion" style="margin-top: 30px; text-align: justify; color: #334155; line-height: 1.8;">
                <!-- JS Injecter le rapport ici -->
            </div>

            <div style="background: #f8fafc; border-left: 5px solid var(--primary); padding: 30px; margin-top: 50px; border-radius: 8px;">
                <h3 style="color: var(--primary-dark); margin-bottom: 15px;">CONCLUSIONS GLOBALES</h3>
                <p id="dynamic-conclusion"></p>
            </div>

            <div style="margin-top: 40px; padding: 20px; border-top: 1px solid #eee; display: flex; justify-content: space-between; align-items: center;">
                <div style="text-align: center;">
                    <br><br>
                    <p style="font-weight: bold; border-top: 1px solid #000; padding-top: 5px; min-width: 200px;">Direction des Soins</p>
                </div>
                <div style="text-align: center;">
                    <br><br>
                    <p style="font-weight: bold; border-top: 1px solid #000; padding-top: 5px; min-width: 200px;">Chercheur Principal</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- MODALS -->
<div class="modal-overlay" id="overlay-details" onclick="window.closeAnyModal(event)">
    <div class="modal-content" onclick="event.stopPropagation()">
        <div class="modal-header">
            <h3 id="m-code">Détails de l'Enquête</h3>
            <span class="close-modal" onclick="window.hideModal('overlay-details')">&times;</span>
        </div>
        <div class="modal-body" id="m-body">
            <!-- JS Dynamic -->
        </div>
        <div style="padding: 20px; background: #f8fafc; text-align: right; border-top: 1px solid #eee;">
            <button class="btn-premium btn-secondary" onclick="window.hideModal('overlay-details')">Fermer</button>
        </div>
    </div>
</div>

<div id="toast">Message synchronisé !</div>

<!-- --- INJECTION JAVASCRIPT --- -->
<script type="module">
    // --- STATE MANAGEMENT ---
    let db = [];
    let isAdmin = false;
    const SERVICES = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
    
    // Initialisation
    window.addEventListener('DOMContentLoaded', () => {
        db = generateMockDatabase(178);
        updateUI();
        initCodeDropdown();
        document.getElementById('last-update').innerText = new Date().toLocaleTimeString();
    });

    // --- LOGIQUE CORE ---

    function generateMockDatabase(count) {
        let items = [];
        for (let i = 1; i <= count; i++) {
            const service = SERVICES[Math.floor(Math.random() * SERVICES.length)];
            const isA1 = Math.random() > 0.3;
            const isGyneco = service === 'Gynécologie-Obstétrique';
            
            // Simuler des corrélations logiques
            let baseK = isGyneco ? 75 : (isA1 ? 55 : 40);
            let scoreSavoir = Math.min(100, Math.max(20, baseK + (Math.random() * 30 - 15)));
            
            let baseP = isGyneco ? 80 : (isA1 ? 50 : 35);
            let scorePratique = Math.min(100, Math.max(10, baseP + (Math.random() * 40 - 20)));

            items.push({
                idx: i,
                id: `INF-MAK-${i.toString().padStart(3, '0')}`,
                service: service,
                niveau: isA1 ? 'A1/LMD - ISTM' : 'A2 - ITM',
                exp: Math.floor(Math.random() * 25),
                age: 22 + Math.floor(Math.random() * 35),
                k_score: Math.round(scoreSavoir),
                p_score: Math.round(scorePratique),
                a_score: (3 + Math.random() * 2).toFixed(1),
                verbatim: "Importance du renforcement des capacités cliniques.",
                risques: ["age", "famille", "tabac"].filter(() => Math.random() > 0.4),
                // Boolean details for Knowledge Table
                k_her2: Math.random() > 0.6,
                k_mammo: Math.random() > 0.4,
                k_aes: Math.random() > 0.3,
                k_risks: scoreSavoir > 60
            });
        }
        return items;
    }

    window.switchTab = function(n) {
        document.querySelectorAll('.tab').forEach((t, i) => {
            if (i === n - 1) t.classList.add('active');
            else t.classList.remove('active');
        });
        document.querySelectorAll('.form-content').forEach((c, i) => {
            if (i === n - 1) c.classList.add('active');
            else c.classList.remove('active');
        });
        if (n === 2 || n === 3) updateUI();
    };

    window.requestAdmin = function() {
        if (isAdmin) return;
        const code = prompt("Veuillez entrer le code d'accès administrateur :");
        if (code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-lock').innerHTML = "🟢 MODE ADMIN ACTIF";
            document.getElementById('btn-lock').style.background = "#10b981";
            showToast("Permissions accordées.");
            window.switchTab(3);
        } else {
            alert("Code invalide.");
        }
    };

    function updateUI() {
        document.getElementById('badge-n').innerText = db.length;
        document.getElementById('n-display-2').innerText = `N = ${db.length}`;
        
        // Matrix Render
        const tbody = document.getElementById('matrix-body');
        tbody.innerHTML = db.map(row => `
            <tr>
                <td><input type="checkbox" class="row-chk" value="${row.id}" onchange="window.evalDeleteBtn()"></td>
                <td style="font-weight:700;">${row.id}</td>
                <td style="font-size:12px;">${row.service}</td>
                <td><small>${row.niveau}</small></td>
                <td>
                    <span class="score-pill ${getScoreClass(row.k_score)}">${row.k_score}%</span>
                </td>
                <td>
                    <span class="score-pill ${getScoreClass(row.p_score)}">${row.p_score}%</span>
                </td>
                <td>${row.k_score > 60 && row.p_score > 60 ? '🎓 Qualifié' : '⚠️ Besoin Formation'}</td>
                <td style="text-align:right;">
                    <button class="btn-premium btn-secondary" style="padding:6px 12px; font-size:11px;" onclick="window.viewDetails('${row.id}')">👁️ DÉTAILS</button>
                </td>
            </tr>
        `).join('');

        if (isAdmin) {
            renderCharts();
            renderAcademicTables();
            updateDiscussion();
        }
    }

    function getScoreClass(s) {
        if (s >= 70) return 'score-high';
        if (s >= 50) return 'score-mid';
        return 'score-low';
    }

    // --- RECHERCHE ET FILTRES ---
    window.filterMatrix = function() {
        const q = document.getElementById('db-search').value.toLowerCase();
        const rows = document.querySelectorAll('#matrix-body tr');
        rows.forEach(r => {
            r.style.display = r.innerText.toLowerCase().includes(q) ? '' : 'none';
        });
    };

    window.evalDeleteBtn = function() {
        const any = document.querySelectorAll('.row-chk:checked').length > 0;
        document.getElementById('btn-del').style.display = any ? 'inline-flex' : 'none';
    };

    window.deleteSelected = function() {
        const ids = Array.from(document.querySelectorAll('.row-chk:checked')).map(el => el.value);
        if (confirm(`Supprimer ${ids.length} fiches ? Cette action est irréversible.`)) {
            db = db.filter(item => !ids.includes(item.id));
            updateUI();
            showToast("Données supprimées.");
        }
    };

    // --- FORMULAIRE ---
    window.saveCurrentForm = function() {
        const code = document.getElementById('f-code').value;
        const service = document.getElementById('f-service').value;
        if (!service) return alert("Veuillez choisir un service.");

        const newItem = {
            id: code,
            service: service,
            niveau: document.getElementById('f-niveau').value,
            exp: document.getElementById('f-exp').value,
            age: document.getElementById('f-age').value,
            k_score: Math.floor(Math.random() * 40 + 50), // Simulation de calcul
            p_score: Math.floor(Math.random() * 40 + 40),
            a_score: "4.2",
            verbatim: document.getElementById('f-reco').value,
            risques: ["age"]
        };

        db.unshift(newItem);
        showToast("Fiche enregistrée avec succès !");
        document.getElementById('kapForm').reset();
        initCodeDropdown();
        window.switchTab(2);
    };

    function initCodeDropdown() {
        const sel = document.getElementById('f-code');
        if(!sel) return;
        sel.innerHTML = "";
        const nextId = db.length + 1;
        const opt = document.createElement('option');
        opt.value = `INF-MAK-${nextId.toString().padStart(3, '0')}`;
        opt.text = `PROCHAINE FICHE DISPONIBLE (${opt.value})`;
        sel.appendChild(opt);
    }

    // --- ANALYSE & GRAPHIQUES (PURE SVG) ---
    function renderCharts() {
        const total = db.length;
        if(total === 0) return;

        // 1. Taux de participation
        renderDonut('svg-participation', [
            {l: 'Accepté / Inclus', v: total, c: '#2e7d32'},
            {l: 'Refusé / Exclu', v: Math.floor(total * 0.04), c: '#c62828'}
        ], 'legend-participation');

        // 3. Répartition - Figure (Grade & Service)
        const a1Count = db.filter(d => d.niveau.includes('A1')).length;
        renderDonut('svg-grade-dist', [
            {l: 'Niveau Supérieur (A1)', v: a1Count, c: '#0d47a1'},
            {l: 'Niveau Technique (A2)', v: total - a1Count, c: '#64b5f6'}
        ], 'legend-grade');

        const serviceCounts = SERVICES.map(s => ({
            l: s,
            v: db.filter(d => d.service === s).length,
            c: s.includes('Gynéco') ? '#b03060' : (s.includes('Médecine') ? '#9c27b0' : (s.includes('Chirurgie') ? '#2196f3' : '#607d8b'))
        }));
        renderDonut('svg-service-dist', serviceCounts, 'legend-service');

        // 5. Attitude
        const posAtt = db.filter(d => parseFloat(d.a_score) >= 3.5).length;
        renderDonut('svg-attitude-dist', [
            {l: 'Attitude Favorable', v: posAtt, c: '#4caf50'},
            {l: 'Attitude Défavorable', v: total - posAtt, c: '#e0e0e0'}
        ], 'legend-attitude');

        // 6. Pratique
        const adePrat = db.filter(d => d.p_score >= 70).length;
        renderDonut('svg-practice-dist', [
            {l: 'Pratique Adéquate', v: adePrat, c: '#b03060'},
            {l: 'Pratique Inadéquate', v: total - adePrat, c: '#f0f0f0'}
        ], 'legend-practice');
    }

    function renderDonut(id, data, legendId, centerText) {
        const container = document.getElementById(id);
        if (!container) return;
        const total = data.reduce((a,c) => a + c.v, 0);
        let current = 0;
        let svg = `<svg viewBox="0 0 42 42" width="100%" height="100%">
            <circle cx="21" cy="21" r="15.915" fill="transparent" stroke="#f1f5f9" stroke-width="5"></circle>`;
        
        data.forEach(item => {
            const perc = (item.v / total) * 100;
            if (perc === 0) return;
            svg += `<circle cx="21" cy="21" r="15.915" fill="transparent" stroke="${item.c}" stroke-width="5" stroke-dasharray="${perc} ${100-perc}" stroke-dashoffset="${25-current}"></circle>`;
            current += perc;
        });

        if (centerText) {
            svg += `<text x="50%" y="55%" text-anchor="middle" style="font-size:5px; font-weight:700; fill:#64748b;">${centerText}</text>`;
        }
        svg += `</svg>`;
        container.innerHTML = svg;

        if (legendId) {
            const leg = document.getElementById(legendId);
            leg.innerHTML = data.map(i => `
                <div class="legend-item">
                    <div class="color-dot" style="background:${i.c}"></div>
                    <span style="font-size:11px;">${i.l}: <b>${i.v} (${Math.round(i.v/total*100)}%)</b></span>
                </div>
            `).join('');
        }
    }

    // --- TABLES ACADÉMIQUES ---
    function renderAcademicTables() {
        const n = db.length;
        if(n === 0) return;

        // Tableau I: Socio-démo
        const a1 = db.filter(d => d.niveau.includes('A1')).length;
        const age_30 = db.filter(d => d.age < 30).length;
        const age_30_45 = db.filter(d => d.age >= 30 && d.age <= 45).length;
        const age_45 = n - age_30 - age_30_45;

        // Tableau II: Connaissances
        const her2 = db.filter(d => d.k_her2).length;
        const aes = db.filter(d => d.k_aes).length;
        const mammo = db.filter(d => d.k_mammo).length;
        const risks = db.filter(d => d.k_risks).length;

        const html1 = `
            <table class="academic-table">
                <thead>
                    <tr><th style="width:60%;">Tableau I : Caractéristiques socio-démographiques (N=${n})</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr>
                </thead>
                <tbody>
                    <tr class="group-head"><td colspan="3">ÂGE DES ENQUÊTÉES</td></tr>
                    <tr><td class="row-head">Moins de 30 ans</td><td>${age_30}</td><td>${(age_30/n*100).toFixed(1)}%</td></tr>
                    <tr><td class="row-head">30 à 45 ans</td><td>${age_30_45}</td><td>${(age_30_45/n*100).toFixed(1)}%</td></tr>
                    <tr><td class="row-head">Plus de 45 ans</td><td>${age_45}</td><td>${(age_45/n*100).toFixed(1)}%</td></tr>
                    
                    <tr class="group-head"><td colspan="3">NIVEAU D'ÉTUDE (GRADE)</td></tr>
                    <tr><td class="row-head">Niveau Supérieur (A1/LMD)</td><td>${a1}</td><td>${(a1/n*100).toFixed(1)}%</td></tr>
                    <tr><td class="row-head">Niveau Technique (A2)</td><td>${n-a1}</td><td>${((n-a1)/n*100).toFixed(1)}%</td></tr>
                    
                    <tr class="group-head"><td colspan="3">SERVICE D'AFFECTATION</td></tr>
                    ${SERVICES.map(s => {
                        const cnt = db.filter(d => d.service === s).length;
                        return `<tr><td class="row-head">${s}</td><td>${cnt}</td><td>${(cnt/n*100).toFixed(1)}%</td></tr>`;
                    }).join('')}
                </tbody>
            </table>
        `;

        const html2 = `
            <table class="academic-table">
                <thead>
                    <tr><th style="width:60%;">Tableau II : Connaissances sur les aspects du dépistage (N=${n})</th><th>Effectifs (n)</th><th>Pourcentage (%)</th></tr>
                </thead>
                <tbody>
                    <tr class="group-head"><td colspan="3">ASPECTS THÉORIQUES</td></tr>
                    <tr><td class="row-head">Classification Moléculaire (HER2)</td><td>${her2}</td><td>${(her2/n*100).toFixed(1)}%</td></tr>
                    <tr><td class="row-head">Facteurs de risque de l'OMS</td><td>${risks}</td><td>${(risks/n*100).toFixed(1)}%</td></tr>
                    <tr class="group-head"><td colspan="3">ASPECTS CLINIQUES</td></tr>
                    <tr><td class="row-head">Auto-Examen des Seins (Technique)</td><td>${aes}</td><td>${(aes/n*100).toFixed(1)}%</td></tr>
                    <tr><td class="row-head">Indications de la Mammographie</td><td>${mammo}</td><td>${(mammo/n*100).toFixed(1)}%</td></tr>
                    <tr class="group-head"><td colspan="3">SCORE DE CONNAISSANCE GLOBAL</td></tr>
                    <tr><td class="row-head">Bonnes connaissances (≥ 70%)</td><td>${db.filter(d => d.k_score >= 70).length}</td><td>${(db.filter(d => d.k_score >= 70).length/n*100).toFixed(1)}%</td></tr>
                    <tr><td class="row-head">Connaissances Insuffisantes (< 70%)</td><td>${db.filter(d => d.k_score < 70).length}</td><td>${(db.filter(d => d.k_score < 70).length/n*100).toFixed(1)}%</td></tr>
                </tbody>
            </table>
        `;
        
        document.getElementById('academic-table-1').innerHTML = html1;
        document.getElementById('academic-table-2').innerHTML = html2;
    }

    // --- DISCUSSION GENERATOR ---
    function updateDiscussion() {
        const n = db.length;
        if(n === 0) return;
        const k_good = Math.round(db.filter(d => d.k_score >= 70).length / n * 100);
        const p_good = Math.round(db.filter(d => d.p_score >= 70).length / n * 100);

        let disc = `Nos résultats révèlent que <b>${k_good}%</b> des infirmières possèdent un niveau de connaissance théorique satisfaisant sur le cancer du sein. Cependant, une disparité majeure est observée au niveau des pratiques cliniques (<b>${p_good}%</b> d'adéquation), ce qui souligne une "failure" dans le transfert des compétences théoriques vers le soin au chevet du patient. `;
        
        if (k_good < 60) {
            disc += "Ce déficit cognitif constitue un frein majeur à la détection précoce dans une zone de santé à forte densité comme Makala. ";
        } else {
            disc += "Bien que le savoir soit globalement présent, l'absence de protocoles standardisés au sein de l'HGR Makala limite l'impact réel sur la survie des patientes. ";
        }

        document.getElementById('dynamic-discussion').innerHTML = disc;
        document.getElementById('dynamic-conclusion').innerText = `En conclusion, l'étude suggère une nécessité impérieuse de formation continue axée sur la pratique de l'examen clinique des seins (ECS) et l'intégration du dépistage opportuniste dans tous les services hospitaliers, et non uniquement en maternité.`;
    }

    // --- UTILS & EXPORTS ---
    window.showToast = (m) => {
        const x = document.getElementById("toast");
        x.innerText = m; x.className = "show";
        setTimeout(() => x.className = x.className.replace("show", ""), 3000);
    };

    window.viewDetails = function(id) {
        const item = db.find(d => d.id === id);
        if (!item) return;
        document.getElementById('m-code').innerText = `DOSSIER : ${item.id}`;
        document.getElementById('m-body').innerHTML = `
            <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px;">
                <div class="card">
                    <p><b>Service :</b> ${item.service}</p>
                    <p><b>Ancienneté :</b> ${item.exp} ans</p>
                    <p><b>Âge :</b> ${item.age} ans</p>
                </div>
                <div class="card">
                    <p><b>Score Savoir :</b> <span class="score-pill ${getScoreClass(item.k_score)}">${item.k_score}%</span></p>
                    <p><b>Score Pratique :</b> <span class="score-pill ${getScoreClass(item.p_score)}">${item.p_score}%</span></p>
                </div>
            </div>
            <div class="section-title">VERBATIM RELEVE</div>
            <p style="font-style:italic; border-left:3px solid var(--primary); padding-left:15px; margin-top:10px;">"${item.verbatim}"</p>
        `;
        document.getElementById('overlay-details').style.display = 'grid';
    };

    window.hideModal = (id) => document.getElementById(id).style.display = 'none';
    window.closeAnyModal = (e) => { if(e.target.classList.contains('modal-overlay')) e.target.style.display = 'none'; };

    window.exportToCSV = function() {
        let csv = "ID,Service,Niveau,Exp,Savoir,Pratique,Status\n";
        db.forEach(r => {
            csv += `${r.id},${r.service},${r.niveau},${r.exp},${r.k_score},${r.p_score},${r.k_score>60?'OK':'LACK'}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url; a.download = `EXPORT_MAKALA_N${db.length}.csv`;
        a.click();
    };

    window.printReport = () => window.print();

    window.exportToWord = function() {
        const content = document.getElementById('academic-reports').innerHTML;
        const blob = new Blob(['<html><body>' + content + '</body></html>'], { type: 'application/msword' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url; a.download = "RAPPORT_TABLEAUX_MAKALA.doc";
        a.click();
    };

</script>
</body>
</html>
