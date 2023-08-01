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

<!-- Hidden gallery container -->
<div id="hidden-gallery" style="display: none;"></div>

<!-- Buttons to trigger the galleries -->
<div class="center-buttons">
  <button id="gallery-button1" onclick="showGallery('ajandek')">Ajándék</button>
  <button id="gallery-button2" onclick="showGallery('bogrek')">Bögrék</button>
  <button id="gallery-button3" onclick="showGallery('mandalak')">Mandalák</button>
</div>

<!-- Kapcsolat section -->
<div class="center-text">
  <h2>Kapcsolat</h2>
  <p>
    További festményekért és árakért érdeklődj: hjudit64(kukac)gmail.com címen
  </p>
</div>

<!-- PhotoSwipe scripts and styles -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe-ui-default.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/default-skin/default-skin.min.css">

<!-- Initialize PhotoSwipe for each gallery -->
<script>
  function initPhotoSwipe(gallerySelector) {
    var parseThumbnailElements = function(el) {
      // Function to parse gallery links and return PhotoSwipe items array
      // You may need to modify this based on your specific image source
      var thumbElements = el.childNodes;
      var items = [];
      for (var i = 0; i < thumbElements.length; i++) {
        var linkEl = thumbElements[i].querySelector('a');
        var size = linkEl.getAttribute('data-size').split('x');
        var item = {
          src: linkEl.getAttribute('href'),
          w: parseInt(size[0], 10),
          h: parseInt(size[1], 10),
          title: linkEl.getAttribute('data-title')
        };
        items.push(item);
      }
      return items;
    };

    // Function to open the PhotoSwipe gallery
    var openPhotoSwipe = function(index, galleryElement) {
      var pswpElement = document.querySelectorAll('.pswp')[0];
      var items = parseThumbnailElements(galleryElement);
      var options = {
        // Your options for PhotoSwipe (e.g., shareButtons, fullscreen, etc.)
        index: index
      };
      var gallery = new PhotoSwipe(pswpElement, PhotoSwipeUI_Default, items, options);
      gallery.init();
    };

    // Find the gallery links within the specified selector
    var galleryElements = document.querySelectorAll(gallerySelector);
    for (var i = 0; i < galleryElements.length; i++) {
      galleryElements[i].setAttribute('data-pswp-uid', i + 1);
      galleryElements[i].onclick = function(e) {
        e.preventDefault();
        var index = parseInt(this.getAttribute('data-pswp-uid'), 10) - 1;
        openPhotoSwipe(index, this);
      };
    }
  }

  // Function to show the gallery for each button
  function showGallery(folder) {
    var button = document.getElementById(`gallery-button${folder}`);
    var hiddenGallery = document.getElementById('hidden-gallery');

    if (hiddenGallery.style.display === 'none') {
      getImagesFromRepo(folder).then(function (imageURLs) {
        for (var i = 0; i < imageURLs.length; i++) {
          var aTag = document.createElement('a');
          aTag.href = imageURLs[i];
          aTag.setAttribute('data-size', '800x600'); // Set the size of the image (you can adjust this)
          aTag.setAttribute('data-title', 'Image ' + (i + 1));

          var imgTag = document.createElement('img');
          imgTag.src = imageURLs[i];
          imgTag.alt = 'Image ' + (i + 1);

          aTag.appendChild(imgTag);
          hiddenGallery.appendChild(aTag);
        }

        hiddenGallery.style.display = 'flex';
        button.innerHTML = 'Bezárás';

        initPhotoSwipe(`#hidden-gallery`);
      });
    } else {
      hiddenGallery.innerHTML = '';
      hiddenGallery.style.display = 'none';
      button.innerHTML = `Galéria ${folder}`;
    }
  }
</script>
