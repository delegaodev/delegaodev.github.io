<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Generador DA Office</title>

<style>
*{box-sizing:border-box;margin:0;padding:0}

:root{
  --red:#8b1117;
  --dark-red:#5f0b10;
  --white:#ffffff;
  --paper:#fffaf2;
  --gold:#c8a44d;
  --text:#1b1b1b;
  --muted:#666;
  --border:#d8c08a;
}

body{
  background:#f0f0f0;
  font-family:Georgia,serif;
  color:var(--text);
}

header{
  background:linear-gradient(180deg,var(--red),var(--dark-red));
  color:white;
  text-align:center;
  padding:32px 20px;
  border-bottom:5px solid var(--gold);
}

header h1{
  font-family:Arial,sans-serif;
  letter-spacing:3px;
  font-size:32px;
}

header p{
  color:#ead08a;
  margin-top:8px;
  font-style:italic;
}

.selector{
  text-align:center;
  padding:22px;
  background:white;
  border-bottom:1px solid #ddd;
}

.selector button,
button{
  background:var(--red);
  color:white;
  border:none;
  padding:11px 18px;
  margin:5px;
  cursor:pointer;
  font-weight:bold;
}

.selector button.active{
  background:var(--gold);
  color:#222;
}

.main{
  max-width:1250px;
  margin:30px auto;
  display:grid;
  grid-template-columns:420px 1fr;
  gap:25px;
  padding:0 20px;
}

.panel{
  background:white;
  border:2px solid var(--border);
  padding:22px;
  box-shadow:0 8px 20px rgba(0,0,0,.12);
}

h2{
  color:var(--red);
  font-family:Arial,sans-serif;
  margin-bottom:18px;
}

.section-title{
  color:var(--dark-red);
  font-family:Arial,sans-serif;
  font-weight:bold;
  margin:20px 0 10px;
  padding-bottom:5px;
  border-bottom:1px solid var(--border);
}

label{
  display:block;
  font-family:Arial,sans-serif;
  font-size:12px;
  font-weight:bold;
  color:#444;
  margin:10px 0 4px;
  text-transform:uppercase;
}

input,textarea{
  width:100%;
  padding:9px;
  border:1px solid #bbb;
  font-family:Georgia,serif;
  font-size:15px;
}

textarea{resize:vertical;min-height:90px}

.row{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
}

.small-btn{
  background:#333;
  padding:8px 12px;
  font-size:12px;
}

.preview-toolbar{
  text-align:right;
  margin-bottom:10px;
}

#document{
  background:var(--paper);
  padding:45px;
  border:1px solid #ccc;
  box-shadow:0 10px 30px rgba(0,0,0,.18);
  min-height:900px;
}

.doc-head{
  text-align:center;
  border-bottom:3px double #333;
  padding-bottom:22px;
  margin-bottom:28px;
}

.doc-agency{
  font-weight:bold;
  letter-spacing:1px;
}

.doc-state{
  margin-top:4px;
  color:#444;
}

.doc-title{
  margin-top:22px;
  color:var(--red);
  font-family:Arial,sans-serif;
  font-size:30px;
  font-weight:bold;
  letter-spacing:3px;
}

.doc-subtitle{
  font-style:italic;
  font-size:20px;
}

.doc-section{
  margin-bottom:24px;
}

.doc-section h3{
  font-family:Arial,sans-serif;
  color:var(--dark-red);
  font-size:16px;
  margin-bottom:8px;
  border-bottom:1px solid #ddd;
  padding-bottom:4px;
}

.field{
  margin:6px 0;
}

.field b{
  display:inline-block;
  min-width:230px;
}

.narrative{
  white-space:pre-wrap;
  margin-top:10px;
  line-height:1.6;
}

.signature-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:20px;
}

.line{
  border-bottom:1px solid #333;
  min-height:24px;
  margin-top:4px;
}

.footer{
  margin-top:35px;
  padding-top:15px;
  border-top:3px double #333;
  text-align:center;
  font-size:12px;
  color:#666;
  letter-spacing:1px;
}

.item-row{
  display:flex;
  gap:8px;
  margin-bottom:8px;
}

.item-row input{flex:1}

@media(max-width:900px){
  .main{grid-template-columns:1fr}
  #document{padding:25px}
}

@media print{
  header,.selector,.panel,.preview-toolbar{display:none}
  body{background:white}
  .main{display:block;margin:0;padding:0}
  #document{box-shadow:none;border:none}
}
</style>
</head>

<body>

<header>
  <h1>LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE</h1>
  <p>State of San Andreas</p>
</header>

<div class="selector">
  <button id="btnArrest" class="active" onclick="setType('arrest')">A. Arrest Warrant</button>
  <button id="btnSearch" onclick="setType('search')">B. Search Warrant</button>
</div>

<div class="main">

<div class="panel">
<h2>Rellenar Documento</h2>

<div id="arrestForm">
  <div class="section-title">I. Solicitud</div>
  <label>Nombre</label><input id="a_nombre">

  <div class="section-title">II. Información del Caso</div>
  <label>Número de Caso</label><input id="a_caso">
  <label>Delito(s) Investigado(s)</label><input id="a_delito">
  <label>Agencia Solicitante</label><input id="a_agencia">
  <label>Detective / Oficial Responsable</label><input id="a_detective">

  <div class="section-title">III. Identificación del Sospechoso</div>
  <label>Nombre Completo</label><input id="a_sospechoso">
  <label>Alias</label><input id="a_alias">
  <label>Fecha de Nacimiento</label><input id="a_dob">
  <label>Identificación(es)</label><input id="a_id">
  <label>Direcciones asociadas</label><input id="a_direcciones">

  <div class="section-title">IV. Causa Probable</div>
  <label>Narrativa</label><textarea id="a_narrativa"></textarea>

  <div class="section-title">V. Observaciones Importantes</div>
  <label>Peligrosidad del sospechoso</label><input id="a_peligro">
  <label>Riesgo de fuga</label><input id="a_fuga">
  <label>Posesión o acceso a armas</label><input id="a_armas">
  <label>Historial criminal relevante</label><input id="a_historial">

  <div class="section-title">VI. Firma del Afianzante</div>
  <label>Nombre del Oficial</label><input id="a_oficial">
  <label>Agencia</label><input id="a_oficial_agencia">
  <label>Fecha y Hora</label><input id="a_fecha_hora">

  <div class="section-title">VII. Revisión DA Office</div>
  <label>Fiscal Revisor</label><input id="a_fiscal">
  <label>Fecha</label><input id="a_fecha_revision">
  <label>Observaciones</label><textarea id="a_observaciones"></textarea>
</div>

<div id="searchForm" style="display:none">
  <div class="section-title">I. Solicitud</div>
  <label>Nombre</label><input id="s_nombre">

  <div class="section-title">II. Identificación del Caso</div>
  <label>Número de Caso</label><input id="s_caso">
  <label>Delito Investigado</label><input id="s_delito">
  <label>Agencia Solicitante</label><input id="s_agencia">
  <label>Detective / Oficial Responsable</label><input id="s_detective">

  <div class="section-title">III. Lugar o Propiedad a Registrar</div>
  <label>Dirección / Ubicación Exacta</label><input id="s_direccion">
  <label>Descripción del Lugar</label><textarea id="s_descripcion"></textarea>
  <label>Persona(s) Involucrada(s)</label><input id="s_personas">

  <div class="section-title">IV. Objetos o Evidencia a Buscar</div>
  <div id="items">
    <div class="item-row"><input class="item" placeholder="1."></div>
    <div class="item-row"><input class="item" placeholder="2."></div>
    <div class="item-row"><input class="item" placeholder="3."></div>
  </div>
  <button class="small-btn" onclick="addItem()" type="button">+ Añadir ítem</button>

  <div class="section-title">V. Declaración de Causa Probable</div>
  <label>Narrativa</label><textarea id="s_narrativa"></textarea>

  <div class="section-title">VII. Firma del Afianzando</div>
  <label>Nombre del Oficial</label><input id="s_oficial">
  <label>Agencia</label><input id="s_oficial_agencia">
  <label>Fecha y Hora</label><input id="s_fecha_hora">

  <div class="section-title">VIII. Revisión DA Office</div>
  <label>Fiscal Revisor</label><input id="s_fiscal">
  <label>Observaciones</label><textarea id="s_observaciones"></textarea>
</div>

<button onclick="generate()">GENERAR DOCUMENTO</button>
</div>

<div>
  <div class="preview-toolbar">
    <button onclick="copyDoc()">Copiar</button>
    <button onclick="window.print()">Guardar PDF</button>
  </div>

  <div id="document">
    <div id="docContent">
      Complete el formulario y pulse generar.
    </div>
  </div>
</div>

</div>

<script>
let type="arrest";

function setType(t){
  type=t;
  document.getElementById("arrestForm").style.display=t==="arrest"?"block":"none";
  document.getElementById("searchForm").style.display=t==="search"?"block":"none";
  document.getElementById("btnArrest").classList.toggle("active",t==="arrest");
  document.getElementById("btnSearch").classList.toggle("active",t==="search");
}

function v(id){
  return document.getElementById(id).value.trim() || "________________";
}

function addItem(){
  const div=document.createElement("div");
  div.className="item-row";
  div.innerHTML='<input class="item" placeholder="Nuevo ítem">';
  document.getElementById("items").appendChild(div);
}

function head(title,sub){
  return `
  <div class="doc-head">
    <div class="doc-agency">LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE</div>
    <div class="doc-state">STATE OF SAN ANDREAS</div>
    <div class="doc-title">${title}</div>
    <div class="doc-subtitle">${sub}</div>
  </div>`;
}

function generate(){
  if(type==="arrest") generateArrest();
  else generateSearch();
}

function generateArrest(){
  document.getElementById("docContent").innerHTML =
  head("ARREST WARRANT","Orden de Arresto") + `
  <div class="doc-section">
    <h3>I. Solicitud</h3>
    <p>Yo, <b>${v("a_nombre")}</b>, solicito a la Honorable Corte Superior del Estado de San Andreas la emisión de una orden de arresto basada en causa probable debidamente fundamentada.</p>
  </div>

  <div class="doc-section">
    <h3>II. Información del Caso</h3>
    <div class="field"><b>Número de Caso:</b> ${v("a_caso")}</div>
    <div class="field"><b>Delito(s) Investigado(s):</b> ${v("a_delito")}</div>
    <div class="field"><b>Agencia Solicitante:</b> ${v("a_agencia")}</div>
    <div class="field"><b>Detective / Oficial Responsable:</b> ${v("a_detective")}</div>
  </div>

  <div class="doc-section">
    <h3>III. Identificación del Sospechoso</h3>
    <div class="field"><b>Nombre Completo:</b> ${v("a_sospechoso")}</div>
    <div class="field"><b>Alias:</b> ${v("a_alias")}</div>
    <div class="field"><b>Fecha de Nacimiento:</b> ${v("a_dob")}</div>
    <div class="field"><b>Identificación(es) conocida(s):</b> ${v("a_id")}</div>
    <div class="field"><b>Direcciones asociadas:</b> ${v("a_direcciones")}</div>
  </div>

  <div class="doc-section">
    <h3>IV. Causa Probable (Affidavit)</h3>
    <p>El oficial abajo firmado declara bajo juramento que existe causa probable para creer que la persona identificada ha cometido el delito señalado.</p>
    <p>Narrativa clara, objetiva y cronológica de los hechos que justifican la orden:</p>
    <div class="narrative">${v("a_narrativa")}</div>
  </div>

  <div class="doc-section">
    <h3>V. Observaciones Importantes</h3>
    <div class="field"><b>Peligrosidad del sospechoso:</b> ${v("a_peligro")}</div>
    <div class="field"><b>Riesgo de fuga:</b> ${v("a_fuga")}</div>
    <div class="field"><b>Posesión o acceso a armas:</b> ${v("a_armas")}</div>
    <div class="field"><b>Historial criminal relevante:</b> ${v("a_historial")}</div>
  </div>

  <div class="doc-section">
    <h3>VI. Firma del Afianzante</h3>
    <div class="signature-grid">
      <div>
        <div class="field"><b>Nombre del Oficial:</b> ${v("a_oficial")}</div>
        <div class="field"><b>Agencia:</b> ${v("a_oficial_agencia")}</div>
      </div>
      <div>
        <div class="field"><b>Firma:</b><div class="line"></div></div>
        <div class="field"><b>Fecha y Hora:</b> ${v("a_fecha_hora")}</div>
      </div>
    </div>
  </div>

  <div class="doc-section">
    <h3>VII. Revisión del District Attorney’s Office</h3>
    <div class="field"><b>Fiscal Revisor:</b> ${v("a_fiscal")}</div>
    <div class="field"><b>Firma:</b><div class="line"></div></div>
    <div class="field"><b>Fecha:</b> ${v("a_fecha_revision")}</div>
    <div class="field"><b>Observaciones:</b> ${v("a_observaciones")}</div>
  </div>

  <div class="footer">LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE — STATE OF SAN ANDREAS</div>`;
}

function generateSearch(){
  const items=[...document.querySelectorAll(".item")]
    .map(i=>i.value.trim())
    .filter(Boolean)
    .map((x,i)=>`<div>${i+1}. ${x}</div>`)
    .join("") || "<div>1. ________________</div><div>2. ________________</div><div>3. ________________</div>";

  document.getElementById("docContent").innerHTML =
  head("SEARCH WARRANT","Orden de Registro") + `
  <div class="doc-section">
    <h3>I. Solicitud</h3>
    <p>Yo, <b>${v("s_nombre")}</b>, solicito a la Tribunal Superior del Estado de San Andreas la aprobación de una orden de registro basada en causa probable debidamente fundamentada.</p>
  </div>

  <div class="doc-section">
    <h3>II. Identificación del Caso</h3>
    <div class="field"><b>Número de Caso:</b> ${v("s_caso")}</div>
    <div class="field"><b>Delito Investigado:</b> ${v("s_delito")}</div>
    <div class="field"><b>Agencia Solicitante:</b> ${v("s_agencia")}</div>
    <div class="field"><b>Detective / Oficial Responsable:</b> ${v("s_detective")}</div>
  </div>

  <div class="doc-section">
    <h3>III. Lugar o Propiedad a Registrar</h3>
    <div class="field"><b>Dirección / Ubicación Exacta:</b> ${v("s_direccion")}</div>
    <div class="field"><b>Descripción del Lugar:</b> ${v("s_descripcion")}</div>
    <div class="field"><b>Persona(s) Involucrada(s):</b> ${v("s_personas")}</div>
  </div>

  <div class="doc-section">
    <h3>IV. Objetos o Evidencia a Buscar</h3>
    <p>(Enumerar de forma clara y específica)</p>
    ${items}
  </div>

  <div class="doc-section">
    <h3>V. Declaración de Causa Probable (Affidavit)</h3>
    <p>El oficial abajo firmado declara bajo juramento que existe causa probable para creer que la evidencia listada se encuentra en el lugar mencionado.</p>
    <p>Resumen claro y directo de hechos, observaciones, reportes y evidencia que sostienen la solicitud:</p>
    <div class="narrative">${v("s_narrativa")}</div>
  </div>

  <div class="doc-section">
    <h3>VI. Limitaciones y Alcance del Registro</h3>
    <p>– Solo se permite registrar las áreas directamente relacionadas con la búsqueda de los objetos descritos.</p>
    <p>– Cualquier evidencia adicional deberá ser documentada conforme a los procedimientos legales.</p>
  </div>

  <div class="doc-section">
    <h3>VII. Firma del Afianzando</h3>
    <div class="signature-grid">
      <div>
        <div class="field"><b>Nombre del Oficial:</b> ${v("s_oficial")}</div>
        <div class="field"><b>Agencia:</b> ${v("s_oficial_agencia")}</div>
      </div>
      <div>
        <div class="field"><b>Firma:</b><div class="line"></div></div>
        <div class="field"><b>Fecha y Hora:</b> ${v("s_fecha_hora")}</div>
      </div>
    </div>
  </div>

  <div class="doc-section">
    <h3>VIII. Revisión del District Attorney’s Office</h3>
    <div class="field"><b>Fiscal Revisor:</b> ${v("s_fiscal")}</div>
    <div class="field"><b>Observaciones:</b> ${v("s_observaciones")}</div>
    <div class="field"><b>Firma:</b><div class="line"></div></div>
  </div>

  <div class="footer">LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE — STATE OF SAN ANDREAS</div>`;
}

function copyDoc(){
  navigator.clipboard.writeText(document.getElementById("document").innerText);
  alert("Documento copiado.");
}
</script>

</body>
</html>
