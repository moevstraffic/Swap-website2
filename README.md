from pathlib import Path
from zipfile import ZipFile

base = Path("/mnt/data/velocity_auto_works_site")
base.mkdir(exist_ok=True)

index_html = """<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Velocity Auto Works | Dallas TX</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
<header><h1>Velocity Auto Works</h1><p>Dallas, TX • HEMI & Hellcat Swap Specialists</p></header>

<section class="hero">
<h2>Build Your Dream Mopar</h2>
<p>5.7 HEMI • 6.4 392 • 6.2 Hellcat Swaps</p>
</section>

<section>
<h2>Quote Calculator</h2>
<select id="engine">
<option value="6500">5.7 HEMI</option>
<option value="9500">6.4 392</option>
<option value="18000">6.2 Hellcat</option>
</select>

<select id="parts">
<option value="0">Customer Supplies Parts</option>
<option value="4000">Velocity Supplies Donor</option>
</select>

<button onclick="calc()">Calculate</button>
<h3 id="quote"></h3>
</section>

<section>
<h2>Book Appointment</h2>
<form>
<input placeholder="Name"><br>
<input placeholder="Phone"><br>
<input placeholder="Email"><br>
<textarea placeholder="Build Details"></textarea><br>
<button type="submit">Submit</button>
</form>
</section>

<section>
<h2>Financing Available</h2>
<ul>
<li>Affirm</li>
<li>LightStream</li>
<li>Snap Finance</li>
</ul>
</section>

<section>
<h2>Gallery</h2>
<div class="gallery">
<div>Charger Build</div>
<div>Challenger Build</div>
<div>Chrysler 300 Build</div>
</div>
</section>

<footer>903-240-9874 • Dallas, TX</footer>
<script src="script.js"></script>
</body>
</html>"""

styles_css = """
body{font-family:Arial,sans-serif;background:#111;color:#fff;margin:0}
header,.hero,section,footer{padding:20px;text-align:center}
header{background:#000}
.hero{background:#1b1b1b}
button{background:#c00;color:#fff;border:none;padding:10px 15px}
input,select,textarea{width:min(500px,90%);padding:10px;margin:5px}
.gallery{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px}
.gallery div{background:#222;padding:30px}
"""

script_js = """
function calc(){
 const e=parseInt(document.getElementById('engine').value);
 const p=parseInt(document.getElementById('parts').value);
 document.getElementById('quote').innerText='Estimated Price: $'+(e+p).toLocaleString();
}
"""

(base/"index.html").write_text(index_html)
(base/"styles.css").write_text(styles_css)
(base/"script.js").write_text(script_js)

zip_path = "/mnt/data/Velocity_Auto_Works_Website.zip"
with ZipFile(zip_path, "w") as z:
    z.write(base/"index.html", "index.html")
    z.write(base/"styles.css", "styles.css")
    z.write(base/"script.js", "script.js")

print(zip_path)
