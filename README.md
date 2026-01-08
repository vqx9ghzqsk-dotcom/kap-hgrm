<script>
// ================== CONFIGURATION ==================
const ADMIN_CODE = "HGRM_KAP_2025"; // change ce code
const KEY = "KAP_HGRM_DATA";
let db = JSON.parse(localStorage.getItem(KEY)) || [];

// ================== ENREGISTREMENT ==================
document.getElementById("kapForm").addEventListener("submit", e => {
    e.preventDefault();
    const f = new FormData(e.target);
    const obj = Object.fromEntries(f.entries());

    // population contrôlée : infirmières (femmes)
    obj.sexe = "Femme";

    obj.id = "HGRM_" + Date.now();
    obj.dateSave = new Date().toLocaleString("fr-FR");

    // obstacles multiples
    obj.obstacles = Array.from(
        e.target.querySelectorAll('input[name="obs"]:checked')
    ).map(o=>o.value).join("|");

    db.push(obj);
    localStorage.setItem(KEY, JSON.stringify(db));

    alert("Données enregistrées avec succès");
    e.target.reset();
});

// ================== ACCÈS ANALYSE (ADMIN) ==================
function accederAnalyse(){
    const code = prompt("Code administrateur");
    if(code !== ADMIN_CODE) return alert("Accès refusé");
    analyserDonnees();
    document.getElementById("analyse").style.display = "block";
}

// ================== ANALYSE AUTOMATIQUE ==================
function analyserDonnees(){
    let total = db.length;
    if(total === 0) return alert("Aucune donnée");

    let autoExam = {Oui:0, Non:0};
    let formation = {Oui:0, Non:0};

    db.forEach(e=>{
        autoExam[e.p1] = (autoExam[e.p1]||0)+1;
        formation[e.formation] = (formation[e.formation]||0)+1;
    });

    document.getElementById("resultats").innerHTML = `
        <h3>Analyse descriptive</h3>
        <p><strong>Effectif :</strong> ${total}</p>

        <h4>Auto-examen des seins</h4>
        Oui : ${autoExam.Oui||0} (${((autoExam.Oui||0)/total*100).toFixed(1)}%)<br>
        Non : ${autoExam.Non||0} (${((autoExam.Non||0)/total*100).toFixed(1)}%)

        <h4>Formation reçue</h4>
        Oui : ${formation.Oui||0} (${((formation.Oui||0)/total*100).toFixed(1)}%)<br>
        Non : ${formation.Non||0} (${((formation.Non||0)/total*100).toFixed(1)}%)

        <p><em>Analyses Chi² et corrélations réalisées via SPSS / Excel après export.</em></p>
    `;
}

// ================== EXPORT SPSS / EXCEL ==================
function exportCSV(){
    if(db.length === 0) return alert("Aucune donnée");

    let csv = "\uFEFF";
    csv += Object.keys(db[0]).join(",") + "\n";

    db.forEach(e=>{
        csv += Object.values(e).map(v=>`"${v||""}"`).join(",") + "\n";
    });

    const blob = new Blob([csv], {type:"text/csv;charset=utf-8"});
    const a = document.createElement("a");
    a.href = URL.createObjectURL(blob);
    a.download = "KAP_HGRM_ANALYSE.csv";
    a.click();
}
</script>
<button onclick="accederAnalyse()">📊 ANALYSE DES DONNÉES</button>

<div id="analyse" style="display:none;">
    <h2>Analyse statistique</h2>
    <div id="resultats"></div>

    <button onclick="exportCSV()">📁 Export SPSS / Excel</button>
</div>
