<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Special Birthday for You</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Montserrat:wght@300;400;600&display=swap');
        
        :root {
            --primary: #ff6b6b;
            --secondary: #f8a5c2;
            --accent: #f7d794;
            --dark: #574b90;
        }
        
        body {
            font-family: 'Montserrat', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #f5f7fa 0%, #f8dbe7 100%);
            color: #333;
            overflow-x: hidden;
        }
        
        .dancing-font {
            font-family: 'Dancing Script', cursive;
        }
        
        .page {
            min-height: 100vh;
            width: 100%;
            display: none;
            padding: 2rem;
            box-sizing: border-box;
            opacity: 0;
            transition: opacity 0.8s ease;
        }
        
        .page.active {
            display: block;
            opacity: 1;
        }
        
        .heart {
            position: fixed;
            pointer-events: none;
            transform: translate(-50%, -50%);
            animation: float 4s ease-in-out infinite;
            z-index: 1000;
        }
        
        @keyframes float {
            0%, 100% { transform: translate(-50%, -50%) rotate(0deg); }
            50% { transform: translate(-50%, -60%) rotate(10deg); }
        }
        
        .bouncing {
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
        
        .float-in {
            animation: floatIn 1s ease-out forwards;
        }
        
        @keyframes floatIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .photo-gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 1rem;
            margin-top: 2rem;
        }
        
        .photo-frame {
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            aspect-ratio: 1/1;
            background: white;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            cursor: pointer;
        }
        
        .photo-frame:hover {
            transform: scale(1.05);
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }
        
        .photo-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, rgba(255, 107, 107, 0.8), rgba(248, 165, 194, 0.8));
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: opacity 0.3s ease;
            color: white;
            font-weight: bold;
            text-align: center;
            padding: 1rem;
        }
        
        .photo-frame:hover .photo-overlay {
            opacity: 1;
        }
        
        .timeline {
            position: relative;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px 0;
        }
        
        .timeline::after {
            content: '';
            position: absolute;
            width: 6px;
            background: linear-gradient(to bottom, var(--primary), var(--secondary));
            top: 0;
            bottom: 0;
            left: 50%;
            margin-left: -3px;
            border-radius: 10px;
        }
        
        .timeline-item {
            padding: 10px 40px;
            position: relative;
            width: 50%;
            box-sizing: border-box;
            animation: slideIn 0.6s ease-out forwards;
            opacity: 0;
        }
        
        @keyframes slideIn {
            from { opacity: 0; transform: translateX(-50px); }
            to { opacity: 1; transform: translateX(0); }
        }
        
        .timeline-item.right {
            animation: slideInRight 0.6s ease-out forwards;
        }
        
        @keyframes slideInRight {
            from { opacity: 0; transform: translateX(50px); }
            to { opacity: 1; transform: translateX(0); }
        }
        
        .timeline-item::after {
            content: '';
            position: absolute;
            width: 25px;
            height: 25px;
            right: -12px;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            border: 4px solid var(--accent);
            top: 15px;
            border-radius: 50%;
            z-index: 1;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        
        .left {
            left: 0;
        }
        
        .right {
            left: 50%;
        }
        
        .left::after {
            left: -12px;
        }
        
        .timeline-content {
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .timeline-content:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .music-toggle {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--primary);
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            z-index: 1000;
            transition: all 0.3s ease;
            border: none;
        }
        
        .music-toggle:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 16px rgba(0,0,0,0.3);
        }
        
        .music-toggle.playing {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { box-shadow: 0 4px 8px rgba(0,0,0,0.2); }
            50% { box-shadow: 0 4px 20px rgba(255, 107, 107, 0.4); }
        }
        
        .nav-dots {
            position: fixed;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 100;
        }
        
        .nav-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: rgba(255,255,255,0.6);
            border: 2px solid var(--primary);
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }
        
        .nav-dot:hover {
            transform: scale(1.2);
            background: rgba(255, 107, 107, 0.3);
        }
        
        .nav-dot.active {
            background: var(--primary);
            transform: scale(1.3);
        }
        
        .nav-dot::after {
            content: attr(data-tooltip);
            position: absolute;
            right: 120%;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(0,0,0,0.8);
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 12px;
            white-space: nowrap;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
        }
        
        .nav-dot:hover::after {
            opacity: 1;
        }
        
        .message-box {
            background: white;
            border-radius: 20px;
            padding: 20px;
            max-width: 600px;
            margin: 2rem auto;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
        }
        
        .message-box::before {
            content: '';
            position: absolute;
            top: -10px;
            left: -10px;
            right: -10px;
            bottom: -10px;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            z-index: -1;
            filter: blur(20px);
            opacity: 0.6;
        }
        
        .countdown {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 2rem 0;
            flex-wrap: wrap;
        }
        
        .countdown-item {
            background: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            text-align: center;
            min-width: 80px;
            transition: transform 0.3s ease;
        }
        
        .countdown-item:hover {
            transform: translateY(-5px);
        }
        
        .countdown-number {
            font-size: 2.5rem;
            font-weight: bold;
            color: var(--primary);
            margin-bottom: 5px;
        }
        
        .countdown-label {
            font-size: 0.9rem;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            transition: opacity 0.5s ease;
        }
        
        .loading-heart {
            font-size: 3rem;
            animation: heartbeat 1s ease-in-out infinite;
        }
        
        @keyframes heartbeat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.2); }
        }
        
        .birthday-cake {
            display: inline-block;
            animation: cake-bounce 2s infinite;
            font-size: 2rem;
        }
        
        @keyframes cake-bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .gift-box {
            display: inline-block;
            animation: gift-shake 3s infinite;
            font-size: 1.5rem;
        }
        
        @keyframes gift-shake {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(-5deg); }
            75% { transform: rotate(5deg); }
        }
        
        .sparkle {
            position: absolute;
            pointer-events: none;
            animation: sparkle 2s ease-in-out infinite;
        }
        
        @keyframes sparkle {
            0%, 100% { opacity: 0; transform: scale(0) rotate(0deg); }
            50% { opacity: 1; transform: scale(1) rotate(180deg); }
        }
        
        @media (max-width: 768px) {
            .timeline::after {
                left: 31px;
            }
            
            .timeline-item {
                width: 100%;
                padding-left: 70px;
                padding-right: 25px;
            }
            
            .timeline-item::after {
                left: 18px;
            }
            
            .left::after, .right::after {
                left: 18px;
            }
            
            .right {
                left: 0%;
            }
            
            .nav-dots {
                flex-direction: row;
                bottom: 20px;
                top: auto;
                right: 50%;
                transform: translateX(50%);
            }
            
            .nav-dot::after {
                display: none;
            }
            
            .countdown {
                gap: 10px;
            }
            
            .countdown-item {
                padding: 10px 15px;
                min-width: 60px;
            }
            
            .countdown-number {
                font-size: 2rem;
            }
        }
        
        @media (max-width: 480px) {
            .page {
                padding: 1rem;
            }
            
            .countdown-number {
                font-size: 1.5rem;
            }
            
            .countdown-item {
                padding: 8px 12px;
                min-width: 50px;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading-overlay" id="loadingOverlay">
        <div class="text-center text-white">
            <div class="loading-heart">💖</div>
            <p class="mt-4 text-xl dancing-font">Preparing something special...</p>
        </div>
    </div>
    
    <button class="music-toggle" onclick="toggleMusic()" id="musicToggle">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 3a9 9 0 0 0-9 9"></path>
            <path d="M19.69 12a6 6 0 0 1-6 6"></path>
            <path d="M3 12a9 9 0 0 0 9 9"></path>
        </svg>
    </button>
    
    <div class="nav-dots">
        <div class="nav-dot active" onclick="goToPage(1)" data-tooltip="Home"></div>
        <div class="nav-dot" onclick="goToPage(2)" data-tooltip="Memories"></div>
        <div class="nav-dot" onclick="goToPage(3)" data-tooltip="Journey"></div>
        <div class="nav-dot" onclick="goToPage(4)" data-tooltip="Birthday"></div>
    </div>
    
    <!-- Page 1: Cover -->
    <div id="page1" class="page active">
        <div class="flex flex-col items-center justify-center min-h-screen text-center">
            <h1 class="dancing-font text-6xl md:text-8xl font-bold text-pink-600 mb-6 float-in">
                Happy Birthday! <span class="birthday-cake">🎂</span>
            </h1>
            <p class="text-xl md:text-2xl mb-8 text-gray-700 max-w-2xl mx-auto float-in" style="animation-delay: 0.3s;">
                To the most amazing person in my life <span class="gift-box">🎁</span>
            </p>
            <div class="relative inline-block" style="animation-delay: 0.6s;">
                <img src="https://placehold.co/600x400/ff6b6b/ffffff?text=Our+Beautiful+Moment" alt="Romantic couple silhouette at sunset on a beach, holding hands, in a warm color palette" class="rounded-xl shadow-2xl w-full max-w-md float-in">
                <div class="absolute -inset-4 bg-pink-200 opacity-20 rounded-xl blur-xl -z-10"></div>
            </div>
            <button onclick="goToPage(2)" class="mt-12 px-8 py-3 bg-gradient-to-r from-pink-500 to-purple-500 text-white rounded-full font-semibold text-lg shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300 float-in" style="animation-delay: 0.9s;">
                Start the Journey
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline ml-2 animate-bounce" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M16.707 10.293a1 1 0 010 1.414l-6 6a1 1 0 01-1.414 0l-6-6a1 1 0 111.414-1.414L9 14.586V3a1 1 0 012 0v11.586l4.293-4.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
            </button>
        </div>
    </div>
    
    <!-- Page 2: Memories -->
    <div id="page2" class="page">
        <div class="container mx-auto py-12">
            <h1 class="dancing-font text-5xl md:text-7xl text-center mb-12 text-pink-600">Our Beautiful Memories</h1>
            
            <div class="photo-gallery">
                <div class="photo-frame" onclick="showPhotoMessage(0)">
                    <img src="https://placehold.co/400x600/f8a5c2/ffffff?text=First+Coffee+Date" alt="Couple laughing together at a cafe table with coffee cups, natural lighting, candid moment" class="w-full h-full object-cover">
                    <div class="photo-overlay">
                        <div>Our first coffee date ☕<br>The beginning of everything</div>
                    </div>
                </div>
                <div class="photo-frame" onclick="showPhotoMessage(1)">
                    <img src="https://placehold.co/600x400/f7d794/ffffff?text=Beach+Sunset" alt="Romantic beach walk at sunset with silhouettes holding hands, orange and pink sky" class="w-full h-full object-cover">
                    <div class="photo-overlay">
                        <div>Sunset walks 🌅<br>Hand in hand forever</div>
                    </div>
                </div>
                <div class="photo-frame" onclick="showPhotoMessage(2)">
                    <img src="https://placehold.co/400x400/ff6b6b/ffffff?text=Happy+Us" alt="Couple smiling for a selfie in a park with green trees in the background" class="w-full h-full object-cover">
                    <div class="photo-overlay">
                        <div>Just us being silly 😄<br>Pure happiness</div>
                    </div>
                </div>
                <div class="photo-frame" onclick="showPhotoMessage(3)">
                    <img src="https://placehold.co/600x600/574b90/ffffff?text=Dinner+Date" alt="Dinner date at a fancy restaurant with candlelight, wine glasses, and fancy plating" class="w-full h-full object-cover">
                    <div class="photo-overlay">
                        <div>Candlelit dinner 🕯️<br>Romantic evening</div>
                    </div>
                </div>
                <div class="photo-frame" onclick="showPhotoMessage(4)">
                    <img src="https://placehold.co/400x400/f8a5c2/ffffff?text=Surprise!" alt="Surprise gift moment with happy expression and gift box with ribbon" class="w-full h-full object-cover">
                    <div class="photo-overlay">
                        <div>Surprise moments 🎉<br>Your shocked face was priceless!</div>
                    </div>
                </div>
                <div class="photo-frame" onclick="showPhotoMessage(5)">
                    <img src="https://placehold.co/600x400/f7d794/ffffff?text=Adventure+Time" alt="Travel moment at a famous landmark, smiling with arms around each other" class="w-full h-full object-cover">
                    <div class="photo-overlay">
                        <div>Adventures together ✈️<br>Exploring the world</div>
                    </div>
                </div>
            </div>
            
            <div class="message-box mt-12">
                <h2 class="text-2xl font-bold text-pink-600 mb-4 dancing-font">Every moment with you is special</h2>
                <p class="text-gray-700">Looking at these pictures brings back so many wonderful memories we've created together. From our first date to all the adventures that followed, each moment has been precious. I cherish every laugh, every conversation, and even every quiet moment just being with you.</p>
            </div>
            
            <div class="text-center mt-8">
                <button onclick="goToPage(3)" class="px-6 py-2 bg-pink-500 text-white rounded-full font-medium shadow-md hover:bg-pink-600 transition-colors duration-300 inline-flex items-center">
                    Our Timeline
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
        </div>
    </div>
    
    <!-- Page 3: Timeline -->
    <div id="page3" class="page">
        <div class="container mx-auto py-12">
            <h1 class="dancing-font text-5xl md:text-7xl text-center mb-12 text-pink-600">Our Journey Together</h1>
            
            <div class="timeline" id="timeline">
                <div class="timeline-item left">
                    <div class="timeline-content">
                        <h3 class="font-bold text-lg text-pink-600">First Meeting 💕</h3>
                        <p class="text-sm text-gray-500">June 2022</p>
                        <p>The day our eyes met and our story began. That first conversation where everything just clicked.</p>
                    </div>
                </div>
                <div class="timeline-item right">
                    <div class="timeline-content">
                        <h3 class="font-bold text-lg text-pink-600">First Date 🍝</h3>
                        <p class="text-sm text-gray-500">July 2022</p>
                        <p>Dinner at that little Italian place. The nerves, the laughter, the realization this was something special.</p>
                    </div>
                </div>
                <div class="timeline-item left">
                    <div class="timeline-content">
                        <h3 class="font-bold text-lg text-pink-600">First "I Love You" ⭐</h3>
                        <p class="text-sm text-gray-500">September 2022</p>
                        <p>That night under the stars when the words slipped out naturally, and I've never meant anything more.</p>
                    </div>
                </div>
                <div class="timeline-item right">
                    <div class="timeline-content">
                        <h3 class="font-bold text-lg text-pink-600">First Vacation 🏖️</h3>
                        <p class="text-sm text-gray-500">December 2022</p>
                        <p>Our beach getaway where we discovered how perfectly we travel together and made unforgettable memories.</p>
                    </div>
                </div>
                <div class="timeline-item left">
                    <div class="timeline-content">
                        <h3 class="font-bold text-lg text-pink-600">Celebrating One Year 🎉</h3>
                        <p class="text-sm text-gray-500">June 2023</p>
                        <p>365 days of love, growth, and happiness. The first of many anniversaries to come.</p>
                    </div>
                </div>
            </div>
            
            <div class="message-box mt-12 mx-auto max-w-2xl">
                <h2 class="text-2xl font-bold text-pink-600 mb-4 dancing-font">Looking Forward</h2>
                <p class="text-gray-700">This timeline shows just the beginning of our journey. I can't wait to fill years to come with more special moments, adventures, and milestones. Every day with you is a blessing I don't take for granted.</p>
            </div>
            
            <div class="text-center mt-8">
                <button onclick="goToPage(4)" class="px-6 py-2 bg-pink-500 text-white rounded-full font-medium shadow-md hover:bg-pink-600 transition-colors duration-300 inline-flex items-center">
                    Birthday Wishes
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
        </div>
    </div>
    
    <!-- Page 4: Birthday Wishes -->
    <div id="page4" class="page">
        <div class="container mx-auto py-12">
            <div class="text-center mb-12">
                <h1 class="dancing-font text-5xl md:text-7xl text-pink-600 mb-6">Happy 20th Birthday! 🎂</h1>
                <p class="text-xl text-gray-700">To the one who makes my world brighter ✨</p>
            </div>
            
            <div class="max-w-4xl mx-auto">
                <div class="message-box">
                    <h2 class="text-2xl font-bold text-pink-600 mb-6 dancing-font">My Dearest Love, 💝</h2>
                    <div class="space-y-4 text-gray-700">
                        <p>On this special day, as you turn 20, I want to tell you how incredibly grateful I am to have you in my life.</p>
                        <p>You are my sunshine on cloudy days, my calm in the chaos, and my happy place no matter where we are. Your kindness, intelligence, and beautiful spirit inspire me every day.</p>
                        <p>As we celebrate this milestone birthday, I hope this year brings you all the happiness, success, and wonderful experiences you deserve. May all your dreams come true and may we continue to grow and love each other more with each passing day.</p>
                        <p>No words can fully express how much you mean to me, but I promise to show you through every action, every day, for as long as I'm lucky enough to have you by my side.</p>
                    </div>
                    <div class="mt-8 flex justify-center">
                        <img src="https://placehold.co/300x200/ff6b6b/ffffff?text=Love+Letter" alt="Romantic handwritten letter with rose petals scattered around, soft lighting" class="rounded-lg shadow-md w-full max-w-xs">
                    </div>
                </div>
                

                        </div>
                        <div class="countdown-item">
                            <div class="countdown-number" id="minutes">00</div>
                            <div class="countdown-label">Minutes</div>

                
                <div class="mt-16 text-center">
                    <button onclick="createHearts()" class="px-8 py-3 bg-gradient-to-r from-pink-500 to-purple-500 text-white rounded-full font-semibold text-lg shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300 inline-flex items-center mr-4 mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                        </svg>
                        Click for Hearts!
                    </button>
                    <button onclick="createSparkles()" class="px-8 py-3 bg-gradient-to-r from-yellow-400 to-orange-500 text-white rounded-full font-semibold text-lg shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300 inline-flex items-center mb-4">
                        <span class="mr-2">✨</span>
                        Make it Sparkle!
                    </button>
                    <p class="mt-4 text-gray-600 text-sm">(Just a little extra love for your special day)</p>
                    
                    <div class="mt-8 p-6 bg-gradient-to-r from-pink-100 to-purple-100 rounded-lg">
                        <h3 class="text-xl font-bold text-pink-600 mb-4 dancing-font">Birthday Wishes 🎁</h3>
                        <div class="grid md:grid-cols-3 gap-4 text-sm">
                            <div class="bg-white p-4 rounded-lg shadow-sm">
                                <div class="text-2xl mb-2">🌟</div>
                                <p>May all your dreams come true this year!</p>
                            </div>
                            <div class="bg-white p-4 rounded-lg shadow-sm">
                                <div class="text-2xl mb-2">💖</div>
                                <p>Here's to another year of love and laughter!</p>
                            </div>
                            <div class="bg-white p-4 rounded-lg shadow-sm">
                                <div class="text-2xl mb-2">🎉</div>
                                <p>Happy birthday to the most amazing person!</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <audio id="bgMusic" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
    </audio>
    
    <script>
        // Loading screen
        window.addEventListener('load', function() {
            setTimeout(() => {
                document.getElementById('loadingOverlay').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('loadingOverlay').style.display = 'none';
                }, 500);
            }, 2000);
        });

        // Background music toggle
        const musicToggle = document.getElementById('musicToggle');
        const bgMusic = document.getElementById('bgMusic');
        let musicPlaying = false;
        
        function toggleMusic() {
            if (musicPlaying) {
                bgMusic.pause();
                musicToggle.innerHTML = '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3a9 9 0 0 0-9 9"></path><path d="M19.69 12a6 6 0 0 1-6 6"></path><path d="M3 12a9 9 0 0 0 9 9"></path></svg>';
                musicToggle.classList.remove('playing');
            } else {
                bgMusic.play().catch(e => console.log('Audio play failed:', e));
                musicToggle.innerHTML = '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M11 5L6 9H2v6h4l5 4V5z"></path><path d="M15.54 8.46a5 5 0 0 1 0 7.07"></path></svg>';
                musicToggle.classList.add('playing');
            }
            musicPlaying = !musicPlaying;
        }
        
        // Page navigation with animations
        let currentPage = 1;
        
        function goToPage(pageNumber) {
            if (pageNumber === currentPage) return;
            
            // Remove active from current page
            document.getElementById(`page${currentPage}`).classList.remove('active');
            document.querySelectorAll('.nav-dot')[currentPage - 1].classList.remove('active');
            
            // Add active to new page
            setTimeout(() => {
                document.getElementById(`page${pageNumber}`).classList.add('active');
                document.querySelectorAll('.nav-dot')[pageNumber - 1].classList.add('active');
                
                // Trigger timeline animations when entering page 3
                if (pageNumber === 3) {
                    animateTimelineItems();
                }
                
                currentPage = pageNumber;
                window.scrollTo(0, 0);
            }, 100);
        }
        
        // Timeline animation
        function animateTimelineItems() {
            const timelineItems = document.querySelectorAll('.timeline-item');
            timelineItems.forEach((item, index) => {
                item.style.animationDelay = `${index * 0.3}s`;
            });
        }
        
        // Photo gallery interactions
        const photoMessages = [
            "Remember our first coffee date? You were so nervous, it was adorable! ☕",
            "That sunset was magical, but not as beautiful as you 🌅",
            "I love how silly we can be together. Never change! 😄",
            "Our fancy dinner date - you looked absolutely stunning 🕯️",
            "Your face when I surprised you was priceless! 🎉",
            "Every adventure is better with you by my side ✈️"
        ];
        
        function showPhotoMessage(index) {
            alert(photoMessages[index]);
        }
        
        // Enhanced floating hearts animation
        function createHearts() {
            for (let i = 0; i < 30; i++) {
                setTimeout(() => createHeart(), i * 100);
            }
        }
        
        function createHeart() {
            const hearts = ['❤️', '💕', '💖', '💝', '💗', '🥰'];
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.innerHTML = hearts[Math.floor(Math.random() * hearts.length)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.top = '100vh';
            heart.style.fontSize = (Math.random() * 20 + 15) + 'px';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            
            // Animate upward
            heart.style.animation = `floatUp ${Math.random() * 3 + 3}s ease-out forwards`;
            
            document.body.appendChild(heart);
            
            setTimeout(() => {
                if (heart.parentNode) {
                    heart.remove();
                }
            }, 6000);
        }
        
        // Add CSS for upward floating animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes floatUp {
                from { 
                    opacity: 1; 
                    transform: translate(-50%, 0) scale(0); 
                }
                10% {
                    opacity: 1;
                    transform: translate(-50%, 0) scale(1);
                }
                90% { 
                    opacity: 1; 
                    transform: translate(-50%, -100vh) scale(1) rotate(720deg); 
                }
                to { 
                    opacity: 0; 
                    transform: translate(-50%, -120vh) scale(0.5) rotate(720deg); 
                }
            }
        `;
        document.head.appendChild(style);
        
        // Sparkles animation
        function createSparkles() {
            for (let i = 0; i < 50; i++) {
                setTimeout(() => createSparkle(), i * 50);
            }
        }
        
        function createSparkle() {
            const sparkles = ['✨', '⭐', '🌟', '💫', '🎇'];
            const sparkle = document.createElement('div');
            sparkle.className = 'sparkle';
            sparkle.innerHTML = sparkles[Math.floor(Math.random() * sparkles.length)];
            sparkle.style.left = Math.random() * 100 + 'vw';
            sparkle.style.top = Math.random() * 100 + 'vh';
            sparkle.style.fontSize = (Math.random() * 15 + 10) + 'px';
            sparkle.style.animationDuration = (Math.random() * 2 + 1) + 's';
            sparkle.style.color = `hsl(${Math.random() * 360}, 70%, 60%)`;
            
            document.body.appendChild(sparkle);
            
            setTimeout(() => {
                if (sparkle.parentNode) {
                    sparkle.remove();
                }
            }, 2000);
        }
        
        // Enhanced countdown timer
        function updateCountdown() {
            // Set to next birthday (you can customize this date)
            const now = new Date();
            const currentYear = now.getFullYear();
            let birthday = new Date(currentYear + 1, 0, 1); // January 1st next year as example
            
            // If birthday already passed this year, set to next year
            const thisYearBirthday = new Date(currentYear, 0, 1);
            if (now < thisYearBirthday) {
                birthday = thisYearBirthday;
            }
            
            const diff = birthday - now;
            
            if (diff > 0) {
                const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                const seconds = Math.floor((diff % (1000 * 60)) / 1000);
                
                document.getElementById('days').textContent = days.toString().padStart(2, '0');
                document.getElementById('hours').textContent = hours.toString().padStart(2, '0');
                document.getElementById('minutes').textContent = minutes.toString().padStart(2, '0');
                document.getElementById('seconds').textContent = seconds.toString().padStart(2, '0');
            } else {
                // If it's the birthday!
                document.getElementById('days').textContent = '🎉';
                document.getElementById('hours').textContent = '🎂';
                document.getElementById('minutes').textContent = '🎁';
                document.getElementById('seconds').textContent = '💖';
            }
        }
        
        setInterval(updateCountdown, 1000);
        updateCountdown();
        
        // Animation on scroll for elements
        function animateOnScroll() {
            const elements = document.querySelectorAll('.float-in');
            
            elements.forEach(element => {
                const elementPosition = element.getBoundingClientRect().top;
                const screenPosition = window.innerHeight / 1.3;
                
                if (elementPosition < screenPosition) {
                    element.style.opacity = '1';
                    element.style.transform = 'translateY(0)';
                }
            });
        }
        
        window.addEventListener('scroll', animateOnScroll);
        animateOnScroll();
        
        // Keyboard navigation
        document.addEventListener('keydown', function(e) {
            if (e.key === 'ArrowLeft' && currentPage > 1) {
                goToPage(currentPage - 1);
            } else if (e.key === 'ArrowRight' && currentPage < 4) {
                goToPage(currentPage + 1);
            } else if (e.key === ' ') { // Spacebar for hearts
                e.preventDefault();
                createHearts();
            }
        });
        
        // Auto-play some effects
        setTimeout(() => {
            createHeart();
        }, 3000);
        
        setInterval(() => {
            if (Math.random() < 0.3) { // 30% chance every 5 seconds
                createHeart();
            }
        }, 5000);
        
        // Confetti effect on page load
        window.addEventListener('load', function() {
            setTimeout(() => {
                createSparkles();
            }, 3000);
        });
        
        // Touch gestures for mobile
        let touchStartX = null;
        let touchStartY = null;
        
        document.addEventListener('touchstart', function(e) {
            touchStartX = e.touches[0].clientX;
            touchStartY = e.touches[0].clientY;
        });
        
        document.addEventListener('touchend', function(e) {
            if (!touchStartX || !touchStartY) return;
            
            const touchEndX = e.changedTouches[0].clientX;
            const touchEndY = e.changedTouches[0].clientY;
            
            const diffX = touchStartX - touchEndX;
            const diffY = touchStartY - touchEndY;
            
            // Only trigger if horizontal swipe is dominant
            if (Math.abs(diffX) > Math.abs(diffY) && Math.abs(diffX) > 50) {
                if (diffX > 0 && currentPage < 4) {
                    // Swipe left - next page
                    goToPage(currentPage + 1);
                } else if (diffX < 0 && currentPage > 1) {
                    // Swipe right - previous page
                    goToPage(currentPage - 1);
                }
            }
            
            touchStartX = null;
            touchStartY = null;
        });
        
        // Add some interactive elements
        document.addEventListener('click', function(e) {
            // Create a small sparkle on click
            if (Math.random() < 0.5) {
                const sparkle = document.createElement('div');
                sparkle.innerHTML = '✨';
                sparkle.style.position = 'fixed';
                sparkle.style.left = e.clientX + 'px';
                sparkle.style.top = e.clientY + 'px';
                sparkle.style.pointerEvents = 'none';
                sparkle.style.fontSize = '12px';
                sparkle.style.animation = 'sparkle 1s ease-out forwards';
                sparkle.style.zIndex = '9999';
                document.body.appendChild(sparkle);
                
                setTimeout(() => {
                    if (sparkle.parentNode) {
                        sparkle.remove();
                    }
                }, 1000);
            }
        });
    </script>
</body>
</html>
