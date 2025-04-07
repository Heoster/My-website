

<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Heoster </title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #8e44ad;
            --secondary-color: #3498db;
            --accent-color: #2ecc71;
            --bg-color: #f8f9fa;
            --text-color: #2c3e50;
            --gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            --card-shadow: 0 10px 20px rgba(0,0,0,0.1);
            --transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .preloader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: white;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 10000;
            transition: opacity 0.8s, visibility 0.8s;
        }

        .preloader.hidden {
            opacity: 0;
            visibility: hidden;
        }

        .loader {
            width: 50px;
            height: 50px;
            border: 5px solid #f3f3f3;
            border-top: 5px solid var(--primary-color);
            border-radius: 50%;
            animation: spin 1s linear infinite, color-change 3s ease-in-out infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes color-change {
            0% { border-top-color: var(--primary-color); }
            50% { border-top-color: var(--secondary-color); }
            100% { border-top-color: var(--primary-color); }
        }

        .loading-bar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--gradient);
            z-index: 9999;
            animation: loading 2s ease-in-out infinite;
        }

        @keyframes loading {
            0% { width: 0; }
            50% { width: 65%; }
            100% { width: 100%; }
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--text-color);
            background-color: #fff;
        }

        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 5%;
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(20px);
            box-shadow: 0 5px 30px rgba(0,0,0,0.1);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            transition: padding 0.3s;
        }

        .navbar:hover {
            padding: 1.2rem 5%;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 800;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            letter-spacing: 1px;
            position: relative;
            padding-bottom: 3px;
        }

        .logo::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            height: 3px;
            width: 0;
            background: var(--gradient);
            transition: width 0.4s;
        }

        .logo:hover::after {
            width: 100%;
        }

        .nav-links a {
            position: relative;
            color: var(--text-color);
            text-decoration: none;
            margin-left: 2rem;
            transition: color 0.3s;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient);
            transition: width 0.3s;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .gallery-section, .events-section, .blog-section, .about-section {
            padding: 5rem 2rem;
            margin-top: 2rem;
        }

        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            padding: 2rem 0;
        }

        .gallery-item {
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: var(--transition);
            position: relative;
        }

        .gallery-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.6) 0%, transparent 100%);
            opacity: 0;
            transition: opacity 0.4s;
            z-index: 1;
        }

        .gallery-item:hover {
            transform: translateY(-10px) scale(1.03);
            box-shadow: var(--card-shadow);
        }

        .gallery-item:hover::before {
            opacity: 1;
        }

        .gallery-item img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            transition: transform 0.6s;
        }

        .gallery-item:hover img {
            transform: scale(1.1);
        }

        .gallery-item p {
            padding: 1rem;
            text-align: center;
            font-weight: 500;
            position: relative;
            z-index: 2;
            background: white;
            transition: var(--transition);
        }

        .gallery-item:hover p {
            background: var(--gradient);
            color: white;
        }

        .event-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            padding: 2rem 0;
        }

        .event-card {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.1);
            transition: var(--transition);
        }

        .event-card:hover {
            transform: translateY(-10px);
            box-shadow: var(--card-shadow);
        }

        .rsvp-btn {
            background: var(--gradient);
            color: white;
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            margin-top: 1rem;
            transition: all 0.3s;
        }

        .rsvp-btn:hover {
            opacity: 0.9;
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .blog-posts {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            padding: 2rem 0;
        }

        .blog-post {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.1);
            transition: var(--transition);
        }

        .blog-post:hover {
            transform: translateY(-10px);
            box-shadow: var(--card-shadow);
        }

        .post-meta {
            color: #666;
            font-size: 0.9rem;
            margin: 0.5rem 0;
        }

        .read-more {
            color: var(--primary-color);
            text-decoration: none;
            font-weight: bold;
            display: inline-block;
            margin-top: 1rem;
            position: relative;
            transition: all 0.3s;
        }

        .read-more::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient);
            transition: width 0.3s;
        }

        .read-more:hover::after {
            width: 100%;
        }

        .about-section {
            text-align: center;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .stat-item {
            background: white;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.1);
            transition: var(--transition);
        }

        .stat-item:hover {
            transform: translateY(-10px);
            box-shadow: var(--card-shadow);
        }

        .stat-item h3 {
            font-size: 2.5rem;
            color: var(--primary-color);
            margin-bottom: 0.5rem;
        }

        .section-title {
            text-align: center;
            margin-bottom: 3rem;
            color: var(--text-color);
            font-size: 2.5rem;
            position: relative;
            padding-bottom: 15px;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 3px;
            background: var(--gradient);
        }

        .section-title .highlight {
            color: var(--primary-color);
        }

        section {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.8s, transform 0.8s;
        }

        section.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .hero {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background:  linear-gradient(rgba(20, 20, 40, 0.85), rgba(20, 20, 40, 0.85)), linear-gradient(135deg, #ff4ecd 0%, #6a82fb 50%,  #00f2fe 100%);,
                        url('https://2024wallepals.simdif.com/images/public/sd_673db7464d01e.jpg?no_cache=1733831618') center/cover;
            background-attachment: fixed;
            padding: 0 20px;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: radial-gradient(circle, transparent 20%, rgba(0,0,0,0.2) 100%);
            z-index: 0;
        }

        .hero h1 {
            font-size: 4rem;
            margin-bottom: 1.5rem;
            color: white;
            text-shadow: 2px 2px 15px rgba(0,0,0,0.3);
            position: relative;
            z-index: 1;
            animation: fadeIn 1.5s ease-out forwards;
        }

        .hero p {
            color: rgba(255,255,255,0.9);
            font-size: 1.5rem;
            max-width: 600px;
            animation: slideUp 1s ease-out 0.5s forwards;
            opacity: 0;
            transform: translateY(20px);
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            to { 
                opacity: 1;
                transform: translateY(0);
            }
        }

        .memory-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            padding: 5rem;
            background-color: white;
        }

        .memory-card {
            background: white;
            padding: 2.5rem;
            border-radius: 15px;
            transition: var(--transition);
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            position: relative;
            overflow: hidden;
            z-index: 1;
        }

        .memory-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: var(--gradient);
            transform: scaleX(0);
            transform-origin: left;
            transition: transform 0.4s;
            z-index: -1;
        }

        .memory-card:hover {
            transform: translateY(-10px) scale(1.03);
            box-shadow: var(--card-shadow);
        }

        .memory-card:hover::before {
            transform: scaleX(1);
        }

        .memory-card h3 {
            color: var(--primary-color);
            font-size: 1.6rem;
            margin-bottom: 0.8rem;
            position: relative;
            display: inline-block;
        }

        .memory-card h3::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent-color);
            transition: width 0.4s;
        }

        .memory-card:hover h3::after {
            width: 100%;
        }

        .chat-section {
            padding: 5rem;
            background-color: #f9f9f9;
        }

        .chat-container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
        }

        .chat-messages {
            height: 400px;
            overflow-y: auto;
            padding: 20px;
        }

        .chat-input {
            display: flex;
            padding: 20px;
            border-top: 1px solid #eee;
        }

        .chat-input input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-right: 10px;
        }

        .chat-input button {
            padding: 10px 20px;
            background: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .chat-input button:hover {
            transform: scale(1.05);
        }

        footer {
            background: var(--gradient);
            color: white;
            text-align: center;
            padding: 3rem 2rem;
            position: relative;
            overflow: hidden;
        }

        footer::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: white;
            opacity: 0.2;
        }

        .social-links {
            margin-bottom: 1.5rem;
        }

        .social-links a {
            color: white;
            font-size: 1.8rem;
            margin: 0 15px;
            transition: transform 0.3s, opacity 0.3s;
            display: inline-block;
            opacity: 0.8;
        }

        .social-links a:hover {
            transform: translateY(-8px) scale(1.2);
            opacity: 1;
        }

        footer p {
            opacity: 0.8;
            font-size: 0.9rem;
            margin-top: 1rem;
            letter-spacing: 1px;
        }

        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .memory-grid {
                padding: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="preloader">
        <div class="loader"></div>
    </div>
    <div class="loading-bar"></div>
    <nav class="navbar">
        <div class="logo">SARRE YAAR</div>
        <div class="nav-links">
            <a href="#home">Home</a>
            <a href="#memories">Memories</a>
            <a href="#gallery">Gallery</a>
            <a href="#events">Events</a>
            <a href="#blog">Blog</a>
            <a href="#chat">Chat</a>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
        </div>
    </nav>

    <header class="hero" id="home">
        <h1>Welcome to Our Memory Lane</h1>
        <p>Cherishing friendships that last forever</p>
    </header>

    <section id="memories" class="memory-grid">
        <div class="memory-card">
            <h3>Our Journey</h3>
            <p>Class of 2024 - A story of friendship and growth</p>
        </div>
        <div class="memory-card">
            <h3>Poetry Corner</h3>
            <p>Express your feelings through words</p>
        </div>
        <div class="memory-card">
            <h3>Photo Gallery</h3>
            <p>Moments captured in time</p>
        </div>
    </section>

    <section id="gallery" class="gallery-section">
        <h2 class="section-title">Photo <span class="highlight">Gallery</span></h2>
        <div class="gallery-grid">
            <div class="gallery-item">
                <img src =" https://2024wallepals.simdif.com/images/th/sd_673b75cba84b7.jpg?no_cache=1731953644" alt="Memory 1">
                <p>First Day Together</p>
            </div>
            <div class="gallery-item">
                <img src=" https://2024wallepals.simdif.com/images/public/sd_673db7464d01e.jpg?no_cache=1733831618" alt="Memory 2">
                <p>Class Trip</p>
            </div>
            <div class="gallery-item">
                <img src=" https://2024wallepals.simdif.com/images/th/sd_67582bda9da2b.jpg?no_cache=1733914677" alt ="Memory 3">
                <p>Graduation Day</p>
            </div>
        </div>
    </section>

    <section id="events" class="events-section">
        <h2 class="section-title">Upcoming <span class="highlight">Events</span></h2>
        <div class="event-cards">
            <div class="event-card">
                <h3>Class Reunion</h3>
                <p>Date: December 25, 2024</p>
                <p>Location: School Auditorium</p>
                <button class="rsvp-btn">RSVP Now</button>
            </div>
            <div class="event-card">
                <h3>Alumni Meet</h3>
                <p>Date: January 15, 2025</p>
                <p>Location: City Park</p>
                <button class="rsvp-btn">RSVP Now</button>
            </div>
        </div>
    </section>

    <section id="blog" class="blog-section">
        <h2 class="section-title">Latest <span class="highlight">Stories</span></h2>
        <div class="blog-posts">
            <article class="blog-post">
                <h3>Memories of 2024</h3>
                <p class="post-meta">Posted on December 1, 2024</p>
                <p>Our journey through the final year was filled with unforgettable moments...</p>
                <a href="#" class="read-more">Read More</a>
            </article>
            <article class="blog-post">
                <h3>Farewell Thoughts</h3>
                <p class="post-meta">Posted on November 15, 2024</p>
                <p>As we prepare to part ways, here's what everyone had to say...</p>
                <a href="#" class="read-more">Read More</a>
            </article>
        </div>
    </section>

    <section id="about" class="about-section">
        <h2 class="section-title">About <span class="highlight">Us</span></h2>
        <div class="about-content">
            <p>We are the class of 2024, a group of friends who shared countless memories and grew together through our academic journey.</p>
            <div class="stats">
                <div class="stat-item">
                    <h3>50+</h3>
                    <p>Classmates</p>
                </div>
                <div class="stat-item">
                    <h3>4</h3>
                    <p>Years Together</p>
                </div>
                <div class="stat-item">
                    <h3>100+</h3>
                    <p>Shared Memories</p>
                </div>
            </div>
        </div>
    </section>

    <section id="chat" class="chat-section">
        <h2 class="section-title">Chat <span class="highlight">Room</span></h2>
        <div class="chat-container">
            <div class="chat-messages" id="messageArea"></div>
            <div class="chat-input">
                <input type="text" id="messageInput" placeholder="Type your message...">
                <button onclick="sendMessage()">Send</button>
            </div>
        </div>
    </section>

    <section id="contact" class="contact-section gallery-section">
        <h2 class="section-title">Contact <span class="highlight">Us</span></h2>
        <div class="contact-form" style="max-width: 600px; margin: 0 auto;">
            <form>
                <div style="margin-bottom: 1rem;">
                    <input type="text" placeholder="Your Name" style="width: 100%; padding: 10px; border-radius: 5px; border: 1px solid #ddd;">
                </div>
                <div style="margin-bottom: 1rem;">
                    <input type="email" placeholder="Your Email" style="width: 100%; padding: 10px; border-radius: 5px; border: 1px solid #ddd;">
                </div>
                <div style="margin-bottom: 1rem;">
                    <textarea placeholder="Your Message" style="width: 100%; padding: 10px; border-radius: 5px; border: 1px solid #ddd; min-height: 150px;"></textarea>
                </div>
                <button type="submit" class="rsvp-btn" style="width: 100%;">Send Message</button>
            </form>
        </div>
    </section>

    <footer>
        <div class="social-links">
            <a href="https://www.instagram.com/codex._.heoster?igsh=MTF1Mzl3MmFnbGxpMg=="><i class="fab fa-instagram"></i></a>
            <a href="https://www.instagram.com/kittu_pandat001?igsh=OXRieXR3aDM0Mzk="><i class="fab fa-instagram"></i></a>
            <a href=" https://www.instagram.com/__pankajthakur7?igsh=bm40Ynppd3h5bjEx"><i class="fab fa-instagram"></i></a>
            <a href=" https://2024wallepals.simdif.com"> <i class="fab fa-chrome"></i></a>
        </div>
        <p>&copy; 2024 Heoster. All rights reserved.</p>
    </footer>

    <script>
        // Hide preloader when page is loaded
        window.addEventListener('load', () => {
            const preloader = document.querySelector('.preloader');
            setTimeout(() => {
                preloader.classList.add('hidden');
            }, 800);
        });

        // Smooth scrolling for navigation links
        document.querySelectorAll('a[href^="https://2024wallepals.simdif.com"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });

        // Chat functionality
        function sendMessage() {
            const input = document.getElementById('messageInput');
            const messageArea = document.getElementById('messageArea');
            
            if (input.value.trim() !== '') {
                const messageDiv = document.createElement('div');
                messageDiv.className = 'message';
                messageDiv.style.padding = '10px';
                messageDiv.style.margin = '5px';
                messageDiv.style.backgroundColor = '#f0f0f0';
                messageDiv.style.borderRadius = '5px';
                messageDiv.textContent = input.value;
                
                messageArea.appendChild(messageDiv);
                messageArea.scrollTop = messageArea.scrollHeight;
                
                input.value = '';
            }
        }

        // Handle Enter key in chat input
        document.getElementById('messageInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });

        // Animate memory cards and sections on scroll
        const cardObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, { threshold: 0.2 });

        document.querySelectorAll('.memory-card').forEach((card) => {
            card.style.opacity = '0';
            card.style.transform = 'translateY(20px)';
            card.style.transition = 'all 0.5s ease-in-out';
            cardObserver.observe(card);
        });

        // Animate sections on scroll
        const sectionObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('section').forEach((section) => {
            sectionObserver.observe(section);
        });

        // Navbar scroll effect
        window.addEventListener('scroll', () => {
            const navbar = document.querySelector('.navbar');
            if (window.scrollY > 100) {
                navbar.style.padding = '0.8rem 5%';
                navbar.style.boxShadow = '0 5px 20px rgba(0,0,0,0.15)';
            } else {
                navbar.style.padding = '1rem 5%';
                navbar.style.boxShadow = '0 5px 30px rgba(0,0,0,0.1)';
            }
        });

        // RSVP button functionality
        document.querySelectorAll('.rsvp-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                alert('Thank you for your RSVP! We look forward to seeing you at the event.');
            });
        });

        // Read More functionality
        document.querySelectorAll('.read-more').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                alert('Full article coming soon!');
            });
        });
    </script>
</body>
</html>
