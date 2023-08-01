---
layout: default
title: My Photo Gallery
background_image: "{{ site.background_images | sample }}"
---

<div class="center-text">
  <h1>Üdvözöllek az oldalamon askhgfkisu! </h1>

  <p>
   Engedd meg, hogy bemutassam magam. A nevem Vámosiné Horváth Judit, és az alkotás, a színek és a művészet iránti szenvedélyem mindig is kísértett. Az életem jelenlegi részét a festészetnek és a kreativitásnak szenteltem, és örömmel osztom meg veled ezeket a műalkotásokat, amelyeket készítettem az elmúlt időszakban.

A munkáim inspirációját a hagyományos ausztrál őslakosok, az Aboriginal Australians pontfestészete adja. Ez az ősi művészetforma a homokba és a földre való apró pontokkal történő ábrázolást jelenti, amelyeket szent jelentésekkel és történetekkel ruháztak fel a törzsi kultúrákban. Mindegyik festmény egyedi rituáléhoz és szertartáshoz kapcsolódott, és a beavatatlanok számára soha nem voltak láthatók, hiszen a földet mindig elsimították a szertartás után, hogy a mintákat a szent titokkal együtt megőrizzék.

Ezeket a hagyományokat és az ausztrál kultúra mély tiszteletét hordozva alkottam meg ezeket a festményeket. Remélem, hogy a művészeti alkotásaimban megtalálod azt a kis csodát, amelyet én is átéltem az alkotásuk közben.

Az online galériámban számos kép található, amelyek között megtalálod az örömteli és mély gondolatokat ébresztő alkotásokat is. Nézz körül, és fedezd fel a színek és formák gazdag világát!

Ha bármilyen kérdésed van az alkotásaimmal kapcsolatban vagy érdeklődsz egy-egy festményem iránt, ne habozz felvenni velem a kapcsolatot. Örömmel válaszolok minden megkeresésre.

Köszönöm, hogy meglátogattál, és remélem, hogy az alkotásaim által éppolyan élményeket élhetsz át, mint én alkotás közben..
  </p>

  <button id="gallery-button1" onclick="showGallery('ajandek')">Galéria 1</button>
  <button id="gallery-button2" onclick="showGallery('bogrek')">Galéria 2</button>
  <button id="gallery-button3" onclick="showGallery('mandalak')">Galéria 3</button>

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
</div>

<div class="center-text">
  <h2>Kapcsolat</h2>
  <p>
    További festményekért és árakért érdeklődj: hjudit64(kukac)gmail.com címen
  </p>
</div>
