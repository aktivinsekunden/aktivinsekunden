# Aktiv in Sekunden
Auf dieser Seite stehen einige kostenfreie Materialien zur Förderung von Aktivität, Beweglichkeit und Entspannung im Alltag zur Verfügung, die an der Hochschule Niederrhein im Rahmen des BMFTR-geförderten Projekts "ActivitySnippets" entwickelt wurden.

Unser Motto: *"Jede Bewegung zählt"*

Viel Spaß!

## Toolbox
Kurze Übungen mit Bildern und Textanleitungen.

<!-- Filtermöglichkeiten -->
<div style="margin-bottom: 20px; padding: 15px; background-color: #f5f5f5; border-radius: 8px;">
  <div style="margin-bottom: 12px;">
    <strong style="font-size:14px;">Übungsart:</strong><br>
    <button class="filter-btn" data-filter="uebungsart" data-value="alle" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Alle</button>
    <button class="filter-btn" data-filter="uebungsart" data-value="aktivitaet" style="margin: 5px 5px 5px 0; padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Aktivität</button>
    <button class="filter-btn" data-filter="uebungsart" data-value="beweglichkeit" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Beweglichkeit</button>
    <button class="filter-btn" data-filter="uebungsart" data-value="entspannung" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Entspannung</button>
  </div>
  <div>
    <strong style="font-size:14px;">Gegenstände:</strong><br>
    <button class="filter-btn" data-filter="gegenstand" data-value="alle" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Alle</button>
    <button class="filter-btn" data-filter="gegenstand" data-value="keine" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Keine</button>
    <button class="filter-btn" data-filter="gegenstand" data-value="stuhl" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Stuhl</button>
    <button class="filter-btn" data-filter="gegenstand" data-value="tisch" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Tisch</button>
    <button class="filter-btn" data-filter="gegenstand" data-value="sonstige" style="margin: 5px 5px 5px 0;padding:5px 10px; border-radius:5px; border:1px solid #007aad; background:white; color:#007aad; font-size:12px; cursor:pointer;">Sonstige</button>
  </div>
  <div style="margin-top: 12px;">
  <button id="reset-filters" style="padding: 5px 10px; background-color: #999; color: white; border: none; border-radius: 5px; cursor: pointer; font-size:13px;">
    Filter löschen
  </button>
</div>
</div>

<!-- Galerie -->
<div id="gallery-wrapper" style="margin-bottom: 30px;">
  <div style="display: flex; align-items: center; gap: 15px;">
    <button id="prev-btn" style="padding: 10px 15px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 18px;">←</button>
    
    <div style="flex: 1; position: relative;">
      <img id="gallery-image" src="" alt="Übung" style="width: 100%; height: auto; border-radius: 8px; cursor: pointer; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
      <p id="image-title" style="text-align: center; margin-top: 10px; font-weight: bold;"></p>
    </div>
    
    <button id="next-btn" style="padding: 10px 15px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 18px;">→</button>
  </div>
  
  <div style="text-align: center; margin-top: 15px;">
    <button id="fullscreen-btn" style="padding: 8px 16px; background-color: #555; color: white; border: none; border-radius: 5px; cursor: pointer;">🔍 Vergrößern</button>
    <span id="image-counter" style="margin-left: 15px; font-size: 11px;"></span>
  </div>
</div>

<!-- Vollbild-Modal -->
<div id="fullscreen-modal" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.95); z-index: 1000; align-items: center; justify-content: center;">
  <img id="fullscreen-image" src="" alt="Übung Vollbild" style="max-width: 90%; max-height: 90%; object-fit: contain;">
  <button id="close-fullscreen" style="position: absolute; top: 20px; right: 30px; background-color: white; color: black; border: none; padding: 10px 15px; font-size: 24px; cursor: pointer; border-radius: 5px;">✕</button>
</div>

<a href="assets/img/Toolbox.pdf" download="Toolbox.pdf">
  <button style="padding: 10px 20px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px;">
    Gesamte Toolbox (PDF) herunterladen
  </button>
</a>

<script>
let allImages = [];
let filteredImages = [];
let currentIndex = 0;
let filters = {
  uebungsart: new Set(),
  gegenstand: new Set()
};

function setBtnActive(btn, isActive) {
  btn.style.backgroundColor = isActive ? '#007aad' : 'white';
  btn.style.color = isActive ? 'white' : '#007aad';
}

// Startzustand: "Alle" Buttons aktiv markieren
document.querySelectorAll('.filter-btn[data-value="alle"]').forEach(b => setBtnActive(b, true));  

// Galerie-Daten laden
fetch('assets/gallery-config.json')
  .then(response => response.json())
  .then(data => {
    allImages = data.toolbox;
    applyFilters();
    renderImage();
  })
  .catch(error => console.log('Galerie konnte nicht geladen werden:', error));

// Filter anwenden
function applyFilters() {
  filteredImages = allImages.filter(img => {
    const uebungMatch =
      filters.uebungsart.size === 0 || filters.uebungsart.has(img.uebungsart);

    // gegenstand kann String ODER Array sein:
    const imgG = Array.isArray(img.gegenstand) ? img.gegenstand : [img.gegenstand];

    const gegenstandMatch =
      filters.gegenstand.size === 0 || imgG.some(g => filters.gegenstand.has(g));

    return uebungMatch && gegenstandMatch;
  });

  currentIndex = 0;
}

// Bild rendern
function renderImage() {
  if (filteredImages.length === 0) {
    document.getElementById('gallery-image').src = '';
    document.getElementById('image-title').textContent = 'Keine Bilder gefunden';
    document.getElementById('image-counter').textContent = '0 / 0';
    return;
  }
  
  const img = filteredImages[currentIndex];
  document.getElementById('gallery-image').src = img.src;
  document.getElementById('image-title').textContent = img.title;
  document.getElementById('fullscreen-image').src = img.src;
  document.getElementById('image-counter').textContent = `${currentIndex + 1} / ${filteredImages.length}`;
}

// Filter-Button Event-Listener
function setBtnActive(btn, isActive) {
  btn.style.backgroundColor = isActive ? '#007aad' : 'white';
  btn.style.color = isActive ? 'white' : '#007aad';
  btn.style.borderColor = '#007aad'; // wichtig: Rand bleibt immer blau
}

document.querySelectorAll('.filter-btn').forEach(btn => {
  btn.addEventListener('click', (e) => {
    const filterType = e.target.dataset.filter;   // "uebungsart" | "gegenstand"
    const filterValue = e.target.dataset.value;   // z.B. "aktivitaet"

    // Sonderfall: "alle" => Set leeren (entspricht: nichts filtern)
    if (filterValue === 'alle') {
      filters[filterType].clear();

      // Buttons dieser Kategorie optisch zurücksetzen, "alle" aktiv markieren
      document.querySelectorAll(`.filter-btn[data-filter="${filterType}"]`).forEach(b => {
        setBtnActive(b, b.dataset.value === 'alle');
      });

      applyFilters();
      renderImage();
      return;
    }

    // "alle" deaktivieren, sobald ein echter Filter gewählt wird
    const alleBtn = document.querySelector(`.filter-btn[data-filter="${filterType}"][data-value="alle"]`);
    if (alleBtn) setBtnActive(alleBtn, false);

    // toggle: rein/raus aus dem Set
    if (filters[filterType].has(filterValue)) {
      filters[filterType].delete(filterValue);
      setBtnActive(e.target, false);
    } else {
      filters[filterType].add(filterValue);
      setBtnActive(e.target, true);
    }

    // Wenn nichts mehr ausgewählt ist, "alle" wieder aktiv markieren
    if (filters[filterType].size === 0 && alleBtn) {
      setBtnActive(alleBtn, true);
    }

    applyFilters();
    renderImage();
  });
});

// Navigation
document.getElementById('prev-btn').addEventListener('click', () => {
  currentIndex = (currentIndex - 1 + filteredImages.length) % filteredImages.length;
  renderImage();
});

document.getElementById('next-btn').addEventListener('click', () => {
  currentIndex = (currentIndex + 1) % filteredImages.length;
  renderImage();
});

// Vollbild
document.getElementById('fullscreen-btn').addEventListener('click', () => {
  document.getElementById('fullscreen-modal').style.display = 'flex';
});

document.getElementById('close-fullscreen').addEventListener('click', () => {
  document.getElementById('fullscreen-modal').style.display = 'none';
});

// Auch durch Klick auf das Bild vergrößern
document.getElementById('gallery-image').addEventListener('click', () => {
  document.getElementById('fullscreen-modal').style.display = 'flex';
});

// Reset-Button
document.getElementById('reset-filters')?.addEventListener('click', () => {
  filters.uebungsart.clear();
  filters.gegenstand.clear();

  document.querySelectorAll('.filter-btn').forEach(b => setBtnActive(b, false));
  document.querySelectorAll('.filter-btn[data-value="alle"]').forEach(b => setBtnActive(b, true));

  applyFilters();
  renderImage();
});  
</script>

## Poster
Vier Poster mit Übungsbeispielen und Ideen zur Ritualisierung im Alltag.

<div style="display:flex; align-items:center; gap:20px; margin-bottom:25px; flex-wrap:wrap;">

  <img src="assets/img/Poster_Abbildung.png" 
       alt="Poster Vorschau Aktiv in Sekunden"
       style="width:220px; border-radius:8px; box-shadow:0 4px 6px rgba(0,0,0,0.1);">

  <a href="assets/img/Poster_Aktiv_in_Sekunden.pdf" download="Poster_Aktiv_in_Sekunden.pdf">
    <button style="padding: 10px 20px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px;">
      zum PDF
    </button>
  </a>

</div>

## 30-Tage-Challenge
Challenge-Vorlagen, um Erfolge zu tracken und im Team mit- bzw. gegeinander anzutreten.

<div style="display:flex; align-items:center; gap:20px; margin-bottom:25px; flex-wrap:wrap;">

  <img src="assets/img/Challenge_Abbildung.png" 
       alt="Challenge Vorschau"
       style="width:220px; border-radius:8px; box-shadow:0 4px 6px rgba(0,0,0,0.1);">

  <a href="assets/img/Aktiv_Challenge.pdf" download="Aktiv_Challenge.pdf">
    <button style="padding: 10px 20px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px;">
      zum PDF
    </button>
  </a>

</div>

## Sticker und Hintergrundbilder
Zur Erinnerung an aktive Sekunden.

<div style="display:flex; align-items:center; gap:20px; margin-bottom:25px; flex-wrap:wrap;">

  <img src="assets/img/Sticker_Abbildung.png" 
       alt="Sticker Vorschau"
       style="width:220px; border-radius:8px; box-shadow:0 4px 6px rgba(0,0,0,0.1);">

  <a href="assets/img/Sticker_Aktiv_in_Sekunden.pdf" download="Sticker_Aktiv_in_Sekunden.pdf">
    <button style="padding: 10px 20px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px;">
      zum PDF
    </button>
  </a>

</div>

<div style="display:flex; align-items:center; gap:20px; margin-bottom:25px; flex-wrap:wrap;">

  <img src="assets/img/Hintergrundbilder_Abbildung.png" 
       alt="Sticker Vorschau"
       style="width:220px; border-radius:8px; box-shadow:0 4px 6px rgba(0,0,0,0.1);">

  <a href="assets/img/Hintergrundbilder.pdf" download="Hintergrundbilder.pdf">
    <button style="padding: 10px 20px; background-color: #007aad; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px;">
      zum PDF
    </button>
  </a>

</div>

# Kontakt
**ActivitySnippets-Team, Hochschule Niederrhein**

Vertr.Prof. Dr. sc. med. Lukas Streese-Schüler

Leonie Reimann

Christina Arnold


E-Mail: [activitysnippets@hs-niederrhein.de](mailto:activitysnippets@hs-niederrhein.de)

Hochschul-Webseite: [https://www.hs-niederrhein.de/gesundheitswesen/forschung/projekt-activity-snippets/](https://www.hs-niederrhein.de/gesundheitswesen/forschung/projekt-activity-snippets/)


Das Projekt wurde gefördert vom Bundesministerium für Forschung, Technologie und Raumfahrt (BMFTR).
