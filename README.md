<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>DA Office Generator</title>

<style>

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

:root{
  --red:#8b1117;
  --dark-red:#5f0b10;
  --gold:#c8a44d;
  --paper:#fffaf2;
  --text:#1b1b1b;
  --border:#d8c08a;
}

body{
  background:#ececec;
  font-family:Georgia,serif;
  color:var(--text);
}

header{
  background:linear-gradient(
    180deg,
    var(--red),
    var(--dark-red)
  );

  color:white;
  text-align:center;
  padding:30px;
  border-bottom:5px solid var(--gold);
}

header h1{
  font-size:32px;
  letter-spacing:3px;
}

header p{
  color:#ecd48e;
  margin-top:8px;
}

.selector{
  background:white;
  padding:20px;
  text-align:center;
  border-bottom:1px solid #ddd;
}

.selector button,
button{
  background:var(--red);
  color:white;
  border:none;
  padding:11px 16px;
  cursor:pointer;
  margin:5px;
  font-weight:bold;
}

.selector button.active{
  background:var(--gold);
  color:#222;
}

.main{
  max-width:1300px;
  margin:30px auto;
  display:grid;
  grid-template-columns:430px 1fr;
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
  margin-bottom:20px;
}

.section-title{
  color:var(--dark-red);
  margin:22px 0 10px;
  padding-bottom:5px;
  border-bottom:1px solid var(--border);
  font-weight:bold;
}

label{
  display:block;
  margin:10px 0 4px;
  font-size:12px;
  font-weight:bold;
  text-transform:uppercase;
}

input,
textarea{
  width:100%;
  padding:9px;
  border:1px solid #bbb;
  font-size:15px;
  font-family:Georgia,serif;
}

textarea{
  resize:vertical;
  min-height:90px;
}

.preview-toolbar{
  text-align:right;
  margin-bottom:10px;
}

#document{
  background:var(--paper);
  padding:45px;
  border:1px solid #ccc;
  min-height:900px;
  box-shadow:0 10px 30px rgba(0,0,0,.16);
}

.doc-head{
  text-align:center;
  border-bottom:3px double #333;
  padding-bottom:20px;
  margin-bottom:28px;
}

.doc-title{
  margin-top:20px;
  color:var(--red);
  font-size:30px;
  font-weight:bold;
  letter-spacing:3px;
}

.doc-subtitle{
  font-style:italic;
  font-size:19px;
}

.doc-section{
  margin-bottom:24px;
}

.doc-section h3{
  color:var(--dark-red);
  margin-bottom:8px;
  border-bottom:1px solid #ddd;
  padding-bottom:4px;
}

.field{
  margin:6px 0;
}

.field b{
  display:inline-block;
  min-width:240px;
}

.narrative{
  margin-top:10px;
  line-height:1.6;
  white-space:pre-wrap;
}

.signature-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:20px;
}

.line{
  border-bottom:1px solid #222;
  min-height:22px;
  margin-top:4px;
}

.footer{
  margin-top:35px;
  border-top:3px double #333;
  padding-top:15px;
  text-align:center;
  font-size:12px;
  color:#666;
}

.item-row{
  display:flex;
  gap:8px;
  margin-bottom:8px;
}

.item-row input{
  flex:1;
}

.small-btn{
  background:#222;
  padding:8px 12px;
  font-size:12px;
}

@media(max-width:950px){

  .main{
    grid-template-columns:1fr;
  }

  #document{
    padding:25px;
  }

}

@media print{

  header,
  .selector,
  .panel,
  .preview-toolbar{
    display:none;
  }

  body{
    background:white;
  }

  .main{
    display:block;
    margin:0;
    padding:0;
  }

  #document{
    box-shadow:none;
    border:none;
  }

}

</style>
</head>

<body>

<header>
  <h1>LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE</h1>
  <p>STATE OF SAN ANDREAS</p>
</header>

<div class="selector">

  <button
    id="btnArrest"
    class="active"
    onclick="setType('arrest')"
  >
    A. Arrest Warrant
  </button>

  <button
    id="btnSearch"
    onclick="setType('search')"
  >
    B. Search Warrant
  </button>

</div>

<div class="main">

<div class="panel">

<h2>Rellenar Documento</h2>

<!-- ARREST -->

<div id="arrestForm">

<div class="section-title">I. Solicitud</div>

<label>Nombre</label>
<input id="a_nombre">

<div class="section-title">II. Información del Caso</div>

<label>Número de Caso</label>
<input id="a_caso">

<label>Delito(s) Investigado(s)</label>
<input id="a_delito">

<label>Agencia Solicitante</label>
<input id="a_agencia">

<label>Detective / Oficial Responsable</label>
<input id="a_detective">

<div class="section-title">
III. Identificación del Sospechoso
</div>

<label>Nombre Completo</label>
<input id="a_sospechoso">

<label>Alias</label>
<input id="a_alias">

<label>Fecha de Nacimiento</label>
<input id="a_dob">

<label>Identificación(es)</label>
<input id="a_id">

<label>Direcciones asociadas</label>
<input id="a_direcciones">

<div class="section-title">
IV. Causa Probable
</div>

<label>Narrativa</label>
<textarea id="a_narrativa"></textarea>

<div class="section-title">
V. Observaciones Importantes
</div>

<label>Peligrosidad del sospechoso</label>
<input id="a_peligro">

<label>Riesgo de fuga</label>
<input id="a_fuga">

<label>Posesión o acceso a armas</label>
<input id="a_armas">

<label>Historial criminal relevante</label>
<input id="a_historial">

<div class="section-title">
VI. Firma del Afianzante
</div>

<label>Nombre del Oficial</label>
<input id="a_oficial">

<label>Agencia</label>
<input id="a_oficial_agencia">

<label>Fecha y Hora</label>
<input id="a_fecha_hora">

<div class="section-title">
VII. Revisión DA Office
</div>

<label>Fiscal Revisor</label>
<input id="a_fiscal">

<label>Fecha</label>
<input id="a_fecha_revision">

<label>Observaciones</label>
<textarea id="a_observaciones"></textarea>

</div>

<!-- SEARCH -->

<div id="searchForm" style="display:none">

<div class="section-title">
I. Solicitud
</div>

<label>Nombre</label>
<input id="s_nombre">

<div class="section-title">
II. Identificación del Caso
</div>

<label>Número de Caso</label>
<input id="s_caso">

<label>Delito Investigado</label>
<input id="s_delito">

<label>Agencia Solicitante</label>
<input id="s_agencia">

<label>Detective / Oficial Responsable</label>
<input id="s_detective">

<div class="section-title">
III. Lugar o Propiedad a Registrar
</div>

<label>Dirección / Ubicación Exacta</label>
<input id="s_direccion">

<label>Descripción del Lugar</label>
<textarea id="s_descripcion"></textarea>

<label>Persona(s) Involucrada(s)</label>
<input id="s_personas">

<div class="section-title">
IV. Objetos o Evidencia a Buscar
</div>

<div id="items"></div>

<button
  class="small-btn"
  onclick="addItem()"
  type="button"
>
  + Añadir ítem
</button>

<div class="section-title">
V. Declaración de Causa Probable
</div>

<label>Narrativa</label>
<textarea id="s_narrativa"></textarea>

<div class="section-title">
VII. Firma del Afianzando
</div>

<label>Nombre del Oficial</label>
<input id="s_oficial">

<label>Agencia</label>
<input id="s_oficial_agencia">

<label>Fecha y Hora</label>
<input id="s_fecha_hora">

<div class="section-title">
VIII. Revisión DA Office
</div>

<label>Fiscal Revisor</label>
<input id="s_fiscal">

<label>Observaciones</label>
<textarea id="s_observaciones"></textarea>

</div>

<button onclick="generate()">
GENERAR DOCUMENTO
</button>

</div>

<!-- PREVIEW -->

<div>

<div class="preview-toolbar">

<button onclick="copyDoc()">
Copiar
</button>

<button onclick="window.print()">
Guardar PDF
</button>

</div>

<div id="document">

<div id="docContent">
Complete el formulario y pulse generar.
</div>

</div>

</div>

</div>

<script>

let type = localStorage.getItem("da_type") || "arrest";

/* TYPE */

function setType(t){

  type = t;

  localStorage.setItem("da_type", t);

  document.getElementById("arrestForm").style.display =
    t === "arrest" ? "block" : "none";

  document.getElementById("searchForm").style.display =
    t === "search" ? "block" : "none";

  document.getElementById("btnArrest")
    .classList.toggle("active", t === "arrest");

  document.getElementById("btnSearch")
    .classList.toggle("active", t === "search");

}

/* VALUE */

function v(id){

  return document.getElementById(id).value.trim()
    || "________________";

}

/* ITEMS */

function addItem(value = ""){

  const container = document.getElementById("items");

  const div = document.createElement("div");

  div.className = "item-row";

  div.innerHTML = `

    <input
      class="item"
      placeholder="Nuevo ítem"
      value="${value.replace(/"/g, "&quot;")}"
    >

    <button
      type="button"
      onclick="removeItem(this)"
      class="small-btn"
      style="
        background:#8b1117;
        color:white;
        min-width:42px;
      "
    >
      ✕
    </button>

  `;

  container.appendChild(div);

  saveFormCache();

}

function removeItem(btn){

  btn.parentElement.remove();

  saveFormCache();

}

function loadItems(itemsArray){

  const container = document.getElementById("items");

  container.innerHTML = "";

  if(!itemsArray || itemsArray.length === 0){

    for(let i = 0; i < 3; i++){
      addItem();
    }

    return;
  }

  itemsArray.forEach(item => {
    addItem(item);
  });

}

/* CACHE */

function saveFormCache(){

  const data = {};

  document.querySelectorAll("input, textarea")
    .forEach(el => {

      if(el.id){
        data[el.id] = el.value;
      }

    });

  data.items = [...document.querySelectorAll(".item")]
    .map(i => i.value);

  localStorage.setItem(
    "da_form_cache",
    JSON.stringify(data)
  );

}

function loadFormCache(){

  const raw = localStorage.getItem("da_form_cache");

  if(!raw){
    loadItems([]);
    return;
  }

  const data = JSON.parse(raw);

  Object.keys(data).forEach(id => {

    const el = document.getElementById(id);

    if(el && typeof data[id] === "string"){
      el.value = data[id];
    }

  });

  loadItems(data.items || []);

}

function clearFormCache(){

  localStorage.removeItem("da_form_cache");

  localStorage.removeItem("da_type");

}

function resetInputs(){

  document.querySelectorAll("input, textarea")
    .forEach(el => {
      el.value = "";
    });

  loadItems([]);

}

/* HEAD */

function head(title,sub){

  return `

  <div class="doc-head">

    <div>
      LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE
    </div>

    <div>
      STATE OF SAN ANDREAS
    </div>

    <div class="doc-title">
      ${title}
    </div>

    <div class="doc-subtitle">
      ${sub}
    </div>

  </div>

  `;

}

/* GENERATE */

function generate(){

  if(type === "arrest"){
    generateArrest();
  } else {
    generateSearch();
  }

  clearFormCache();

  resetInputs();

}

/* ARREST */

function generateArrest(){

  document.getElementById("docContent").innerHTML =

  head("ARREST WARRANT","Orden de Arresto") +

  `

  <div class="doc-section">

    <h3>I. Solicitud</h3>

    <p>
      Yo, <b>${v("a_nombre")}</b>,
      solicito a la Honorable Corte Superior
      del Estado de San Andreas la emisión
      de una orden de arresto basada en
      causa probable debidamente fundamentada.
    </p>

  </div>

  <div class="footer">
    LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE
  </div>

  `;

}

/* SEARCH */

function generateSearch(){

  const items = [...document.querySelectorAll(".item")]
    .map(i => i.value.trim())
    .filter(Boolean)
    .map((x,i) => `<div>${i+1}. ${x}</div>`)
    .join("");

  document.getElementById("docContent").innerHTML =

  head("SEARCH WARRANT","Orden de Registro") +

  `

  <div class="doc-section">

    <h3>IV. Objetos o Evidencia a Buscar</h3>

    ${items}

  </div>

  <div class="footer">
    LOS SANTOS COUNTY DISTRICT ATTORNEY’S OFFICE
  </div>

  `;

}

/* COPY */

function copyDoc(){

  navigator.clipboard.writeText(
    document.getElementById("document").innerText
  );

  alert("Documento copiado.");

}

/* AUTOSAVE */

document.addEventListener("input", function(e){

  if(e.target.matches("input, textarea")){
    saveFormCache();
  }

});

/* LOAD */

window.addEventListener("DOMContentLoaded", function(){

  loadFormCache();

  setType(type);

});

</script>

</body>
</html>
