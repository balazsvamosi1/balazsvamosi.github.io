---
layout: default
title: My Photo Gallery
---

# Üdvözöllek az oldalamon

A pontfestészet az ausztrál őslakosok (Aboriginal Australians) művészetének egyedülálló és szerves része. Kezdetben a homokba, földre pöttyözték az ábrákat, mintákat, mely törzsi történeteknek szent jelentései voltak. Egy-egy festmény adott szertartáshoz, rituáléhoz tartozott. A beavatatlanok soha nem láthatták ezeket a rajzokat, szent mintákat, mivel a földet újra elsimították a szertartás után.

## Galéria

<button id="gallery-button" onclick="showGallery()">Galéria</button>

<div id="hidden-gallery" style="display: none;">
  {% for file in site.static_files %}
    {% if file.extname == '.jpeg' or file.extname == '.jpg' %}
      {% if file.tags contains 'include-in-gallery' %}
        <a href="{{ file.path | relative_url }}" data-lightbox="gallery" data-title="{{ file.name }}">
          <img src="{{ file.path | relative_url }}" alt="{{ file.name }}">
        </a>
      {% endif %}
    {% endif %}
  {% endfor %}
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.css">

<style>
  .gallery-container {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
  }
</style>

<script>
  function showGallery() {
    var button = document.getElementById('gallery-button');
    var hiddenGallery = document.getElementById('hidden-gallery');
    
    if (hiddenGallery.style.display === 'none') {
      hiddenGallery.style.display = 'flex';
      button.innerHTML = 'Bezárás';
    } else {
      hiddenGallery.style.display = 'none';
      button.innerHTML = 'Galéria';
    }

    var gallery = new SimpleLightbox('#hidden-gallery a');
  }
</script>
