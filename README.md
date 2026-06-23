<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bita No | Official Artist Website</title>
    
    <!-- SEO Meta Tags -->
    <meta name="description" content="Website chính thức của Bita No - Vocalist, Bassist và Thành viên ban nhạc Mũ Len. Khám phá âm nhạc, video TikTok và hành trình nghệ thuật sáng tạo.">
    <meta name="keywords" content="Bita No, Mũ Len, Bassist, Vocalist, Ban nhạc Mũ Len, Sáng tạo âm nhạc, Hồ Chí Minh">
    
    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website">
    <meta property="og:title" content="Bita No | Official Artist Website">
    <meta property="og:description" content="Kênh truyền thông và không gian âm nhạc chính thức của nghệ sĩ Bita No.">
    <meta property="og:image" content="bitano.jpg">

    <!-- Google Fonts & Font Awesome -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Plus+Jakarta+Sans:wght@300;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --bg-dark: #0a0512;
            --purple-neon: #bc13fe;
            --blue-neon: #00f3ff;
            --text-light: #ffffff;
            --text-muted: #a19fad;
            --glass-bg: rgba(18, 10, 36, 0.6);
            --glass-border: rgba(188, 19, 254, 0.2);
            --font-title: 'Orbitron', sans-serif;
            --font-body: 'Plus Jakarta Sans', sans-serif;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            font-family: var(--font-body);
            overflow-x: hidden;
            background-image: radial-gradient(circle at 20% 30%, rgba(188, 19, 254, 0.15) 0%, transparent 40%),
                              radial-gradient(circle at 80% 70%, rgba(0, 243, 331, 0.1) 0%, transparent 45%);
            background-attachment: fixed;
        }

        /* Loading Screen */
        #loading-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #05020a;
            z-index: 9999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            transition: opacity 0.5s ease;
        }
        .loader-logo {
            font-family: var(--font-title);
            font-size: 2.5rem;
            font-weight: 900;
            color: #fff;
            text-shadow: 0 0 10px var(--purple-neon), 0 0 30px var(--blue-neon);
            animation: pulse 1.5s infinite alternate;
            margin-bottom: 20px;
        }
        .loader-bar {
            width: 200px; height: 3px; background: rgba(255,255,255,0.1);
            border-radius: 5px; overflow: hidden;
        }
        .loader-progress {
            width: 0%; height: 100%; background: linear-gradient(90deg, var(--purple-neon), var(--blue-neon));
            animation: load 2s forwards ease-in-out;
        }

        /* Custom Cursor */
        .custom-cursor {
            width: 20px; height: 20px;
            border: 2px solid var(--blue-neon);
            border-radius: 50%;
            position: fixed;
            transform: translate(-50%, -50%);
            pointer-events: none;
            z-index: 10000;
            transition: width 0.2s, height 0.2s, background-color 0.2s;
            display: none;
        }
        @media (min-width: 1025px) { .custom-cursor { display: block; } }

        /* Canvas Particle */
        #particle-canvas {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            z-index: -1; pointer-events: none;
        }

        /* Navigation */
        header {
            position: fixed; top: 0; left: 0; width: 100%; z-index: 1000;
            background: rgba(10, 5, 18, 0.8);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--glass-border);
        }
        .navbar {
            max-width: 1400px; margin: 0 auto; padding: 20px;
            display: flex; justify-content: space-between; align-items: center;
        }
        .logo {
            font-family: var(--font-title); font-weight: 900; font-size: 1.8rem;
            color: #fff; text-decoration: none; letter-spacing: 2px;
            text-shadow: 0 0 8px var(--purple-neon);
        }
        .nav-links { display: flex; list-style: none; gap: 25px; }
        .nav-links a {
            color: var(--text-light); text-decoration: none; font-weight: 500;
            font-size: 0.95rem; text-transform: uppercase; letter-spacing: 1px;
            transition: 0.3s; position: relative;
        }
        .nav-links a::after {
            content: ''; position: absolute; bottom: -5px; left: 0; width: 0; height: 2px;
            background: var(--blue-neon); transition: 0.3s;
        }
        .nav-links a:hover::after { width: 100%; }
        .nav-links a:hover { color: var(--blue-neon); text-shadow: 0 0 10px var(--blue-neon); }
        
        .menu-toggle { display: none; color: #fff; font-size: 1.5rem; cursor: pointer; }

        /* Global Sections & Layout Components */
        section { padding: 100px 20px; max-width: 1400px; margin: 0 auto; }
        .section-title {
            font-family: var(--font-title); font-size: 2.5rem; text-align: center;
            margin-bottom: 60px; text-transform: uppercase; letter-spacing: 3px;
            text-shadow: 0 0 10px var(--purple-neon); position: relative;
        }
        .section-title::after {
            content: ''; display: block; width: 60px; height: 4px; 
            background: linear-gradient(90deg, var(--purple-neon), var(--blue-neon));
            margin: 15px auto 0; border-radius: 2px;
        }
        .glass-panel {
            background: var(--glass-bg); border: 1px solid var(--glass-border);
            border-radius: 16px; backdrop-filter: blur(16px); padding: 30px;
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        /* Hero Section */
        #home {
            min-height: 100vh; display: flex; align-items: center; justify-content: center;
            padding-top: 120px; position: relative;
        }
        .hero-container {
            display: grid; grid-template-columns: 1fr 1fr; gap: 50px; align-items: center; width: 100%;
        }
        .hero-art { position: relative; display: flex; justify-content: center; }
        .hero-img-wrapper {
            position: relative; width: 380px; height: 380px; border-radius: 50%;
            padding: 5px; background: linear-gradient(45deg, var(--purple-neon), var(--blue-neon));
            animation: float 6s ease-in-out infinite;
            box-shadow: 0 0 30px rgba(188, 19, 254, 0.4);
        }
        .hero-img-wrapper img {
            width: 100%; height: 100%; object-fit: cover; border-radius: 50%;
        }
        .hero-info h2 { font-size: 1.2rem; color: var(--blue-neon); letter-spacing: 4px; margin-bottom: 10px; font-family: var(--font-title);}
        .hero-info h1 { font-family: var(--font-title); font-size: 4.5rem; font-weight: 900; line-height: 1.1; margin-bottom: 20px; text-shadow: 0 0 15px rgba(255,255,255,0.2); }
        .hero-slogan { font-size: 1.2rem; italic: true; color: var(--text-muted); margin-bottom: 30px; border-left: 3px solid var(--purple-neon); padding-left: 15px; }
        
        .social-buttons { display: flex; gap: 15px; flex-wrap: wrap; margin-bottom: 35px; }
        .btn-social {
            padding: 12px 25px; border-radius: 30px; text-decoration: none; font-weight: 700;
            display: inline-flex; align-items: center; gap: 10px; transition: 0.3s;
            font-size: 0.9rem; letter-spacing: 0.5px;
        }
        .btn-tiktok { background: #000; color: #fff; border: 1px solid rgba(255,255,255,0.2); }
        .btn-facebook { background: #1877f2; color: #fff; }
        .btn-youtube { background: #ff0000; color: #fff; }
        .btn-instagram { background: linear-gradient(45deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%); color: #fff; }
        .btn-social:hover { transform: translateY(-3px); box-shadow: 0 5px 15px rgba(255,255,255,0.2); }
        
        .btn-primary {
            display: inline-flex; align-items: center; gap: 10px; padding: 15px 40px;
            background: linear-gradient(90deg, var(--purple-neon), var(--blue-neon));
            color: #fff; font-family: var(--font-title); font-weight: 700; text-decoration: none;
            border-radius: 50px; border: none; cursor: pointer; transition: 0.3s;
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.3);
        }
        .btn-primary:hover { transform: scale(1.05); box-shadow: 0 0 30px var(--purple-neon); }

        /* About Section */
        .about-grid { display: grid; grid-template-columns: 1fr 1.2fr; gap: 40px; }
        .about-stats-mini { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; margin-top: 30px; }
        .stat-mini-box { padding: 20px; text-align: center; background: rgba(255,255,255,0.03); border-radius: 12px; border: 1px solid rgba(255,255,255,0.05); }
        .stat-mini-box i { font-size: 1.8rem; color: var(--blue-neon); margin-bottom: 10px; }
        .about-text p { color: var(--text-muted); line-height: 1.8; margin-bottom: 20px; font-size: 1.05rem; }

        /* Music Section - Spotify Style */
        .music-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; }
        .music-card {
            background: #120c1f; border: 1px solid rgba(255,255,255,0.05); border-radius: 12px;
            padding: 20px; transition: 0.3s ease; display: flex; flex-direction: column; gap: 15px;
        }
        .music-card:hover {
            background: #1c142e; border-color: var(--purple-neon); transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(188,19,254,0.15);
        }
        .thumb-container {
            width: 100%; aspect-ratio: 16/9; border-radius: 8px; overflow: hidden; position: relative;
            background: #000;
        }
        .thumb-container img { width: 100%; height: 100%; object-fit: cover; transition: 0.5s; }
        .music-card:hover .thumb-container img { transform: scale(1.05); }
        .video-overlay-btn {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.4); display: flex; justify-content: center; align-items: center;
            opacity: 0; transition: 0.3s; cursor: pointer; border: none;
        }
        .video-overlay-btn i { color: #fff; font-size: 2.5rem; text-shadow: 0 0 10px var(--blue-neon); }
        .thumb-container:hover .video-overlay-btn { opacity: 1; }
        .music-info h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 5px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .music-info p { color: var(--text-muted); font-size: 0.85rem; }
        .btn-listen-yt {
            margin-top: auto; width: 100%; padding: 10px; background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.1); border-radius: 6px; color: #fff; text-decoration: none;
            text-align: center; font-size: 0.85rem; font-weight: 600; display: flex; justify-content: center;
            align-items: center; gap: 8px; transition: 0.3s;
        }
        .btn-listen-yt:hover { background: #ff0000; border-color: #ff0000; }

        /* TikTok Section */
        .tiktok-grid {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 20px;
        }
        .tiktok-card {
            background: #000; border-radius: 14px; overflow: hidden; position: relative;
            border: 1px solid rgba(255,255,255,0.05); transition: 0.3s; aspect-ratio: 9/16;
        }
        .tiktok-card:hover {
            transform: translateY(-5px); border-color: var(--blue-neon);
            box-shadow: 0 10px 25px rgba(0, 243, 255, 0.2);
        }
        .tiktok-placeholder {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            background: linear-gradient(180deg, #111, #000); padding: 20px; text-align: center;
            z-index: 1; transition: 0.3s;
        }
        .tiktok-placeholder i { font-size: 2.5rem; margin-bottom: 15px; color: var(--blue-neon); }
        .tiktok-placeholder a {
            margin-top: 15px; padding: 8px 18px; background: var(--text-light); color: #000;
            text-decoration: none; font-weight: 700; border-radius: 20px; font-size: 0.8rem;
        }
        .tiktok-card iframe {
            width: 100%; height: 100%; border: none; position: absolute; top: 0; left: 0; z-index: 2;
            opacity: 0; transition: opacity 0.5s;
        }

        /* Dashboard Statistics */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 25px; }
        .stat-card {
            padding: 30px; border-radius: 16px; text-align: center; transition: 0.3s;
            position: relative; overflow: hidden;
        }
        .stat-card::before {
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 4px;
        }
        .stat-tiktok::before { background: var(--blue-neon); }
        .stat-youtube::before { background: #ff0000; }
        .stat-facebook::before { background: #1877f2; }
        .stat-instagram::before { background: var(--purple-neon); }
        
        .stat-icon { font-size: 2.2rem; margin-bottom: 15px; }
        .stat-card h4 { font-size: 0.9rem; text-transform: uppercase; color: var(--text-muted); letter-spacing: 1px; margin-bottom: 10px; }
        .counter-group { display: flex; flex-direction: column; gap: 8px; margin-bottom: 5px; }
        .counter-item { font-size: 1.8rem; font-family: var(--font-title); font-weight: 700; color: #fff; }
        .counter-label { font-size: 0.75rem; color: var(--text-muted); display: block; margin-top: -3px; margin-bottom: 8px; }

        /* Band Section */
        .band-intro { text-align: center; max-width: 800px; margin: 0 auto 50px; }
        .band-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 30px; }
        .flip-card { background-color: transparent; width: 100%; height: 350px; perspective: 1000px; }
        .flip-card-inner {
            position: relative; width: 100%; height: 100%; text-align: center;
            transition: transform 0.6s; transform-style: preserve-3d;
        }
        .flip-card:hover .flip-card-inner { transform: rotateY(180deg); }
        .flip-card-front, .flip-card-back {
            position: absolute; width: 100%; height: 100%; -webkit-backface-visibility: hidden;
            backface-visibility: hidden; border-radius: 16px; display: flex; flex-direction: column;
            justify-content: center; align-items: center; padding: 20px;
        }
        .flip-card-front {
            background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05);
        }
        .member-avatar {
            width: 120px; height: 120px; border-radius: 50%; background: #222; margin-bottom: 20px;
            display: flex; justify-content: center; align-items: center; font-size: 2.5rem; color: var(--purple-neon);
            border: 2px solid var(--glass-border);
        }
        .flip-card-front h3 { font-family: var(--font-title); font-size: 1.3rem; margin-bottom: 8px; }
        .flip-card-front p { color: var(--blue-neon); font-size: 0.9rem; font-weight: 600; }
        .flip-card-back {
            background: linear-gradient(135deg, rgba(188,19,254,0.2), rgba(0,243,255,0.2));
            border: 1px solid var(--purple-neon); transform: rotateY(180deg);
        }
        .flip-card-back p { font-size: 0.95rem; line-height: 1.6; }

        /* Photo Gallery */
        .gallery-filter { display: flex; justify-content: center; gap: 15px; margin-bottom: 40px; flex-wrap: wrap; }
        .filter-btn {
            background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1);
            color: #fff; padding: 10px 22px; border-radius: 25px; cursor: pointer; transition: 0.3s;
            font-family: var(--font-title); font-size: 0.8rem;
        }
        .filter-btn.active, .filter-btn:hover {
            background: var(--purple-neon); border-color: var(--purple-neon);
            box-shadow: 0 0 15px var(--purple-neon);
        }
        .gallery-masonry {
            columns: 4 250px; column-gap: 20px;
        }
        .gallery-item {
            background: var(--glass-bg); border-radius: 12px; overflow: hidden;
            margin-bottom: 20px; break-inside: avoid; border: 1px solid rgba(255,255,255,0.05);
            position: relative; cursor: pointer;
        }
        .gallery-item img { width: 100%; display: block; transition: 0.4s; }
        .gallery-img-placeholder {
            width: 100%; height: 200px; background: #1a1326; display: flex;
            flex-direction: column; justify-content: center; align-items: center; color: var(--text-muted);
        }
        .gallery-img-placeholder i { font-size: 2rem; margin-bottom: 10px; color: var(--purple-neon); }
        .gallery-item:hover img { transform: scale(1.05); }
        
        /* Lightbox Layout */
        #lightbox {
            position: fixed; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.9);
            z-index: 10000; display: none; justify-content: center; align-items: center;
        }
        #lightbox img { max-width: 90%; max-height: 80%; border-radius: 8px; box-shadow: 0 0 30px rgba(0,0,0,0.5); }
        .lightbox-close { position: absolute; top: 30px; right: 40px; color: #fff; font-size: 2.5rem; cursor: pointer; }

        /* Fan Club */
        .fan-grid { display: grid; grid-template-columns: 1fr 1.2fr; gap: 40px; }
        .fan-form-group { margin-bottom: 20px; }
        .fan-form-group label { display: block; font-size: 0.85rem; text-transform: uppercase; margin-bottom: 8px; color: var(--text-muted); }
        .fan-input {
            width: 100%; padding: 14px; background: rgba(0,0,0,0.2); border: 1px solid var(--glass-border);
            border-radius: 8px; color: #fff; font-family: var(--font-body); transition: 0.3s;
        }
        .fan-input:focus { outline: none; border-color: var(--blue-neon); box-shadow: 0 0 10px rgba(0,243,255,0.2); }
        
        .fan-stats-display {
            display: flex; align-items: center; gap: 20px; padding: 20px;
            background: linear-gradient(90deg, rgba(188,19,254,0.1), rgba(0,243,255,0.1));
            border-radius: 12px; margin-bottom: 30px; border: 1px solid rgba(255,255,255,0.05);
        }
        .fan-counter-number { font-size: 2.5rem; font-family: var(--font-title); font-weight: 900; color: var(--blue-neon); }
        .messages-list { max-height: 320px; overflow-y: auto; padding-right: 10px; display: flex; flex-direction: column; gap: 15px; }
        .message-item {
            padding: 15px; background: rgba(255,255,255,0.02); border-radius: 8px;
            border-left: 3px solid var(--purple-neon);
        }
        .message-header { display: flex; justify-content: space-between; font-size: 0.85rem; margin-bottom: 5px; }
        .message-name { font-weight: 700; color: var(--blue-neon); }
        .message-date { color: var(--text-muted); }
        .message-body { font-size: 0.95rem; color: rgba(255,255,255,0.85); line-height: 1.4; }

        /* Contact Section */
        .contact-wrapper { max-width: 600px; margin: 0 auto; text-align: center; }
        .contact-email {
            font-size: 1.8rem; font-family: var(--font-title); color: #fff; text-decoration: none;
            margin-top: 20px; display: inline-block; transition: 0.3s;
            text-shadow: 0 0 10px rgba(0,243,255,0.3);
        }
        .contact-email:hover { color: var(--blue-neon); text-shadow: 0 0 20px var(--blue-neon); }

        /* Footer */
        footer {
            background: #05020a; padding: 40px 20px; text-align: center;
            border-top: 1px solid var(--glass-border); font-size: 0.9rem; color: var(--text-muted);
        }
        .back-to-top {
            position: fixed; bottom: 30px; right: 30px; width: 45px; height: 45px;
            background: var(--purple-neon); color: #fff; border: none; border-radius: 50%;
            cursor: pointer; display: none; justify-content: center; align-items: center;
            z-index: 99; transition: 0.3s; box-shadow: 0 0 15px var(--purple-neon);
        }
        .back-to-top:hover { transform: translateY(-5px); background: var(--blue-neon); box-shadow: 0 0 15px var(--blue-neon); }

        /* Video Modal Player */
        #video-modal {
            position: fixed; top:0; left:0; width:100%; height:100%; background: rgba(0,0,0,0.95);
            z-index: 10001; display: none; justify-content: center; align-items: center;
        }
        .modal-content { width: 90%; max-width: 800px; aspect-ratio: 16/9; position: relative; }
        .modal-content iframe { width: 100%; height: 100%; border: none; }
        .modal-close { position: absolute; top: -40px; right: 0; color: #fff; font-size: 2rem; cursor: pointer; }

        /* Animations */
        @keyframes load { 0% { width: 0%; } 100% { width: 100%; } }
        @keyframes pulse { 0% { opacity: 0.6; } 100% { opacity: 1; } }
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }

        /* Responsive Design */
        @media (max-width: 992px) {
            .hero-container, .about-grid, .fan-grid { grid-template-columns: 1fr; text-align: center; }
            .hero-art { order: -1; }
            .hero-info h1 { font-size: 3rem; }
            .hero-slogan { border-left: none; border-top: 2px solid var(--purple-neon); padding-left: 0; padding-top: 15px; }
            .social-buttons { justify-content: center; }
            .menu-toggle { display: block; }
            .nav-links {
                position: absolute; top: 100%; left: 0; width: 100%; background: #0a0512;
                flex-direction: column; padding: 20px; gap: 15px; display: none;
                border-bottom: 1px solid var(--glass-border);
            }
            .nav-links.active { display: flex; }
        }
    </style>
</head>
<body>

    <!-- Loading Screen -->
    <div id="loading-screen">
        <div class="loader-logo">BITA NO</div>
        <div class="loader-bar"><div class="loader-progress"></div></div>
    </div>

    <!-- Custom Cursor Customization -->
    <div class="custom-cursor" id="cursor"></div>

    <!-- Background Particle Dynamic Effect -->
    <canvas id="particle-canvas"></canvas>

    <!-- Header Navigation -->
    <header>
        <div class="navbar">
            <a href="#home" class="logo">BITA NO</a>
            <div class="menu-toggle" id="mobile-menu-btn"><i class="fas fa-bars"></i></div>
            <ul class="nav-links" id="nav-menu">
                <li><a href="#home">Trang Chủ</a></li>
                <li><a href="#about">Giới Thiệu</a></li>
                <li><a href="#music">Âm Nhạc</a></li>
                <li><a href="#tiktok">TikTok</a></li>
                <li><a href="#stats">Thống Kê</a></li>
                <li><a href="#band">Mũ Len.</a></li>
                <li><a href="#gallery">Thư Viện</a></li>
                <li><a href="#fanclub">Fan Club</a></li>
                <li><a href="#contact">Liên Hệ</a></li>
            </ul>
        </div>
    </header>

    <!-- Hero Section -->
    <section id="home">
        <div class="hero-container">
            <div class="hero-info">
                <h2>OFFICIAL ARTIST SITE</h2>
                <h1>BITA NO</h1>
                <p class="hero-slogan">"Âm nhạc là cách tôi kể câu chuyện của mình."</p>
                <div class="social-buttons">
                    <a href="https://www.tiktok.com/@basskitball08" target="_blank" class="btn-social btn-tiktok"><i class="fab fa-tiktok"></i> TikTok</a>
                    <a href="https://www.facebook.com/profile.php?id=61590635181855" target="_blank" class="btn-social btn-facebook"><i class="fab fa-facebook-f"></i> Facebook</a>
                    <a href="https://www.youtube.com/@Bi-Ta-No-08" target="_blank" class="btn-social btn-youtube"><i class="fab fa-youtube"></i> YouTube</a>
                    <a href="https://www.instagram.com/Basskitball" target="_blank" class="btn-social btn-instagram"><i class="fab fa-instagram"></i> Instagram</a>
                </div>
                <a href="#music" class="btn-primary"><i class="fas fa-play"></i> Nghe Nhạc Ngay</a>
            </div>
            <div class="hero-art">
                <div class="hero-img-wrapper">
                    <!-- Ảnh Đại diện chính của Artist -->
                    <img src="bitano.jpg" alt="Bita No Official Picture" onerror="this.src='https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?q=80&w=600&auto=format&fit=crop'">
                </div>
            </div>
        </div>
    </section>

    <!-- About Section -->
    <section id="about">
        <h2 class="section-title">Giới Thiệu</h2>
        <div class="glass-panel about-grid">
            <div class="about-text">
                <p><strong>Bita No</strong> là một nghệ sĩ trẻ đa tài năng hiện đang sinh sống, học tập và hoạt động nghệ thuật tại Thành phố Hồ Chí Minh, Việt Nam. Với tư duy âm nhạc hiện đại cùng niềm đam mê cháy bỏng, Bita No không ngừng biến hóa và khẳng định dấu ấn riêng trên thị trường âm nhạc.</p>
                <p>Hoạt động năng nổ với nhiều vai trò như <em>Vocalist, Bassist, Singer, Content Creator</em> và <em>Music Creator</em>, anh mang tới một làn gió sáng tạo mới mẻ thông qua từng giai điệu và nội dung số truyền tải đến cộng đồng.</p>
                <p>Hiện tại, Bita No đang giữ vai trò cốt lõi là <strong>Vocalist & Bassist</strong> của ban nhạc <strong>Mũ Len.</strong> - một tập hợp những cá tính âm nhạc độc đáo, cùng nhau kiến tạo nên những không gian âm thanh đầy nhiệt huyết và chiều sâu cảm xúc định hướng tương lai vững chắc.</p>
            </div>
            <div>
                <div class="stat-mini-box" style="margin-bottom: 20px;">
                    <i class="fas fa-map-marker-alt"></i>
                    <h3>Hoạt Động</h3>
                    <p style="color: var(--text-muted); margin-top:5px;">TP. Hồ Chí Minh, Việt Nam</p>
                </div>
                <div class="about-stats-mini">
                    <div class="stat-mini-box">
                        <i class="fas fa-microphone"></i>
                        <h4>Vocalist</h4>
                    </div>
                    <div class="stat-mini-box">
                        <i class="fas fa-guitar"></i>
                        <h4>Bassist</h4>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Music Section (Spotify Style) -->
    <section id="music">
        <h2 class="section-title">Âm Nhạc</h2>
        <div class="music-grid">
            <!-- Demo 1 -->
            <div class="music-card">
                <div class="thumb-container">
                    <img src="https://img.youtube.com/vi/lm78h9jjgdM/hqdefault.jpg" alt="Demo Cover">
                    <button class="video-overlay-btn" onclick="openVideoPlayer('lm78h9jjgdM')">
                        <i class="fas fa-play-circle"></i>
                    </button>
                </div>
                <div class="music-info">
                    <h3>Bita No Shorts Demo 1</h3>
                    <p>Mũ Len. Records</p>
                </div>
                <a href="https://youtube.com/shorts/lm78h9jjgdM" target="_blank" class="btn-listen-yt"><i class="fab fa-youtube"></i> Mở YouTube</a>
            </div>

            <!-- Demo 2 -->
            <div class="music-card">
                <div class="thumb-container">
                    <img src="https://img.youtube.com/vi/Qiyv9q0zIXk/hqdefault.jpg" alt="Demo Cover">
                    <button class="video-overlay-btn" onclick="openVideoPlayer('Qiyv9q0zIXk')">
                        <i class="fas fa-play-circle"></i>
                    </button>
                </div>
                <div class="music-info">
                    <h3>Bita No Shorts Demo 2</h3>
                    <p>Mũ Len. Records</p>
                </div>
                <a href="https://youtube.com/shorts/Qiyv9q0zIXk" target="_blank" class="btn-listen-yt"><i class="fab fa-youtube"></i> Mở YouTube</a>
            </div>

            <!-- Track 3 -->
            <div class="music-card">
                <div class="thumb-container">
                    <img src="https://img.youtube.com/vi/gPPXkHWE0HA/hqdefault.jpg" alt="Demo Cover">
                    <button class="video-overlay-btn" onclick="openVideoPlayer('gPPXkHWE0HA')">
                        <i class="fas fa-play-circle"></i>
                    </button>
                </div>
                <div class="music-info">
                    <h3>Bita No Performance Track</h3>
                    <p>Mũ Len. Official</p>
                </div>
                <a href="https://youtu.be/gPPXkHWE0HA" target="_blank" class="btn-listen-yt"><i class="fab fa-youtube"></i> Mở YouTube</a>
            </div>

            <!-- Track 4 -->
            <div class="music-card">
                <div class="thumb-container">
                    <img src="https://img.youtube.com/vi/wMlG5hIaBCM/hqdefault.jpg" alt="Demo Cover">
                    <button class="video-overlay-btn" onclick="openVideoPlayer('wMlG5hIaBCM')">
                        <i class="fas fa-play-circle"></i>
                    </button>
                </div>
                <div class="music-info">
                    <h3>Bita No Studio Release</h3>
                    <p>Mũ Len. Official</p>
                </div>
                <a href="https://youtu.be/wMlG5hIaBCM" target="_blank" class="btn-listen-yt"><i class="fab fa-youtube"></i> Mở YouTube</a>
            </div>
        </div>
    </section>

    <!-- TikTok Gallery Section -->
    <section id="tiktok">
        <h2 class="section-title">Video TikTok</h2>
        <div class="tiktok-grid" id="tiktok-container">
            <!-- Sẽ được render tự động qua JavaScript cấu trúc tối ưu lười tải (Lazy Load) -->
        </div>
    </section>

    <!-- Dashboard Statistics -->
    <section id="stats">
        <h2 class="section-title">Thống Kê Kênh</h2>
        <div class="stats-grid">
            <div class="glass-panel stat-card stat-tiktok">
                <div class="stat-icon" style="color: var(--blue-neon);"><i class="fab fa-tiktok"></i></div>
                <h4>TikTok</h4>
                <div class="counter-group">
                    <div><span class="counter-item" data-target="15200">0</span></div>
                    <span class="counter-label">Followers</span>
                    <div><span class="counter-item" data-target="243000">0</span></div>
                    <span class="counter-label">Likes</span>
                </div>
            </div>
            <div class="glass-panel stat-card stat-youtube">
                <div class="stat-icon" style="color: #ff0000;"><i class="fab fa-youtube"></i></div>
                <h4>YouTube</h4>
                <div class="counter-group">
                    <div><span class="counter-item" data-target="3400">0</span></div>
                    <span class="counter-label">Subscribers</span>
                    <div><span class="counter-item" data-target="150000">0</span></div>
                    <span class="counter-label">Views</span>
                </div>
            </div>
            <div class="glass-panel stat-card stat-facebook">
                <div class="stat-icon" style="color: #1877f2;"><i class="fab fa-facebook-f"></i></div>
                <h4>Facebook</h4>
                <div class="counter-group">
                    <div><span class="counter-item" data-target="5800">0</span></div>
                    <span class="counter-label">Followers</span>
                </div>
            </div>
            <div class="glass-panel stat-card stat-instagram">
                <div class="stat-icon" style="color: var(--purple-neon);"><i class="fab fa-instagram"></i></div>
                <h4>Instagram</h4>
                <div class="counter-group">
                    <div><span class="counter-item" data-target="2100">0</span></div>
                    <span class="counter-label">Followers</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Band Mũ Len. Section -->
    <section id="band">
        <h2 class="section-title">Ban Nhạc Mũ Len.</h2>
        <div class="band-intro">
            <p class="glass-panel"><strong>Mũ Len.</strong> là tổ hợp âm nhạc tự do sáng tạo, nơi tụ hội những mảnh ghép nghệ thuật cá tính sắc nét. Với định hướng lấy trải nghiệm và cảm xúc người nghe làm trung tâm, Mũ Len. đang không ngừng hoàn thiện các dự án phòng thu âm chuyên nghiệp cùng chuỗi hoạt động Live Performance ấn tượng.</p>
        </div>
        <div class="band-grid">
            <!-- Member 1 -->
            <div class="flip-card">
                <div class="flip-card-inner">
                    <div class="flip-card-front">
                        <div class="member-avatar"><i class="fas fa-user"></i></div>
                        <h3>Vịt Vàng</h3>
                        <p>Vocalist / Guitarist</p>
                    </div>
                    <div class="flip-card-back">
                        <h3>Vịt Vàng</h3>
                        <p style="margin-top: 15px;">Dẫn dắt tuyến giai điệu mộc mạc và truyền tải linh hồn của các sáng tác qua từng phím đàn và giọng hát cuốn hút.</p>
                    </div>
                </div>
            </div>
            <!-- Member 2 -->
            <div class="flip-card">
                <div class="flip-card-inner">
                    <div class="flip-card-front">
                        <div class="member-avatar" style="color: var(--blue-neon); border-color: var(--blue-neon);"><i class="fas fa-star"></i></div>
                        <h3>Bita No</h3>
                        <p>Vocalist / Bassist</p>
                    </div>
                    <div class="flip-card-back">
                        <h3>Bita No</h3>
                        <p style="margin-top: 15px;">Giữ nhịp điệu xương sống của ban nhạc bằng các câu bass uy lực, đồng thời đảm nhiệm các bè phối vocal đỉnh cao.</p>
                    </div>
                </div>
            </div>
            <!-- Member 3 -->
            <div class="flip-card">
                <div class="flip-card-inner">
                    <div class="flip-card-front">
                        <div class="member-avatar"><i class="fas fa-user"></i></div>
                        <h3>Len Nguyễn</h3>
                        <p>Guitarist</p>
                    </div>
                    <div class="flip-card-back">
                        <h3>Len Nguyễn</h3>
                        <p style="margin-top: 15px;">Phù thủy âm thanh kiến tạo những dải không gian riff kịch tính, lấp đầy năng lượng cho các bài phối khí phối hợp.</p>
                    </div>
                </div>
            </div>
            <!-- Member 4 -->
            <div class="flip-card">
                <div class="flip-card-inner">
                    <div class="flip-card-front">
                        <div class="member-avatar"><i class="fas fa-user"></i></div>
                        <h3>Sơnn Đinhh</h3>
                        <p>Drummer</p>
                    </div>
                    <div class="flip-card-back">
                        <h3>Sơnn Đinhh</h3>
                        <p style="margin-top: 15px;">Cỗ máy thời gian định hình tốc độ, tạo điểm nhấn cao trào bùng nổ cho mọi buổi trình diễn trực tiếp.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Photo Gallery Section -->
    <section id="gallery">
        <h2 class="section-title">Thư Viện Ảnh</h2>
        <div class="gallery-filter">
            <button class="filter-btn active" onclick="filterGallery('all')">Tất Cả</button>
            <button class="filter-btn" onclick="filterGallery('lifestyle')">Đời Thường</button>
            <button class="filter-btn" onclick="filterGallery('performance')">Biểu Diễn</button>
            <button class="filter-btn" onclick="filterGallery('backstage')">Hậu Trường</button>
            <button class="filter-btn" onclick="filterGallery('band-cat')">Ban Nhạc</button>
        </div>
        <div class="gallery-masonry" id="masonry-gallery">
            <!-- Sử dụng placeholder nghệ thuật tích hợp sẫn để hiển thị kiến trúc Masonry hoàn hảo -->
            <div class="gallery-item lifestyle" onclick="openLightbox(this)">
                <div class="gallery-img-placeholder"><i class="fas fa-camera"></i><span>Đời Thường 1</span></div>
            </div>
            <div class="gallery-item performance" onclick="openLightbox(this)">
                <div class="gallery-img-placeholder"><i class="fas fa-music"></i><span>Biểu Diễn 1</span></div>
            </div>
            <div class="gallery-item backstage" onclick="openLightbox(this)">
                <div class="gallery-img-placeholder"><i class="fas fa-user-friends"></i><span>Hậu Trường 1</span></div>
            </div>
            <div class="gallery-item band-cat" onclick="openLightbox(this)">
                <div class="gallery-img-placeholder"><i class="fas fa-guitar"></i><span>Mũ Len. Photo</span></div>
            </div>
            <div class="gallery-item performance" onclick="openLightbox(this)">
                <div class="gallery-img-placeholder"><i class="fas fa-microphone-alt"></i><span>Biểu Diễn 2</span></div>
            </div>
            <div class="gallery-item lifestyle" onclick="openLightbox(this)">
                <div class="gallery-img-placeholder"><i class="fas fa-image"></i><span>Đời Thường 2</span></div>
            </div>
        </div>
    </section>

    <!-- Lightbox Element -->
    <div id="lightbox">
        <span class="lightbox-close" onclick="closeLightbox()">&times;</span>
        <div class="gallery-img-placeholder" id="lightbox-img" style="width: 80%; height: 60vh;"></div>
    </div>

    <!-- Fan Club Section -->
    <section id="fanclub">
        <h2 class="section-title">Fan Club Cộng Đồng</h2>
        <div class="fan-grid">
            <div class="glass-panel">
                <h3 style="font-family: var(--font-title); margin-bottom: 20px; color: var(--blue-neon);">ĐĂNG KÝ THÀNH VIÊN</h3>
                <form id="fan-form" onsubmit="handleFanSubmit(event)">
                    <div class="fan-form-group">
                        <label>Tên của bạn</label>
                        <input type="text" class="fan-input" id="fan-name" required placeholder="Nhập biệt danh của bạn...">
                    </div>
                    <div class="fan-form-group">
                        <label>Lời nhắn gửi đến Bita No</label>
                        <textarea class="fan-input" id="fan-msg" rows="4" required placeholder="Viết những lời yêu thương hoặc lời chúc..."></textarea>
                    </div>
                    <button type="submit" class="btn-primary" style="width: 100%; justify-content: center;">Gửi Lời Nhắn</button>
                </form>
            </div>
            <div class="glass-panel" style="display: flex; flex-direction: column;">
                <div class="fan-stats-display">
                    <div>
                        <div class="fan-counter-number" id="fan-total-count">1,248</div>
                        <span style="font-size: 0.85rem; text-transform: uppercase; color: var(--text-muted);">Người hâm mộ chính thức</span>
                    </div>
                </div>
                <h4 style="font-family: var(--font-title); margin-bottom: 15px; font-size: 0.9rem; letter-spacing: 1px;">LỜI NHẮN MỚI NHẤT</h4>
                <div class="messages-list" id="messages-container">
                    <div class="message-item">
                        <div class="message-header">
                            <span class="message-name">Minh Hoàng</span>
                            <span class="message-date">Vừa xong</span>
                        </div>
                        <div class="message-body">Tiếng bass trong bài demo cuốn quá anh ơi! Mong chờ sản phẩm chính thức từ Mũ Len.!</div>
                    </div>
                    <div class="message-item">
                        <div class="message-header">
                            <span class="message-name">Phương Linh</span>
                            <span class="message-date">10 phút trước</span>
                        </div>
                        <div class="message-body">Chúc anh Bita No và ban nhạc gặt hái được thật nhiều thành công tại Sài Gòn ạ. Luôn ủng hộ anh!</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact">
        <h2 class="section-title">Liên Hệ Hợp Tác</h2>
        <div class="glass-panel contact-wrapper">
            <p style="color: var(--text-muted); font-size: 1.1rem;">Mọi yêu cầu công việc, Booking Show diễn của Bita No hoặc Ban nhạc Mũ Len., vui lòng liên hệ qua email chính thức:</p>
            <a href="mailto:congviet550@gmail.com" class="contact-email">congviet550@gmail.com</a>
            <div style="margin-top: 30px; display: flex; justify-content: center; gap: 20px; font-size: 1.5rem;">
                <a href="https://www.tiktok.com/@basskitball08" target="_blank" style="color: #fff;"><i class="fab fa-tiktok"></i></a>
                <a href="https://www.facebook.com/profile.php?id=61590635181855" target="_blank" style="color: #fff;"><i class="fab fa-facebook"></i></a>
                <a href="https://www.youtube.com/@Bi-Ta-No-08" target="_blank" style="color: #fff;"><i class="fab fa-youtube"></i></a>
                <a href="https://www.instagram.com/Basskitball" target="_blank" style="color: #fff;"><i class="fab fa-instagram"></i></a>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <p>&copy; 2026 BITA NO Official Website. All Rights Reserved. | Designed with Passion</p>
        <p style="font-size: 0.75rem; color: rgba(255,255,255,0.2); margin-top: 5px;">Lượt truy cập hệ thống: <span id="visitor-count">24,512</span></p>
    </footer>

    <!-- Video Multi-player Modal Component -->
    <div id="video-modal">
        <div class="modal-content">
            <span class="modal-close" onclick="closeVideoPlayer()">&times;</span>
            <iframe id="modal-iframe" src="" allow="autoplay; encrypted-media" allowfullscreen></iframe>
        </div>
    </div>

    <!-- Back To Top Button -->
    <button class="back-to-top" id="scrollTopBtn" onclick="scrollToTop()"><i class="fas fa-chevron-up"></i></button>

    <script>
        // Array dữ liệu video TikTok được cấp sẵn từ nguồn yêu cầu
        const tiktokVideos = [
            "7647041715697683719", "7641635799502474503", "7627896752695299346", 
            "7624198861057166599", "7617161966867533074", "7598585394648616200", 
            "7594795845074078984", "7584462533327736071", "7582615323472301332", 
            "7575607481057938706", "7562211229868117268", "7532104438480260370", 
            "7525489182467247381"
        ];

        // Khởi chạy khi tài liệu tải hoàn tất
        window.addEventListener('DOMContentLoaded', () => {
            initTikTokGrid();
            initParticles();
            initCustomCursor();
            setupCounterAnimation();
            
            // Tắt màn hình chờ sau khoảng thời gian dựng khung hình xong
            setTimeout(() => {
                const loader = document.getElementById('loading-screen');
                loader.style.opacity = '0';
                setTimeout(() => loader.style.display = 'none', 500);
            }, 1200);

            // Cập nhật số đếm khách ngẫu nhiên sinh động cho môi trường giả lập Static
            document.getElementById('visitor-count').innerText = (Math.floor(Math.random() * 500) + 24512).toLocaleString();
        });

        // Thiết lập Menu điều hướng di động linh hoạt
        const mobileMenuBtn = document.getElementById('mobile-menu-btn');
        const navMenu = document.getElementById('nav-menu');
        mobileMenuBtn.addEventListener('click', () => {
            navMenu.classList.toggle('active');
        });
        navMenu.querySelectorAll('a').forEach(link => {
            link.addEventListener('click', () => navMenu.classList.remove('active'));
        });

        // Render cấu trúc lưới liên kết mạng xã hội TikTok thông minh tránh treo tài nguyên hệ thống
        function initTikTokGrid() {
            const container = document.getElementById('tiktok-container');
            tiktokVideos.forEach((id, index) => {
                const card = document.createElement('div');
                card.className = 'tiktok-card';
                card.innerHTML = `
                    <div class="tiktok-placeholder" id="placeholder-${id}">
                        <i class="fab fa-tiktok"></i>
                        <h5>TikTok Clip #${index + 1}</h5>
                        <a href="https://www.tiktok.com/@basskitball08/video/${id}" target="_blank">Xem Clip</a>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Trình phát Media Modal YouTube đa năng hỗ trợ cả Shorts & Video chuẩn
        function openVideoPlayer(videoId) {
            const modal = document.getElementById('video-modal');
            const iframe = document.getElementById('modal-iframe');
            iframe.src = `https://www.youtube.com/embed/${videoId}?autoplay=1`;
            modal.style.display = 'flex';
        }
        function closeVideoPlayer() {
            const modal = document.getElementById('video-modal');
            const iframe = document.getElementById('modal-iframe');
            iframe.src = '';
            modal.style.display = 'none';
        }

        // Hệ thống cấu trúc bộ đếm Số liệu tăng trưởng mượt mà (Dashboard Counter)
        function setupCounterAnimation() {
            const counters = document.querySelectorAll('.counter-item');
            const speed = 60;

            const startCounter = (counter) => {
                const target = +counter.getAttribute('data-target');
                const updateCount = () => {
                    const count = +counter.innerText.replace(/,/g, '');
                    const inc = target / speed;
                    if (count < target) {
                        counter.innerText = Math.ceil(count + inc).toLocaleString();
                        setTimeout(updateCount, 25);
                    } else {
                        counter.innerText = target.toLocaleString();
                    }
                };
                updateCount();
            };

            // Sử dụng IntersectionObserver tối ưu tài nguyên chỉ chạy khi cuộn tới vị trí Dashboard
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if(entry.isIntersecting) {
                        startCounter(entry.target);
                        observer.unobserve(entry.target);
                    }
                });
            }, { threshold: 0.5 });

            counters.forEach(counter => observer.observe(counter));
        }

        // Bộ lọc chuyên mục Thư viện ảnh (Masonry Gallery Filter)
        function filterGallery(category) {
            const items = document.querySelectorAll('.gallery-item');
            const buttons = document.querySelectorAll('.filter-btn');
            
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            items.forEach(item => {
                if (category === 'all' || item.classList.contains(category)) {
                    item.style.display = 'block';
                } else {
                    item.style.display = 'none';
                }
            });
        }

        // Hệ thống Lightbox hiển thị ảnh phóng to tiện ích
        function openLightbox(element) {
            const lightbox = document.getElementById('lightbox');
            const lightboxImg = document.getElementById('lightbox-img');
            lightboxImg.innerHTML = element.innerHTML;
            lightbox.style.display = 'flex';
        }
        function closeLightbox() {
            document.getElementById('lightbox').style.display = 'none';
        }

        // Xử lý Sự kiện Tương tác Đăng ký gửi thông điệp của Fan Club
        function handleFanSubmit(e) {
            e.preventDefault();
            const nameInput = document.getElementById('fan-name');
            const msgInput = document.getElementById('fan-msg');
            const container = document.getElementById('messages-container');
            const totalCount = document.getElementById('fan-total-count');

            if(!nameInput.value.trim() || !msgInput.value.trim()) return;

            // Đưa tin nhắn mới lên đầu danh sách hiển thị
            const newItem = document.createElement('div');
            newItem.className = 'message-item';
            newItem.style.borderLeftColor = 'var(--blue-neon)';
            newItem.innerHTML = `
                <div class="message-header">
                    <span class="message-name">${escapeHTML(nameInput.value)}</span>
                    <span class="message-date">Vừa xong</span>
                </div>
                <div class="message-body">${escapeHTML(msgInput.value)}</div>
            `;
            container.insertBefore(newItem, container.firstChild);

            // Cập nhật số lượng fan tăng lên tượng trưng lập tức
            let currentFans = parseInt(totalCount.innerText.replace(/,/g, ''));
            totalCount.innerText = (currentFans + 1).toLocaleString();

            // Reset form
            nameInput.value = '';
            msgInput.value = '';
        }

        function escapeHTML(str) {
            return str.replace(/[&<>'"]/g, tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag));
        }

        // Điều khiển Nút di chuyển nhanh lên đầu trang (Back To Top Button)
        const scrollTopBtn = document.getElementById('scrollTopBtn');
        window.onscroll = function() {
            if (document.body.scrollTop > 400 || document.documentElement.scrollTop > 400) {
                scrollTopBtn.style.display = "flex";
            } else {
                scrollTopBtn.style.display = "none";
            }
        };
        function scrollToTop() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Hiệu ứng Con trỏ Chuột Custom di chuyển mượt
        function initCustomCursor() {
            const cursor = document.getElementById('cursor');
            document.addEventListener('mousemove', (e) => {
                cursor.style.left = e.clientX + 'px';
                cursor.style.top = e.clientY + 'px';
            });
            document.querySelectorAll('a, button, .gallery-item, .flip-card').forEach(elem => {
                elem.addEventListener('mouseenter', () => {
                    cursor.style.width = '40px'; cursor.style.height = '40px';
                    cursor.style.backgroundColor = 'rgba(0, 243, 255, 0.1)';
                });
                elem.addEventListener('mouseleave', () => {
                    cursor.style.width = '20px'; cursor.style.height = '20px';
                    cursor.style.backgroundColor = 'transparent';
                });
            });
        }

        // Công cụ tạo Hạt Neon chuyển động nền cao cấp (Particle Animation Layer)
        function initParticles() {
            const canvas = document.getElementById('particle-canvas');
            const ctx = canvas.getContext('2d');
            let particlesArray = [];
            
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            window.addEventListener('resize', () => {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            });

            class Particle {
                constructor() {
                    this.x = Math.random() * canvas.width;
                    this.y = Math.random() * canvas.height;
                    this.size = Math.random() * 2 + 0.5;
                    this.speedX = Math.random() * 0.5 - 0.25;
                    this.speedY = Math.random() * 0.5 - 0.25;
                    this.color = Math.random() > 0.5 ? 'rgba(188, 19, 254, 0.3)' : 'rgba(0, 243, 255, 0.2)';
                }
                update() {
                    this.x += this.speedX;
                    this.y += this.speedY;
                    if (this.x > canvas.width) this.x = 0;
                    if (this.x < 0) this.x = canvas.width;
                    if (this.y > canvas.height) this.y = 0;
                    if (this.y < 0) this.y = canvas.height;
                }
                draw() {
                    ctx.fillStyle = this.color;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                    ctx.fill();
                }
            }

            for (let i = 0; i < 65; i++) {
                particlesArray.push(new Particle());
            }

            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                particlesArray.forEach(p => {
                    p.update();
                    p.draw();
                });
                requestAnimationFrame(animate);
            }
            animate();
        }
    </script>
</body>
</html>
