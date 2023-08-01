---
layout: default
title: My Photo Gallery
background_image: "{{ site.background_images | sample }}"
---

<style>
  .center-text {
    text-align: center;
    margin: 0 auto;
    max-width: 800px;
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

  /* Scale the thumbnails to 30% of the original size */
  .thumbnail img {
    max-width: 10%;
    max-height: auto;
  }
</style>

<div class="center-text">
  {% include_relative _includes/introduction.html %}
</div>

<!-- Galéria section -->
<div class="center-text">
  <h2>Galéria</h2>
  <!-- Add any additional content or description for the gallery here -->
</div>

<!-- Hidden gallery container for Galéria 1 -->
<div id="hidden-gallery-ajandek" style="display: none;"></div>

<!-- Button to trigger Galéria 1 -->
<div class="center-text">
  <button onclick="showAjandekGallery()">Ajándék</button>
</div>

<!-- Galéria section -->
<div class="center-text">
  <h2> </h2>
  <!-- Add any additional content or description for the gallery here -->
</div>

<!-- Hidden gallery container for Galéria 2 -->
<div id="hidden-gallery-bogrek" style="display: none;"></div>

<!-- Button to trigger Galéria 2 -->
<div class="center-text">
  <button onclick="showBogrekGallery()">Bögrék</button>
</div>

<!-- Galéria section -->
<div class="center-text">
  <h2> </h2>
  <!-- Add any additional content or description for the gallery here -->
</div>

<!-- Hidden gallery container for Galéria 3 -->
<div id="hidden-gallery-mandalak" style="display: none;"></div>

<!-- Button to trigger Galéria 3 -->
<div class="center-text">
  <button onclick="showMandalakGallery()">Mandalák</button>
</div>

<!-- Kapcsolat section -->
<div class="center-text">
  <h2>Kapcsolat</h2>
  <p>
    További festményekért és árakért érdeklődj: hjudit64(kukac)gmail.com címen
  </p>
</div>

<!-- simplelightbox scripts and styles -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.css">

<!-- Function for Galéria 1 -->
<script>
  function showAjandekGallery() {
    var button = document.querySelector('button[onclick="showAjandekGallery()"]');
    var hiddenGallery = document.getElementById('hidden-gallery-ajandek');

    if (hiddenGallery.style.display === 'none') {
      getImagesFromRepo('ajandek').then(function (imageURLs) {
        hiddenGallery.innerHTML = ''; // Clear previous images
        for (var i = 0; i < imageURLs.length; i++) {
          var aTag = document.createElement('a');
          aTag.href = imageURLs[i];
          aTag.setAttribute('data-lightbox', 'gallery-ajandek');
          aTag.setAttribute('data-title', 'Photo ' + (i + 1));

          var imgTag = document.createElement('img');
          imgTag.src = imageURLs[i];
          imgTag.alt = 'Photo ' + (i + 1);

          var thumbnailDiv = document.createElement('div');
          thumbnailDiv.classList.add('thumbnail');
          thumbnailDiv.appendChild(imgTag);
          aTag.appendChild(thumbnailDiv);
          hiddenGallery.appendChild(aTag);
        }

        hiddenGallery.style.display = 'flex';
        button.innerHTML = 'Bezárás';

        var gallery = new SimpleLightbox('#hidden-gallery-ajandek a');
      });
    } else {
      hiddenGallery.innerHTML = '';
      hiddenGallery.style.display = 'none';
      button.innerHTML = 'Ajándék';
    }
  }
</script>

<!-- Function for Galéria 2 -->
<script>
  function showBogrekGallery() {
    var button = document.querySelector('button[onclick="showBogrekGallery()"]');
    var hiddenGallery = document.getElementById('hidden-gallery-bogrek');

    if (hiddenGallery.style.display === 'none') {
      getImagesFromRepo('bogrek').then(function (imageURLs) {
        hiddenGallery.innerHTML = ''; // Clear previous images
        for (var i = 0; i < imageURLs.length; i++) {
          var aTag = document.createElement('a');
          aTag.href = imageURLs[i];
          aTag.setAttribute('data-lightbox', 'gallery-bogrek');
          aTag.setAttribute('data-title', 'Photo ' + (i + 1));

          var imgTag = document.createElement('img');
          imgTag.src = imageURLs[i];
          imgTag.alt = 'Photo ' + (i + 1);

          var thumbnailDiv = document.createElement('div');
          thumbnailDiv.classList.add('thumbnail');
          thumbnailDiv.appendChild(imgTag);
          aTag.appendChild(thumbnailDiv);
          hiddenGallery.appendChild(aTag);
        }

        hiddenGallery.style.display = 'flex';
        button.innerHTML = 'Bezárás';

        var gallery = new SimpleLightbox('#hidden-gallery-bogrek a');
      });
    } else {
      hiddenGallery.innerHTML = '';
      hiddenGallery.style.display = 'none';
      button.innerHTML = 'Bögrék';
    }
  }
</script>

<!-- Function for Galéria 3 -->
<script>
  function showMandalakGallery() {
    var button = document.querySelector('button[onclick="showMandalakGallery()"]');
    var hiddenGallery = document.getElementById('hidden-gallery-mandalak');

    if (hiddenGallery.style.display === 'none') {
      getImagesFromRepo('mandalak').then(function (imageURLs) {
        hiddenGallery.innerHTML = ''; // Clear previous images
        for (var i = 0; i < imageURLs.length; i++) {
          var aTag = document.createElement('a');
          aTag.href = imageURLs[i];
          aTag.setAttribute('data-lightbox', 'gallery-mandalak');
          aTag.setAttribute('data-title', 'Photo ' + (i + 1));

          var imgTag = document.createElement('img');
          imgTag.src = imageURLs[i];
          imgTag.alt = 'Photo ' + (i + 1);

          var thumbnailDiv = document.createElement('div');
          thumbnailDiv.classList.add('thumbnail');
          thumbnailDiv.appendChild(imgTag);
          aTag.appendChild(thumbnailDiv);
          hiddenGallery.appendChild(aTag);
        }

        hiddenGallery.style.display = 'flex';
        button.innerHTML = 'Bezárás';

        var gallery = new SimpleLightbox('#hidden-gallery-mandalak a');
      });
    } else {
      hiddenGallery.innerHTML = '';
      hiddenGallery.style.display = 'none';
      button.innerHTML = 'Mandalák';
    }
  }
</script>

<script>
  function getImagesFromRepo(folder) {
    var username = 'balazsvamosi1';
    var repo = 'balazsvamosi.github.io';
    var path = 'assets/images/' + folder; // Set the correct path here

    return fetch('https://api.github.com/repos/' + username + '/' + repo + '/contents/' + path)
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
