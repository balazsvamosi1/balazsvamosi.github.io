---
layout: default
title: My Photo Gallery
---

# Üdvözöllek az oldalamon

A pontfestészet az ausztrál őslakosok (Aboriginal Australians) művészetének egyedülálló és szerves része. Kezdetben a homokba, földre pöttyözték az ábrákat, mintákat, mely törzsi történeteknek szent jelentései voltak. Egy-egy festmény adott szertartáshoz, rituáléhoz tartozott. A beavatatlanok soha nem láthatták ezeket a rajzokat, szent mintákat, mivel a földet újra elsimították a szertartás után.

## Galéria

<div id="hidden-gallery" style="display: none;">
  {% for file in site.static_files %}
    {% if file.extname == '.jpeg' or file.extname == '.jpg' %}
      <a href="{{ file.path | relative_url }}" data-lightbox="gallery" data-title="{{ file.name }}">
        <img src="{{ file.path | relative_url }}" alt="{{ file.name }}">
      </a>
    {% endif %}
  {% endfor %}
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.css">

<button id="gallery-button">Galéria</button>

<script>
  document.getElementById('gallery-button').addEventListener('click', function() {
    var hiddenGallery = document.getElementById('hidden-gallery');
    hiddenGallery.style.display = 'block';

    var gallery = new SimpleLightbox('#hidden-gallery a');

    // Hide the button after the gallery is opened
    this.style.display = 'none';
  });
</script>
