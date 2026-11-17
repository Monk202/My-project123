
Hey .I have created this from Basic HTML codes.
<!
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Stepwells of Mandi District - NCSC Project</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css">
<style>
  * { box-sizing: border-box; }
  body { font-family: Arial, sans-serif; margin: 0; background: #f3f1ea; color: #222; line-height: 1.5; }
  header { background: linear-gradient(135deg, #1f4d2b, #3f7d4e); color: white; padding: 22px 14px; text-align: center; }
  header h1 { margin: 0 0 8px; font-size: 24px; }
  header p { margin: 0; font-size: 16px; }
  nav { background: #1f4d2b; text-align: center; padding: 8px; position: sticky; top: 0; z-index: 1000; }
  nav a { color: white; text-decoration: none; margin: 0 8px; font-size: 14px; }
  main { max-width: 950px; margin: auto; padding: 12px; }
  section { background: white; border-radius: 10px; padding: 14px; margin-bottom: 16px; box-shadow: 0 1px 4px rgba(0,0,0,0.15); }
  h2 { margin-top: 0; font-size: 19px; color: #1f4d2b; border-bottom: 2px solid #cfe3c8; padding-bottom: 6px; }
  .cards { display: flex; gap: 10px; flex-wrap: wrap; }
  .card { flex: 1; min-width: 130px; background: #e8f1e4; border-radius: 8px; padding: 12px; text-align: center; }
  .card b { display: block; font-size: 30px; color: #1f4d2b; }
  .card.bad { background: #fde8e6; }
  .card.bad b { color: #c0281c; }
  #map { height: 420px; border-radius: 8px; }
  button { background: #1f4d2b; color: white; border: none; border-radius: 6px; padding: 8px 12px; font-size: 14px; margin-top: 8px; }
  .scroll { overflow-x: auto; }
  table { border-collapse: collapse; width: 100%; font-size: 14px; }
  th, td { border: 1px solid #bbb; padding: 6px 8px; text-align: left; }
  th { background: #1f4d2b; color: white; }
  tr.row:hover { background: #f0f7ec; cursor: pointer; }
  tfoot td { font-weight: bold; background: #e8f1e4; }
  .note { font-size: 13px; color: #666; }
  .warn { background: #fff6dc; border-left: 4px solid #e0a800; padding: 8px 10px; font-size: 13px; margin-top: 10px; }
  .pin { width: 18px; height: 18px; background: #e02020; border: 2px solid white; border-radius: 50% 50% 50% 0; transform: rotate(-45deg); box-shadow: 0 0 3px rgba(0,0,0,0.6); }
  .label { font-size: 11px; font-weight: bold; background: white; border: 1px solid #e02020; color: #222; padding: 1px 4px; }
  .popimg { width: 100%; max-height: 160px; object-fit: cover; border-radius: 6px; margin: 6px 0 2px; display: block; }
  .nophoto { background: #eee; color: #777; text-align: center; padding: 18px 6px; border-radius: 6px; margin: 6px 0 2px; font-size: 12px; }
  .leaflet-popup-content { margin: 10px 12px; }
  ul { padding-left: 20px; margin: 6px 0; }
  footer { text-align: center; font-size: 13px; color: #666; padding: 14px; }
</style>
</head>
<body>

<header>
  <h1>Stepwells of Mandi District</h1>
  <p>My name is Anshul and this is for my NCSC project.</p>
</header>

<nav>
  <a href="#about">About</a>
  <a href="#results">Results</a>
  <a href="#mapsec">Map</a>
  <a href="#table">Table</a>
  <a href="#science">Science</a>
</nav>

<main>

  <section id="about">
    <h2>About the Project</h2>
    <p>
      A <b>stepwell</b> (called <i>bavdi</i> in Himachal) is a traditional water source built with steps
      going down to the water. For years, stepwells gave clean water to people of Mandi district.
      In this project I located the stepwells of Mandi, collected water samples, and tested them
      to find out whether this water is still safe.
    </p>
  </section>

  <section id="results">
    <h2>Project Results</h2>
    <div class="cards">
      <div class="card"><b id="totalMapped">0</b>Stepwells located on map</div>
      <div class="card"><b>4</b>Water samples collected</div>
      <div class="card bad"><b>4</b>Stepwells failed in microbiological contamination test</div>
    </div>
    <p class="note">All 4 out of 4 samples (100%) failed the microbiological test.</p>
  </section>

  <section id="mapsec">
    <h2>Map of Mandi District</h2>
    <div id="map"></div>
    <button onclick="showTown()">Zoom to stepwells</button>
    <button onclick="showDistrict()">Show whole Mandi district</button>
    <p class="note">Red marks show stepwells. Tap a mark to see details.</p>
    <div class="warn">
      Note: The positions of the stepwells are approximate. They must be corrected with the exact
      GPS location (latitude/longitude) taken at each stepwell.
    </div>
  </section>

  <section id="table">
    <h2>Stepwell Details</h2>
    <div class="scroll">
      <table>
        <thead>
          <tr>
            <th>S.No.</th>
            <th>Stepwell Name</th>
            <th>Place</th>
            <th>Location (Lat, Long)</th>
            <th>Number of Stepwells</th>
          </tr>
        </thead>
        <tbody id="tableBody"></tbody>
        <tfoot>
          <tr><td colspan="4">Total</td><td id="footTotal">0</td></tr>
        </tfoot>
      </table>
    </div>
    <p class="note">Tap a row to see it on the map.</p>
  </section>

  <section id="science">
    <h2>The Science Behind the Test</h2>
    <ul>
      <li><b>Microbiological contamination</b> means that harmful germs (bacteria, viruses) are present in water.</li>
      <li><b>Coliform bacteria</b> and <b>E. coli</b> are used as indicators. They live in the gut of humans and animals, so finding them shows that sewage or animal waste has mixed with the water.</li>
      <li>As per Indian drinking water standard (BIS IS 10500), coliform bacteria should be <b>absent</b> in 100 ml of drinking water.</li>
      <li>Drinking contaminated water can cause diarrhoea, typhoid, cholera and jaundice.</li>
    </ul>
    <h2 style="margin-top:16px">What can be done?</h2>
    <ul>
      <li>Do not drink stepwell water directly. Boil it or treat it with chlorine first.</li>
      <li>Keep the stepwell and its surroundings clean, and keep drains and waste away from it.</li>
      <li>Cover the stepwell and clean it regularly.</li>
      <li>Protect these stepwells as heritage and use them again after proper treatment and testing.</li>
    </ul>
  </section>

</main>

<footer>Made by Anshul | NCSC Project | Mandi, Himachal Pradesh</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<script>
  // ------------------------------------------------------------
  // STEPWELL DATA
  // The names are real stepwells of Mandi given by the student.
  // The lat/lng numbers are APPROXIMATE - replace them with the real GPS
  // location. (On Google Maps: long-press on the stepwell and copy the numbers.)
  // To add one more stepwell, copy one line and change the values.
  // ------------------------------------------------------------
  var stepwells = [
    { name: "Jail Road Stepwell",                  place: "Mandi town",        lat: 31.7075, lng: 76.9335, count: 1 },
    { name: "Jenchu Nauna",                        place: "Mandi town",        lat: 31.7100, lng: 76.9300, count: 1 },
    { name: "Sadar Thana Paddal Stepwell",         place: "Paddal, Mandi",     lat: 31.7120, lng: 76.9390, count: 1 },
    { name: "Ram Mandir Paddal Stepwell",          place: "Paddal, Mandi",     lat: 31.7115, lng: 76.9405, count: 1 },
    { name: "Dugli Ghat Samkhetar Stepwell",       place: "Samkhetar, Mandi",  lat: 31.7040, lng: 76.9280, count: 1 },
    { name: "Laderi Bai Bagla Mohalla Stepwell",   place: "Bagla Mohalla",     lat: 31.7050, lng: 76.9250, count: 1 },
    { name: "Shiva Stepwell",                      place: "Mandi town",        lat: 31.7090, lng: 76.9270, count: 1 },
    { name: "Shamshan Ghat Bagla Stepwell",        place: "Bagla Mohalla",     lat: 31.7030, lng: 76.9235, count: 1 },
    { name: "Dhibba Stepwell",                     place: "Mandi",             lat: 31.7140, lng: 76.9330, count: 1 },
    { name: "Sauli Khad Stepwell",                 place: "Sauli Khad, Mandi", lat: 31.7000, lng: 76.9350, count: 1 },
    { name: "Sain Math Stepwell",                  place: "Mandi town",        lat: 31.7065, lng: 76.9310, count: 1 },
    { name: "Neeldhar Gurudwara Stepwell",         place: "Neeldhar, Mandi",   lat: 31.7160, lng: 76.9280, count: 1 }
  ];

  // OPTIONAL: paste Mandi district boundary (GeoJSON) here. null = no boundary.
  var mandiBoundary = null;

  // ---------------- Map ----------------
  var map = L.map('map');
  var mandiCenter = [31.708, 76.932];

  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 18,
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map);

  var boundaryLayer = null;
  if (mandiBoundary) {
    boundaryLayer = L.geoJSON(mandiBoundary, {
      style: { color: "#1f4d2b", weight: 3, fillColor: "#7bb36f", fillOpacity: 0.15 }
    }).addTo(map);
  }

  var redIcon = L.divIcon({ className: "", html: '<div class="pin"></div>', iconSize: [18, 18], iconAnchor: [9, 18], popupAnchor: [0, -18] });

  var tbody = document.getElementById("tableBody");
  var markers = [];
  var total = 0;

  stepwells.forEach(function (s, i) {
    total += s.count;

    var marker = L.marker([s.lat, s.lng], { icon: redIcon }).addTo(map);
    marker.bindTooltip(s.name, { permanent: true, direction: "right", offset: [8, -10], className: "label" });
    // Photo of this stepwell: photos/1.jpg, photos/2.jpg ... (same number as S.No. in the table)
    var photo = s.photo || ("photos/" + (i + 1) + ".jpg");
    marker.bindPopup(
      "<b>" + (i + 1) + ". " + s.name + "</b>" +
      '<a href="' + photo + '" target="_blank">' +
        '<img class="popimg" src="' + photo + '" alt="' + s.name + '" onerror="imgFail(this)">' +
        '<div class="nophoto" style="display:none">Photo coming soon</div>' +
      "</a>" +
      "Place: " + s.place + "<br>Location: " + s.lat + ", " + s.lng + "<br>Number of stepwells: " + s.count,
      { maxWidth: 240 }
    );
    markers.push(marker);

    var tr = document.createElement("tr");
    tr.className = "row";
    tr.innerHTML =
      "<td>" + (i + 1) + "</td><td>" + s.name + "</td><td>" + s.place + "</td>" +
      "<td>" + s.lat + ", " + s.lng + "</td><td>" + s.count + "</td>";
    tr.onclick = function () {
      map.setView([s.lat, s.lng], 16);
      marker.openPopup();
      document.getElementById("mapsec").scrollIntoView({ behavior: "smooth" });
    };
    tbody.appendChild(tr);
  });

  document.getElementById("totalMapped").textContent = total;
  document.getElementById("footTotal").textContent = total;

  // If a photo file is missing, show "Photo coming soon" instead of a broken image
  function imgFail(img) {
    img.style.display = "none";
    img.nextSibling.style.display = "block";
  }

  function showTown() {
    map.fitBounds(L.featureGroup(markers).getBounds().pad(0.2));
  }
  function showDistrict() {
    if (boundaryLayer) { map.fitBounds(boundaryLayer.getBounds()); }
    else { map.setView(mandiCenter, 9); }
  }
  showTown();
</script>

</body>
</html>
Precautions: It is just for research purpose.Data not to be used for any other purposes is prohibited.