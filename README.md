<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KAP-Expert Cancer du Sein HGRM</title>
<style>
    body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 10px; }
    .container { max-width: 1250px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 5px 30px rgba(0,0,0,0.15); }
    .header-tabs { display: flex; background: #fff; border-bottom: 5px solid #b03060; padding: 15px; gap: 10px; position: sticky; top: 0; z-index: 1000; }
    .tab { padding: 12px 20px; font-weight: bold; font-size: 13px; border-radius: 6px; border: 1px solid #ddd; color: #555; background: #f9f9f9; cursor: pointer; }
    .tab.active { background: #b03060; color: white; border-color: #b03060; }
    .section-title { background: #fff0f5; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 14px; }
    .field { display: flex; flex-direction: column; margin-bottom: 25px; }
    label { font-size: 14px; font-weight: 800; margin-bottom: 12px; color: #1a1a1a; background: #fdfdfd; padding: 5px; border-bottom: 1px solid #eee; }
    select, input, textarea { padding: 14px; border: 2px solid #ddd; border-radius: 8px; font-size: 14px; transition: all 0.3s; }
    select:focus { border-color: #b03060; box-shadow: 0 0 8px rgba(176, 48, 96, 0.2); }
    .radio-group { display: flex; flex-direction: column; gap: 10px; padding-left: 10px; }
    .radio-item { display: flex; align-items: center; gap: 12px; cursor: pointer; padding: 8px; border-radius: 5px; transition: 0.2s; }
    .radio-item:hover { background: #fce4ec; }
    .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 10px; font-size: 20px; font-weight: bold; cursor: pointer; text-transform: uppercase; margin: 40px 0; }
    .admin-only { display: none !important; }
</style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active" onclick="showTab(1)">1. COLLECTE (QUESTIONNAIRE COMPLET)</div>
        <div class="tab admin-only" onclick="showTab(2)">2. BASE DE DONNÉES</div>
        <div class="tab admin-only" onclick="showTab(3)">3. ANALYSE COMPARATIVE</div>
        <button class="admin-only" onclick="exportExcel()" style="margin-left:auto; background:#2e7d32; color:white; border:none; padding:10px; border-radius:5px; cursor:pointer;">📥 EXPORTER EXCEL</button>
    </div>

    <div id="tab1" class="content-section active" style="padding: 30px;">
        <form id="kapForm">
            
            <div class="section-title">I. IDENTIFICATION ET DONNÉES SOCIO-DÉMOGRAPHIQUES</div>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;">
                <div class="field"><label>Code de l'Agent</label><input type="text" name="id_agent" required placeholder="Ex: INF-HGRM-01"></div>
                <div class="field"><label>Âge du soignant</label><select name="age" id="age-select"></select></div>
                <div class="field"><label>Niveau de formation</label>
                    <select name="niveau" required>
                        <option value="A1">Infirmier(e) Gradué(e) (A1)</option>
                        <option value="A0">Infirmier(e) Licencié(e) (A0)</option>
                        <option value="Doc">Médecin / Spécialiste</option>
                        <option value="Autre">Autre personnel soignant</option>
                    </select>
                </div>
                <div class="field"><label>Ancienneté à l'HGRM</label><select name="exp" id="exp-select"></select></div>
            </div>

            <div class="section-title">II. CONNAISSANCES APPROFONDIES (SAVOIR)</div>

            <div class="field">
                <label>1. Quelle est, selon vous, la prévalence du cancer du sein chez les femmes en RDC ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="k_prev" value="0"> C'est une maladie rare qui touche surtout les femmes occidentales</label>
                    <label class="radio-item"><input type="radio" name="k_prev" value="1"> C'est le 2ème cancer après celui du col de l'utérus</label>
                    <label class="radio-item"><input type="radio" name="k_prev" value="2"> C'est le 1er cancer en termes de fréquence et de mortalité féminine (Réponse experte)</label>
                    <label class="radio-item"><input type="radio" name="k_prev" value="0"> Je ne connais pas les statistiques actuelles</label>
                </div>
            </div>

            <div class="field">
                <label>2. À quel moment une femme doit-elle idéalement pratiquer son autopalpation ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="k_moment" value="0"> N'importe quand, cela n'a pas d'importance</label>
                    <label class="radio-item"><input type="radio" name="k_moment" value="1"> Pendant la période des règles (menstruations)</label>
                    <label class="radio-item"><input type="radio" name="k_moment" value="2"> 2 à 3 jours après la fin des règles (période de souplesse mammaire)</label>
                    <label class="radio-item"><input type="radio" name="k_moment" value="1"> Une fois par an seulement</label>
                </div>
            </div>

            <div class="field">
                <label>3. Lesquels de ces éléments sont des facteurs de risque réels ? (Plusieurs choix possibles)</label>
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; background: #f9f9f9; padding: 15px; border-radius: 8px;">
                    <label class="radio-item"><input type="checkbox" name="k_fr1"> Allaitement maternel prolongé (Facteur protecteur)</label>
                    <label class="radio-item"><input type="checkbox" name="k_fr2"> Première grossesse après 35 ans</label>
                    <label class="radio-item"><input type="checkbox" name="k_fr3"> Obésité et sédentarité après la ménopause</label>
                    <label class="radio-item"><input type="checkbox" name="k_fr4"> Port de soutiens-gorge trop serrés (Mythe)</label>
                    <label class="radio-item"><input type="checkbox" name="k_fr5"> Antécédent familial direct (Mère/Sœur)</label>
                </div>
            </div>

            

            <div class="field">
                <label>4. Quel est le signe clinique le plus précoce d'une tumeur maligne ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="k_signe" value="0"> Une douleur vive et soudaine au sein</label>
                    <label class="radio-item"><input type="radio" name="k_signe" value="2"> Un nodule indolore, dur, à contours irréguliers</label>
                    <label class="radio-item"><input type="radio" name="k_signe" value="1"> Un écoulement de lait chez une femme qui n'allaite pas</label>
                    <label class="radio-item"><input type="radio" name="k_signe" value="0"> Une rougeur sur toute la poitrine</label>
                </div>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (POSTURE)</div>

            <div class="field">
                <label>1. Face à une patiente de 45 ans sans symptômes, quelle est votre attitude ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="at_posture" value="0"> Je ne fais rien si elle ne se plaint pas</label>
                    <label class="radio-item"><input type="radio" name="at_posture" value="1"> Je lui conseille de revenir si elle sent quelque chose</label>
                    <label class="radio-item"><input type="radio" name="at_posture" value="2"> Je profite de la consultation pour faire un examen clinique des seins</label>
                    <label class="radio-item"><input type="radio" name="at_posture" value="2"> Je l'éduque systématiquement sur l'autopalpation</label>
                </div>
            </div>

            <div class="field">
                <label>2. Que pensez-vous de la mammographie à Kinshasa ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="at_mammo" value="0"> C'est un examen dangereux à cause des rayons</label>
                    <label class="radio-item"><input type="radio" name="at_mammo" value="1"> C'est trop cher, inutile de le proposer aux patientes pauvres</label>
                    <label class="radio-item"><input type="radio" name="at_mammo" value="2"> C'est l'examen clé que tout soignant devrait encourager malgré le coût</label>
                </div>
            </div>

            <div class="section-title">IV. PRATIQUES ET APTITUDES (ACTION)</div>

            <div class="field">
                <label>1. Comment effectuez-vous la palpation mammaire en pratique ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="p_tech" value="0"> Avec la main entière en pressant le sein</label>
                    <label class="radio-item"><input type="radio" name="p_tech" value="1"> Avec le bout de l'index uniquement</label>
                    <label class="radio-item"><input type="radio" name="p_tech" value="2"> Avec la pulpe des 3 doigts moyens, par mouvements circulaires</label>
                    <label class="radio-item"><input type="radio" name="p_tech" value="0"> Je délègue toujours cet examen au médecin</label>
                </div>
            </div>

            

            <div class="field">
                <label>2. Lors de l'examen, recherchez-vous les ganglions axillaires (sous l'aisselle) ?</label>
                <div class="radio-group">
                    <label class="radio-item"><input type="radio" name="p_gang" value="2"> Oui, systématiquement de chaque côté</label>
                    <label class="radio-item"><input type="radio" name="p_gang" value="1"> Seulement si je trouve une boule dans le sein</label>
                    <label class="radio-item"><input type="radio" name="p_gang" value="0"> Non, je ne savais pas que c'était lié</label>
                </div>
            </div>

            <div class="section-title">V. OBSTACLES ET RECOMMANDATIONS</div>
            <div class="field">
                <label>Quel est l'obstacle majeur qui vous empêche de dépister à l'HGRM ?</label>
                <select name="obstacle_principal">
                    <option value="formation">Mon manque de formation technique</option>
                    <option value="temps">La surcharge de travail (pas le temps)</option>
                    <option value="espace">Le manque d'intimité (pas de rideaux/paravents)</option>
                    <option value="culture">La pudeur des patientes qui refusent de se déshabiller</option>
                    <option value="materiel">L'absence de matériel de démonstration</option>
                </select>
            </div>

            <div class="field">
                <label>Suggestion libre pour améliorer le service :</label>
                <textarea name="reco_libre" rows="4" placeholder="Ex: Créer une unité mobile, baisser les prix des biopsies..."></textarea>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">ENREGISTRER LA FICHE D'EXPERTISE</button>
        </form>
    </div>

    <div id="tab2" class="content-section">
        <div class="section-title">DÉPOUILLEMENT EN TEMPS RÉEL</div>
        <div id="tableOut"></div>
    </div>
</div>

<div style="position:fixed; bottom:5px; right:5px; opacity:0.1;">
    <input type="password" oninput="if(this.value==='1398') document.querySelectorAll('.admin-only').forEach(e=>e.style.setProperty('display','block','important'))">
</div>

<script>
    let storage = [];
    function showTab(n) {
        document.querySelectorAll('.content-section, .tab').forEach(el => el.classList.remove('active'));
        document.querySelectorAll('.content-section')[n-1].classList.add('active');
        document.querySelectorAll('.tab')[n-1].classList.add('active');
    }

    function saveData() {
        const form = document.getElementById('kapForm');
        const fd = new FormData(form);
        const data = Object.fromEntries(fd.entries());
        
        // Calcul d'un score de compétence rapide
        let score = 0;
        if(data.k_prev === "2") score++;
        if(data.k_moment === "2") score++;
        if(data.k_signe === "2") score++;
        if(data.p_tech === "2") score++;
        
        data.scoreFinal = score;
        storage.push(data);
        
        alert("Fiche enregistrée avec succès !");
        form.reset();
        refreshTable();
    }

    function refreshTable() {
        let html = `<table border="1" style="width:100%; border-collapse:collapse;"><tr><th>ID Agent</th><th>Niveau</th><th>Score Savoir/Pratique</th></tr>`;
        storage.forEach(s => {
            html += `<tr><td>${s.id_agent}</td><td>${s.niveau}</td><td>${s.scoreFinal}/4</td></tr>`;
        });
        document.getElementById('tableOut').innerHTML = html + "</table>";
    }

    window.onload = () => {
        const as = document.getElementById('age-select');
        for(let i=20; i<=70; i++) as.options.add(new Option(i+" ans", i));
        const es = document.getElementById('exp-select');
        for(let i=0; i<=45; i++) es.options.add(new Option(i+" ans", i));
    };
</script>
</body>
</html>
