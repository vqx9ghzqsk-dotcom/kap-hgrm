<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enquête CAP - Cancer du Sein (HGR RDC) - Version Cloud Complète</title>
    <style>
        /* --- STYLE GLOBAL --- */
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
        th { background: #f8f9fa; padding: 10px; border: 1px solid #ddd; text-align: center; }
        td { border: 1px solid #eee; padding: 10px; text-align: center; }
        .td-left { text-align: left; padding-left: 15px; width: 50%; }

        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 10px; background: #fdfdfd; padding: 15px; border: 1px solid #eee; border-radius: 8px; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; }
        .check-item input { margin-right: 12px; transform: scale(1.2); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; }
        
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 20px; border-radius: 10px; margin: 0 15px; overflow: hidden; }
        .bar-fill { height: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 10px; transition: width 1s; }
        
        #toast { visibility: hidden; min-width: 250px; background-color: #333; color: #fff; text-align: center; border-radius: 2px; padding: 16px; position: fixed; z-index: 1000; left: 50%; bottom: 30px; transform: translateX(-50%); }
        #toast.show { visibility: visible; animation: fadein 0.5s, fadeout 0.5s 2.5s; }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">COLLECTE <span id="count-badge" class="counter-badge">...</span></button>
        <button class="tab admin-only" id="tab-2" onclick="switchTab(2)">MATRICE DE DÉPOUILLEMENT</button>
        <button class="tab admin-only" id="tab-3" onclick="switchTab(3)">RÉSULTATS & ANALYSE</button>
        <button class="tab admin-only" id="tab-4" onclick="switchTab(4)">CONCLUSION</button>
        <button type="button" class="btn-auth" id="btn-auth" onclick="window.requestAdmin()">🔒 ACCÈS ADMIN</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL PROFESSIONNEL</div>
            <div class="row">
                <div class="field"><label>Code Enquêté(e)</label><select id="code-enquete"></select></div>
                <div class="field"><label style="color:#b03060;">Consentement Éclairé</label><select id="consentement"><option value="oui">Oui</option><option value="non">Non</option></select></div>
                <div class="field"><label>Service d'affectation</label>
                    <select id="service">
                        <option value="" disabled selected>Choisir...</option>
                        <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option><option>Chirurgie</option><option>Urgences / Autre</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Niveau d'étude</label><select id="niveau"><option>A2</option><option>A1</option><option>A0</option></select></div>
                <div class="field"><label>Ancienneté (années)</label><input type="number" id="anciennete"></div>
                <div class="field"><label>Sexe</label><select id="sexe"><option value="F">Féminin</option><option value="M">Masculin</option></select></div>
            </div>
            <div class="row">
                <div class="field"><label>État Civil</label><select id="etat-civil"><option>Célibataire</option><option>Mariée</option><option>Divorcée</option><option>Veuve</option></select></div>
                <div class="field"><label>Province d'exercice</label><select id="province"><option>Kinshasa</option><option>Kongo Central</option><option>Haut-Katanga</option><option>Nord/Sud Kivu</option><option>Autre</option></select></div>
                <div class="field"><label>Catégorie Professionnelle</label><select id="cat-pro"><option>Médecin</option><option>Infirmier(e)</option><option>Sage-femme</option></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES THÉORIQUES</div>
            <div class="sub-title">Biologie & Classification (Source Document RDC)</div>
            <div class="row">
                <div class="field"><label>Entendu parler de la classification moléculaire ?</label><select id="q-moleculaire"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Connaissez-vous le terme "HER2 Low" ?</label><select id="q-her2"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Connaissez-vous les thérapies ciblées ?</label><select id="q-therapie"><option value="non">Non</option><option value="oui">Oui</option></select></div>
            </div>

            <div class="sub-title">Épidémiologie & Dépistage</div>
            <div class="row">
                <div class="field"><label>1ère cause de décès par cancer en RDC ?</label><select id="q-cause"><option value="vrai">Vrai</option><option value="faux">Faux</option></select></div>
                <div class="field"><label>Moment idéal pour l'AES ?</label><select id="q-moment-aes"><option value="apres">7-10 jours après règles</option><option value="regles">Pendant</option></select></div>
            </div>

            <div class="sub-title">Facteurs de risque (Scientifiques)</div>
            <div class="check-group" id="group-risques">
                <label class="check-item"><input type="checkbox" value="age"> Âge (>50 ans)</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool / Tabac</label>
                <label class="check-item"><input type="checkbox" value="graisse"> Régime riche en graisses</label>
                <label class="check-item"><input type="checkbox" value="contraceptif"> Contraceptifs oraux</label>
            </div>

            <div class="sub-title">Signes d’alerte</div>
            <div class="check-group" id="group-signes">
                <label class="check-item"><input type="checkbox" value="nodule"> Nodule dur</label>
                <label class="check-item"><input type="checkbox" value="ulceration"> Ulcération du sein</label>
                <label class="check-item"><input type="checkbox" value="peau"> Aspect peau d’orange</label>
                <label class="check-item"><input type="checkbox" value="asymetrie"> Asymétrie nouvelle</label>
            </div>

            <div class="section-title">III. ATTITUDES & PRATIQUES</div>
            <table>
                <thead><tr><th class="td-left">Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr></thead>
                <tbody>
                    <tr><td class="td-left">L'éducation à l'AES est mon rôle.</td><td><input type="radio" name="att1" value="1"></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td><td><input type="radio" name="att1" value="4"></td><td><input type="radio" name="att1" value="5"></td></tr>
                </tbody>
            </table>

            <div class="sub-title">Technique de Palpation</div>
            <div class="row">
                <div class="field"><label>Partie de la main ?</label><select id="prac-main"><option value="pulpe">La pulpe des 3 doigts</option><option value="pointe">La pointe</option></select></div>
                <div class="field"><label>Zone indispensable ?</label><select id="prac-zone"><option value="axillaire">Le creux axillaire</option><option value="mamelon">Mamelon</option></select></div>
            </div>

            <div class="section-title">IV. POLITIQUE DE SANTÉ</div>
            <div class="row">
                <div class="field"><label>Connaissance du CNLC ?</label><select id="connaissance-cnlc"><option value="non">Non</option><option value="oui">Oui</option></select></div>
                <div class="field"><label>Intérêt Registre National ?</label><select id="interet-registre"><option value="oui">Oui</option><option value="non">Non</option></select></div>
            </div>

            <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">BASE DE DONNÉES (N = <span id="n-total">0</span>)</div>
        <table id="database-table"><thead><tr><th>Code</th><th>Province</th><th>Savoir %</th><th>Pratique %</th><th>Actions</th></tr></thead><tbody id="database-body"></tbody></table>
    </div>
</div>

<div id="toast">Opération réussie !</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, collection, addDoc, onSnapshot, Timestamp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

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
        snapshot.forEach(doc => { database.push({ ...doc.data(), firestoreId: doc.id }); });
        updateUI();
    });

    window.saveRecord = async function() {
        const btn = document.getElementById('save-btn');
        btn.disabled = true; btn.innerText = "Traitement...";

        let r = {
            id: document.getElementById('code-enquete').value,
            createdAt: Timestamp.now(),
            service: document.getElementById('service').value,
            province: document.getElementById('province').value,
            q_moleculaire: document.getElementById('q-moleculaire').value,
            q_her2: document.getElementById('q-her2').value,
            risques: Array.from(document.querySelectorAll('#group-risques input:checked')).map(i => i.value),
            signes: Array.from(document.querySelectorAll('#group-signes input:checked')).map(i => i.value),
            prac_main: document.getElementById('prac-main').value,
            prac_zone: document.getElementById('prac-zone').value,
        };

        // Calcul Scores
        let ptsS = (r.q_moleculaire === "oui" ? 2 : 0) + (r.q_her2 === "oui" ? 2 : 0) + r.risques.length + r.signes.length;
        r.scoreSavoir = Math.min(100, Math.round((ptsS / 20) * 100));
        r.scorePratique = (r.prac_main === "pulpe" ? 50 : 0) + (r.prac_zone === "axillaire" ? 50 : 0);

        try {
            await addDoc(surveysCollection, r);
            alert("Données sauvegardées !");
            document.getElementById('kapForm').reset();
        } catch (e) { alert("Erreur de connexion."); }
        finally { btn.disabled = false; btn.innerText = "☁️ ENREGISTRER DANS LE CLOUD"; }
    };

    window.requestAdmin = function() {
        let code = prompt("Code admin :");
        if(code === "1398") {
            isAdmin = true;
            document.querySelectorAll('.admin-only').forEach(el => el.classList.add('admin-visible'));
            document.getElementById('btn-auth').style.display = 'none';
        }
    };

    window.updateUI = function() {
        document.getElementById('count-badge').textContent = database.length;
        document.getElementById('n-total').textContent = database.length;
        const tbody = document.getElementById('database-body');
        tbody.innerHTML = database.map(row => `
            <tr><td>${row.id}</td><td>${row.province || '-'}</td><td>${row.scoreSavoir}%</td><td>${row.scorePratique}%</td><td><button>👁️</button></td></tr>
        `).join('');
    };

    window.switchTab = function(i) {
        document.querySelectorAll('.form-content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    // Init codes
    const sel = document.getElementById('code-enquete');
    for(let i=1; i<=100; i++) { 
        let o = document.createElement('option'); 
        o.value = "RDC-"+i; o.text = "Fiche "+i; 
        sel.appendChild(o); 
    }
</script>
</body>
</html>
