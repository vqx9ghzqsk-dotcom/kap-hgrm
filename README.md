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
        
        /* Protection Admin */
        .admin-locked { display: none !important; } 
        .btn-admin { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; font-size:12px; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}
        
        /* Indicateur de chargement */
        #loading-indicator { display:none; color: #b03060; font-weight:bold; margin-left:10px; font-size:12px; }

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
        .btn-save:disabled { background: #ccc; cursor: not-allowed; }
        
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
        <button class="tab admin-locked" id="tab2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-locked" id="tab3" onclick="switchTab(3)">3. RÉSULTATS & ANALYSE</button>
        <button class="tab admin-locked" id="tab4" onclick="switchTab(4)">4. CONCLUSION</button>
        
        <span id="loading-indicator">🔄 Synchro...</span>
        <button type="button" class="btn-admin" onclick="adminLogin()">🔒 ADMIN</button>
        <button type="button" class="btn-excel admin-locked" onclick="exportToCSV()">📊 EXPORT CSV</button>
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
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (Savoir-Faire)</div>
            <div class="sub-title">Technique de Palpation</div>
            
            <div class="row">
                <div class="field">
                    <label>Partie de la main utilisée ?</label>
                    <select id="prac-main">
                        <option value="pointe">La pointe des doigts</option>
                        <option value="pulpe" selected>La pulpe des 3 doigts du milieu</option>
                        <option value="paume">La paume entière</option>
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

            <button type="button" id="btn-submit" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER CETTE FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE CLOUD (N = <span id="n-total">0</span>)</div>
        <div style="overflow-x:auto;"><table id="data-table"><thead><tr><th>ID</th><th>Sexe</th><th>Savoir %</th><th>Pratique %</th></tr></thead><tbody id="database-body"></tbody></table></div>
    </div>
    
    <div id="content-3" class="form-content"><div id="graph-savoir"></div><div id="graph-pratique"></div></div>
    <div id="content-4" class="form-content"><div id="final-conclusion"></div></div>
</div>

<script>
    // --- CONFIGURATION URL ---
    const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/AKfycbyMX8dcz3yHj3Y7ou8ByVSORkN0hjkCPkE7eaq0bxbzSxpzC_8n5kEZyt45lharxPYI/exec";
    
    let database = [];
    let isAdmin = false;

    // Initialisation codes
    const codeSel = document.getElementById('code-enquete');
    for(let i=1; i<=200; i++) { 
        let o=document.createElement('option'); o.value="INF-"+i.toString().padStart(3, '0'); o.text="Fiche N° "+i; codeSel.appendChild(o); 
    }

    window.onload = loadDataFromCloud;

    function loadDataFromCloud() {
        document.getElementById('loading-indicator').style.display = "inline";
        fetch(GOOGLE_SCRIPT_URL).then(r => r.json()).then(data => {
            database = data;
            document.getElementById('count-badge').textContent = database.length;
            document.getElementById('loading-indicator').style.display = "none";
            if(isAdmin) updateAnalysis();
        }).catch(() => { document.getElementById('loading-indicator').textContent = "Erreur Cloud"; });
    }

    function adminLogin() {
        if(prompt("Code Administrateur :") === "2020") {
            isAdmin = true;
            document.querySelectorAll('.admin-locked').forEach(el => el.classList.remove('admin-locked'));
            updateAnalysis();
        }
    }

    function saveRecord() {
        const btn = document.getElementById('btn-submit');
        btn.disabled = true; btn.textContent = "⏳ ENVOI...";

        let r = {
            id: document.getElementById('code-enquete').value,
            sexe: document.getElementById('sexe').value,
            scoreSavoir: Math.floor(Math.random() * 100), // Logique de calcul à inclure
            scorePratique: Math.floor(Math.random() * 100),
            obstacles: getCheckedValues('group-risques')
        };

        fetch(GOOGLE_SCRIPT_URL, {
            method: 'POST',
            mode: 'no-cors',
            body: JSON.stringify(r)
        }).then(() => {
            alert("✅ Enregistré sur le Cloud !");
            loadDataFromCloud();
            btn.disabled = false; btn.textContent = "💾 ENREGISTRER CETTE FICHE";
        });
    }

    function updateAnalysis() {
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(r => `<tr><td>${r.id}</td><td>${r.sexe}</td><td>${r.scoreSavoir}%</td><td>${r.scorePratique}%</td></tr>`).join('');
        document.getElementById('n-total').textContent = database.length;
    }

    function getCheckedValues(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); }
    function switchTab(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab').forEach((t, idx) => { if(idx+1===i) t.classList.add('active'); else t.classList.remove('active'); });
    }
</script>
</body>
</html>
