---
layout: default
title: My Photo Gallery
background_image: "{{ site.background_images | sample }}"
---

<style>
  /* Your existing styles here */
</style>

<div class="center-text">
  {% include_relative _includes/introduction.html %}
</div>

<!-- Galéria section -->
<div class="center-text">
  <h2>Galéria 4 </h2>
  <!-- Add any additional content or description for the gallery here -->
</div>

<!-- Buttons to trigger the galleries -->
<div class="center-buttons">
  <button onclick="showAjandekGallery()">Ajándék</button>
  <button onclick="showBogrekGallery()">Bögrék</button>
  <button onclick="showMandalakGallery()">Mandalák</button>
</div>

<!-- Hidden gallery container -->
<div id="hidden-gallery" style="display: none;"></div>

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

<script>
  function showAjandekGallery() {
    showGallery('ajandek');
  }

  function showBogrekGallery() {
    showGallery('bogrek');
  }

  function showMandalakGallery() {
    showGallery('mandalak');
  }

  function showGallery(folder) {
    var button = document.getElementById(`gallery-button${folder}`);
    var hiddenGallery = document.getElementById('hidden-gallery');

    if (hiddenGallery.style.display === 'none') {
      getImagesFromRepo(folder).then(function (imageURLs) {
        for (var i = 0; i < imageURLs.length; i++) {
          var aTag = document.createElement('a');
          aTag.href = imageURLs[i];
          aTag.setAttribute('data-lightbox', `gallery-${folder}`);
          aTag.setAttribute('data-title', 'Photo ' + (i + 1));

          var imgTag = document.createElement('img');
          imgTag.src = imageURLs[i];
          imgTag.alt = 'Photo ' + (i + 1);

          aTag.appendChild(imgTag);
          hiddenGallery.appendChild(aTag);
        }

        hiddenGallery.style.display = 'flex';
        button.innerHTML = 'Bezárás';

        var gallery = new SimpleLightbox(`#hidden-gallery [data-lightbox="gallery-${folder}"]`);
      });
    } else {
      hiddenGallery.innerHTML = '';
      hiddenGallery.style.display = 'none';
      button.innerHTML = `Galéria ${folder}`;
    }
  }

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
