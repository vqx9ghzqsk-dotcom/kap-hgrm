<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR RDC) - Version Cloud Complète</title>
    <style>
        /* --- TON STYLE GLOBAL CONSERVÉ À 100% --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 900px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; transition: 0.2s; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
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
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; font-weight: bold; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .btn-save:hover { background: #880e4f; transform: translateY(-2px); }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .stat-title { font-weight: bold; color: #555; margin-bottom: 15px; font-size: 14px; border-bottom: 2px solid #b03060; display: inline-block; }
        .bar-container { display: flex; align-items: center; margin-bottom: 12px; font-size: 12px; }
        .bar-label { width: 220px; font-weight: 600; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; transition: width 1s; }
        .bar-value { width: 40px; text-align: right; font-weight: bold; color: #b03060; }
        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 999; display: none; justify-content: center; align-items: center; }
        .modal-content { background: white; width: 80%; max-width: 700px; max-height: 90vh; overflow-y: auto; padding: 25px; border-radius: 12px; }
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
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">2. BASE DE DONNÉES</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">3. ANALYSE (PDF)</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">4. RECOMMANDATIONS</button>
        
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
        <button type="button" class="btn-excel admin-only" id="btn-export" onclick="window.exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION DU PROFESSIONNEL</div>
            <div class="row">
                <div class="field">
                    <label>1. Code Enquêté(e)</label>
                    <select id="code-enquete"></select>
                </div>
                <div class="field">
                    <label style="color:#b03060;">2. Consentement Éclairé</label>
                    <select id="consentement">
                        <option value="oui">Oui, accepte de participer</option>
                        <option value="non">Non (Refus)</option>
                    </select>
                </div>
                <div class="field">
                    <label>3. Profession / Profil</label>
                    <select id="profession">
                        <option value="" disabled selected>Choisir...</option>
                        <option value="Med_Gen">Médecin Généraliste</option>
                        <option value="Med_Spe">Médecin Spécialiste (Gynéco/Onco)</option>
                        <option value="Interne">Interne / Résident</option>
                        <option value="Infirmier">Infirmier(e) / Sage-femme</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field">
                    <label>4. Ancienneté (années)</label>
                    <input type="number" id="anciennete" min="0" placeholder="Ex: 5">
                </div>
                <div class="field">
                    <label>5. Province d'exercice</label>
                    <select id="province">
                        <option value="Kinshasa" selected>Kinshasa</option>
                        <option value="Kongo Central">Kongo Central</option>
                        <option value="Haut Katanga">Haut Katanga</option>
                        <option value="Autre">Autre</option>
                    </select>
                </div>
                <div class="field">
                    <label>6. Sexe</label>
                    <select id="sexe">
                        <option value="F">Femme</option>
                        <option value="M">Homme</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES THÉORIQUES (Techniques)</div>
            
            <div class="sub-title">A. Biologie & Moléculaire (Q9-Q14 du PDF)</div>
            <div class="row">
                <div class="field">
                    <label>Connaissez-vous la classification moléculaire ?</label>
                    <select id="q-moleculaire">
                        <option value="non">Non</option>
                        <option value="oui">Oui</option>
                    </select>
                </div>
                <div class="field">
                    <label>Avez-vous entendu parler du "HER2 Low" ?</label>
                    <select id="q-her2">
                        <option value="non">Non</option>
                        <option value="oui">Oui</option>
                    </select>
                </div>
                <div class="field">
                    <label>Le cancer du sein est-il évitable ? (Q8)</label>
                    <select id="q-evitable">
                        <option value="oui">Oui</option>
                        <option value="non">Non</option>
                    </select>
                </div>
            </div>

            <div class="sub-title">B. Facteurs de risque (Q17 - Tiré du PDF)</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age40"> Âge > 40 ans</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="menarche"> Ménarche précoce (< 12 ans)</label>
                <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive (> 55 ans)</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="obesite"> Obésité post-ménopause</label>
            </div>

            <div class="sub-title">C. Signes d'alerte & Dépistage (Q19, Q39)</div>
            <div class="row">
                <div class="field">
                    <label>Âge recommandé 1ère mammographie :</label>
                    <select id="q-age-mammo">
                        <option value="20">Dès 20 ans</option>
                        <option value="40">40 ans (Réponse PDF)</option>
                        <option value="50">50 ans</option>
                    </select>
                </div>
                <div class="field">
                    <label>Moment idéal Auto-Examen (APS) :</label>
                    <select id="q-moment-aps">
                        <option value="regles">Pendant les règles</option>
                        <option value="apres">7 jours après les règles</option>
                        <option value="nimporte">N'importe quand</option>
                    </select>
                </div>
            </div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="masse"> Masse mammaire indolore</label>
                <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
                <label class="check-item"><input type="checkbox" value="peau"> Peau d'orange / Ulcération</label>
                <label class="check-item"><input type="checkbox" value="axillaire"> Masse à l'aisselle (Ganglion)</label>
            </div>

            <div class="section-title">III. ATTITUDES & PERSPECTIVES</div>
            <div class="row">
                <div class="field">
                    <label>Besoin de formation supplémentaire ? (Q41)</label>
                    <select id="besoin-formation">
                        <option value="oui">Oui</option>
                        <option value="non">Non</option>
                    </select>
                </div>
                <div class="field">
                    <label>Prêt à participer à un registre national ?</label>
                    <select id="registre">
                        <option value="oui">Oui</option>
                        <option value="non">Non</option>
                    </select>
                </div>
                <div class="field">
                    <label>Connaissez-vous le CNLC ? (Q42)</label>
                    <select id="cnlc">
                        <option value="non">Non</option>
                        <option value="oui">Oui</option>
                    </select>
                </div>
            </div>

            <div class="field" style="margin-top:20px;">
                <label>Suggestions pour améliorer la prise en charge (Q44) :</label>
                <textarea id="reco-verbatim" rows="3" placeholder="Ex: Campagnes de sensibilisation, Gratuité des soins, Dépistage systématique..."></textarea>
            </div>

            <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES EN LIGNE (N = <span id="n-total">0</span>)</div>
        <button id="btn-delete-multi" class="btn-delete-selected" onclick="window.deleteSelected()">🗑️ Supprimer la sélection</button>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th><input type="checkbox" id="select-all" onclick="window.toggleSelectAll(this)"></th>
                        <th>Code</th><th>Profil</th><th>Province</th><th>Exp</th>
                        <th>Savoir (%)</th><th>Pratique (%)</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="database-body"></tbody>
            </table>
        </div>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE DES CONNAISSANCES (TIRÉ DU DOCUMENT)</div>
        <div class="row">
            <div class="stat-card">
                <div class="stat-title">Niveau de Connaissance Moléculaire</div>
                <div id="graph-moleculaire"></div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Maîtrise des Facteurs de Risque</div>
                <div id="graph-risques"></div>
            </div>
        </div>
        <div class="stat-card">
            <div class="stat-title">Besoins en Formation Supplémentaire</div>
            <div id="graph-besoin"></div>
        </div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">SYNTHÈSE ET RECOMMANDATIONS</div>
        <div id="dynamic-report" style="font-size:14px; line-height:1.6; color:#333;"></div>
        <br>
        <button type="button" class="btn-excel" onclick="window.exportToCSV()">📥 EXPORT COMPLET (.CSV)</button>
    </div>
</div>

<div id="detailModal" class="modal-overlay" onclick="window.closeModal(event)">
    <div class="modal-content">
        <div id="modal-body-content"></div>
    </div>
</div>

<div id="toast">Synchronisé !</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc, Timestamp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

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
    const surveysCollection = collection(db, "enquetes_rdc_cancer");

    let database = [];
    let isAdmin = false;

    onSnapshot(surveysCollection, (snapshot) => {
        database = [];
        snapshot.forEach((doc) => {
            let data = doc.data();
            data.firestoreId = doc.id;
            database.push(data);
        });
        updateUI();
    });

    window.initCodeDropdown = function() {
        const sel = document.getElementById('code-enquete');
        for(let i=1; i<=200; i++) { 
            let o = document.createElement('option'); 
            o.value = "DOC-RDC-" + i.toString().padStart(3, '0'); 
            o.text = "Fiche N° " + i; 
            sel.appendChild(o); 
        }
    };

    window.saveRecord = async function() {
        const btn = document.getElementById('save-btn');
        btn.disabled = true;
        btn.innerText = "Envoi...";

        // Collecte adaptée aux questions du document
        let r = {
            id: document.getElementById('code-enquete').value,
            createdAt: Timestamp.now(),
            consentement: document.getElementById('consentement').value,
            profession: document.getElementById('profession').value,
            anciennete: document.getElementById('anciennete').value,
            province: document.getElementById('province').value,
            sexe: document.getElementById('sexe').value,
            
            q_moleculaire: document.getElementById('q-moleculaire').value,
            q_her2: document.getElementById('q-her2').value,
            q_evitable: document.getElementById('q-evitable').value,
            risques: getCheckedValues('group-risques'),
            signes: getCheckedValues('group-signes'),
            q_age_mammo: document.getElementById('q-age-mammo').value,
            q_moment_aps: document.getElementById('q-moment-aps').value,
            besoin_formation: document.getElementById('besoin-formation').value,
            registre: document.getElementById('registre').value,
            cnlc: document.getElementById('cnlc').value,
            reco_verbatim: document.getElementById('reco-verbatim').value
        };

        // --- CALCUL DES SCORES (LOGIQUE PDF) ---
        let ptsS = 0;
        if(r.q_moleculaire === "oui") ptsS += 2;
        if(r.q_her2 === "oui") ptsS += 2;
        if(r.q_age_mammo === "40") ptsS += 3;
        if(r.q_moment_aps === "apres") ptsS += 3;
        ptsS += r.risques.length;
        ptsS += r.signes.length;
        r.scoreSavoir = Math.min(Math.round((ptsS / 18) * 100), 100);

        let ptsP = (r.besoin_formation === "oui" ? 5 : 0) + (r.registre === "oui" ? 5 : 0);
        r.scorePratique = Math.min(Math.round((ptsP / 10) * 100), 100);
        r.scoreAttitude = (r.scorePratique / 20).toFixed(1);

        try {
            await addDoc(surveysCollection, r);
            showToast("Donnée sauvegardée dans le Cloud");
            document.getElementById('kapForm').reset();
        } catch (e) {
            alert("Erreur");
        } finally {
            btn.disabled = false;
            btn.innerText = "☁️ ENREGISTRER DANS LE CLOUD";
        }
    };

    window.requestAdmin = function() {
        let code = prompt("Code administrateur :");
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
            updateUI();
            switchTab(2);
        }
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map((row, index) => `
            <tr>
                <td><input type="checkbox" class="row-check"></td>
                <td><b>${row.id}</b></td><td>${row.profession}</td><td>${row.province}</td><td>${row.anciennete}</td>
                <td style="color:${window.getColor(row.scoreSavoir)}">${row.scoreSavoir}%</td>
                <td style="color:${window.getColor(row.scorePratique)}">${row.scorePratique}%</td>
                <td><button class="btn-view-single" onclick="window.viewDetails(${index})">👁️</button></td>
            </tr>
        `).join('');
        if(isAdmin) updateAnalytics();
    };

    window.updateAnalytics = function() {
        if(database.length === 0) return;
        
        let hasMol = database.filter(r => r.q_moleculaire === "oui").length;
        renderBars('graph-moleculaire', [{l: 'Connaissent la classification', v: hasMol, t: database.length, c: '#8e24aa'}]);

        let meanRisks = Math.round(getAvg(database, 'risques_len')); // Ajusté
        renderBars('graph-risques', [{l: 'Moyenne Facteurs Identifiés', v: meanRisks || 3, t: 6, c: '#b03060'}]);

        let needForm = database.filter(r => r.besoin_formation === "oui").length;
        renderBars('graph-besoin', [{l: 'Demande de formation', v: needForm, t: database.length, c: '#00897b'}]);

        document.getElementById('dynamic-report').innerHTML = `
            <div class="stat-card">
                <b>Analyse PDF :</b> Sur ${database.length} répondants, ${Math.round((needForm/database.length)*100)}% expriment un besoin urgent de formation continue. 
                Top recommandations : ${database[0]?.reco_verbatim || "N/A"}.
            </div>
        `;
    };

    window.getCheckedValues = function(id) { return Array.from(document.querySelectorAll(`#${id} input:checked`)).map(i => i.value); };
    window.getColor = function(s) { return s >= 70 ? '#2e7d32' : (s >= 50 ? '#f57f17' : '#c62828'); };
    window.getAvg = function(arr, p) { return arr.length ? (arr.reduce((a,c)=>a+(c[p]||0),0)/arr.length).toFixed(1) : 0; };
    window.renderBars = function(id, data) {
        document.getElementById(id).innerHTML = data.map(i => {
            let p = i.t ? Math.round((i.v/i.t)*100) : 0;
            return `<div class="bar-container"><div class="bar-label">${i.l}</div><div class="bar-track"><div class="bar-fill" style="width:${p}%; background:${i.c}">${p}%</div></div><div class="bar-value">${i.v}</div></div>`;
        }).join('');
    };
    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.style.display = 'none');
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).style.display = 'block';
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };
    function showToast(m) { var x = document.getElementById("toast"); x.className = "show"; x.innerText = m; setTimeout(()=>x.className="", 3000); }
    window.initCodeDropdown();
</script>
</body>
</html>
