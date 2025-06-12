<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Lumina Games - Visual Novel Studio</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Crimson+Text:wght@400;600;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Crimson Text', serif;
            background: #0a0a0f;
            color: #ffffff;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        /* Animated background */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 40% 40%, rgba(120, 119, 198, 0.2) 0%, transparent 50%),
                linear-gradient(135deg, #0f0c29 0%, #24243e 50%, #302b63 100%);
            z-index: -2;
            animation: backgroundShift 20s ease-in-out infinite;
        }
        
        @keyframes backgroundShift {
            0%, 100% { 
                background: 
                    radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                    radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.15) 0%, transparent 50%),
                    radial-gradient(circle at 40% 40%, rgba(120, 119, 198, 0.2) 0%, transparent 50%),
                    linear-gradient(135deg, #0f0c29 0%, #24243e 50%, #302b63 100%);
            }
            50% { 
                background: 
                    radial-gradient(circle at 80% 20%, rgba(120, 119, 198, 0.4) 0%, transparent 50%),
                    radial-gradient(circle at 20% 80%, rgba(255, 119, 198, 0.2) 0%, transparent 50%),
                    radial-gradient(circle at 60% 60%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                    linear-gradient(135deg, #24243e 0%, #302b63 50%, #0f0c29 100%);
            }
        }
        
        /* Floating particles */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }
        
        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            animation: float 6s infinite linear;
        }
        
        .particle:nth-child(1) { left: 10%; animation-delay: 0s; animation-duration: 8s; }
        .particle:nth-child(2) { left: 20%; animation-delay: 1s; animation-duration: 10s; }
        .particle:nth-child(3) { left: 30%; animation-delay: 2s; animation-duration: 6s; }
        .particle:nth-child(4) { left: 40%; animation-delay: 3s; animation-duration: 12s; }
        .particle:nth-child(5) { left: 50%; animation-delay: 4s; animation-duration: 8s; }
        .particle:nth-child(6) { left: 60%; animation-delay: 5s; animation-duration: 10s; }
        .particle:nth-child(7) { left: 70%; animation-delay: 6s; animation-duration: 6s; }
        .particle:nth-child(8) { left: 80%; animation-delay: 7s; animation-duration: 12s; }
        .particle:nth-child(9) { left: 90%; animation-delay: 8s; animation-duration: 8s; }
        
        @keyframes float {
            0% {
                transform: translateY(100vh) scale(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
                transform: scale(1);
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) scale(0);
                opacity: 0;
            }
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 2rem;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
            z-index: 1;
        }
        
        .hero-section {
            text-align: center;
            margin-bottom: 4rem;
        }
        
        .logo {
            font-family: 'Crimson Text', serif;
            font-size: clamp(3rem, 8vw, 5rem);
            font-weight: 600;
            margin-bottom: 1rem;
            background: linear-gradient(135deg, #ffffff 0%, #e0e7ff 30%, #c7d2fe 60%, #a5b4fc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            animation: glow 3s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from {
                text-shadow: 0 0 20px rgba(139, 92, 246, 0.5);
            }
            to {
                text-shadow: 0 0 30px rgba(139, 92, 246, 0.8), 0 0 40px rgba(139, 92, 246, 0.3);
            }
        }
        
        .logo::before {
            content: '✦';
            position: absolute;
            left: -2rem;
            top: 50%;
            transform: translateY(-50%);
            font-size: 2rem;
            animation: sparkle 2s ease-in-out infinite;
        }
        
        .logo::after {
            content: '✦';
            position: absolute;
            right: -2rem;
            top: 50%;
            transform: translateY(-50%);
            font-size: 2rem;
            animation: sparkle 2s ease-in-out infinite reverse;
        }
        
        @keyframes sparkle {
            0%, 100% { opacity: 0.4; transform: translateY(-50%) scale(1); }
            50% { opacity: 1; transform: translateY(-50%) scale(1.2); }
        }
        
        .tagline {
            font-size: clamp(1.1rem, 4vw, 1.5rem);
            font-weight: 300;
            margin-bottom: 2rem;
            color: #e0e7ff;
            letter-spacing: 0.5px;
        }
        
        .description {
            font-size: 1.1rem;
            line-height: 1.8;
            margin-bottom: 3rem;
            color: #cbd5e1;
            max-width: 600px;
            font-weight: 300;
        }
        
        .project-card {
            background: linear-gradient(135deg, 
                rgba(255, 255, 255, 0.1) 0%, 
                rgba(255, 255, 255, 0.05) 100%);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 24px;
            padding: 3rem 2.5rem;
            margin: 2rem 0;
            max-width: 700px;
            position: relative;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            overflow: hidden;
        }
        
        .project-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent 30%, rgba(139, 92, 246, 0.1) 50%, transparent 70%);
            transform: rotate(45deg);
            transition: all 0.6s;
            opacity: 0;
        }
        
        .project-card:hover::before {
            opacity: 1;
            transform: rotate(45deg) translate(20%, 20%);
        }
        
        .project-card:hover {
            transform: translateY(-10px);
            border-color: rgba(139, 92, 246, 0.4);
            box-shadow: 
                0 25px 50px rgba(0, 0, 0, 0.3),
                0 0 50px rgba(139, 92, 246, 0.2);
        }
        
        .project-title {
            font-family: 'Crimson Text', serif;
            font-size: 2.5rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 50%, #d97706 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            z-index: 1;
        }
        
        .project-desc {
            font-size: 1.1rem;
            line-height: 1.7;
            margin-bottom: 2rem;
            color: #e2e8f0;
            font-weight: 300;
            position: relative;
            z-index: 1;
        }
        
        .release-badge {
            display: inline-block;
            padding: 0.75rem 2rem;
            background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
            color: #1e293b;
            font-weight: 600;
            border-radius: 50px;
            font-size: 1rem;
            letter-spacing: 0.5px;
            box-shadow: 0 8px 25px rgba(251, 191, 36, 0.3);
            transition: all 0.3s ease;
            position: relative;
            z-index: 1;
        }
        
        .release-badge:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 35px rgba(251, 191, 36, 0.4);
        }
        
        .status-section {
            background: linear-gradient(135deg, 
                rgba(251, 191, 36, 0.1) 0%, 
                rgba(245, 158, 11, 0.05) 100%);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(251, 191, 36, 0.3);
            border-radius: 20px;
            padding: 2rem;
            margin: 2rem 0;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .status-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            animation: shimmer 3s infinite;
        }
        
        @keyframes shimmer {
            0% { left: -100%; }
            100% { left: 100%; }
        }
        
        .status-text {
            font-size: 1.2rem;
            font-weight: 500;
            color: #fbbf24;
            position: relative;
            z-index: 1;
        }
        
        .social-grid {
            display: flex;
            gap: 1.5rem;
            margin-top: 3rem;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .social-link {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            padding: 1rem 2rem;
            background: linear-gradient(135deg, 
                rgba(255, 255, 255, 0.1) 0%, 
                rgba(255, 255, 255, 0.05) 100%);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 50px;
            color: #ffffff;
            text-decoration: none;
            font-weight: 500;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }
        
        .social-link::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(139, 92, 246, 0.2), transparent);
            transition: left 0.5s;
        }
        
        .social-link:hover::before {
            left: 100%;
        }
        
        .social-link:hover {
            transform: translateY(-3px);
            border-color: rgba(139, 92, 246, 0.5);
            box-shadow: 0 15px 35px rgba(139, 92, 246, 0.2);
        }
        
        .social-icon {
            width: 20px;
            height: 20px;
            position: relative;
            z-index: 1;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 0 1rem;
            }
            
            .project-card {
                padding: 2rem 1.5rem;
                margin: 1rem 0;
            }
            
            .social-grid {
                gap: 1rem;
            }
            
            .social-link {
                padding: 0.75rem 1.5rem;
            }
            
            .logo::before,
            .logo::after {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="particles">
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
        <div class="particle"></div>
    </div>
    
    <div class="container">
        <div class="hero-section">
            <h1 class="logo">The Lumina Games</h1>
            <p class="tagline">Crafting Compelling Visual Novels</p>
            <p class="description">
                We create emotionally rich visual novels across multiple genres, exploring complex relationships through compelling characters and meaningful choices.
            </p>
        </div>
        
        <div class="project-card">
            <h2 class="project-title">🌿 Illithrin & Kira</h2>
            <p class="project-desc">
                Our debut fantasy romance visual novel. A desperate healer crosses forbidden territory and meets an ancient guardian. When duty collides with unexpected connection, both must choose what matters most.
            </p>
            <div class="release-badge">Demo Coming Q3 2025</div>
        </div>
        
        <div class="status-section">
            <p class="status-text">
                🚀 Website Under Development<br>
                Follow our journey as we bring this magical story to life!
            </p>
        </div>
        
        <div class="social-grid">
            <a href="https://twitter" class="social-link" target="_blank">
                <span class="social-icon">🐦</span>
                Twitter
            </a>
            <a href="https://instagrams" class="social-link" target="_blank">
                <span class="social-icon">📷</span>
                Instagram
            </a>
            <a href="https://luminagames.itch.io" class="social-link" target="_blank">
                <span class="social-icon">🎮</span>
                Itch.io
            </a>
        </div>
    </div>
</body>
</html>
