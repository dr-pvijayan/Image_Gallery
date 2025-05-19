# Ex.08 Design of Interactive Image Gallery
## DATE:19-05-2025

## AIM
  To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS

## Step 1:

Clone the github repository and create Django admin interface

## Step 2:

Change settings.py file to allow request from all hosts.

## Step 3:

Use CSS for positioning and styling.

## Step 4:

Write JavaScript program for implementing interactivit

## Step 5:

Validate the HTML and CSS code

## Step 6:

Publish the website in the given URL.

## PROGRAM
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Photo Gallery</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }
        
        header {
            background-color: #2c3e50;
            color: white;
            padding: 1.5rem;
            text-align: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        h1 {
            margin-bottom: 0.5rem;
        }
        
        .gallery-container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }
        
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }
        
        .gallery-item {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.2);
            transition: transform 0.3s ease;
            cursor: pointer;
        }
        
        .gallery-item:hover {
            transform: scale(1.03);
        }
        
        .gallery-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            display: block;
        }
        
        .image-info {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 1rem;
            transform: translateY(100%);
            transition: transform 0.3s ease;
        }
        
        .gallery-item:hover .image-info {
            transform: translateY(0);
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.9);
            z-index: 1000;
            overflow: auto;
        }
        
        .modal-content {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100%;
            padding: 20px;
        }
        
        .modal-image {
            max-width: 95%;
            max-height: 85vh;
            object-fit: contain;
            border: 2px solid white;
            box-shadow: 0 0 20px rgba(255,255,255,0.2);
        }
        
        .modal-info {
            color: white;
            text-align: center;
            margin-top: 1.5rem;
            max-width: 800px;
            padding: 1rem;
            background-color: rgba(0,0,0,0.7);
            border-radius: 8px;
        }
        
        .close {
            position: absolute;
            top: 20px;
            right: 30px;
            color: white;
            font-size: 35px;
            font-weight: bold;
            cursor: pointer;
            z-index: 1001;
        }
        
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            width: 100%;
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            padding: 0 20px;
        }
        
        .nav-button {
            background-color: rgba(255,255,255,0.3);
            color: white;
            border: none;
            padding: 15px 25px;
            font-size: 28px;
            cursor: pointer;
            border-radius: 50%;
            transition: background-color 0.3s;
            z-index: 1001;
        }
        
        .nav-button:hover {
            background-color: rgba(255,255,255,0.5);
        }
        
        footer {
            text-align: center;
            padding: 1.5rem;
            background-color: #2c3e50;
            color: white;
            margin-top: 2rem;
        }
        
        @media (max-width: 768px) {
            .gallery {
                grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            }
            
            .modal-image {
                max-width: 100%;
                max-height: 70vh;
            }
            
            .nav-button {
                padding: 12px 20px;
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Interactive Photo Gallery</h1>
    </header>
    
    <div class="gallery-container">
        <div class="gallery" id="gallery">
            <!-- Gallery items will be added here dynamically -->
        </div>
    </div>
    
    <div class="modal" id="modal">
        <span class="close" id="close-modal">&times;</span>
        <div class="nav-buttons">
            <button class="nav-button" id="prev-btn">&#10094;</button>
            <button class="nav-button" id="next-btn">&#10095;</button>
        </div>
        <div class="modal-content">
            <img class="modal-image" id="modal-image" src="" alt="">
            <div class="modal-info">
                <h2 id="modal-title"></h2>
                <p id="modal-description"></p>
            </div>
        </div>
    </div>
    
    <footer>
        <p>&copy; 2023 Interactive Photo Gallery. All rights reserved.</p>
    </footer>
    
    <script>
        // Sample photo data
        const photos = [
            {
                id: 1,
                title: "Mountain View",
                description: "Beautiful mountain landscape",
                filename:"file:///C:/Users/admin/Desktop/images.jpeg"
            },
            {
                id: 2,
                title: "City Skyline",
                description: "Modern city architecture",
                filename: "file:///C:/Users/admin/Desktop/images%20(1).jpeg"
            },
            {
                id: 3,
                title: "Wildlife",
                description: "Lion in its natural habitat",
                filename: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRAlaBWxnQcfTZcl5dnmwdtkQB9ZnVFsPweodqI2OOstyNq4z-NPNtOWWDPcwOn"
            },
            {
                id: 4,
                title: "Portrait",
                description: "Close-up portrait",
                filename: "https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTbeeiwAdMsHM5NRg8_ybT16zeGcElv-TLiXSa8TOftLsJrTda6t7tzd4WIti9a"
            },
            {
                id: 5,
                title: "Beach Sunset",
                description: "Sun setting over the ocean",
                filename: "https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcTbeeiwAdMsHM5NRg8_ybT16zeGcElv-TLiXSa8TOftLsJrTda6t7tzd4WIti9a"
            },
            {
                id: 6,
                title: "Historical Building",
                description: "Ancient architecture with intricate details",
                filename: "https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcT-g_vsKypukDvocApuhGCmsNOPY4iVXi90l83Q5Jz2Mo1VaVSi7r8-D7vpAmYX"
            },
            {
                id: 7,
                title: "Bird in Flight",
                description: "Bird soaring through the sky",
                filename: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRfdq3ppmWX6RxyFxqVdB0P0IFXXG20aJt0zuBhTk0-R1hM38tK9MupG86TWpiN"
            },
            {
                id: 8,
                title: "Street Photography",
                description: "Candid moment in the city",
                filename: "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcQ7UzalP7gL6jzM02_dN4CBeX1HKkVUKqAwb9jIUxmO21KnhMcXxF0Y9UjE69KY"
            }
        ];
        
        // DOM elements
        const gallery = document.getElementById('gallery');
        const modal = document.getElementById('modal');
        const modalImage = document.getElementById('modal-image');
        const modalTitle = document.getElementById('modal-title');
        const modalDescription = document.getElementById('modal-description');
        const closeModal = document.getElementById('close-modal');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        
        // Current photo index for modal navigation
        let currentPhotoIndex = 0;
        
        // Initialize the gallery
        function initGallery() {
            gallery.innerHTML = '';
            
            photos.forEach((photo, index) => {
                const galleryItem = document.createElement('div');
                galleryItem.className = 'gallery-item';
                
                galleryItem.innerHTML = `
                    <img src="${photo.filename}" alt="${photo.title}" class="gallery-image">
                    <div class="image-info">
                        <h3>${photo.title}</h3>
                    </div>
                `;
                
                galleryItem.addEventListener('click', () => openModal(index));
                gallery.appendChild(galleryItem);
            });
        }
        
        // Open modal with photo details
        function openModal(index) {
            currentPhotoIndex = index;
            const photo = photos[index];
            
            modalImage.src = photo.filename;
            modalImage.alt = photo.title;
            modalTitle.textContent = photo.title;
            modalDescription.textContent = photo.description;
            
            modal.style.display = 'block';
            document.body.style.overflow = 'hidden';
        }
        
        // Close modal
        function closeModalFunc() {
            modal.style.display = 'none';
            document.body.style.overflow = 'auto';
        }
        
        // Navigate to previous photo
        function prevPhoto() {
            currentPhotoIndex = (currentPhotoIndex - 1 + photos.length) % photos.length;
            const photo = photos[currentPhotoIndex];
            
            modalImage.src = photo.filename;
            modalImage.alt = photo.title;
            modalTitle.textContent = photo.title;
            modalDescription.textContent = photo.description;
        }
        
        // Navigate to next photo
        function nextPhoto() {
            currentPhotoIndex = (currentPhotoIndex + 1) % photos.length;
            const photo = photos[currentPhotoIndex];
            
            modalImage.src = photo.filename;
            modalImage.alt = photo.title;
            modalTitle.textContent = photo.title;
            modalDescription.textContent = photo.description;
        }
        
        // Event listeners
        closeModal.addEventListener('click', closeModalFunc);
        
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                closeModalFunc();
            }
        });
        
        document.addEventListener('keydown', (e) => {
            if (modal.style.display === 'block') {
                if (e.key === 'Escape') {
                    closeModalFunc();
                } else if (e.key === 'ArrowLeft') {
                    prevPhoto();
                } else if (e.key === 'ArrowRight') {
                    nextPhoto();
                }
            }
        });
        
        prevBtn.addEventListener('click', prevPhoto);
        nextBtn.addEventListener('click', nextPhoto);
        
        // Initialize the gallery on page load
        window.addEventListener('load', initGallery);
    </script>
</body>
</html>
```
## OUTPUT
![alt text](1.png)
![alt text](2.png)

## RESULT
  The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
