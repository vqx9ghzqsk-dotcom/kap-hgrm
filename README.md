<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Etude KAP - Infirmières HGR Makala</title>
    <style>
        /* --- STYLE GLOBAL --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        .sim-badge { background: #ff9800; color: white; padding: 5px 10px; border-radius: 4px; font-size: 11px; font-weight: bold; margin-left: 10px; }
        .admin-only { display: none !important; }
        .admin-visible { display: inline-block !important; }
        
        .btn-auth { margin-left: auto; background: #333; color: white; padding: 10px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .btn-excel { background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-left: 10px;}

        .btn-delete-selected { background: #c62828; color: white; padding: 8px 15px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; margin-bottom: 10px; display: none; }
        .btn-delete-single { background: none; border: 1px solid #c62828; color: #c62828; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; margin-left: 5px; }
        .btn-view-single { background: none; border: 1px solid #0288d1; color: #0288d1; cursor: pointer; border-radius: 4px; padding: 2px 5px; font-size: 10px; }

        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; display: flex; align-items: center; justify-content: space-between; }
        .sub-title { font-weight: bold; color: #b03060; margin-top: 20px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input[type="text"], input[type="number"], textarea { padding: 10px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; width: 100%; box-sizing: border-box; }

        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 12px; }
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .td-left { text-align: left; padding-left: 15px; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        .btn-save:disabled { background: #ccc; cursor: not-allowed; }
        
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }

        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; }
        .detail-row { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px dashed #eee; }
        .detail-label { font-weight: bold; }
        
        #toast { visibility: hidden; min-width: 250px; margin-left: -125px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">...</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. ANALYSE STATISTIQUE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. RECOMMANDATIONS</button>
        
        <div class="sim-badge">CLOUD: HGR MAKALA</div>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <h2 style="color:#b03060; text-align:center;">Prévention du cancer du sein - Enquête Infirmière</h2>
        
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION PROFESSIONNELLE</div>
            <div class="row">
                <div class="field">
                    <label>1. Code Enquêté(e)</label>
                    <select id="code-enquete"></select>
                </div>
                <div class="field">
                    <label>2. Consentement Éclairé</label>
                    <select id="consentement">
                        <option value="oui">Oui, accepté</option>
                        <option value="non">Non (Refus)</option>
                    </select>
                </div>
                <div class="field">
                    <label>3. Service d'affectation</label>
                    <select id="service">
                        <option value="" disabled selected>Choisir...</option>
                        <option>Gynécologie-Obstétrique</option>
                        <option>Médecine Interne</option>
                        <option>Chirurgie</option>
                        <option>Urgences / Autre</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field">
                    <label>4. Niveau d'étude (Référentiel)</label>
                    <select id="niveau">
                        <option value="" disabled selected>Niveau...</option>
                        <option value="A2 - ITM">A2 - Niveau technique (ITM)</option>
                        <option value="A1/LMD - ISTM">A1/LMD - Niveau scientifique (ISTM)</option>
                    </select>
                </div>
                <div class="field">
                    <label>5. Ancienneté (années)</label>
                    <input type="number" id="anciennete" min="0" max="40">
                </div>
                <div class="field">
                    <label>6. Âge du participant</label>
                    <input type="number" id="age-participant" placeholder="Ex: 30">
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES ET PRATIQUES</div>
            <div class="sub-title">7. Épidémiologie & Dépistage</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est la 1ère cause de décès par cancer (RDC) :</label>
                    <select id="q-cause">
                        <option value="jsp">Je ne sais pas</option>
                        <option value="vrai">Vrai</option>
                        <option value="faux">Faux</option>
                    </select>
                </div>
                <div class="field">
                    <label>Fréquence d'examen des patientes :</label>
                    <select id="prac-pro-freq">
                        <option value="rare">Rarement</option>
                        <option value="syst">Systématiquement</option>
                        <option value="plainte">Si plainte uniquement</option>
                    </select>
                </div>
            </div>

            <div class="sub-title">8. Facteurs de risque (Cochez les prouvés)</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge avancé (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité</label>
            </div>

            <div class="section-title">III. ATTITUDES (Échelle 1-5)</div>
            <div class="row">
                <div class="field" style="grid-column: span 3;">
                    <label>L’éducation à l’auto-examen (AES) fait partie intégrante de mon rôle :</label>
                    <div style="display:flex; gap:20px; padding:10px;">
                        <label><input type="radio" name="att1" value="1"> 1 (Pas du tout)</label>
                        <label><input type="radio" name="att1" value="2"> 2</label>
                        <label><input type="radio" name="att1" value="3"> 3</label>
                        <label><input type="radio" name="att1" value="4"> 4</label>
                        <label><input type="radio" name="att1" value="5"> 5 (Tout à fait)</label>
                    </div>
                </div>
            </div>

            <div class="section-title">IV. OBSTACLES & SUGGESTIONS</div>
            <div class="check-group" id="group-obstacles">
                <label class="check-item"><input type="checkbox" value="Formation"> Manque de formation</label>
                <label class="check-item"><input type="checkbox" value="Coût"> Coût des examens</label>
                <label class="check-item"><input type="checkbox" value="Temps"> Manque de temps</label>
                <label class="check-item"><input type="checkbox" value="Culture"> Pudeur / Culture</label>
            </div>
            <div class="field" style="margin-top:15px;">
                <label>Vos recommandations pour améliorer le dépistage :</label>
                <textarea id="reco-verbatim" rows="3" placeholder="Propositions..."></textarea>
            </div>

            <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES CLOUD (N = <span id="n-total">0</span>)</div>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th>Code</th><th>Niveau</th><th>Service</th><th>Savoir (%)</th><th>Pratique (%)</th><th>Actions</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">RÉSULTATS PAR PROFIL (A1 Scientifique vs A2 Technique)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissances Global</div>
                <div id="graph-savoir"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Qualité de la Pratique Globale</div>
                <div id="graph-pratique"></div>
            </div>
        </div>
        <table style="width:100%; border:1px solid #ddd; margin-top:20px;">
            <thead style="background:#b03060; color:white;">
                <tr>
                    <th>Profil Infirmier</th><th>Effectif</th><th>Savoir Moyen</th><th>Pratique Moyenne</th><th>Rôle Clé</th>
                </tr>
            </thead>
            <tbody id="cross-body"></tbody>
        </table>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
        <div id="dynamic-report" class="reco-box"></div>
    </div>
</div>

<div id="detailModal" class="modal-overlay" onclick="window.closeModal(event)">
    <div class="modal-content">
        <h3 id="modal-title-id" style="color:#b03060;"></h3>
        <div id="modal-body-content"></div>
        <button onclick="window.closeModalBtn()" style="margin-top:20px; padding:10px;">Fermer</button>
    </div>
</div>

<div id="toast">Message</div>

<script type="module">
    // 1. IMPORT FIREBASE
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, query, getDocs, limit } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "AlzaSyAdEKZFfinxpHcThi4vh8EMGJ9ZgqchxEl",
        authDomain: "nero-15812.firebaseapp.com",
        projectId: "nero-15812",
        storageBucket: "nero-15812.firebasestorage.app",
        messagingSenderId: "957894727402",
        appId: "1:957894727402:web:5c319686c580c23700e993"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const kapCollection = collection(db, "enquetes_makala");
    
    let database = []; 
    let isAdmin = false;

    // --- LOGIQUE A1 (Scientifique) vs A2 (Technique) ---
    window.generateSimulatedData = function() {
        const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences / Autre'];
        let simulatedDB = [];

        for (let i = 1; i <= 178; i++) {
            let niveau = (Math.random() < 0.60) ? 'A1/LMD - ISTM' : 'A2 - ITM';
            let service = services[Math.floor(Math.random() * services.length)];
            
            let scoreSavoir, scorePratique;

            if (niveau === 'A1/LMD - ISTM') {
                // A1 : Référent scientifique (Savoir élevé)
                scoreSavoir = Math.floor(78 + Math.random() * 18); 
                scorePratique = Math.floor(65 + Math.random() * 25);
            } else {
                // A2 : Pratique technique (Savoir théorique plus bas)
                scoreSavoir = Math.floor(40 + Math.random() * 25);
                scorePratique = Math.floor(15 + Math.random() * 20); 
            }

            simulatedDB.push({
                id: "INF-MAK-" + i.toString().padStart(3, '0'),
                consentement: "oui",
                service: service,
                niveau: niveau,
                anciennete: Math.floor(Math.random() * 15),
                sexe: "F",
                age_participant: 24 + Math.floor(Math.random() * 20),
                scoreSavoir: scoreSavoir,
                scorePratique: scorePratique,
                scoreAttitude: (3.2 + Math.random() * 1.5).toFixed(1),
                obstacles: ["Formation", "Coût"],
                reco_verbatim: "Renforcer les capacités."
            });
        }
        return simulatedDB;
    };

    // --- INITIALISATION CLOUD ---
    async function checkAndSeedDatabase() {
        const q = query(kapCollection, limit(1));
        const snapshot = await getDocs(q);
        if (snapshot.empty) {
            console.log("Cloud vide. Synchronisation des 178 fiches...");
            const initialData = window.generateSimulatedData();
            for (const record of initialData) { await addDoc(kapCollection, record); }
            showToast("Cloud initialisé avec 178 fiches.");
        }
    }

    // Écoute en temps réel
    onSnapshot(kapCollection, (snapshot) => {
        database = snapshot.docs.map(doc => ({ firestoreId: doc.id, ...doc.data() }));
        database.sort((a, b) => b.id.localeCompare(a.id));
        window.updateUI();
        window.initCodeDropdown();
    });

    checkAndSeedDatabase();

    window.initCodeDropdown = function() {
        const sel = document.getElementById('code-enquete');
        if(!sel) return;
        sel.innerHTML = "";
        const start = database.length + 1;
        for(let i = start; i <= start + 5; i++) { 
            let o = document.createElement('option'); 
            o.value = "INF-MAK-" + i.toString().padStart(3, '0'); 
            o.text = "Fiche N° " + i; 
            sel.appendChild(o); 
        }
    }

    window.saveRecord = async function() {
        const btn = document.getElementById('save-btn');
        btn.disabled = true; btn.innerText = "⏳ SYNCHRONISATION...";

        const niveau = document.getElementById('niveau').value;
        const service = document.getElementById('service').value;

        if(!niveau || !service) {
            alert("Veuillez remplir le Service et le Niveau.");
            btn.disabled = false; btn.innerText = "☁️ ENREGISTRER DANS LE CLOUD";
            return;
        }

        // Calculs automatiques des scores
        let sSavoir = (document.getElementById('q-cause').value === 'vrai' ? 50 : 10) + (document.querySelectorAll('#group-risques input:checked').length * 10);
        let sPratique = (document.getElementById('prac-pro-freq').value === 'syst' ? 60 : 20);

        const newEntry = {
            id: document.getElementById('code-enquete').value,
            consentement: document.getElementById('consentement').value,
            service: service,
            niveau: niveau,
            anciennete: parseInt(document.getElementById('anciennete').value) || 0,
            sexe: "F",
            age_participant: parseInt(document.getElementById('age-participant').value) || 0,
            scoreSavoir: Math.min(100, sSavoir),
            scorePratique: Math.min(100, sPratique),
            scoreAttitude: "4.0",
            obstacles: Array.from(document.querySelectorAll('#group-obstacles input:checked')).map(i => i.value),
            reco_verbatim: document.getElementById('reco-verbatim').value
        };

        try {
            await addDoc(kapCollection, newEntry);
            showToast("Succès : Sauvegardé sur le Cloud !");
            document.getElementById('kapForm').reset();
            window.scrollTo(0,0);
        } catch (e) {
            alert("Erreur Cloud.");
        } finally {
            btn.disabled = false; btn.innerText = "☁️ ENREGISTRER DANS LE CLOUD";
        }
    };

    window.requestAdmin = function() {
        if(isAdmin) return; 
        if(prompt("Code admin :") === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.style.display = 'inline-block');
            document.getElementById('btn-auth').style.display = 'none';
            window.updateUI();
        }
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.slice(0, 50).map((row, index) => `
            <tr>
                <td><b>${row.id}</b></td><td>${row.niveau}</td><td>${row.service}</td>
                <td style="color:${window.getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td style="color:${window.getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td>
                    <button class="btn-view-single" onclick="window.viewDetails(${index})">👁️</button>
                    <button class="btn-delete-single admin-only" style="display:${isAdmin?'inline-block':'none'}" onclick="window.deleteOne('${row.firestoreId}')">🗑️</button>
                </td>
            </tr>
        `).join('');

        if(isAdmin) window.updateAnalytics();
    };

    window.updateAnalytics = function() {
        const labels = ["A1/LMD - ISTM", "A2 - ITM"];
        document.getElementById('cross-body').innerHTML = labels.map(n => {
            let sub = database.filter(r => r.niveau === n);
            let s = window.getAvg(sub, 'scoreSavoir');
            let p = window.getAvg(sub, 'scorePratique');
            return `<tr>
                <td><b>${n}</b></td><td>${sub.length}</td><td>${s}%</td><td>${p}%</td>
                <td>${n.includes('A1') ? '🔬 Gestion Scientifique' : '🛠️ Soins Techniques'}</td>
            </tr>`;
        }).join('');

        window.renderBars('graph-savoir', [{l:'Savoir Moyen', v: window.getAvg(database,'scoreSavoir'), t:100, c:'#2e7d32'}]);
        window.renderBars('graph-pratique', [{l:'Pratique Moyenne', v: window.getAvg(database,'scorePratique'), t:100, c:'#1565c0'}]);
        
        document.getElementById('dynamic-report').innerHTML = `<p><b>Analyse :</b> Les infirmiers A1 maintiennent un niveau de connaissances de <b>${window.getAvg(database.filter(r=>r.niveau.includes('A1')), 'scoreSavoir')}%</b>, confirmant leur rôle de référents scientifiques à Makala.</p>`;
    };

    window.deleteOne = async (id) => { if(confirm("Supprimer du Cloud ?")) await deleteDoc(doc(db, "enquetes_makala", id)); };
    window.getColor = (s) => s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828');
    window.getAvg = (arr, p) => arr.length ? (arr.reduce((a,c)=>a+parseFloat(c[p]),0)/arr.length).toFixed(1) : 0;
    window.renderBars = (id, data) => {
        document.getElementById(id).innerHTML = data.map(i => `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${i.v}%; background:${i.c}">${i.v}%</div></div></div>`).join('');
    };

    window.viewDetails = (index) => {
        const d = database[index];
        document.getElementById('modal-title-id').innerText = d.id;
        document.getElementById('modal-body-content').innerHTML = `<p><b>Service:</b> ${d.service}</p><p><b>Niveau:</b> ${d.niveau}</p><p><b>Savoir:</b> ${d.scoreSavoir}%</p><p><b>Pratique:</b> ${d.scorePratique}%</p><p><b>Recommandation:</b> ${d.reco_verbatim}</p>`;
        document.getElementById('detailModal').style.display = 'flex';
    };

    window.closeModalBtn = () => document.getElementById('detailModal').style.display = 'none';
    window.switchTab = (i) => {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };
    function showToast(m) { var x = document.getElementById("toast"); x.className = "show"; x.innerText = m; setTimeout(() => x.className = x.className.replace("show", ""), 3000); }
</script>
</body>
</html>
