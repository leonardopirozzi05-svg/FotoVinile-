# FotoVinile-
<!DOCTYPE html>
<html lang="it" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Concert Vinyl Memories</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@400;600;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                        display: ['Space Grotesk', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f3ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            900: '#1e1b4b',
                        }
                    },
                    animation: {
                        'spin-slow': 'spin 20s linear infinite',
                        'pulse-glow': 'pulseGlow 3s ease-in-out infinite',
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%, 100%': { opacity: 0.4, transform: 'scale(1)' },
                            '50%': { opacity: 0.8, transform: 'scale(1.03)' }
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Custom Vinyl Styling and Textures */
        .vinyl-grooves {
            background: repeating-radial-gradient(
                circle at center,
                #18181b 0px,
                #18181b 2px,
                #09090b 3px,
                #27272a 4px,
                #09090b 5px
            );
        }

        .vinyl-shine {
            background: conic-gradient(
                from 0deg at 50% 50%,
                rgba(255, 255, 255, 0.15) 0deg,
                transparent 45deg,
                rgba(255, 255, 255, 0.05) 90deg,
                transparent 135deg,
                rgba(255, 255, 255, 0.15) 180deg,
                transparent 225deg,
                rgba(255, 255, 255, 0.05) 270deg,
                transparent 315deg,
                rgba(255, 255, 255, 0.15) 360deg
            );
        }

        .paused {
            animation-play-state: paused !important;
        }

        /* Smooth Hide Scrollbars */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="bg-zinc-950 text-zinc-100 font-sans min-h-screen flex flex-col justify-between overflow-x-hidden selection:bg-indigo-500 selection:text-white">

    <!-- Ambient Background Glows -->
    <div class="fixed inset-0 pointer-events-none overflow-hidden z-0">
        <div class="absolute -top-40 -left-40 w-96 h-96 bg-indigo-600/20 rounded-full blur-3xl animate-pulse-glow"></div>
        <div class="absolute -bottom-40 -right-40 w-96 h-96 bg-purple-600/20 rounded-full blur-3xl animate-pulse-glow" style="animation-delay: 1.5s;"></div>
    </div>

    <!-- Header Navigation -->
    <header class="relative z-10 w-full px-6 py-4 flex items-center justify-between border-b border-zinc-800/60 bg-zinc-950/70 backdrop-blur-md">
        <div class="flex items-center space-x-3">
            <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-500 to-purple-500 flex items-center justify-center shadow-lg shadow-indigo-500/30">
                <i data-lucide="disc" class="w-5 h-5 text-white animate-spin-slow"></i>
            </div>
            <div>
                <h1 class="font-display font-bold text-lg tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-white via-zinc-200 to-zinc-400">
                    Live Concert Vinyl
                </h1>
                <p class="text-xs text-zinc-400 font-medium">Memory Album &bull; Interactive Edition</p>
            </div>
        </div>

        <div class="flex items-center space-x-3">
            <!-- Audio Vinyl Crackle Toggle -->
            <button id="crackle-btn" title="Toggle Vinyl Audio Crackle" class="px-3.5 py-2 rounded-xl border border-zinc-800 bg-zinc-900/80 hover:bg-zinc-800 text-zinc-300 hover:text-white transition flex items-center space-x-2 text-xs font-semibold">
                <i id="crackle-icon" data-lucide="volume-x" class="w-4 h-4 text-zinc-400"></i>
                <span class="hidden sm:inline" id="crackle-label">Crackle Sound</span>
            </button>

            <!-- Add Photo Button -->
            <button id="open-upload-modal" class="px-3.5 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-500 text-white transition flex items-center space-x-2 text-xs font-semibold shadow-lg shadow-indigo-600/20">
                <i data-lucide="plus-circle" class="w-4 h-4"></i>
                <span class="hidden sm:inline">Aggiungi Foto</span>
            </button>
        </div>
    </header>

    <!-- Main Player Area -->
    <main class="relative z-10 flex-1 flex flex-col items-center justify-center p-4 md:p-8 max-w-5xl mx-auto w-full">
        
        <!-- Track & Concert Info Header -->
        <div class="text-center mb-6 max-w-lg">
            <div class="inline-flex items-center space-x-2 px-3 py-1 rounded-full bg-indigo-950/60 border border-indigo-800/40 text-indigo-300 text-xs font-medium mb-3">
                <i data-lucide="music" class="w-3.5 h-3.5"></i>
                <span id="track-counter">Traccia 1 di 4</span>
            </div>
            <h2 id="photo-title" class="text-2xl md:text-3xl font-display font-bold text-white tracking-tight leading-tight">
                Live Concert Night
            </h2>
            <p id="photo-subtitle" class="text-xs md:text-sm text-zinc-400 mt-1">
                7 Novembre 2026 &bull; Momenti indimenticabili
            </p>
        </div>

        <!-- Interactive Vinyl Disc Container -->
        <div class="relative group my-4 flex items-center justify-center">
            
            <!-- Glow Shadow behind Vinyl -->
            <div class="absolute inset-0 rounded-full bg-indigo-600/10 blur-2xl transform scale-110 group-hover:scale-125 transition duration-500 pointer-events-none"></div>

            <!-- The Vinyl Disk -->
            <div id="vinyl-record" class="relative w-72 h-72 sm:w-80 sm:h-80 md:w-96 md:h-96 rounded-full vinyl-grooves shadow-2xl border-4 border-zinc-900 flex items-center justify-center animate-spin-slow paused transition-transform duration-300">
                
                <!-- Shiny Reflection Overlay -->
                <div class="absolute inset-0 rounded-full vinyl-shine pointer-events-none"></div>

                <!-- Vinyl Center Label (Holds the Photo Album Cover) -->
                <div class="relative w-36 h-36 sm:w-40 sm:h-40 md:w-48 md:h-48 rounded-full border-4 border-zinc-800/90 shadow-inner overflow-hidden flex items-center justify-center bg-zinc-900 group/label">
                    
                    <!-- Displayed Image -->
                    <img id="vinyl-image" src="" alt="Concert Photo" class="w-full h-full object-cover transition-opacity duration-700 opacity-100">

                    <!-- Subtle Inner Shadow for Depth -->
                    <div class="absolute inset-0 shadow-[inset_0_0_20px_rgba(0,0,0,0.6)] rounded-full pointer-events-none"></div>

                    <!-- Center Spindle Hole -->
                    <div class="absolute w-4 h-4 sm:w-5 sm:h-5 bg-zinc-950 rounded-full border-2 border-zinc-700 shadow-md z-20 flex items-center justify-center">
                        <div class="w-1.5 h-1.5 bg-zinc-400 rounded-full"></div>
                    </div>
                </div>
            </div>

            <!-- Tonearm / Needle (Visual Decor) -->
            <div id="tonearm" class="absolute -top-6 right-2 sm:right-6 md:right-10 w-24 h-44 pointer-events-none transition-transform duration-700 origin-top-right transform rotate-[18deg]">
                <svg viewBox="0 0 100 200" class="w-full h-full drop-shadow-xl">
                    <!-- Base -->
                    <circle cx="80" cy="20" r="16" fill="#27272a" stroke="#3f3f46" stroke-width="3" />
                    <circle cx="80" cy="20" r="8" fill="#52525b" />
                    <!-- Arm -->
                    <path d="M 80 20 L 75 100 L 40 160" fill="none" stroke="#a1a1aa" stroke-width="4" stroke-linecap="round"/>
                    <!-- Cartridge / Headshell -->
                    <rect x="25" y="152" width="22" height="14" rx="2" fill="#6366f1" transform="rotate(-30 35 160)"/>
                </svg>
            </div>
        </div>

        <!-- Timeline / Progress Indicator -->
        <div class="w-full max-w-md mt-6 px-4">
            <div class="w-full bg-zinc-800/80 rounded-full h-1.5 overflow-hidden">
                <div id="progress-bar" class="bg-indigo-500 h-full w-0 transition-all duration-300"></div>
            </div>
        </div>

        <!-- Controls Bar -->
        <div class="flex items-center justify-center space-x-4 sm:space-x-6 mt-6 bg-zinc-900/90 border border-zinc-800/80 px-6 py-3.5 rounded-full shadow-xl backdrop-blur-md">
            
            <!-- Previous Button -->
            <button id="prev-btn" title="Foto Precedente" class="p-2.5 rounded-full text-zinc-400 hover:text-white hover:bg-zinc-800 transition active:scale-95">
                <i data-lucide="skip-back" class="w-5 h-5"></i>
            </button>

            <!-- Play/Pause Button -->
            <button id="play-btn" title="Riproduci / Pausa" class="w-12 h-12 rounded-full bg-indigo-600 hover:bg-indigo-500 text-white flex items-center justify-center transition shadow-lg shadow-indigo-600/30 active:scale-95">
                <i id="play-icon" data-lucide="play" class="w-6 h-6 fill-current ml-0.5"></i>
            </button>

            <!-- Next Button -->
            <button id="next-btn" title="Prossima Foto" class="p-2.5 rounded-full text-zinc-400 hover:text-white hover:bg-zinc-800 transition active:scale-95">
                <i data-lucide="skip-forward" class="w-5 h-5"></i>
            </button>

            <div class="w-px h-6 bg-zinc-800 my-auto"></div>

            <!-- Auto-rotate Slideshow Toggle -->
            <button id="auto-btn" title="Toggle Autoplay" class="p-2.5 rounded-full text-indigo-400 bg-indigo-950/60 border border-indigo-800/40 hover:bg-indigo-900/60 transition active:scale-95">
                <i data-lucide="repeat" class="w-5 h-5"></i>
            </button>
        </div>
    </main>

    <!-- Thumbnail Strip (Bottom Gallery) -->
    <footer class="relative z-10 w-full p-4 border-t border-zinc-800/60 bg-zinc-950/80 backdrop-blur-md">
        <div class="max-w-4xl mx-auto flex items-center space-x-3 overflow-x-auto no-scrollbar py-1" id="thumbnail-container">
            <!-- Dynamically populated thumbnails -->
        </div>
    </footer>

    <!-- Upload Photo Modal -->
    <div id="upload-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/70 backdrop-blur-sm opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-zinc-900 border border-zinc-800 rounded-2xl max-w-md w-full p-6 shadow-2xl transform scale-95 transition-transform duration-300" id="modal-card">
            
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-display font-bold text-white">Aggiungi i tuoi ricordi</h3>
                <button id="close-upload-modal" class="text-zinc-400 hover:text-white p-1 rounded-lg">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <form id="upload-form" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-zinc-400 mb-1">Seleziona o Scatta Foto</label>
                    <input type="file" id="file-input" accept="image/*" multiple class="w-full text-xs text-zinc-400 file:mr-3 file:py-2 file:px-4 file:rounded-xl file:border-0 file:text-xs file:font-semibold file:bg-indigo-600 file:text-white hover:file:bg-indigo-500 cursor-pointer bg-zinc-950 rounded-xl border border-zinc-800 p-2">
                </div>

                <div>
                    <label class="block text-xs font-semibold text-zinc-400 mb-1">Titolo (Opzionale)</label>
                    <input type="text" id="photo-title-input" placeholder="Es. Canzone Preferita Live!" class="w-full text-xs bg-zinc-950 border border-zinc-800 rounded-xl p-3 text-zinc-200 focus:outline-none focus:border-indigo-500">
                </div>

                <div>
                    <label class="block text-xs font-semibold text-zinc-400 mb-1">Sottotitolo / Data (Opzionale)</label>
                    <input type="text" id="photo-subtitle-input" placeholder="Es. Palazzetto dello Sport - 7 Nov" class="w-full text-xs bg-zinc-950 border border-zinc-800 rounded-xl p-3 text-zinc-200 focus:outline-none focus:border-indigo-500">
                </div>

                <div class="flex justify-end space-x-3 pt-2">
                    <button type="button" id="cancel-upload-btn" class="px-4 py-2 rounded-xl text-xs font-semibold text-zinc-400 hover:bg-zinc-800">Annulla</button>
                    <button type="submit" class="px-4 py-2 rounded-xl text-xs font-semibold bg-indigo-600 hover:bg-indigo-500 text-white shadow-lg shadow-indigo-600/20">Carica su Vinile</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Application Logic -->
    <script>
        // Initial Default Playlist / Memories
        const DEFAULT_MEMORIES = [
            {
                url: "https://images.unsplash.com/photo-1470225620780-dba8ba36b745?auto=format&fit=crop&w=800&q=80",
                title: "Opening Light Show",
                subtitle: "7 Novembre 2026 • L'attesa è finita!"
            },
            {
                url: "https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=800&q=80",
                title: "Live on Stage",
                subtitle: "7 Novembre 2026 • Energia pura"
            },
            {
                url: "https://images.unsplash.com/photo-1516450360452-9312f5e86fc7?auto=format&fit=crop&w=800&q=80",
                title: "Sotto il Palco",
                subtitle: "7 Novembre 2026 • Cantando a squarciagola"
            },
            {
                url: "https://images.unsplash.com/photo-1459749411175-04bf5292ceea?auto=format&fit=crop&w=800&q=80",
                title: "Gran Finale",
                subtitle: "7 Novembre 2026 • Un ricordo per sempre"
            }
        ];

        // App State
        let memories = [];
        let currentIndex = 0;
        let isPlaying = false;
        let isAutoplay = true;
        let autoplayInterval = null;
        const AUTOPLAY_DELAY = 4500; // 4.5 seconds per slide

        // Audio State (Synthesized Crackle)
        let audioCtx = null;
        let crackleNode = null;
        let isCrackleActive = false;

        // DOM Elements
        const vinylRecord = document.getElementById('vinyl-record');
        const vinylImage = document.getElementById('vinyl-image');
        const tonearm = document.getElementById('tonearm');
        const playBtn = document.getElementById('play-btn');
        const playIcon = document.getElementById('play-icon');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const autoBtn = document.getElementById('auto-btn');
        const photoTitle = document.getElementById('photo-title');
        const photoSubtitle = document.getElementById('photo-subtitle');
        const trackCounter = document.getElementById('track-counter');
        const progressBar = document.getElementById('progress-bar');
        const thumbnailContainer = document.getElementById('thumbnail-container');
        
        // Modal Elements
        const openUploadModalBtn = document.getElementById('open-upload-modal');
        const closeUploadModalBtn = document.getElementById('close-upload-modal');
        const cancelUploadBtn = document.getElementById('cancel-upload-btn');
        const uploadModal = document.getElementById('upload-modal');
        const modalCard = document.getElementById('modal-card');
        const uploadForm = document.getElementById('upload-form');

        // Audio Elements
        const crackleBtn = document.getElementById('crackle-btn');
        const crackleIcon = document.getElementById('crackle-icon');

        // Initialize App
        window.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            loadMemories();
            renderGallery();
            setupEventListeners();
        });

        // Load Memories from LocalStorage or Defaults
        function loadMemories() {
            const saved = localStorage.getItem('concert_vinyl_memories');
            if (saved) {
                try {
                    memories = JSON.parse(saved);
                } catch (e) {
                    memories = [...DEFAULT_MEMORIES];
                }
            } else {
                memories = [...DEFAULT_MEMORIES];
            }
        }

        // Save Custom Memories to LocalStorage
        function saveMemories() {
            try {
                localStorage.setItem('concert_vinyl_memories', JSON.stringify(memories));
            } catch (e) {
                console.warn("Could not save to localStorage", e);
            }
        }

        // Render Current Track and Thumbnails
        function renderGallery() {
            if (memories.length === 0) return;

            const item = memories[currentIndex];
            
            // Fade out vinyl photo then fade back in
            vinylImage.style.opacity = '0';
            setTimeout(() => {
                vinylImage.src = item.url;
                vinylImage.style.opacity = '1';
            }, 300);

            // Update Track Information
            photoTitle.textContent = item.title || "Concert Memory";
            photoSubtitle.textContent = item.subtitle || "7 Novembre 2026";
            trackCounter.textContent = `Traccia ${currentIndex + 1} di ${memories.length}`;

            // Update Thumbnails
            thumbnailContainer.innerHTML = '';
            memories.forEach((mem, idx) => {
                const thumb = document.createElement('button');
                thumb.className = `relative flex-shrink-0 w-14 h-14 rounded-xl overflow-hidden border-2 transition duration-300 ${
                    idx === currentIndex 
                    ? 'border-indigo-500 scale-105 shadow-md shadow-indigo-500/30' 
                    : 'border-zinc-800 opacity-60 hover:opacity-100'
                }`;
                thumb.innerHTML = `<img src="${mem.url}" class="w-full h-full object-cover">`;
                thumb.addEventListener('click', () => {
                    currentIndex = idx;
                    renderGallery();
                    resetProgress();
                });
                thumbnailContainer.appendChild(thumb);
            });

            resetProgress();
        }

        // Toggle Vinyl Rotation & Playback State
        function togglePlay() {
            isPlaying = !isPlaying;
            
            if (isPlaying) {
                vinylRecord.classList.remove('paused');
                tonearm.style.transform = 'rotate(0deg)';
                playIcon.setAttribute('data-lucide', 'pause');
                startAutoplayTimer();
                if (isCrackleActive) startCrackleAudio();
            } else {
                vinylRecord.classList.add('paused');
                tonearm.style.transform = 'rotate(18deg)';
                playIcon.setAttribute('data-lucide', 'play');
                stopAutoplayTimer();
                stopCrackleAudio();
            }
            
            lucide.createIcons();
        }

        // Next & Previous Navigation
        function nextTrack() {
            currentIndex = (currentIndex + 1) % memories.length;
            renderGallery();
        }

        function prevTrack() {
            currentIndex = (currentIndex - 1 + memories.length) % memories.length;
            renderGallery();
        }

        // Slideshow Timer & Progress Bar
        function startAutoplayTimer() {
            stopAutoplayTimer();
            if (!isAutoplay || !isPlaying) return;

            let startTime = Date.now();
            autoplayInterval = setInterval(() => {
                let elapsed = Date.now() - startTime;
                let percent = (elapsed / AUTOPLAY_DELAY) * 100;
                progressBar.style.width = `${Math.min(percent, 100)}%`;

                if (elapsed >= AUTOPLAY_DELAY) {
                    nextTrack();
                    startTime = Date.now();
                }
            }, 50);
        }

        function stopAutoplayTimer() {
            if (autoplayInterval) clearInterval(autoplayInterval);
            progressBar.style.width = '0%';
        }

        function resetProgress() {
            if (isPlaying && isAutoplay) {
                startAutoplayTimer();
            } else {
                progressBar.style.width = '0%';
            }
        }

        // Web Audio API - Synthesized Vinyl Crackle Sound
        function initAudioContext() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
        }

        function startCrackleAudio() {
            initAudioContext();
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }

            if (crackleNode) return;

            // Generate Pink/Brownian Noise Buffer for Vinyl Crackle
            const bufferSize = audioCtx.sampleRate * 2;
            const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
            const data = buffer.getChannelData(0);
            
            for (let i = 0; i < bufferSize; i++) {
                // Occasional sharp pops/crackles
                if (Math.random() < 0.001) {
                    data[i] = (Math.random() * 2 - 1) * 0.8;
                } else if (Math.random() < 0.01) {
                    data[i] = (Math.random() * 2 - 1) * 0.15;
                } else {
                    data[i] = (Math.random() * 2 - 1) * 0.02; // soft background hiss
                }
            }

            crackleNode = audioCtx.createBufferSource();
            crackleNode.buffer = buffer;
            crackleNode.loop = true;

            const gainNode = audioCtx.createGain();
            gainNode.gain.value = 0.08; // subtle volume

            crackleNode.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            crackleNode.start();
        }

        function stopCrackleAudio() {
            if (crackleNode) {
                crackleNode.stop();
                crackleNode.disconnect();
                crackleNode = null;
            }
        }

        function toggleCrackle() {
            isCrackleActive = !isCrackleActive;
            if (isCrackleActive) {
                crackleIcon.setAttribute('data-lucide', 'volume-2');
                crackleBtn.classList.add('border-indigo-500', 'text-indigo-400');
                if (isPlaying) startCrackleAudio();
            } else {
                crackleIcon.setAttribute('data-lucide', 'volume-x');
                crackleBtn.classList.remove('border-indigo-500', 'text-indigo-400');
                stopCrackleAudio();
            }
            lucide.createIcons();
        }

        // Setup Event Listeners
        function setupEventListeners() {
            playBtn.addEventListener('click', togglePlay);
            nextBtn.addEventListener('click', () => { nextTrack(); });
            prevBtn.addEventListener('click', () => { prevTrack(); });

            autoBtn.addEventListener('click', () => {
                isAutoplay = !isAutoplay;
                autoBtn.classList.toggle('text-indigo-400');
                autoBtn.classList.toggle('text-zinc-500');
                resetProgress();
            });

            crackleBtn.addEventListener('click', toggleCrackle);

            // Modal Toggles
            openUploadModalBtn.addEventListener('click', openModal);
            closeUploadModalBtn.addEventListener('click', closeModal);
            cancelUploadBtn.addEventListener('click', closeModal);

            // Form Submit for Uploading Photos
            uploadForm.addEventListener('submit', (e) => {
                e.preventDefault();
                const fileInput = document.getElementById('file-input');
                const titleInput = document.getElementById('photo-title-input');
                const subtitleInput = document.getElementById('photo-subtitle-input');

                const files = fileInput.files;
                if (!files || files.length === 0) return;

                Array.from(files).forEach((file, index) => {
                    const reader = new FileReader();
                    reader.onload = function(evt) {
                        memories.push({
                            url: evt.target.result,
                            title: titleInput.value.trim() || `Ricordo #${memories.length + 1}`,
                            subtitle: subtitleInput.value.trim() || "7 Novembre 2026"
                        });
                        saveMemories();
                        if (index === files.length - 1) {
                            currentIndex = memories.length - files.length;
                            renderGallery();
                            closeModal();
                        }
                    };
                    reader.readAsDataURL(file);
                });
            });
        }

        function openModal() {
            uploadModal.classList.remove('opacity-0', 'pointer-events-none');
            modalCard.classList.remove('scale-95');
            modalCard.classList.add('scale-100');
        }

        function closeModal() {
            uploadModal.classList.add('opacity-0', 'pointer-events-none');
            modalCard.classList.remove('scale-100');
            modalCard.classList.add('scale-95');
            uploadForm.reset();
        }
    </script>
</body>
</html>