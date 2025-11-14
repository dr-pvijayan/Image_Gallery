## Ex.08 Design of Interactive Image Gallery
## SARANKUMAR.V(212224220089)
## AIM
To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS
Step 1:
Clone the github repository and create Django admin interface

Step 2:
Change settings.py file to allow request from all hosts.

Step 3:
Use CSS for positioning and styling.

Step 4:
Write JavaScript program for implementing interactivit

Step 5:
Validate the HTML and CSS code

Step 6:
Publish the website in the given URL.

## PROGRAM
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Image Gallery</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background: #f5f5f5;
    }

    h1 {
      text-align: center;
      margin-bottom: 25px;
    }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
    }

    .gallery img {
      width: 100%;
      height: 220px;
      object-fit: cover;
      border-radius: 10px;
      cursor: pointer;
      transition: 0.3s;
    }

    .gallery img:hover {
      transform: scale(1.03);
    }

    /* Lightbox */
    .lightbox {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.8);
      display: none;
      justify-content: center;
      align-items: center;
    }

    .lightbox img {
      max-width: 80%;
      max-height: 80%;
      border-radius: 10px;
    }

    .closeBtn {
      position: absolute;
      top: 20px;
      right: 30px;
      font-size: 35px;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Image Gallery</h1>

  <div class="gallery" id="gallery">
    <img src="https://images.unsplash.com/photo-1503023345310-bd7c1de61c7d?w=800" alt="Image 1" />
    <img src="https://images.unsplash.com/photo-1504198453319-5ce911bafcde?w=800" alt="Image 2" />
    <img src="https://images.unsplash.com/photo-1482192505345-5655af888cc4?w=800" alt="Image 3" />
    <img src="https://images.unsplash.com/photo-1491553895911-0055eca6402d?w=800" alt="Image 4" />
    <img src="https://images.unsplash.com/photo-1526772662000-3f88f10405ff?w=800" alt="Image 5" />
    <img src="https://images.unsplash.com/photo-1482192596544-9eb780fc7f66?w=800" alt="Image 6" />
  </div>

  <!-- Lightbox -->
  <div class="lightbox" id="lightbox">
    <span class="closeBtn" onclick="closeLightbox()">&times;</span>
    <img id="lightboxImg" src="" alt="" />
  </div>

  <script>
    const lightbox = document.getElementById("lightbox");
    const lightboxImg = document.getElementById("lightboxImg");
    const galleryImages = document.querySelectorAll(".gallery img");

    galleryImages.forEach(img => {
      img.addEventListener("click", () => {
        lightbox.style.display = "flex";
        lightboxImg.src = img.src;
      });
    });

    function closeLightbox() {
      lightbox.style.display = "none";
    }
  </script>
</body>
</html>
```
## OUTPUT

<img width="1009" height="727" alt="Screenshot 2025-11-14 101818" src="https://github.com/user-attachments/assets/28dfab07-cd89-4a24-9708-5c063f8f9411" />

## RESULT
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
