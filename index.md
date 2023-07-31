---
layout: default
title: My Photo Gallery
background_image: "{{ site.background_images | sample }}"
---

<div class="center-text">
  <h1>Üdvözöllek az oldalamon</h1>

  <p>
    A pontfestészet az ausztrál őslakosok (Aboriginal Australians) művészetének egyedülálló és szerves része. Kezdetben a homokba, földre pöttyözték az ábrákat, mintákat, mely törzsi történeteknek szent jelentései voltak. Egy-egy festmény adott szertartáshoz, rituáléhoz tartozott. A beavatatlanok soha nem láthatták ezeket a rajzokat, szent mintákat, mivel a földet újra elsimították a szertartás után.
  </p>

  <button id="gallery-button" onclick="showGallery()">Galéria</button>

  <div id="hidden-gallery" style="display: none;"></div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.css">

  <style>
    .center-text {
      text-align: center;
      margin: 0 auto;
      max-width: 800px; /* Set a maximum width for better presentation */
    }

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

    /* Scale the images in the pop-up to 70% of the screen size */
    #hidden-gallery img {
      max-width: 70%;
      max-height: 70vh;
    }
  </style>

  <script>
    // Rest of the JavaScript code for the gallery remains unchanged
    // ...
  </script>
</div>

<div class="center-text">
  <h2>Kapcsolat</h2>
  <p>
    További festményekért és árakért érdeklődj: email(kukac)email.com címen
  </p>
</div>
