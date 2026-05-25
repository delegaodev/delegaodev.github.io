from PIL import Image
import base64
from pathlib import Path

# Paths
img_path = "/mnt/data/IMG_2022.webp"
out_path = "/mnt/data/da_generator_logo_updated.html"

# Read image and convert to base64
with open(img_path, "rb") as f:
    b64 = base64.b64encode(f.read()).decode("utf-8")

# Minimal replacement-ready HTML
html = f"""<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DA Office Generator</title>

<style>
:root{{
  --red:#8d1117;
  --darkred:#650d12;
  --white:#f5f5f5;
  --gold:#c8a44d;
}}

body{{
  margin:0;
  background:#f3f3f3;
  font-family:Arial,sans-serif;
}}

.site-header{{
  background:linear-gradient(180deg,var(--red),var(--darkred));
  color:white;
  padding:24px;
  text-align:center;
  border-bottom:4px solid var(--gold);
}}

.logo-row{{
  display:flex;
  justify-content:center;
  align-items:center;
  gap:30px;
}}

.logo{{
  width:110px;
  height:110px;
  object-fit:contain;
}}

h1{{
  font-size:2rem;
  margin:0;
  letter-spacing:2px;
}}

.subtitle{{
  margin-top:8px;
  color:#f0d890;
}}

.content{{
  max-width:900px;
  margin:40px auto;
  background:white;
  padding:30px;
  border:1px solid #ddd;
  box-shadow:0 10px 30px rgba(0,0,0,.15);
}}

.btn{{
  background:var(--red);
  color:white;
  border:none;
  padding:12px 18px;
  cursor:pointer;
  border-radius:4px;
}}

.btn:hover{{
  background:var(--darkred);
}}
</style>
</head>
<body>

<header class="site-header">
  <div class="logo-row">
    <img class="logo" src="data:image/webp;base64,{b64}">
    <div>
      <h1>DISTRICT ATTORNEY'S OFFICE</h1>
      <div class="subtitle">County of Los Santos</div>
    </div>
    <img class="logo" src="data:image/webp;base64,{b64}">
  </div>
</header>

<div class="content">
  <h2>Generador Legal</h2>
  <p>Los logos han sido reemplazados correctamente.</p>

  <button class="btn">Generar Documento</button>
</div>

</body>
</html>
"""

Path(out_path).write_text(html, encoding="utf-8")

print(f"Archivo generado: {out_path}")
