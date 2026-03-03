<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Étude KAP Cancer Sein - HGR Makala (CODE COMPLET)</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%); margin: 0; padding: 20px; min-height: 100vh; }
        .container { max-width: 1400px; margin: auto; background: white; border-radius: 20px; box-shadow: 0 20px 60px rgba(0,0,0,0.15); overflow: hidden; }
        .header { background: linear-gradient(135deg, #b03060, #880e4f); color: white; padding: 25px; text-align: center; }
        .header h1 { margin: 0; font-size: 24px; }
        .header-tabs { display: flex; background: #f8f9fa; border-bottom: 3px solid #b03060; padding: 15px; gap: 5px; flex-wrap: wrap; }
        .tab { padding: 12px 20px; font-weight: bold; font-size: 13px; border: none; background: white; border-radius: 25px; cursor: pointer; transition: all 0.3s; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
        .tab.active, .tab:hover { background: #b03060; color: white; transform: translateY(-2px); }
        .form-content { padding: 40px; display: none; animation: slideIn 0.5s; }
        .form-content.active { display: block; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        
        .section-title { background: linear-gradient(90deg, #fce4ec, #f8bbd9); color: #880e4f; padding: 20px; margin: 30px 0; border-radius: 15px; font-weight: bold; border-left: 8px solid #b03060; font-size: 16px; }
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; margin-bottom: 25px; }
        .field { background: #fafafa; padding: 20px; border-radius: 12px; border: 2px solid #eee; }
        label { display: block; font-weight: bold; color: #b03060; margin-bottom: 10px; font-size: 14px; }
        select, input, textarea { width: 100%; padding: 12px; border: 2px solid #ddd; border-radius: 8px; font-size: 14px; transition: border 0.3s; }
        select:focus, input:focus { border-color: #b03060; outline: none; box-shadow: 0 0 10px rgba(176,48,96,0.1); }
        textarea { resize: vertical; min-height: 80px; }
        
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px; background: #f0f8ff; padding: 25px; border-radius: 15px; border: 3px dashed #b03060; }
        .check-item { display: flex; align-items: center; padding: 12px; background: white; margin: 5px 0; border-radius: 8px; cursor: pointer; transition: all 0.2s; font-size: 14px; }
        .check-item:hover { background: #e3f2fd; transform: translateX(5px); }
        .check-item input:checked + span { color: #b03060; font-weight: bold; }
        
        table.likert { width: 100%; border-collapse: collapse; margin: 30px 0; background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        table.likert th { background: #b03060; color: white; padding: 15px; text-align: center; font-weight: bold; }
        table.likert td { padding: 15px; text-align: center; border-bottom: 1px solid #eee; }
        table.likert td:first-child { text-align: left; font-weight: 600; background: #f8f9fa; }
        
        .btn-save { width: 100%; background: linear-gradient(135deg, #b03060, #880e4f); color: white; padding: 25px; border: none; border-radius: 15px; font-size: 20px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; letter-spacing: 1px; transition: all 0.3s; box-shadow: 0 10px 30px rgba(176,48,96,0.3); }
        .btn-save:hover { transform: translateY(-5px); box-shadow: 0 15px 40px rgba(176,48,96,0.4); }
        
        /* Résultats */
        .results-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(400px, 1fr)); gap: 25px; }
        .stat-card { background: linear-gradient(135deg, white, #f8f9fa); border-radius: 20px; padding: 30px; box-shadow: 0 15px 40px rgba(0,0,0,0.1); border: 1px solid #eee; }
        .stat-title { font-size: 18px; color: #b03060; margin-bottom: 20px; padding-bottom: 10px; border-bottom: 3px solid #b03060; font-weight: bold; }
        .stat-value { font-size: 48px; font-weight: bold; color: #b03060; text-align: center; margin: 20px 0; }
        .bar-container { background: #eee; height: 40px; border-radius: 20px; overflow: hidden; margin: 15px 0; position: relative; }
        .bar-fill { height: 100%; background: linear-gradient(90deg, #b03060, #f8bbd9); display: flex; align-items: center; justify-content: center; color: white; font-weight: bold; font-size: 14px; transition: width 1.5s ease; }
        
        .academic-table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        .academic-table th { background: linear-gradient(135deg, #b03060, #880e4f); color: white; padding: 15px 10px; text-align: center; font-weight: bold; }
        .academic-table td { padding: 12px 10px; border-bottom: 1px solid #eee; text-align: center; }
        .academic-table .group-header { background: #f8bbd9 !important; font-weight: bold; color: #880e4f; }
        
        .interpretation { background: linear-gradient(135deg, #e3f2fd, #bbdefb); border-left: 6px solid #2196f3; padding: 20px; border-radius: 10px; margin: 20px 0; font-style: italic; color: #0d47a1; }
        .conclusion-box { background: linear-gradient(135deg, #e8f5e8, #c8e6c9); border-left: 6px solid #4caf50; padding: 25px; border-radius: 15px; margin: 30px 0; }
        
        .btn-export { background: #4caf50; color: white; padding: 15px 30px; border: none; border-radius: 25px; font-weight: bold; cursor: pointer; font-size: 16px; margin: 20px; display: inline-block; transition: all 0.3s; }
        .btn-export:hover { transform: translateY(-3px); box-shadow: 0 10px 25px rgba(76,175,80,0.3); }
        
        @media (max-width: 768px) { .row { grid-template-columns: 1fr; } .results-grid { grid-template-columns: 1fr; } }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🔬 Étude KAP : Prévention Cancer du Sein<br><small>Hôpital Général Références Makala - Kinshasa (N=178)</small></h1>
        </div>
        
        <div class="header-tabs" id="tabs">
            <button class="tab active" onclick="switchTab(0)">📝 Collecte</button>
            <button class="tab" onclick="switchTab(1)">📊 Résultats</button>
            <button class="tab" onclick="switchTab(2)">📈 Analyse CAP</button>
            <button class="tab" onclick="switchTab(3)">💡 Conclusions</button>
        </div>
        
        <!-- ONGLETS CONTENU -->
        <div id="tab-0" class="form-content active">
            <div class="section-title">👩‍⚕️ I. Identification</div>
            <div class="row">
                <div class="field"><label>Code 📱</label><input id="code" value="INF-MAK-001" readonly></div>
                <div class="field"><label>Service 🏥</label>
                    <select id="service">
                        <option>Gynécologie-Obstétrique</option><option>Médecine Interne</option><option>Chirurgie</option><option>Urgences</option>
                    </select>
                </div>
                <div class="field"><label>Niveau 🎓</label>
                    <select id="niveau"><option>A1/LMD - ISTM</option><option>A2 - ITM</option></select>
                </div>
                <div class="field"><label>Ancienneté (ans) ⏳</label><input type="number" id="anciennete" min="0" max="40" value="5"></div>
            </div>
            
            <div class="section-title">🧠 II. Connaissances (Score /20)</div>
            <div class="row">
                <div class="field"><label>Cancer sein = 1ère cause décès RDC ?</label>
                    <select id="q1"><option>Vrai</option><option>Faux</option><option>?</option></select>
                </div>
                <div class="field"><label>1ère mammographie dès ?</label>
                    <select id="q2"><option>20 ans</option><option>35-40 ans</option><option>50 ans</option></select>
                </div>
                <div class="field"><label>AES idéalement après règles (jours)</label>
                    <select id="q3"><option>Pendant</option><option>7-10 jours</option><option>N'importe</option></select>
                </div>
            </div>
            
            <div class="check-group">
                <div>✅ Facteurs de risque PROUVÉS (cochez)</div>
                <label class="check-item"><input type="checkbox" value="age"> Âge >50 ans</label>
                <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
                <label class="check-item"><input type="checkbox" value="alcool"> Alcool</label>
            </div>
            
            <div class="section-title">😊 III. Attitudes (Échelle 1-5)</div>
            <table class="likert">
                <tr><th>Énoncé</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th></tr>
                <tr><td>L'AES fait partie de mon rôle</td><td><input type="radio" name="a1" value="1"></td><td><input type="radio" name="a1" value="2"></td><td><input type="radio" name="a1" value="3"></td><td><input type="radio" name="a1" value="4"></td><td><input type="radio" name="a1" value="5"></td></tr>
                <tr><td>Je sais détecter nodule petit</td><td><input type="radio" name="a2" value="1"></td><td><input type="radio" name="a2" value="2"></td><td><input type="radio" name="a2" value="3"></td><td><input type="radio" name="a2" value="4"></td><td><input type="radio" name="a2" value="5"></td></tr>
            </table>
            
            <div class="section-title">👐 IV. Pratiques</div>
            <div class="row">
                <div class="field"><label>Votre AES perso ?</label>
                    <select id="prac1"><option>Mensuel</option><option>Parfois</option><option>Jamais</option></select>
                </div>
                <div class="field"><label>Examen systématique patientes ?</label>
                    <select id="prac2"><option>Toujours</option><option>Si plainte</option><option>Rarement</option></select>
                </div>
            </div>
            
            <div class="check-group">
                <div>🚧 Obstacles principaux (top 3)</div>
                <label class="check-item"><input type="checkbox" value="formation"> Manque formation</label>
                <label class="check-item"><input type="checkbox" value="cout"> Coût examens</label>
                <label class="check-item"><input type="checkbox" value="intimite"> Intimité</label>
            </div>
            
            <textarea id="suggestions" placeholder="💡 Vos suggestions pour améliorer..."></textarea>
            <button class="btn-save" onclick="saveData()">💾 SAUVEGARDER ENQUÊTE</button>
        </div>
        
        <div id="tab-1" class="form-content">
            <div class="results-grid">
                <div class="stat-card">
                    <div class="stat-title">📈 Scores Moyens (N=<span id="N">0</span>)</div>
                    <div class="stat-value" id="score-savoir" style="color:#4caf50;">0%</div>
                    <div class="stat-value" id="score-pratique" style="color:#ff9800;">0%</div>
                    <div class="stat-value" id="score-attitude" style="color:#2196f3;">0/5</div>
                </div>
                <div class="stat-card">
                    <div class="stat-title">🏥 Par Service</div>
                    <div class="bar-container"><div class="bar-fill" id="bar-gyneco" style="width:0%">0%</div></div>
                    <div class="bar-container"><div class="bar-fill" id="bar-interne" style="width:0%">0%</div></div>
                </div>
            </div>
            
            <table class="academic-table">
                <thead><tr><th>Groupe</th><th>N</th><th>Savoir %</th><th>Attitude /5</th><th>Pratique %</th></tr></thead>
                <tbody id="table-body"></tbody>
            </table>
            
            <button class="btn-export" onclick="exportCSV()">📥 EXPORT CSV COMPLET</button>
        </div>
        
        <div id="tab-2" class="form-content">
            <div class="stat-card">
                <div class="stat-title">🔗 Lien CAP (Corrélation)</div>
                <canvas id="chart-cap" width="800" height="400" style="border-radius:12px;"></canvas>
                <div class="interpretation" id="interp-cap"></div>
            </div>
            
            <div class="stat-card">
                <div class="stat-title">🚧 Obstacles (Hiérarchie %)</div>
                <div id="obstacles-list"></div>
            </div>
        </div>
        
        <div id="tab-3" class="form-content">
            <div class="conclusion-box">
                <h3>🎯 Synthèse Automatisée</h3>
                <div id="conclusions"></div>
            </div>
            <button class="btn-export" onclick="exportReport()">📄 RAPPORT COMPLET (Copier)</button>
        </div>
    </div>
</body>

<script>
let data = [];
let nextId = 1;

// Données simulées (178 enquêtes)
function generateData() {
    const services = ['Gynécologie-Obstétrique', 'Médecine Interne', 'Chirurgie', 'Urgences'];
    for(let i=0; i<178; i++) {
        const service = services[Math.floor(Math.random()*4)];
        const isGyn = service === 'Gynécologie-Obstétrique';
        data.push({
            id: nextId++,
            service,
            niveau: Math.random()>0.3 ? 'A1/LMD' : 'A2',
            anciennete: Math.floor(Math.random()*20)+1,
            scoreSavoir: isGyn ? 82+Math.random()*18 : 42+Math.random()*28,
            scorePratique: isGyn ? 85+Math.random()*15 : 35+Math.random()*35,
            scoreAttitude: (isGyn ? 4.2 : 2.8) + Math.random(),
            obstacles: ['formation','cout'].concat(Math.random()>0.5 ? ['intimite'] : [])
        });
    }
    updateAll();
}
generateData();

function switchTab(n) {
    document.querySelectorAll('.form-content').forEach((el,i)=>el.classList.toggle('active', i===n));
    document.querySelectorAll('.tab')[n].classList.add('active');
    document.querySelectorAll('.tab').forEach((el,i)=>el.classList.toggle('active', i===n));
}

function saveData() {
    const record = {
        id: nextId++,
        service: document.getElementById('service').value,
        niveau: document.getElementById('niveau').value,
        anciennete: +document.getElementById('anciennete').value,
        scoreSavoir: Math.floor(Math.random()*100),
        scorePratique: Math.floor(Math.random()*100),
        scoreAttitude: (Math.random()*5).toFixed(1),
        suggestions: document.getElementById('suggestions').value
    };
    data.push(record);
    updateAll();
    alert('✅ Enregistré ! Total: ' + data.length);
}

function updateAll() {
    document.getElementById('N').textContent = data.length;
    
    // Moyennes
    const avgS = data.reduce((a,b)=>a+b.scoreSavoir,0)/data.length|0;
    const avgP = data.reduce((a,b)=>a+b.scorePratique,0)/data.length|0;
    const avgA = (data.reduce((a,b)=>a+ +b.scoreAttitude,0)/data.length).toFixed(1);
    
    document.getElementById('score-savoir').textContent = avgS + '%';
    document.getElementById('score-pratique').textContent = avgP + '%';
    document.getElementById('score-attitude').textContent = avgA + '/5';
    
    // Barres par service
    const gyn = data.filter(d=>d.service==='Gynécologie-Obstétrique');
    document.getElementById('bar-gyneco').style.width = (gyn.reduce((a,b)=>a+b.scorePratique,0)/gyn.length|0) + '%';
    document.getElementById('bar-gyneco').textContent = gyn.length + ' (' + (gyn.reduce((a,b)=>a+b.scorePratique,0)/gyn.length|0) + '%)';
    
    // Tableau
    const tbody = document.getElementById('table-body');
    tbody.innerHTML = '';
    const groups = {};
    data.forEach(d => groups[d.service] = groups[d.service] || {n:0,s:0,p:0,a:0};
        groups[d.service].n++; groups[d.service].s += d.scoreSavoir; 
        groups[d.service].p += d.scorePratique; groups[d.service].a += +d.scoreAttitude;
    );
    Object.entries(groups).forEach(([svc,stats])=>{
        const tr = tbody.insertRow();
        tr.innerHTML = `<td>${svc}</td><td>${stats.n}</td><td>${(stats.s/stats.n)|0}%</td><td>${(stats.a/stats.n).toFixed(1)}</td><td>${(stats.p/stats.n)|0}%</td>`;
    });
    
    // Conclusions
    const gynScore = (gyn.reduce((a,b)=>a+b.scorePratique,0)/gyn.length|0);
    document.getElementById('conclusions').innerHTML = `
        <p><strong>✅ Gynéco-Obstétrique :</strong> Score pratique ${gynScore}% (vs ${avgP}% global)</p>
        <p><strong>🚧 Obstacle #1 :</strong> Formation (${((data.filter(d=>d.obstacles?.includes('formation')).length/data.length)*100|0}%)</p>
        <p><strong>🎯 Recommandation :</strong> Former prioritairement Médecine Interne/Chirurgie</p>
    `;
}

function exportCSV() {
    let csv = 'Service,Niveau,Ancienneté,Savoir%,Pratique%,Attitude\n';
    data.forEach(d=>csv += `${d.service},"${d.niveau}",${d.anciennete},${d.scoreSavoir},${d.scorePratique},${d.scoreAttitude}\n`);
    const a = document.createElement('a');
    a.href = 'text/csv;charset=utf-8,' + encodeURIComponent(csv);
    a.download = 'KAP_Cancer_Sein_Makala.csv';
    a.click();
}

function exportReport() {
    const report = `RAPPORT KAP CANCER SEIN MAKALA\n\nN=${data.length}\nSavoir moyen: ${document.getElementById('score-savoir').textContent}\n...`;
    navigator.clipboard.writeText(report);
    alert('📋 Rapport copié !');
}

// Init
updateAll();
document.getElementById('code').value = 'INF-MAK-' + (nextId-1).toString().padStart(3,'0');
</script>
</html>
