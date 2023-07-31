---
layout: default
title: My Photo Gallery
---

# Üdvözöllek az oldalamon

A pontfestészet az ausztrál őslakosok (Aboriginal Australians) művészetének egyedülálló és szerves része. Kezdetben a homokba, földre pöttyözték az ábrákat, mintákat, mely törzsi történeteknek szent jelentései voltak. Egy-egy festmény adott szertartáshoz, rituáléhoz tartozott. A beavatatlanok soha nem láthatták ezeket a rajzokat, szent mintákat, mivel a földet újra elsimították a szertartás után.

## Galéria

<div class="gallery" id="gallery-container">
  <!-- The gallery images will be loaded here -->
</div>

<script>
  const galleryContainer = document.getElementById('gallery-container');

  // Fetch the list of repository contents using GitHub API
  fetch('https://api.github.com/repos/balazsvamosi/balazsvamosi.github.io/contents/')
    .then((response) => response.json())
    .then((data) => {
      // Filter the JPEG images from the fetched data
      const jpegImages = data.filter((file) => file.name.toLowerCase().endsWith('.jpeg') || file.name.toLowerCase().endsWith('.jpg'));

      // Create the gallery elements and append them to the container
      jpegImages.forEach((image) => {
        const galleryImage = document.createElement('a');
        galleryImage.href = image.download_url;
        galleryImage.setAttribute('data-lightbox', 'gallery');
        galleryImage.setAttribute('data-title', image.name);

        const imageElement = document.createElement('img');
        imageElement.src = image.download_url;
        imageElement.alt = image.name;

        galleryImage.appendChild(imageElement);
        galleryContainer.appendChild(galleryImage);
      });

      // Initialize SimpleLightbox after all images are loaded
      var gallery = new SimpleLightbox('.gallery a');
    })
    .catch((error) => {
      console.error('Error fetching repository contents:', error);
    });
</script>
