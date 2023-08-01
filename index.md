---
layout: default
title: My Photo Gallery
background_image: "{{ site.background_images | sample }}"
---

<div class="center-text">
  <h1>Üdvözöllek az oldalamon !TEST PAGE22! </h1>

  <p>
   Engedd meg, hogy bemutassam magam. A nevem Vámosiné Horváth Judit, és az alkotás, a színek és a művészet iránti szenvedélyem mindig is kísértett. Az életem jelenlegi részét a festészetnek és a kreativitásnak szenteltem, és örömmel osztom meg veled ezeket a műalkotásokat, amelyeket készítettem az elmúlt időszakban.

   A munkáim inspirációját a hagyományos ausztrál őslakosok, az Aboriginal Australians pontfestészete adja. Ez az ősi művészetforma a homokba és a földre való apró pontokkal történő ábrázolást jelenti, amelyeket szent jelentésekkel és történetekkel ruháztak fel a törzsi kultúrákban.

   Ezeket a hagyományokat és az ausztrál kultúra mély tiszteletét hordozva alkottam meg ezeket a festményeket. Remélem, hogy a művészeti alkotásaimban megtalálod azt a kis csodát, amelyet én is átéltem az alkotásuk közben.

   Az online galériámban számos kép található, amelyek között megtalálod az örömteli és mély gondolatokat ébresztő alkotásokat is. Nézz körül, és fedezd fel a színek és formák gazdag világát!

   Ha bármilyen kérdésed van az alkotásaimmal kapcsolatban vagy érdeklődsz egy-egy festményem iránt, ne habozz felvenni velem a kapcsolatot. Örömmel válaszolok minden megkeresésre.

   Köszönöm, hogy meglátogattál, és remélem, hogy az alkotásaim által éppolyan élményeket élhetsz át, mint én alkotás közben..
  </p>

  <div class="center-text">
    <h2>Galéria</h2>
    <p></p>
  </div>

  <button id="gallery-button1" onclick="showGallery('ajandek')">Ajándék</button>
  <button id="gallery-button2" onclick="showGallery('bogrek')">Bögrék</button>
  <button id="gallery-button3" onclick="showGallery('mandalak')">Mandalák</button>

  <div id="hidden-gallery" style="display: none;"></div>

  <!-- PhotoSwipe CSS and JS files -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/default-skin/default-skin.min.css">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/photoswipe/4.1.3/photoswipe-ui-default.min.js"></script>
  
  <!-- SimpleLightbox CSS and JS files -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.css">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/simplelightbox/2.7.0/simple-lightbox.min.js"></script>

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
</div>

<div class="center-text">
  <h2>Kapcsolat</h2>
  <p>
    További festményekért és árakért érdeklődj: hjudit64(kukac)gmail.com címen
  </p>
</div>

 <script>
  function showGallery(folder) {
    // Code for showing and hiding the gallery, as provided in the previous responses
  }

  function getImagesFromRepo(folder) {
    // Code for fetching image URLs, as provided in the previous responses
  }

  // Function to initialize PhotoSwipe from DOM elements
  function initPhotoSwipeFromDOM(gallerySelector) {
    var parseThumbnailElements = function(el) {
      // Implement your parsing logic for the thumbnail elements here
    };

    var openPhotoSwipe = function(index, galleryElement, disableAnimation, fromURL) {
      // Implement the logic to open PhotoSwipe here
    };

    // Loop through each gallery element and initialize PhotoSwipe for each one
    var galleryElements = document.querySelectorAll(gallerySelector);
    for (var i = 0; i < galleryElements.length; i++) {
      galleryElements[i].setAttribute('data-pswp-uid', i + 1);
      galleryElements[i].onclick = onThumbnailsClick;
    }

    // Function to handle the click event on the thumbnails
    var onThumbnailsClick = function(e) {
      e = e || window.event;
      e.preventDefault ? e.preventDefault() : e.returnValue = false;

      var eTarget = e.target || e.srcElement;

      // Find the root of the clicked element, which should be the gallery container
      var clickedGallery = eTarget.closest(gallerySelector);
      if (!clickedGallery) {
        return;
      }

      // Parse the thumbnail elements to get the index and other relevant data
      var index = Array.prototype.indexOf.call(galleryElements, clickedGallery);
      if (index >= 0) {
        openPhotoSwipe(index, clickedGallery);
      }
      return false;
    };
  }

  // Call the function to initialize PhotoSwipe from the DOM elements
  document.addEventListener('DOMContentLoaded', function() {
    initPhotoSwipeFromDOM('[data-lightbox]');
  });
</script>
