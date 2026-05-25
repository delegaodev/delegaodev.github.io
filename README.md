<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Generador de Papeleo — DA's Office San Andreas</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400;0,500;0,600;1,400&family=Courier+Prime:wght@400;700&family=Oswald:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --navy: #0a1628;
    --navy-mid: #152847;
    --gold: #c9a84c;
    --gold-light: #e8c97a;
    --cream: #f5f0e8;
    --paper: #faf7f2;
    --ink: #1a1a1a;
    --ink-mid: #3a3a3a;
    --ink-light: #6a6a6a;
    --rule: #c8c0b0;
    --red-seal: #8b1a1a;
    --border-accent: #2a4a7a;
    --field-bg: #fff;
    --field-border: #b0a898;
  }

  body {
    background: var(--navy);
    font-family: 'EB Garamond', Georgia, serif;
    color: var(--ink);
    min-height: 100vh;
    padding: 0;
  }

  /* ── HEADER ── */
  .site-header {
    background: var(--navy);
    border-bottom: 2px solid var(--gold);
    padding: 1.5rem 2rem;
    text-align: center;
  }
  .site-header .seal-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1.5rem;
    margin-bottom: 0.5rem;
  }
  .seal {
    width: 56px;
    height: 56px;
    border: 2px solid var(--gold);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Oswald', sans-serif;
    font-size: 9px;
    color: var(--gold);
    text-align: center;
    letter-spacing: 0.05em;
    line-height: 1.2;
  }
  .site-header h1 {
    font-family: 'Oswald', sans-serif;
    font-size: 1.4rem;
    font-weight: 600;
    color: var(--gold);
    letter-spacing: 0.12em;
    text-transform: uppercase;
  }
  .site-header p {
    font-family: 'EB Garamond', serif;
    font-style: italic;
    color: #8fa0c0;
    font-size: 0.95rem;
    margin-top: 0.2rem;
  }

  /* ── SELECTOR ── */
  .selector-section {
    background: var(--navy-mid);
    padding: 2rem;
    text-align: center;
    border-bottom: 1px solid rgba(201,168,76,0.3);
  }
  .selector-label {
    font-family: 'Oswald', sans-serif;
    font-size: 0.85rem;
    letter-spacing: 0.15em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 1rem;
  }
  .warrant-btns {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }
  .warrant-btn {
    font-family: 'Oswald', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.75rem 2rem;
    border: 1.5px solid var(--gold);
    background: transparent;
    color: var(--gold);
    cursor: pointer;
    transition: all 0.2s;
  }
  .warrant-btn:hover {
    background: rgba(201,168,76,0.12);
  }
  .warrant-btn.active {
    background: var(--gold);
    color: var(--navy);
  }

  /* ── MAIN LAYOUT ── */
  .main {
    display: flex;
    justify-content: center;
    padding: 2.5rem 1.5rem;
    gap: 2rem;
    align-items: flex-start;
  }

  /* ── FORM PANEL ── */
  .form-panel {
    background: var(--cream);
    border: 1px solid #b0a070;
    max-width: 540px;
    width: 100%;
    padding: 2rem;
  }
  .form-panel h2 {
    font-family: 'Oswald', sans-serif;
    font-size: 1rem;
    letter-spacing: 0.1em;
    color: var(--navy);
    text-transform: uppercase;
    border-bottom: 1.5px solid var(--navy);
    padding-bottom: 0.5rem;
    margin-bottom: 1.5rem;
  }
  .form-section {
    margin-bottom: 1.5rem;
  }
  .form-section-title {
    font-family: 'Oswald', sans-serif;
    font-size: 0.78rem;
    letter-spacing: 0.12em;
    color: var(--border-accent);
    text-transform: uppercase;
    margin-bottom: 0.75rem;
    padding-bottom: 0.3rem;
    border-bottom: 0.5px solid var(--rule);
  }
  .field-group {
    margin-bottom: 0.85rem;
  }
  label {
    display: block;
    font-size: 0.78rem;
    font-family: 'Oswald', sans-serif;
    letter-spacing: 0.06em;
    color: var(--ink-mid);
    text-transform: uppercase;
    margin-bottom: 0.3rem;
  }
  input[type="text"],
  input[type="date"],
  input[type="time"],
  textarea,
  select {
    width: 100%;
    padding: 0.5rem 0.7rem;
    border: 1px solid var(--field-border);
    background: var(--field-bg);
    font-family: 'EB Garamond', serif;
    font-size: 1rem;
    color: var(--ink);
    outline: none;
    transition: border-color 0.15s;
    border-radius: 0;
  }
  input:focus, textarea:focus, select:focus {
    border-color: var(--navy);
  }
  textarea {
    resize: vertical;
    min-height: 100px;
    line-height: 1.6;
  }
  .row-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.75rem;
  }

  .generate-btn {
    width: 100%;
    padding: 0.85rem;
    background: var(--navy);
    color: var(--gold);
    border: none;
    font-family: 'Oswald', sans-serif;
    font-size: 1rem;
    font-weight: 600;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    cursor: pointer;
    margin-top: 0.5rem;
    transition: background 0.2s;
  }
  .generate-btn:hover { background: var(--navy-mid); }

  /* ── PREVIEW PANEL ── */
  .preview-panel {
    max-width: 680px;
    width: 100%;
  }
  .preview-toolbar {
    display: flex;
    justify-content: flex-end;
    gap: 0.75rem;
    margin-bottom: 0.75rem;
  }
  .tool-btn {
    font-family: 'Oswald', sans-serif;
    font-size: 0.78rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.45rem 1rem;
    background: rgba(201,168,76,0.15);
    border: 1px solid var(--gold);
    color: var(--gold);
    cursor: pointer;
    transition: background 0.15s;
  }
  .tool-btn:hover { background: rgba(201,168,76,0.3); }

  /* ── DOCUMENT ── */
  #document {
    background: var(--paper);
    border: 1px solid #c8c0b0;
    padding: 3rem 3.5rem;
    font-family: 'EB Garamond', serif;
    font-size: 1rem;
    color: var(--ink);
    line-height: 1.7;
    box-shadow: 0 4px 24px rgba(0,0,0,0.35);
    position: relative;
  }
  #document::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 6px;
    background: linear-gradient(90deg, var(--navy) 0%, var(--border-accent) 50%, var(--navy) 100%);
  }

  .doc-header {
    text-align: center;
    margin-bottom: 1.5rem;
    padding-bottom: 1.5rem;
    border-bottom: 2px double var(--ink-mid);
  }
  .doc-agency {
    font-family: 'Oswald', sans-serif;
    font-size: 0.75rem;
    letter-spacing: 0.18em;
    color: var(--ink-mid);
    text-transform: uppercase;
  }
  .doc-state {
    font-family: 'Oswald', sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.14em;
    color: var(--ink-light);
    text-transform: uppercase;
    margin-top: 0.1rem;
  }
  .doc-title-en {
    font-family: 'Oswald', sans-serif;
    font-size: 1.7rem;
    font-weight: 600;
    letter-spacing: 0.14em;
    color: var(--navy);
    text-transform: uppercase;
    margin: 0.7rem 0 0.1rem;
  }
  .doc-title-es {
    font-family: 'EB Garamond', serif;
    font-style: italic;
    font-size: 1.1rem;
    color: var(--ink-mid);
    letter-spacing: 0.04em;
  }
  .doc-case-badge {
    display: inline-block;
    margin-top: 0.7rem;
    font-family: 'Courier Prime', monospace;
    font-size: 0.82rem;
    color: var(--ink-light);
    background: rgba(0,0,0,0.05);
    padding: 0.2rem 0.7rem;
    border: 0.5px solid var(--rule);
  }

  /* Roman numeral sections */
  .doc-section {
    margin-bottom: 1.4rem;
  }
  .doc-section-title {
    font-family: 'Oswald', sans-serif;
    font-size: 0.85rem;
    font-weight: 500;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--navy);
    border-bottom: 1px solid var(--rule);
    padding-bottom: 0.3rem;
    margin-bottom: 0.7rem;
  }
  .doc-field-row {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 0.35rem;
    font-size: 0.97rem;
  }
  .doc-field-label {
    font-weight: 600;
    min-width: 180px;
    color: var(--ink-mid);
    font-size: 0.92rem;
  }
  .doc-field-value {
    flex: 1;
    border-bottom: 0.5px solid var(--rule);
    padding-bottom: 0.1rem;
    color: var(--ink);
    min-height: 1.4em;
  }
  .doc-narrative {
    font-size: 0.97rem;
    line-height: 1.8;
    color: var(--ink-mid);
    padding: 0.75rem 0;
    font-style: italic;
  }
  .doc-narrative-content {
    font-style: normal;
    color: var(--ink);
    white-space: pre-wrap;
  }
  .doc-note {
    font-size: 0.88rem;
    color: var(--ink-light);
    font-style: italic;
    margin-bottom: 0.5rem;
  }
  .doc-bullet-list {
    margin: 0.3rem 0 0.3rem 0;
    padding: 0;
    list-style: none;
  }
  .doc-bullet-list li {
    font-size: 0.95rem;
    padding: 0.15rem 0 0.15rem 1rem;
    position: relative;
    border-bottom: 0.5px dotted var(--rule);
  }
  .doc-bullet-list li::before {
    content: '–';
    position: absolute;
    left: 0;
    color: var(--ink-light);
  }

  .doc-sig-block {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    margin-top: 0.5rem;
  }
  .sig-line {
    margin-bottom: 0.75rem;
  }
  .sig-line .label { font-size: 0.8rem; color: var(--ink-light); font-family: 'Oswald', sans-serif; letter-spacing: 0.06em; text-transform: uppercase; }
  .sig-line .value { border-bottom: 1px solid var(--ink-mid); padding-bottom: 0.2rem; min-height: 1.5em; font-size: 0.95rem; margin-top: 0.15rem; }

  .doc-footer {
    margin-top: 2rem;
    padding-top: 1rem;
    border-top: 2px double var(--ink-mid);
    text-align: center;
    font-family: 'Oswald', sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    color: var(--ink-light);
    text-transform: uppercase;
  }

  .confidential-stamp {
    position: absolute;
    top: 3.5rem;
    right: 2.5rem;
    border: 2.5px solid var(--red-seal);
    color: var(--red-seal);
    font-family: 'Oswald', sans-serif;
    font-size: 0.7rem;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    padding: 0.3rem 0.6rem;
    transform: rotate(8deg);
    opacity: 0.6;
  }

  .items-list {
    margin: 0.3rem 0;
  }
  .items-list .item-row {
    display: flex;
    gap: 0.5rem;
    align-items: flex-start;
    border-bottom: 0.5px dotted var(--rule);
    padding: 0.25rem 0;
    font-size: 0.95rem;
  }
  .items-list .item-num { color: var(--ink-light); min-width: 1.5rem; }
  .items-list .item-val { flex: 1; }

  /* Print */
  @media print {
    body { background: white; }
    .site-header, .selector-section, .form-panel, .preview-toolbar { display: none !important; }
    .main { padding: 0; }
    .preview-panel { max-width: 100%; }
    #document { box-shadow: none; border: none; padding: 1.5rem 2rem; }
    #document::before { display: none; }
    .confidential-stamp { opacity: 0.4; }
  }

  @media (max-width: 900px) {
    .main { flex-direction: column; align-items: center; }
    #document { padding: 2rem 1.5rem; }
    .doc-sig-block { grid-template-columns: 1fr; }
    .doc-field-label { min-width: 130px; }
    .row-2 { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<header class="site-header">
  <div class="seal-row">
    <div class="seal">LSC<br>DA<br>OFFICE</div>
    <h1>District Attorney's Office</h1>
    <div class="seal">SAN<br>ANDREAS<br>STATE</div>
  </div>
  <p>Generador de Documentos Legales — Los Santos County</p>
</header>

<div class="selector-section">
  <div class="selector-label">Seleccionar Tipo de Orden</div>
  <div class="warrant-btns">
    <button class="warrant-btn active" onclick="setType('arrest')">A. Orden de Arresto</button>
    <button class="warrant-btn" onclick="setType('search')">B. Orden de Registro</button>
  </div>
</div>

<div class="main">

  <!-- FORM PANEL -->
  <div class="form-panel">
    <h2>Rellenar Datos</h2>

    <!-- ARREST WARRANT FORM -->
    <div id="form-arrest">

      <div class="form-section">
        <div class="form-section-title">I. Solicitud</div>
        <div class="field-group">
          <label>Nombre del Oficial Solicitante</label>
          <input type="text" id="a-nombre" placeholder="Ej. Det. James Rivera">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">II. Información del Caso</div>
        <div class="field-group">
          <label>Número de Caso</label>
          <input type="text" id="a-caso" placeholder="Ej. LSPD-2024-001234">
        </div>
        <div class="field-group">
          <label>Delito(s) Investigado(s)</label>
          <input type="text" id="a-delito" placeholder="Ej. Homicidio en primer grado, PC §187">
        </div>
        <div class="field-group">
          <label>Agencia Solicitante</label>
          <input type="text" id="a-agencia" placeholder="Ej. Los Santos Police Department">
        </div>
        <div class="field-group">
          <label>Detective / Oficial Responsable</label>
          <input type="text" id="a-detective" placeholder="Ej. Det. James Rivera, Homicidios">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">III. Identificación del Sospechoso</div>
        <div class="field-group">
          <label>Nombre Completo</label>
          <input type="text" id="a-sospechoso" placeholder="Ej. Michael Antonio Torres">
        </div>
        <div class="field-group">
          <label>Alias (si aplica)</label>
          <input type="text" id="a-alias" placeholder="Ej. 'El Toro'">
        </div>
        <div class="row-2">
          <div class="field-group">
            <label>Fecha de Nacimiento</label>
            <input type="text" id="a-dob" placeholder="Ej. 14/03/1985">
          </div>
          <div class="field-group">
            <label>Identificación(es)</label>
            <input type="text" id="a-id" placeholder="Ej. DL #SA-5512233">
          </div>
        </div>
        <div class="field-group">
          <label>Direcciones Asociadas</label>
          <input type="text" id="a-direccion" placeholder="Ej. 3421 Grove St., Apt. 4B, LS">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">IV. Causa Probable (Affidavit)</div>
        <div class="field-group">
          <label>Narrativa de hechos</label>
          <textarea id="a-narrativa" rows="6" placeholder="Describir de forma clara, objetiva y cronológica los hechos, observaciones, reportes y evidencia que justifican la orden..."></textarea>
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">V. Observaciones Importantes</div>
        <div class="field-group">
          <label>Peligrosidad del sospechoso</label>
          <input type="text" id="a-peligro" placeholder="Ej. Alta — antecedentes violentos">
        </div>
        <div class="field-group">
          <label>Riesgo de fuga</label>
          <input type="text" id="a-fuga" placeholder="Ej. Moderado — sin residencia fija">
        </div>
        <div class="field-group">
          <label>Posesión o acceso a armas</label>
          <input type="text" id="a-armas" placeholder="Ej. Sí — portación ilegal registrada">
        </div>
        <div class="field-group">
          <label>Historial criminal relevante</label>
          <input type="text" id="a-historial" placeholder="Ej. 2 condenas previas por asalto">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">VI. Firma del Afianzante</div>
        <div class="field-group">
          <label>Nombre del Oficial</label>
          <input type="text" id="a-ofic-nombre" placeholder="">
        </div>
        <div class="field-group">
          <label>Agencia</label>
          <input type="text" id="a-ofic-agencia" placeholder="">
        </div>
        <div class="row-2">
          <div class="field-group">
            <label>Fecha</label>
            <input type="text" id="a-fecha" placeholder="Ej. 15/07/2024">
          </div>
          <div class="field-group">
            <label>Hora</label>
            <input type="text" id="a-hora" placeholder="Ej. 14:30 hrs">
          </div>
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">VII. Revisión del DA's Office</div>
        <div class="field-group">
          <label>Fiscal Revisor</label>
          <input type="text" id="a-fiscal" placeholder="Ej. ADA Sarah Chen">
        </div>
        <div class="field-group">
          <label>Fecha de Revisión</label>
          <input type="text" id="a-fiscal-fecha" placeholder="">
        </div>
        <div class="field-group">
          <label>Observaciones</label>
          <textarea id="a-observaciones" rows="2" placeholder="Observaciones del fiscal revisor..."></textarea>
        </div>
      </div>
    </div>

    <!-- SEARCH WARRANT FORM -->
    <div id="form-search" style="display:none;">

      <div class="form-section">
        <div class="form-section-title">I. Solicitud</div>
        <div class="field-group">
          <label>Nombre del Oficial Solicitante</label>
          <input type="text" id="s-nombre" placeholder="Ej. Det. Maria Castillo">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">II. Identificación del Caso</div>
        <div class="field-group">
          <label>Número de Caso</label>
          <input type="text" id="s-caso" placeholder="Ej. BCSO-2024-005678">
        </div>
        <div class="field-group">
          <label>Delito Investigado</label>
          <input type="text" id="s-delito" placeholder="Ej. Tráfico de drogas, HS §11352">
        </div>
        <div class="field-group">
          <label>Agencia Solicitante</label>
          <input type="text" id="s-agencia" placeholder="Ej. Blaine County Sheriff's Office">
        </div>
        <div class="field-group">
          <label>Detective / Oficial Responsable</label>
          <input type="text" id="s-detective" placeholder="Ej. Det. Maria Castillo, Narcóticos">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">III. Lugar o Propiedad a Registrar</div>
        <div class="field-group">
          <label>Dirección / Ubicación Exacta</label>
          <input type="text" id="s-direccion" placeholder="Ej. 7890 Stab City Rd., Sandy Shores">
        </div>
        <div class="field-group">
          <label>Descripción del Lugar</label>
          <textarea id="s-desc-lugar" rows="3" placeholder="Ej. Vivienda de estructura metálica de color gris, una planta, con portón azul oxidado..."></textarea>
        </div>
        <div class="field-group">
          <label>Persona(s) Involucrada(s) (si aplica)</label>
          <input type="text" id="s-personas" placeholder="Ej. Trevor Philips, alias 'T'">
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">IV. Objetos o Evidencia a Buscar</div>
        <div id="items-container">
          <div class="field-group">
            <label>Ítem 1</label>
            <input type="text" class="item-input" placeholder="Ej. Metanfetamina o precursores químicos">
          </div>
          <div class="field-group">
            <label>Ítem 2</label>
            <input type="text" class="item-input" placeholder="Ej. Registros de ventas y comunicaciones">
          </div>
          <div class="field-group">
            <label>Ítem 3</label>
            <input type="text" class="item-input" placeholder="Ej. Armas de fuego ilegales">
          </div>
        </div>
        <button type="button" onclick="addItem()" style="font-family:'Oswald',sans-serif;font-size:0.78rem;letter-spacing:0.08em;text-transform:uppercase;padding:0.4rem 1rem;background:transparent;border:1px solid var(--field-border);color:var(--ink-mid);cursor:pointer;margin-top:0.25rem;">+ Agregar Ítem</button>
      </div>

      <div class="form-section">
        <div class="form-section-title">V. Declaración de Causa Probable (Affidavit)</div>
        <div class="field-group">
          <label>Narrativa de hechos</label>
          <textarea id="s-narrativa" rows="6" placeholder="Resumen claro y directo de hechos, observaciones, reportes y evidencia que sostienen la solicitud..."></textarea>
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">VII. Firma del Afianzante</div>
        <div class="field-group">
          <label>Nombre del Oficial</label>
          <input type="text" id="s-ofic-nombre" placeholder="">
        </div>
        <div class="field-group">
          <label>Agencia</label>
          <input type="text" id="s-ofic-agencia" placeholder="">
        </div>
        <div class="row-2">
          <div class="field-group">
            <label>Fecha</label>
            <input type="text" id="s-fecha" placeholder="Ej. 15/07/2024">
          </div>
          <div class="field-group">
            <label>Hora</label>
            <input type="text" id="s-hora" placeholder="Ej. 09:15 hrs">
          </div>
        </div>
      </div>

      <div class="form-section">
        <div class="form-section-title">VIII. Revisión del DA's Office</div>
        <div class="field-group">
          <label>Fiscal Revisor</label>
          <input type="text" id="s-fiscal" placeholder="Ej. ADA Robert Kim">
        </div>
        <div class="field-group">
          <label>Observaciones</label>
          <textarea id="s-observaciones" rows="2" placeholder="Observaciones del fiscal revisor..."></textarea>
        </div>
      </div>
    </div>

    <button class="generate-btn" onclick="generateDoc()">Generar Documento ↓</button>
  </div>

  <!-- PREVIEW PANEL -->
  <div class="preview-panel">
    <div class="preview-toolbar">
      <button class="tool-btn" onclick="window.print()">Imprimir / Guardar PDF</button>
      <button class="tool-btn" onclick="copyText()">Copiar Texto</button>
    </div>

    <div id="document">
      <div class="confidential-stamp">Confidencial</div>

      <!-- DOCUMENT CONTENT injected by JS -->
      <div id="doc-content">
        <div style="text-align:center;padding:3rem 0;color:var(--ink-light);font-style:italic;">
          Complete el formulario y presione "Generar Documento"
        </div>
      </div>

    </div>
  </div>
</div>

<script>
let currentType = 'arrest';
let itemCount = 3;

function setType(type) {
  currentType = type;
  document.querySelectorAll('.warrant-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('form-arrest').style.display = type === 'arrest' ? 'block' : 'none';
  document.getElementById('form-search').style.display = type === 'search' ? 'block' : 'none';
  document.getElementById('doc-content').innerHTML = '<div style="text-align:center;padding:3rem 0;color:var(--ink-light);font-style:italic;">Complete el formulario y presione "Generar Documento"</div>';
}

function val(id) {
  const el = document.getElementById(id);
  return el ? el.value.trim() : '';
}

function field(label, value) {
  return `<div class="doc-field-row">
    <span class="doc-field-label">${label}</span>
    <span class="doc-field-value">${value || '&nbsp;'}</span>
  </div>`;
}

function addItem() {
  itemCount++;
  const container = document.getElementById('items-container');
  const div = document.createElement('div');
  div.className = 'field-group';
  div.innerHTML = `<label>Ítem ${itemCount}</label><input type="text" class="item-input" placeholder="Describir elemento...">`;
  container.appendChild(div);
}

function getItems() {
  return Array.from(document.querySelectorAll('.item-input'))
    .map(i => i.value.trim())
    .filter(v => v);
}

function generateDoc() {
  if (currentType === 'arrest') generateArrest();
  else generateSearch();
}

function generateArrest() {
  const nombre = val('a-nombre') || '[NOMBRE DEL OFICIAL]';
  const caso = val('a-caso') || '_________________';
  const delito = val('a-delito') || '_________________';
  const agencia = val('a-agencia') || '_________________';
  const detective = val('a-detective') || '_________________';
  const sospechoso = val('a-sospechoso') || '_________________';
  const alias = val('a-alias') || 'N/A';
  const dob = val('a-dob') || '_________________';
  const idDoc = val('a-id') || '_________________';
  const direccion = val('a-direccion') || '_________________';
  const narrativa = val('a-narrativa') || '[Narrativa no proporcionada]';
  const peligro = val('a-peligro') || '_________________';
  const fuga = val('a-fuga') || '_________________';
  const armas = val('a-armas') || '_________________';
  const historial = val('a-historial') || '_________________';
  const oficNombre = val('a-ofic-nombre') || nombre;
  const oficAgencia = val('a-ofic-agencia') || agencia;
  const fecha = val('a-fecha') || '_________________';
  const hora = val('a-hora') || '_________________';
  const fiscal = val('a-fiscal') || '_________________';
  const fiscalFecha = val('a-fiscal-fecha') || '_________________';
  const observaciones = val('a-observaciones') || 'Sin observaciones adicionales.';

  document.getElementById('doc-content').innerHTML = `
    <div class="doc-header">
      <div class="doc-agency">Los Santos County District Attorney's Office</div>
      <div class="doc-state">Estado de San Andreas</div>
      <div class="doc-title-en">Arrest Warrant</div>
      <div class="doc-title-es">Orden de Arresto</div>
      <div class="doc-case-badge">Caso N.° ${caso}</div>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">I. Solicitud</div>
      <p style="font-size:0.97rem;line-height:1.7;">Yo, <strong>${nombre}</strong>, solicito a la Honorable Corte Superior del Estado de San Andreas la emisión de una orden de arresto basada en causa probable debidamente fundamentada.</p>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">II. Información del Caso</div>
      ${field('Número de Caso:', caso)}
      ${field('Delito(s) Investigado(s):', delito)}
      ${field('Agencia Solicitante:', agencia)}
      ${field('Detective / Oficial Responsable:', detective)}
    </div>

    <div class="doc-section">
      <div class="doc-section-title">III. Identificación del Sospechoso</div>
      ${field('Nombre Completo:', sospechoso)}
      ${field('Alias:', alias)}
      ${field('Fecha de Nacimiento:', dob)}
      ${field('Identificación(es) conocida(s):', idDoc)}
      ${field('Direcciones asociadas:', direccion)}
    </div>

    <div class="doc-section">
      <div class="doc-section-title">IV. Causa Probable (Affidavit)</div>
      <p class="doc-note">El oficial abajo firmado declara bajo juramento que existe causa probable para creer que la persona identificada ha cometido el delito señalado. Narrativa clara, objetiva y cronológica de los hechos:</p>
      <div class="doc-narrative">
        <span class="doc-narrative-content">${narrativa}</span>
      </div>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">V. Observaciones Importantes</div>
      ${field('Peligrosidad del sospechoso:', peligro)}
      ${field('Riesgo de fuga:', fuga)}
      ${field('Posesión o acceso a armas:', armas)}
      ${field('Historial criminal relevante:', historial)}
    </div>

    <div class="doc-section">
      <div class="doc-section-title">VI. Firma del Afianzante</div>
      <div class="doc-sig-block">
        <div>
          <div class="sig-line"><div class="label">Nombre del Oficial</div><div class="value">${oficNombre}</div></div>
          <div class="sig-line"><div class="label">Agencia</div><div class="value">${oficAgencia}</div></div>
        </div>
        <div>
          <div class="sig-line"><div class="label">Firma</div><div class="value">&nbsp;</div></div>
          <div class="sig-line"><div class="label">Fecha y Hora</div><div class="value">${fecha} — ${hora}</div></div>
        </div>
      </div>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">VII. Revisión del District Attorney's Office</div>
      <div class="doc-sig-block">
        <div>
          <div class="sig-line"><div class="label">Fiscal Revisor</div><div class="value">${fiscal}</div></div>
          <div class="sig-line"><div class="label">Fecha</div><div class="value">${fiscalFecha}</div></div>
        </div>
        <div>
          <div class="sig-line"><div class="label">Firma</div><div class="value">&nbsp;</div></div>
          <div class="sig-line"><div class="label">Observaciones</div><div class="value" style="font-size:0.88rem;">${observaciones}</div></div>
        </div>
      </div>
    </div>

    <div class="doc-footer">
      Los Santos County District Attorney's Office — Estado de San Andreas — Documento Oficial
    </div>
  `;
}

function generateSearch() {
  const nombre = val('s-nombre') || '[NOMBRE DEL OFICIAL]';
  const caso = val('s-caso') || '_________________';
  const delito = val('s-delito') || '_________________';
  const agencia = val('s-agencia') || '_________________';
  const detective = val('s-detective') || '_________________';
  const direccion = val('s-direccion') || '_________________';
  const descLugar = val('s-desc-lugar') || '_________________';
  const personas = val('s-personas') || 'N/A';
  const items = getItems();
  const narrativa = val('s-narrativa') || '[Narrativa no proporcionada]';
  const oficNombre = val('s-ofic-nombre') || nombre;
  const oficAgencia = val('s-ofic-agencia') || agencia;
  const fecha = val('s-fecha') || '_________________';
  const hora = val('s-hora') || '_________________';
  const fiscal = val('s-fiscal') || '_________________';
  const observaciones = val('s-observaciones') || 'Sin observaciones adicionales.';

  const itemsHtml = items.length > 0
    ? `<div class="items-list">${items.map((it, i) => `<div class="item-row"><span class="item-num">${i+1}.</span><span class="item-val">${it}</span></div>`).join('')}</div>`
    : `<p style="font-style:italic;color:var(--ink-light);font-size:0.9rem;">No se especificaron ítems.</p>`;

  document.getElementById('doc-content').innerHTML = `
    <div class="doc-header">
      <div class="doc-agency">Los Santos County District Attorney's Office</div>
      <div class="doc-state">Estado de San Andreas</div>
      <div class="doc-title-en">Search Warrant</div>
      <div class="doc-title-es">Orden de Registro</div>
      <div class="doc-case-badge">Caso N.° ${caso}</div>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">I. Solicitud</div>
      <p style="font-size:0.97rem;line-height:1.7;">Yo, <strong>${nombre}</strong>, solicito al Tribunal Superior del Estado de San Andreas la aprobación de una orden de registro basada en causa probable debidamente fundamentada.</p>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">II. Identificación del Caso</div>
      ${field('Número de Caso:', caso)}
      ${field('Delito Investigado:', delito)}
      ${field('Agencia Solicitante:', agencia)}
      ${field('Detective / Oficial Responsable:', detective)}
    </div>

    <div class="doc-section">
      <div class="doc-section-title">III. Lugar o Propiedad a Registrar</div>
      ${field('Dirección / Ubicación Exacta:', direccion)}
      ${field('Descripción del Lugar:', descLugar)}
      ${field('Persona(s) Involucrada(s):', personas)}
    </div>

    <div class="doc-section">
      <div class="doc-section-title">IV. Objetos o Evidencia a Buscar</div>
      <p class="doc-note">Enumerados de forma clara y específica:</p>
      ${itemsHtml}
    </div>

    <div class="doc-section">
      <div class="doc-section-title">V. Declaración de Causa Probable (Affidavit)</div>
      <p class="doc-note">El oficial abajo firmado declara bajo juramento que existe causa probable para creer que la evidencia listada se encuentra en el lugar mencionado:</p>
      <div class="doc-narrative">
        <span class="doc-narrative-content">${narrativa}</span>
      </div>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">VI. Limitaciones y Alcance del Registro</div>
      <ul class="doc-bullet-list">
        <li>Solo se permite registrar las áreas directamente relacionadas con la búsqueda de los objetos descritos.</li>
        <li>Cualquier evidencia adicional deberá ser documentada conforme a los procedimientos legales.</li>
        <li>El registro deberá ejecutarse en horario diurno salvo autorización expresa del tribunal.</li>
      </ul>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">VII. Firma del Afianzante</div>
      <div class="doc-sig-block">
        <div>
          <div class="sig-line"><div class="label">Nombre del Oficial</div><div class="value">${oficNombre}</div></div>
          <div class="sig-line"><div class="label">Agencia</div><div class="value">${oficAgencia}</div></div>
        </div>
        <div>
          <div class="sig-line"><div class="label">Firma</div><div class="value">&nbsp;</div></div>
          <div class="sig-line"><div class="label">Fecha y Hora</div><div class="value">${fecha} — ${hora}</div></div>
        </div>
      </div>
    </div>

    <div class="doc-section">
      <div class="doc-section-title">VIII. Revisión del District Attorney's Office</div>
      <div class="doc-sig-block">
        <div>
          <div class="sig-line"><div class="label">Fiscal Revisor</div><div class="value">${fiscal}</div></div>
          <div class="sig-line"><div class="label">Firma</div><div class="value">&nbsp;</div></div>
        </div>
        <div>
          <div class="sig-line"><div class="label">Observaciones</div><div class="value" style="font-size:0.88rem;">${observaciones}</div></div>
        </div>
      </div>
    </div>

    <div class="doc-footer">
      Los Santos County District Attorney's Office — Estado de San Andreas — Documento Oficial
    </div>
  `;
}

function copyText() {
  const text = document.getElementById('doc-content').innerText;
  navigator.clipboard.writeText(text).then(() => {
    const btn = event.target;
    btn.textContent = 'Copiado ✓';
    setTimeout(() => btn.textContent = 'Copiar Texto', 2000);
  });
}
</script>
</body>
</html>
