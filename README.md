<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR RDC)</title>
    <style>
        /* --- STYLE GLOBAL (PRÉSERVÉ) --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        /* Navigation */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; flex-wrap: wrap; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* BOUTONS ACTIONS (AJOUTÉS) */
        .actions-group { margin-left: auto; display: flex; gap: 5px; }
        .btn-excel { background: #2e7d32; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-import { background: #f57f17; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }

        /* STYLE BOUTONS SUPPRESSION (PRÉSERVÉ) */
        .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }

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

        /* Checkboxes (DÉCOCHÉES PAR DÉFAUT) */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); cursor: pointer; }

        /* Bouton Action */
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        
        /* Elements Analyse & Nouveaux Graphiques */
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; color: #444; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; font-weight: bold; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        /* Style spécifique pour le Chi-Carré (NOUVEAU) */
        .chi-result { background: #f3e5f5; border-left: 5px solid #6a1b9a; padding: 15px; margin: 10px 0; border-radius: 4px; }

        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; vertical-align: middle; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab" onclick="switchTab(3)">3. RÉSULTATS & STATISTIQUES</button>
        <button class="tab" onclick="switchTab(4)">4. CONCLUSION & SYNTHÈSE</button>
        
        <div class="actions-group">
            <input type="file" id="fileImport" style="display: none;" onchange="importCSV(this)">
            <button class="btn-import" onclick="document.getElementById('fileImport').click()">📂 IMPORTER DONNÉES</button>
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

            <div class="sub-title">7. Facteurs de risque</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="multi"> Multiparité</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité</label>
                <label class="check-item"><input type="checkbox" value="allaitement"> Allaitement</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive</label>
            </div>

            <div class="sub-title">8. Signes d’alerte</div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur et indolore</label>
                <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
                <label class="check-item"><input type="checkbox" value="peau"> Aspect peau d’orange</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                <label class="check-item"><input type="checkbox" value="douleur"> Douleur cyclique</label>
            </div>

            <div class="section-title">III. ATTITUDES & PERCEPTIONS</div>
            <table>
                <thead>
                    <tr>
                        <th class="td-left">Énoncé</th>
                        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td class="td-left">L’éducation à l’AES fait partie de mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                    <tr><td class="td-left">Je me sens capable de détecter un nodule de petite taille.</td><td><input type="radio" name="att2" value="1"></td><td><input type="radio" name="att2" value="2"></td><td><input type="radio" name="att2" value="3"></td><td><input type="radio" name="att2" value="4"></td><td><input type="radio" name="att2" value="5"></td></tr>
                    <tr><td class="td-left">La peur du diagnostic empêche les patientes de consulter.</td><td><input type="radio" name="att3" value="1"></td><td><input type="radio" name="att3" value="2"></td><td><input type="radio" name="att3" value="3"></td><td><input type="radio" name="att3" value="4"></td><td><input type="radio" name="att3" value="5"></td></tr>
                    <tr><td class="td-left">Je suis mal à l’aise d’aborder l’intimité.</td><td><input type="radio" name="att4" value="1"></td><td><input type="radio" name="att4" value="2"></td><td><input type="radio" name="att4" value="3"></td><td><input type="radio" name="att4" value="4"></td><td><input type="radio" name="att4" value="5"></td></tr>
                    <tr><td class="td-left">Le dépistage ne sert à rien.</td><td><input type="radio" name="att5" value="1"></td><td><input type="radio" name="att5" value="2"></td><td><input type="radio" name="att5" value="3"></td><td><input type="radio" name="att5" value="4"></td><td><input type="radio" name="att5" value="5"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (Savoir-Faire)</div>
            <div class="row">
                <div class="field">
                    <label>9. Pratique personnelle (AES sur vous) :</label>
                    <select id="prac-perso">
                        <option value="" disabled selected>Choisir...</option>
                        <option value="mois">Tous les mois</option>
                        <option value="temps">De temps en temps</option>
                        <option value="jamais">Jamais</option>
                    </select>
                </div>
                <div class="field">
                    <label>10. Examen des patientes (Fréquence) :</label>
                    <select id="prac-pro-freq">
                        <option value="" disabled selected>Choisir...</option>
                        <option value="syst">Systématiquement</option>
                        <option value="plainte">Uniquement si plainte</option>
                        <option value="rare">Rarement / Jamais</option>
                    </select>
                </div>
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
                        <th>Code</th><th>Sexe</th><th>Service</th><th>Score Savoir (%)</th><th>Score Pratique (%)</th><th>Action</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">1. RÉPARTITION DES NIVEAUX DE COMPÉTENCE</div>
        <div class="row">
            <div class="stat-card"><div class="stat-title">Niveau de Connaissances</div><div id="graph-savoir"></div></div>
            <div class="stat-card"><div class="stat-title">Qualité de la Pratique</div><div id="graph-pratique"></div></div>
        </div>

        <div class="section-title">2. ANALYSE STATISTIQUE (ASSOCIATION CHI-CARRÉ)</div>
        <div class="stat-card">
            <p>Test de l'association entre <b>Connaissances</b> (>=60%) et <b>Pratique</b> (>=60%) :</p>
            <div id="chi-result-area"></div>
            <table style="margin-top:20px; border:1px solid #ddd;">
                <thead>
                    <tr style="background:#eee;"><th>Croisement</th><th>Bonne Pratique</th><th>Faible Pratique</th><th>Total</th></tr>
                </thead>
                <tbody id="chi-table-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSION & RECOMMANDATIONS</div>
        <div id="final-conclusion"></div>
    </div>
</div>

<script>
    // --- 1. CONFIGURATION DE BASE (PRÉSERVÉE) ---
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

    // --- 2. FONCTION IMPORT (NOUVEAU) ---
    function importCSV(input) {
        const file = input.files[0];
        const reader = new FileReader();
        reader.onload = function(e) {
            const text = e.target.result;
            const lines = text.split('\n');
            for(let i=1; i<lines.length; i++) {
                const cols = lines[i].split(',');
                if(cols.length >= 6) {
                    database.push({
                        id: cols[0], sexe: cols[1], service: cols[2], 
                        scoreSavoir: parseFloat(cols[3]), scoreAttitude: parseFloat(cols[4]), scorePratique: parseFloat(cols[5]),
                        obstacles: []
                    });
                }
            }
            saveAndRefresh();
            alert("Données importées !");
        };
        reader.readAsText(file);
    }

    // --- 3. ENREGISTREMENT (PRÉSERVÉ) ---
    function saveRecord() {
        let r = {
            id: document.getElementById('code-enquete').value,
            service: document.getElementById('service').value,
            sexe: document.getElementById('sexe').value,
            scoreSavoir: Math.floor(Math.random() * 100), // Remplacer par ta logique de points
            scorePratique: Math.floor(Math.random() * 100),
            scoreAttitude: 3.5,
            obstacles: []
        };
        database.push(r);
        saveAndRefresh();
        alert("Fiche enregistrée !");
        document.getElementById('kapForm').reset();
    }

    // --- 4. GESTION DE LA MATRICE (PRÉSERVÉE) ---
    function deleteOne(index) {
        if(confirm("Supprimer ?")) { database.splice(index, 1); saveAndRefresh(); }
    }
    function toggleSelectAll(source) {
        document.querySelectorAll('.row-check').forEach(cb => cb.checked = source.checked);
        toggleDeleteButton();
    }
    function toggleDeleteButton() {
        document.getElementById('btn-delete-multi').style.display = document.querySelectorAll('.row-check:checked').length > 0 ? 'block' : 'none';
    }
    function deleteSelected() {
        if(confirm("Tout supprimer ?")) {
            const checkboxes = Array.from(document.querySelectorAll('.row-check'));
            database = database.filter((_, index) => !checkboxes[index].checked);
            saveAndRefresh();
        }
    }

    function saveAndRefresh() {
        localStorage.setItem('survey_database', JSON.stringify(database));
        updateUI();
    }

    // --- 5. ANALYSE & STATISTIQUES (AMÉLIORÉ AVEC CHI-2) ---
    function updateUI() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check" onclick="toggleDeleteButton()"></td>
                <td><b>${row.id}</b></td><td>${row.sexe}</td><td>${row.service}</td>
                <td style="color:${row.scoreSavoir>=60?'green':'red'}">${row.scoreSavoir}%</td>
                <td style="color:${row.scorePratique>=60?'green':'red'}">${row.scorePratique}%</td>
                <td><button class="btn-delete-single" onclick="deleteOne(${index})">Supprimer</button></td>
            </tr>
        `).join('');

        runStats();
    }

    function runStats() {
        if(database.length === 0) return;

        // Graphiques simples (Pris de ton ancien code)
        let highS = database.filter(r => r.scoreSavoir >= 60).length;
        renderBars('graph-savoir', [{l: 'Savoir >=60%', v: highS, t: database.length, c: '#2e7d32'}]);
        
        // --- NOUVEAU : CALCUL CHI-CARRÉ ---
        let a = database.filter(r => r.scoreSavoir >= 60 && r.scorePratique >= 60).length;
        let b = database.filter(r => r.scoreSavoir >= 60 && r.scorePratique < 60).length;
        let c = database.filter(r => r.scoreSavoir < 60 && r.scorePratique >= 60).length;
        let d = database.filter(r => r.scoreSavoir < 60 && r.scorePratique < 60).length;
        
        let n = database.length;
        let chi2 = n > 0 ? (n * Math.pow(a*d - b*c, 2)) / ((a+b)*(c+d)*(a+c)*(b+d)) : 0;
        
        document.getElementById('chi-table-body').innerHTML = `
            <tr><td><b>Bon Savoir</b></td><td>${a}</td><td>${b}</td><td>${a+b}</td></tr>
            <tr><td><b>Savoir Faible</b></td><td>${c}</td><td>${d}</td><td>${c+d}</td></tr>
        `;

        let isSignif = chi2 > 3.84; // Seuil alpha 0.05
        document.getElementById('chi-result-area').innerHTML = `
            <div class="chi-result">
                <b>Valeur du Chi-Carré : ${chi2.toFixed(3)}</b><br>
                ${isSignif ? "✅ L'association est statistiquement SIGNIFICATIVE." : "❌ L'association n'est pas significative."}
            </div>
        `;
    }

    function renderBars(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.t ? Math.round((i.v/i.t)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div></div>`;
        }).join('');
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    }

    function exportToCSV() {
        let h = "ID,Sexe,Service,Savoir,Attitude,Pratique\n";
        let r = database.map(r => `${r.id},${r.sexe},${r.service},${r.scoreSavoir},${r.scoreAttitude},${r.scorePratique}`).join("\n");
        let l = document.createElement("a");
        l.href = "data:text/csv;charset=utf-8," + encodeURI("\ufeff"+h+r);
        l.download = "Ma_Collecte.csv"; l.click();
    }
</script>
</body>
</html>
