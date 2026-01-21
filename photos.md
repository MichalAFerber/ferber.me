---
layout: base
title: Photos
permalink: /photos/
---

# Ferber Photos
  
A collection of family photos throughout the years. Click any photo to view it in full size and use the arrows to navigate.
  
  <div class="photo-gallery" id="gallery">
    {% assign photos = "4af756d1,25bd0da3,e56bb567,f1105d60,f0e19ddf,30cf44f3,a2dcd8f7,81eed74d,7a2fdd2e,9b32d92c,190f0c7c,59518d4b,238d20aa,ea4a1fed,48b606af,ad6dfed5,6be4aa2d,07acaa00,2e50f2fb,33fa6c78,f82e4fd5,cd2fd8ca,0b2c03cc,44b10e60,52769412,506129b7,dca5f48b,c7b81c46,f880f7c6,5932d9d9,fa9555b8,82a72efc,645df9be,1c6e579b,4a04ca68,af65cf54,d5c67fed,b600b773,ffc8fef2,70b6a898,45f52dc1,41d2c121" | split: "," %}
    {% for photo in photos %}
    <div class="gallery-item" data-index="{{ forloop.index0 }}" data-full="/assets/images/gallery/{{ photo }}_original.jpg">
      <img src="/assets/images/gallery/{{ photo }}.jpg" alt="Ferber Family Photo {{ forloop.index }}">
    </div>
    {% endfor %}
  </div>

<!-- Lightbox -->
<div class="lightbox-overlay" id="lightbox">
  <button class="lightbox-close" aria-label="Close">&times;</button>
  <button class="lightbox-nav lightbox-prev" aria-label="Previous">&#10094;</button>
  <div class="lightbox-content">
    <img src="" alt="Full size photo" id="lightbox-img">
  </div>
  <button class="lightbox-nav lightbox-next" aria-label="Next">&#10095;</button>
  <div class="lightbox-counter"><span id="lightbox-current">1</span> / <span id="lightbox-total">42</span></div>
</div>

<script>
(function() {
  const gallery = document.getElementById('gallery');
  const lightbox = document.getElementById('lightbox');
  const lightboxImg = document.getElementById('lightbox-img');
  const lightboxCurrent = document.getElementById('lightbox-current');
  const lightboxTotal = document.getElementById('lightbox-total');
  const items = gallery.querySelectorAll('.gallery-item');
  let currentIndex = 0;
  
  lightboxTotal.textContent = items.length;
  
  function openLightbox(index) {
    currentIndex = index;
    const item = items[index];
    lightboxImg.src = item.dataset.full;
    lightboxCurrent.textContent = index + 1;
    lightbox.classList.add('active');
    document.body.style.overflow = 'hidden';
  }
  
  function closeLightbox() {
    lightbox.classList.remove('active');
    document.body.style.overflow = '';
  }
  
  function navigate(direction) {
    currentIndex = (currentIndex + direction + items.length) % items.length;
    const item = items[currentIndex];
    lightboxImg.src = item.dataset.full;
    lightboxCurrent.textContent = currentIndex + 1;
  }
  
  items.forEach((item, index) => {
    item.addEventListener('click', () => openLightbox(index));
  });
  
  lightbox.querySelector('.lightbox-close').addEventListener('click', closeLightbox);
  lightbox.querySelector('.lightbox-prev').addEventListener('click', () => navigate(-1));
  lightbox.querySelector('.lightbox-next').addEventListener('click', () => navigate(1));
  
  lightbox.addEventListener('click', (e) => {
    if (e.target === lightbox) closeLightbox();
  });
  
  document.addEventListener('keydown', (e) => {
    if (!lightbox.classList.contains('active')) return;
    if (e.key === 'Escape') closeLightbox();
    if (e.key === 'ArrowLeft') navigate(-1);
    if (e.key === 'ArrowRight') navigate(1);
  });
})();
</script>
