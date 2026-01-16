<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Analyse Expert & Techniques de Palpation</title>
    <style>
        /* --- STYLE --- */
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1200px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); min-height: 800px;}
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        .btn-excel { margin-left: auto; background: #2e7d32; color: white; padding: 10px 20px; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .form-content { padding: 30px; display: none; }
        .form-content.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; width: 100%; box-sizing: border-box; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; }
        .btn-save { width: 100%; background: #b03060; color: white; padding: 20px; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 30px; }
        .stat-card { background: white; border: 1px solid #e0e0e0; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .bar-container { display: flex; align-items: center; margin-bottom: 8px; font-size: 12px; }
        .bar-label { width: 180px; }
        .bar-track { flex-grow: 1; background: #f0f0f0; height: 18px; border-radius: 4px; margin: 0 10px; overflow: hidden; }
        .bar-fill { height: 100%; color: white; display: flex; align-items: center; justify-content: center; font-size: 10px; }
        .counter-badge { background: #b03060; color: white; padding: 2px 8px; border-radius: 10px; font-size: 11px; margin-left: 5px;}
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <button class="tab active" onclick="switchTab(1)">1. COLLECTE <span id="count-badge" class="counter-badge">0</span></button>
        <button class="tab" onclick="switchTab(2)">2. MATRICE DE DONNÉES</button>
        <button class="tab" onclick="switchTab(3)">3. ANALYSE DES PRATIQUES</button>
        <button class="tab" onclick="switchTab(4)">4. SYNTHÈSE</button>
        <button type="button" class="btn-excel" onclick="exportToCSV()">📊 EXPORT CSV</button>
    </div>

    <div id="content-1" class="form-content active">
        <form id="kapForm">
            <div class="section-title">I. PROFIL DE L'ENQUÊTÉ(E)</div>
            <div class="row">
                <div class="field"><label>Code Enquêté</label><select id="code-enquete"></select></div>
                <div class="field"><label>Service</label><select id="service"><option>Gynécologie</option><option>Maternité</option><option>Chirurgie</option><option>Urgences</option></select></div>
                <div class="field"><label>Ancienneté</label><select id="exp-select"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES THÉORIQUES</div>
            <div class="row">
                <div class="field"><label>Période d'AES</label><select id="q-moment"><option>Pendant les règles</option><option selected>2 à 7 jours après les règles</option><option>N'importe quand</option></select></div>
                <div class="field"><label>Âge de début dépistage</label><select id="q-age"><option>40 ans</option><option selected>20-25 ans</option><option>60 ans</option></select></div>
            </div>

            <div class="section-title">III. ATTITUDES</div>
            <table>
                <thead><tr><th class="text-left">Énoncé</th><th>Accord</th><th>Neutre</th><th>Désaccord</th></tr></thead>
                <tbody>
                    <tr><td class="text-left">La prévention peut sauver des vies à l'HGRM.</td><td><input type="radio" name="att1" value="1" checked></td><td><input type="radio" name="att1" value="2"></td><td><input type="radio" name="att1" value="3"></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES (TECHNIQUES DE PALPATION)</div>
            <div class="row">
                <div class="field">
                    <label>Quelle technique de palpation appliquez-vous ?</label>
                    <select id="prac-methode">
                        <option value="1">1. Palpation rapide sans méthode précise</option>
                        <option value="2">2. Méthode systématique (Quadrant par quadrant)</option>
                        <option value="3" selected>3. Méthode complète (Quadrant + creux axillaire + mamelon)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Fréquence de réalisation</label>
                    <select id="prac-freq">
                        <option>Systématique</option>
                        <option>Si plainte</option>
                        <option>Rarement</option>
                    </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveRecord()">💾 ENREGISTRER LA FICHE</button>
        </form>
    </div>

    <div id="content-2" class="form-content">
        <div class="section-title">MATRICE DE DÉPOUILLEMENT</div>
        <table>
            <thead>
                <tr>
                    <th>Code</th>
                    <th>Service</th>
                    <th>Technique Utilisée</th>
                    <th>Score Pratique (%)</th>
                </tr>
            </thead>
            <tbody id="db-body"></tbody>
        </table>
    </div>

    <div id="content-3" class="form-content">
        <div class="section-title">ANALYSE DE LA QUALITÉ DES TECHNIQUES</div>
        <div class="stat-card">
            <div id="graph-prac"></div>
        </div>
        <div id="interpret-box" style="padding:15px; background:#f0f7ff; border-radius:8px; border-left: 5px solid #007bff;"></div>
    </div>

    <div id="content-4" class="form-content">
        <div class="section-title">CONCLUSION DU MÉMOIRE</div>
        <div id="conclusion-text" style="line-height: 1.6;"></div>
    </div>
</div>

<script>
    let db = [];
    const codeS = document.getElementById('code-enquete');
    for(let i=1; i<=100; i++) { let o = document.createElement('option'); o.value="E-"+i; o.text="Fiche n° "+i; codeS.appendChild(o); }
    const expS = document.getElementById('exp-select');
    for(let i=0; i<=40; i++) { let o = document.createElement('option'); o.value=i; o.text=i+" ans"; expS.appendChild(o); }

    function saveRecord() {
        let methodeVal = document.getElementById('prac-methode').value;
        let methodeText = document.getElementById('prac-methode').options[document.getElementById('prac-methode').selectedIndex].text;
        
        let rec = {
            id: document.getElementById('code-enquete').value,
            service: document.getElementById('service').value,
            methodeId: methodeVal,
            methodeLabel: methodeText,
            scorePratique: (methodeVal == "3") ? 100 : (methodeVal == "2" ? 60 : 30)
        };

        db.push(rec);
        document.getElementById('count-badge').textContent = db.length;
        codeS.selectedIndex++;
        updateUI();
        alert("Fiche ajoutée !");
    }

    function updateUI() {
        const tbody = document.getElementById('db-body');
        tbody.innerHTML = '';
        db.forEach(r => {
            tbody.innerHTML += `<tr>
                <td>${r.id}</td><td>${r.service}</td>
                <td>${r.methodeLabel}</td>
                <td style="font-weight:bold; color:${r.scorePratique == 100 ? 'green':'orange'}">${r.scorePratique}%</td>
            </tr>`;
        });

        // Calcul stats
        let m3 = db.filter(r => r.methodeId == "3").length;
        let m2 = db.filter(r => r.methodeId == "2").length;
        let m1 = db.filter(r => r.methodeId == "1").length;
        
        let total = db.length;
        document.getElementById('graph-prac').innerHTML = `
            <strong>Répartition des techniques de palpation (N=${total})</strong><br><br>
            ${renderBar("Complète (Q+A+M)", m3, total, "green")}
            ${renderBar("Systématique (Q)", m2, total, "orange")}
            ${renderBar("Rapide / Sans méthode", m1, total, "red")}
        `;

        document.getElementById('interpret-box').innerHTML = `
            <strong>Interprétation :</strong><br>
            ${(m3/total*100).toFixed(1)}% des infirmières pratiquent la <strong>méthode complète</strong>. 
            Le reste (${((m2+m1)/total*100).toFixed(1)}%) utilise une technique incomplète, ce qui représente un risque de non-détection des nodules axillaires.
        `;

        document.getElementById('conclusion-text').innerHTML = `
            <p>L'étude menée à l'HGRM démontre une disparité dans les techniques de palpation.</p>
            <p><strong>Recommandation :</strong> Standardiser la <em>Méthode Complète (Quadrant + creux axillaire + mamelon)</em> via des sessions de formation continue pour garantir un dépistage efficace.</p>
        `;
    }

    function renderBar(label, val, total, color) {
        let pct = total > 0 ? Math.round(val/total*100) : 0;
        return `<div class="bar-container">
            <div class="bar-label">${label}</div>
            <div class="bar-track"><div class="bar-fill" style="width:${pct}%; background:${color};">${pct}%</div></div>
            <div style="width:30px">${val}</div>
        </div>`;
    }

    function switchTab(i) {
        document.querySelectorAll('.form-content, .tab').forEach(e => e.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelector(`.header-tabs button:nth-child(${i})`).classList.add('active');
    }

    function exportToCSV() {
        let csv = "ID,Service,Technique,Score\n";
        db.forEach(r => csv += `${r.id},${r.service},"${r.methodeLabel}",${r.scorePratique}\n`);
        let link = document.createElement("a");
        link.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
        link.download = "resultats_palpation.csv";
        link.click();
    }
</script>

</body>
</html>
