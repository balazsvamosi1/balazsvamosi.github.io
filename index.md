---
layout: default
title: My Photo Gallery
background_image: "{{ site.background_images | sample }}"
---

<div class="center-text">
  <h1>Üdvözöllek az oldalamon!</h1>

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

    /* Make the "Galéria" button bigger on handy screens */
    @media (max-width: 767px) {
      #gallery-button {
        font-size: 1.5rem;
        padding: 10px 20px;
      }
    }
  </style>

  <script>
    function showGallery() {
      var button = document.getElementById('gallery-button');
      var hiddenGallery = document.getElementById('hidden-gallery');

      if (hiddenGallery.style.display === 'none') {
        getImagesFromRepo('ajendak').then(function (imageURLs) {
          for (var i = 0; i < imageURLs.length; i++) {
            var aTag = document.createElement('a');
            aTag.href = imageURLs[i];
            aTag.setAttribute('data-lightbox', 'gallery');
            aTag.setAttribute('data-title', 'Ajendak Image ' + (i + 1));

            var imgTag = document.createElement('img');
            imgTag.src = imageURLs[i];
            imgTag.alt = 'Ajendak Image ' + (i + 1);

            aTag.appendChild(imgTag);
            hiddenGallery.appendChild(aTag);
          }

          hiddenGallery.style.display = 'flex';
          button.innerHTML = 'Bezárás';

          var gallery = new SimpleLightbox('#hidden-gallery a');
        });
      } else {
        hiddenGallery.innerHTML = '';
        hiddenGallery.style.display = 'none';
        button.innerHTML = 'Galéria';
      }
    }

    function getImagesFromRepo(subfolder) {
      var username = 'balazsvamosi1';
      var repo = 'balazsvamosi.github.io';

      return fetch('https://api.github.com/repos/' + username + '/' + repo + '/contents/assets/images/' + subfolder)
        .then(function (response) {
          return response.json();
        })
        .then(function (data) {
          var imageUrls = data.filter(function (item) {
            return item.name.endsWith('.jpeg') || item.name.endsWith('.jpg');
          }).map(function (item) {
            return item.download_url;
          });

          return imageUrls;
        });
    }
  </script>
</div>

<div class="center-text">
  <h2>Kapcsolat</h2>
  <p>
    További festményekért és árakért érdeklődj: hjudit64(kukac)gmail.com címen
  </p>
</div>
