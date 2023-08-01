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

  .center-buttons {
    text-align: center;
    margin-top: 20px;
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

  #hidden-gallery img {
    max-width: 70%;
    max-height: 70vh;
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

<!-- Buttons to trigger the galleries -->
<div class="center-buttons">
  <button id="gallery-button1" onclick="showGallery('ajandek')">Ajándék</button>
  <button id="gallery-button2" onclick="showGallery('bogrek')">Bögrék</button>
  <button id="gallery-button3" onclick="showGallery('mandalak')">Mandalák</button>
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

<script src="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe-ui-default.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/default-skin/default-skin.min.css">

<script>
  function showGallery(folder) {
    var button = document.getElementById(`gallery-button${folder}`);
    var hiddenGallery = document.getElementById('hidden-gallery');

    if (hiddenGallery.style.display === 'none') {
      getImagesFromRepo(folder).then(function (imageURLs) {
        for (var i = 0; i < imageURLs.length; i++) {
          var aTag = document.createElement('a');
          aTag.href = imageURLs[i];

          var imgTag = document.createElement('img');
          imgTag.src = imageURLs[i];
          imgTag.alt = 'Photo ' + (i + 1);

          aTag.appendChild(imgTag);
          hiddenGallery.appendChild(aTag);
        }

        hiddenGallery.style.display = 'flex';
        button.innerHTML = 'Bezárás';

        initPhotoSwipeFromDOM(`#hidden-gallery`);
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

  // Function to initialize PhotoSwipe from the gallery links
  function initPhotoSwipeFromDOM(gallerySelector) {
  // Get the gallery element
  var galleryElement = document.querySelector(gallerySelector);

  // Find all the link elements within the gallery element
  var galleryItems = galleryElement.getElementsByTagName('a');

  // Create an array to store the slides
  var slides = [];

  // Loop through each link element and add it to the slides array
  for (var i = 0; i < galleryItems.length; i++) {
    var item = galleryItems[i];

    // Create a slide object for each link element
    var slide = {
      src: item.getAttribute('href'),
      w: parseInt(item.getAttribute('data-width')),
      h: parseInt(item.getAttribute('data-height')),
      title: item.getAttribute('data-title')
    };

    // Add the slide object to the slides array
    slides.push(slide);
  }

  // Define PhotoSwipe options (customize as needed)
  var options = {
    index: 0, // Starting slide index
    bgOpacity: 0.8, // Background opacity
    history: false, // Disable history/back button
    showHideOpacity: true // Show/hide the gallery using opacity
  };

  // Generate PhotoSwipe instance
  var gallery = new PhotoSwipe(
    document.querySelectorAll('.pswp')[0],
    PhotoSwipeUI_Default,
    slides,
    options
  );

  // Bind event listener for close button click
  gallery.listen('close', function () {
    // Reset the gallery on close
    gallery.close();
    gallery = null;
  });

  // Initialize PhotoSwipe
  gallery.init();
}
</script>
