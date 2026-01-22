<div class="section-title">I. PROFIL SOCIODÉMOGRAPHIQUE</div>
<div class="row">
    <div class="field">
        <label>1. Code Enquêté(e)</label>
        <select id="code-enquete"></select> </div>
    <div class="field">
        <label style="color:#b03060;">2. Consentement</label>
        <select id="consentement">
            <option value="oui">Oui, accepte</option>
            <option value="non">Non</option>
        </select>
    </div>
    <div class="field">
        <label>3. [span_0](start_span)Province d'exercice[span_0](end_span)</label>
        <select id="province">
            <option value="Kinshasa" selected>Kinshasa</option>
            <option value="Kongo Central">Kongo Central</option>
            <option value="Haut Katanga">Haut Katanga</option>
            <option value="Autre">Autre</option>
        </select>
    </div>
</div>

<div class="row">
    <div class="field">
        <label>4. [span_1](start_span)Profession[span_1](end_span)</label>
        <select id="profession">
            <option value="" disabled selected>Choisir...</option>
            <option value="Generaliste">Médecin Généraliste</option>
            <option value="Specialiste">Spécialiste (Gynéco/Onco)</option>
            <option value="Interne">Résident / Interne</option>
            <option value="Autre">Autre (Infirmier, etc.)</option>
        </select>
    </div>
    <div class="field">
        <label>5. [span_2](start_span)Années de pratique[span_2](end_span)</label>
        <input type="number" id="anciennete" min="0" placeholder="Ex: 5">
    </div>
    <div class="field">
        <label>6. [span_3](start_span)Etablissement[span_3](end_span)</label>
        <select id="etablissement">
            <option value="Hôpital Universitaire">Hôpital Universitaire</option>
            <option value="HGR">Hôpital Général de Réf.</option>
            <option value="Privé">Clinique Privée</option>
            <option value="CS">Centre de Santé</option>
        </select>
    </div>
</div>

<div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN</div>

<div class="sub-title">A. Classification & Biologie (Niveau Expert)</div>
<div class="row">
    <div class="field">
        [span_4](start_span)<label>Classification moléculaire connue ?[span_4](end_span)</label>
        <select id="q-moleculaire">
            <option value="non">Non</option>
            <option value="oui">Oui</option>
        </select>
    </div>
    <div class="field">
        [span_5](start_span)<label>Entendu parler du "HER2 Low" ?[span_5](end_span)</label>
        <select id="q-her2">
            <option value="non">Non</option>
            <option value="oui">Oui</option>
        </select>
    </div>
    <div class="field">
        [span_6](start_span)<label>Connaissance thérapies ciblées ?[span_6](end_span)</label>
        <select id="q-therapie">
            <option value="non">Non</option>
            <option value="oui">Oui</option>
        </select>
    </div>
</div>

<div class="sub-title">B. [span_7](start_span)Facteurs de Risque (Cochez les VRAIS)[span_7](end_span)</div>
<div class="check-group" id="group-risques">
    <label class="check-item"><input type="checkbox" value="age40"> Âge avancé (> 40 ans)</label>
    <label class="check-item"><input type="checkbox" value="famille"> Antécédent familial</label>
    <label class="check-item"><input type="checkbox" value="menarche"> Ménarche précoce (< 12 ans)</label>
    <label class="check-item"><input type="checkbox" value="menopause"> Ménopause tardive (> 55 ans)</label>
    <label class="check-item"><input type="checkbox" value="alcool"> Consommation d'alcool</label>
    <label class="check-item"><input type="checkbox" value="obesite"> Obésité (post-ménopause)</label>
</div>

<div class="sub-title">C. [span_8](start_span)[span_9](start_span)[span_10](start_span)Signes d'alerte & Dépistage[span_8](end_span)[span_9](end_span)[span_10](end_span)</div>
<div class="row">
    <div class="field">
        [span_11](start_span)<label>Âge début mammographie ?[span_11](end_span)</label>
        <select id="q-age-mammo">
            <option value="20">Dès 20 ans</option>
            <option value="40">À partir de 40 ans</option> <option value="50">À partir de 50 ans</option>
        </select>
    </div>
    <div class="field">
        [span_12](start_span)<label>Meilleur moment Auto-Palpation (APS) ?[span_12](end_span)</label>
        <select id="q-moment-aps">
            <option value="nimporte">N'importe quand</option>
            <option value="regles">Pendant les règles</option>
            <option value="apres">Une semaine après les règles</option> </select>
    </div>
</div>

[span_13](start_span)<label style="margin:10px 0; display:block; font-weight:bold; color:#b03060;">Signes cliniques suspects (Cochez) :[span_13](end_span)</label>
<div class="check-group" id="group-signes">
    <label class="check-item"><input type="checkbox" value="masse"> Masse mammaire indolore</label>
    <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
    <label class="check-item"><input type="checkbox" value="asymetrie"> Asymétrie / Modif. forme</label>
    <label class="check-item"><input type="checkbox" value="peau"> Peau d'orange / Ulcération</label>
    <label class="check-item"><input type="checkbox" value="axillaire"> Masse à l'aisselle (Ganglion)</label>
</div>

<div class="section-title">III. ATTITUDES & RECOMMANDATIONS</div>

<div class="row">
    <div class="field">
        [span_14](start_span)<label>Besoin de formation supplémentaire ?[span_14](end_span)</label>
        <select id="besoin-formation">
            <option value="oui">Oui</option>
            <option value="non">Non</option>
        </select>
    </div>
    <div class="field">
        [span_15](start_span)<label>Intéressé par registre national ?[span_15](end_span)</label>
        <select id="registre">
            <option value="oui">Oui</option>
            <option value="non">Non</option>
        </select>
    </div>
    <div class="field">
        [span_16](start_span)<label>Connaissez-vous le CNLC ?[span_16](end_span)</label>
        <select id="cnlc">
            <option value="non">Non</option>
            <option value="oui">Oui</option>
        </select>
    </div>
</div>

<div class="field">
    [span_17](start_span)<label>Recommandations prioritaires (Q44)[span_17](end_span)</label>
    <textarea id="reco-verbatim" rows="2" placeholder="Ex: Campagnes de sensibilisation, Gratuité des soins..."></textarea>
</div>

<button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>

