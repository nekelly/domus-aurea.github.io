---
title: Recommended Books
type: page
reading_time: false
show_related: false
pager: false
---

<style>
.book-item {
  cursor: pointer;
}

.book-item img {
  height: 150px;
  width: 100%;
  object-fit: cover;
}

.lightbox {
  display: none;
  position: fixed;
  z-index: 9999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.9);
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.lightbox.active {
  display: flex;
}

.lightbox img {
  max-width: 90%;
  max-height: 90vh;
  object-fit: contain;
  border-radius: 8px;
}

.lightbox-close {
  position: absolute;
  top: 20px;
  right: 40px;
  color: white;
  font-size: 40px;
  font-weight: bold;
  cursor: pointer;
  z-index: 10000;
}

.lightbox-close:hover {
  color: #ccc;
}
</style>

<p class="text-lg text-gray-600 dark:text-gray-400 mb-8" style="margin-top: -3rem">(Hover over the book thumbnail to see a full-sized image)</p>

<div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 md:gap-6 mb-8">
  <div class="book-item" onclick="openLightbox('/books/baltimore.jpg')">
    <img src="/books/baltimore.jpg" alt="Book Title 1" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/catechism_trent.jpg')">
    <img src="/books/catechism_trent.jpg" alt="Book Title 2" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/liberalism_sin.jpg')">
    <img src="/books/liberalism_sin.jpg" alt="Book Title 3" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/raccolta.jpg')">
    <img src="/books/raccolta.jpg" alt="Book Title 4" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/work_hands.jpg')">
    <img src="/books/work_hands.jpg" alt="Book Title 5" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/vatican2.jpg')">
    <img src="/books/vatican2.jpg" alt="Book Title 6" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/robber_church.webp')">
    <img src="/books/robber_church.webp" alt="Book Title 7" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/garrigou1.jpg')">
    <img src="/books/garrigou1.jpg" alt="Book Title 8" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/garrigou2.png')">
    <img src="/books/garrigou2.png" alt="Book Title 9" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
  <div class="book-item" onclick="openLightbox('/books/true_devotion.jpg')">
    <img src="/books/true_devotion.jpg" alt="Book Title 10" class="w-full h-auto rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
  </div>
</div>

<div id="lightbox" class="lightbox" onclick="closeLightbox()">
  <span class="lightbox-close" onclick="closeLightbox()">&times;</span>
  <img id="lightbox-img" src="" alt="Book cover">
</div>

<script>
function openLightbox(imgSrc) {
  const lightbox = document.getElementById('lightbox');
  const lightboxImg = document.getElementById('lightbox-img');
  lightboxImg.src = imgSrc;
  lightbox.classList.add('active');
  document.body.style.overflow = 'hidden';
}

function closeLightbox() {
  const lightbox = document.getElementById('lightbox');
  lightbox.classList.remove('active');
  document.body.style.overflow = 'auto';
}

// Close lightbox with Escape key
document.addEventListener('keydown', function(event) {
  if (event.key === 'Escape') {
    closeLightbox();
  }
});
</script>
