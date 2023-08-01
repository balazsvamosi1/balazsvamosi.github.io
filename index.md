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

<!-- Script to initialize PhotoSwipe from the gallery links -->
<script>
  function initPhotoSwipeFromDOM(gallerySelector) {
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
</script>

<!-- Initialize PhotoSwipe after the content is loaded -->
<script>
  document.addEventListener('DOMContentLoaded', function () {
    initPhotoSwipeFromDOM('#hidden-gallery');
  });
</script>
