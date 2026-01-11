<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-HGRM Expert v3</title>
<style>
    body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4f7f9; color: #333; line-height: 1.6; margin: 0; padding: 10px; }
    .container { max-width: 1100px; margin: auto; background: #fff; border-radius: 12px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
    .header-tabs { display: flex; background: #b03060; padding: 10px; border-radius: 12px 12px 0 0; gap: 10px; overflow-x: auto; }
    .tab { padding: 12px 20px; color: #fff; font-weight: bold; cursor: pointer; border-radius: 8px; border: 1px solid rgba(255,255,255,0.3); white-space: nowrap; }
    .tab.active { background: #fff; color: #b03060; }
    .section-content { padding: 30px; display: none; }
    .section-content.active { display: block; }
    .section-title { color: #b03060; border-bottom: 2px solid #fce4ec; padding-bottom: 10px; margin: 30px 0 20px 0; text-transform: uppercase; font-size: 16px; display: flex; align-items: center; gap: 10px; }
    .question-block { margin-bottom: 25px; padding: 15px; border-radius: 8px; background: #fafafa; border: 1px solid #eee; }
    .question-label { font-weight: 700; display: block; margin-bottom: 15px; color: #111; }
    .options-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 12px; }
    .option-item { display: flex; align-items: center; gap: 12px; background: #fff; padding: 12px; border: 1px solid #ddd; border-radius: 6px; cursor: pointer; transition: 0.2s; }
    .option-item:hover { border-color: #b03060; background: #fff9fb; }
    .option-item input { transform: scale(1.2); }
    .btn-submit { width: 100%; padding: 20px; background: #b03060; color: #fff; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 20px; }
    .admin-only { display: none !important; }
    textarea { width: 100%; padding: 15px; border-radius: 8px; border: 1px solid #ddd; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="switchTab(1)">1. COLLECTE</div>
        <div class="tab admin-only" onclick="switchTab(2)">2. BASE DE DONNÉES</div>
        <div class="tab admin-only" onclick="switchTab(3)">3. ANALYSE STATISTIQUE</div>
    </div>

    <div id="tab1" class="section-content active">
        <form id="mainForm">
            
            <div class="section-title">I. Identification & Consentement</div>
            <div class="options-grid">
                <div class="question-block">
                    <label class="question-label">Niveau d'Étude Professionnel</label>
                    <select name="niveau" style="width:100%; padding:10px;" required>
                        <option value="">Sélectionner...</option>
                        <option value="A1">Infirmier Gradué (A1)</option>
                        <option value="A0">Infirmier Licencié (A0)</option>
                        <option value="Doc">Médecin Généraliste / Spécialiste</option>
                    </select>
                </div>
                <div class="question-block">
                    <label class="question-label">Ancienneté dans le métier</label>
                    <select name="anciennete" id="select-exp" style="width:100%; padding:10px;"></select>
                </div>
            </div>
            <div class="option-item" style="border: 2px solid #b03060;">
                <input type="checkbox" required name="consent">
                <span>Je confirme mon consentement libre et éclairé pour cette étude.</span>
            </div>

            <div class="section-title">II. Évaluation des Connaissances</div>
            
            <div class="question-block">
                <span class="question-label">1. Quel est l'examen de référence (Gold Standard) pour le dépistage du cancer du sein chez une femme de plus de 40 ans ?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="k_ref" value="0"> L'échographie mammaire simple</label>
                    <label class="option-item"><input type="radio" name="k_ref" value="0"> La ponction à l'aiguille fine</label>
                    <label class="option-item"><input type="radio" name="k_ref" value="2"> La mammographie bilatérale</label>
                    <label class="option-item"><input type="radio" name="k_ref" value="0"> L'IRM mammaire systématique</label>
                </div>
            </div>

            <div class="question-block">
                <span class="question-label">2. Quels sont les signes évocateurs d'un cancer du sein ? (Choisir la réponse la plus complète)</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="k_signe" value="0"> Une douleur mammaire bilatérale pendant les règles</label>
                    <label class="option-item"><input type="radio" name="k_signe" value="1"> Un écoulement de lait chez une femme allaitante</label>
                    <label class="option-item"><input type="radio" name="k_signe" value="2"> Un nodule dur, fixe, indolore avec rétraction cutanée</label>
                    <label class="option-item"><input type="radio" name="k_signe" value="0"> Une augmentation globale du volume des deux seins</label>
                </div>
            </div>
            

            <div class="section-title">III. Attitudes vis-à-vis du dépistage</div>
            
            <div class="question-block">
                <span class="question-label">3. Selon votre conviction, quelle est la cause réelle du cancer du sein ?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="at_cause" value="0"> Une punition divine ou un mauvais sort</label>
                    <label class="option-item"><input type="radio" name="at_cause" value="1"> Un choc ou un coup reçu sur le sein par mégarde</label>
                    <label class="option-item"><input type="radio" name="at_cause" value="2"> Une mutation génétique et des facteurs environnementaux</label>
                    <label class="option-item"><input type="radio" name="at_cause" value="0"> Une mauvaise hygiène de vie uniquement</label>
                </div>
            </div>

            <div class="question-block">
                <span class="question-label">4. Que pensez-vous du pronostic vital d'une femme diagnostiquée au stade 1 à Kinshasa ?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="at_pro" value="0"> La mort est inévitable peu importe le stade</label>
                    <label class="option-item"><input type="radio" name="at_pro" value="1"> La guérison dépend surtout de la foi de la patiente</label>
                    <label class="option-item"><input type="radio" name="at_pro" value="2"> La guérison est très probable avec un traitement médical précoce</label>
                </div>
            </div>

            <div class="section-title">IV. Pratiques Professionnelles</div>
            
            <div class="question-block">
                <span class="question-label">5. À quelle fréquence pratiquez-vous l'examen physique des seins lors d'une consultation ?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="pr_freq" value="0"> Jamais (Ce n'est pas mon rôle)</label>
                    <label class="option-item"><input type="radio" name="pr_freq" value="1"> Seulement si la patiente se plaint d'une boule</label>
                    <label class="option-item"><input type="radio" name="pr_freq" value="2"> Systématiquement pour toute femme en âge de procréer</label>
                </div>
            </div>
            

            <div class="section-title">V. Obstacles au dépistage (Plusieurs choix possibles)</div>
            <div class="question-block">
                <span class="question-label">Quels sont les freins majeurs que vous rencontrez à l'HGRM ? (Cochez tout ce qui s'applique)</span>
                <div class="options-grid">
                    <label class="option-item"><input type="checkbox" name="obs" value="Formation"> Manque de formation continue sur le cancer</label>
                    <label class="option-item"><input type="checkbox" name="obs" value="Temps"> Surcharge de travail / manque de temps</label>
                    <label class="option-item"><input type="checkbox" name="obs" value="Intimite"> Absence de local isolé (respect de la pudeur)</label>
                    <label class="option-item"><input type="checkbox" name="obs" value="Cout"> Coût élevé des examens pour les patientes</label>
                    <label class="option-item"><input type="checkbox" name="obs" value="Culture"> Croyances culturelles et refus des patientes</label>
                    <label class="option-item"><input type="checkbox" name="obs" value="Plateau"> Absence de plateau technique (Mammographe absent)</label>
                </div>
            </div>

            <div class="section-title">VI. Recommandations</div>
            <textarea name="recom" rows="4" placeholder="Quelles solutions proposez-vous pour améliorer la situation à l'HGRM ?"></textarea>

            <button type="button" class="btn-submit" onclick="processData()">ENREGISTRER LA FICHE DE COLLECTE</button>
        </form>
    </div>

    <div id="tab2" class="section-content">
        <div class="section-title">Base de Données Cumulative</div>
        <div id="db-view"></div>
    </div>
</div>

<div style="position:fixed; bottom:10px; right:10px; opacity:0.2;">
    <input type="password" placeholder="PIN" oninput="if(this.value==='1398') document.querySelectorAll('.admin-only').forEach(e=>e.style.setProperty('display','block','important'))">
</div>

<script>
    let db = [];

    function switchTab(n) {
        document.querySelectorAll('.section-content, .tab').forEach(el => el.classList.remove('active'));
        document.getElementById('tab'+n).classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
    }

    function processData() {
        const form = document.getElementById('mainForm');
        if(!form.checkValidity()) { alert("Veuillez remplir les champs obligatoires et accepter le consentement."); return; }
        
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        
        // Récupérer les obstacles multiples
        data.obstacles = Array.from(document.querySelectorAll('input[name="obs"]:checked')).map(cb => cb.value);
        
        db.push(data);
        alert("Enregistré ! Total fiches : " + db.length);
        form.reset();
        refreshDB();
    }

    function refreshDB() {
        let html = `<table border="1" style="width:100%; border-collapse:collapse;">
            <tr style="background:#eee;"><th>Niveau</th><th>Savoir</th><th>Obstacles cités</th></tr>`;
        db.forEach(f => {
            html += `<tr>
                <td>${f.niveau}</td>
                <td>${f.k_ref == "2" ? "Correct" : "Incorrect"}</td>
                <td>${f.obstacles.join(', ')}</td>
            </tr>`;
        });
        document.getElementById('db-view').innerHTML = html + "</table>";
    }

    window.onload = () => {
        const exp = document.getElementById('select-exp');
        for(let i=0; i<=40; i++) exp.options.add(new Option(i + (i<2?" an":" ans"), i));
    };
</script>
</body>
</html>
