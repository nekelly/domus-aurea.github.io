---
title: Gallery
type: page
---

<style>
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin: 2rem 0;
}

.gallery-grid img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 8px;
  transition: transform 0.3s ease;
}

.gallery-grid img:hover {
  transform: scale(1.05);
  cursor: pointer;
}

@media (max-width: 768px) {
  .gallery-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .gallery-grid {
    grid-template-columns: 1fr;
  }
}
</style>

<div class="gallery-grid">
  <img src="https://picsum.photos/400/300?random=1" alt="Gallery Image 1">
  <img src="https://picsum.photos/400/300?random=2" alt="Gallery Image 2">
  <img src="https://picsum.photos/400/300?random=3" alt="Gallery Image 3">
  <img src="https://picsum.photos/400/300?random=4" alt="Gallery Image 4">
  <img src="https://picsum.photos/400/300?random=5" alt="Gallery Image 5">
  <img src="https://picsum.photos/400/300?random=6" alt="Gallery Image 6">
  <img src="https://picsum.photos/400/300?random=7" alt="Gallery Image 7">
  <img src="https://picsum.photos/400/300?random=8" alt="Gallery Image 8">
  <img src="https://picsum.photos/400/300?random=9" alt="Gallery Image 9">
</div>
