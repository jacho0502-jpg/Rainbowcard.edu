# Rainbowcard.edu
Rainbow cards for teachers
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teacher's Rainbow Cards | Daily Educator Inspiration</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['"Inter"', '"Noto Sans TC"', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    <style>
        .perspective-1000 {
            perspective: 1000px;
        }
        .transform-style-3d {
            transform-style: preserve-3d;
        }
        .backface-hidden {
            backface-visibility: hidden;
        }
        .rotate-y-180 {
            transform: rotateY(180deg);
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.88);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(255, 255, 255, 0.7);
        }
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="bg-gradient-to-br from-amber-50 via-sky-50 to-emerald-50 min-h-screen text-slate-700 font-sans flex flex-col justify-between selection:bg-indigo-200 selection:text-indigo-900">

    <!-- Header Navigation -->
    <header class="w-full glass-panel sticky top-0 z-50 shadow-sm">
        <div class="max-w-6xl mx-auto px-4 py-3 flex flex-col sm:flex-row items-center justify-between gap-3">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-2xl bg-gradient-to-tr from-yellow-400 via-pink-400 to-indigo-400 flex items-center justify-center text-white shadow-md text-xl">
                    <i class="fa-solid fa-rainbow"></i>
                </div>
                <div>
                    <h1 class="text-base sm:text-lg font-bold bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">Teacher's Rainbow Cards</h1>
                    <p class="text-xs text-slate-500">Nurturing Educators with Positive Daily Energy</p>
                </div>
            </div>

            <!-- Navigation Tabs & Top-Right Favorites Button -->
            <div class="flex items-center gap-2 flex-wrap justify-center">
                <nav class="flex bg-slate-100/90 p-1 rounded-xl shadow-inner text-sm font-medium">
                    <button onclick="switchTab('draw')" id="nav-draw" class="px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 bg-white text-indigo-600 shadow-sm flex items-center gap-1.5">
                        <i class="fa-solid fa-wand-magic-sparkles"></i> Daily Draw
                    </button>
                    <button onclick="switchTab('history')" id="nav-history" class="px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 text-slate-600 hover:text-indigo-600 flex items-center gap-1.5">
                        <i class="fa-solid fa-book-bookmark"></i> History <span id="history-badge" class="bg-indigo-100 text-indigo-600 text-xs px-1.5 py-0.5 rounded-full">0</span>
                    </button>
                    <button onclick="switchTab('library')" id="nav-library" class="px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 text-slate-600 hover:text-indigo-600 flex items-center gap-1.5">
                        <i class="fa-solid fa-layer-group"></i> Library
                    </button>
                </nav>

                <!-- Top-Right Favorite Quotes Button with Counter Badge -->
                <button onclick="openFavoritesModal()" class="px-3.5 py-2 rounded-xl bg-white hover:bg-rose-50 border border-slate-200 text-rose-600 font-semibold text-sm shadow-sm transition-all flex items-center gap-1.5">
                    <i class="fa-solid fa-heart"></i> Favorites <span id="favorites-badge" class="bg-rose-100 text-rose-600 text-xs px-2 py-0.5 rounded-full">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="max-w-5xl w-full mx-auto px-4 py-8 flex-grow flex flex-col items-center justify-center">

        <!-- 1. Daily Draw Tab -->
        <section id="tab-draw" class="w-full flex flex-col items-center">
            
            <!-- Draw Controls / Category Selection Buttons -->
            <div class="mb-6 w-full max-w-3xl">
                <p class="text-center text-sm font-medium text-slate-500 mb-3"><i class="fa-solid fa-filter mr-1"></i> Choose your energy mode or draw from a specific color category:</p>
                <div class="grid grid-cols-2 sm:grid-cols-5 gap-2" id="category-selector">
                    <button onclick="drawCard('all')" class="px-3 py-2.5 rounded-2xl font-medium text-xs sm:text-sm transition-all shadow-sm bg-gradient-to-r from-indigo-600 to-purple-600 text-white hover:scale-105 active:scale-95 flex items-center justify-center gap-1.5 shadow-indigo-200 col-span-2 sm:col-span-1">
                        <i class="fa-solid fa-star"></i> Random Draw
                    </button>
                    <button onclick="drawCard('yellow')" class="px-3 py-2.5 rounded-2xl font-medium text-xs sm:text-sm transition-all shadow-sm bg-white hover:bg-yellow-50 border border-yellow-300 text-slate-700 hover:scale-105 active:scale-95 flex items-center justify-center gap-1.5">
                        <span class="w-3 h-3 rounded-full bg-yellow-400 inline-block"></span> Yellow · Joy
                    </button>
                    <button onclick="drawCard('blue')" class="px-3 py-2.5 rounded-2xl font-medium text-xs sm:text-sm transition-all shadow-sm bg-white hover:bg-sky-50 border border-sky-300 text-slate-700 hover:scale-105 active:scale-95 flex items-center justify-center gap-1.5">
                        <span class="w-3 h-3 rounded-full bg-sky-400 inline-block"></span> Blue · Calm
                    </button>
                    <button onclick="drawCard('red')" class="px-3 py-2.5 rounded-2xl font-medium text-xs sm:text-sm transition-all shadow-sm bg-white hover:bg-rose-50 border border-rose-300 text-slate-700 hover:scale-105 active:scale-95 flex items-center justify-center gap-1.5">
                        <span class="w-3 h-3 rounded-full bg-rose-400 inline-block"></span> Red · Passion
                    </button>
                    <button onclick="drawCard('green')" class="px-3 py-2.5 rounded-2xl font-medium text-xs sm:text-sm transition-all shadow-sm bg-white hover:bg-emerald-50 border border-emerald-300 text-slate-700 hover:scale-105 active:scale-95 flex items-center justify-center gap-1.5">
                        <span class="w-3 h-3 rounded-full bg-emerald-400 inline-block"></span> Green · Growth
                    </button>
                </div>
            </div>

            <!-- Card Container with 3D Flip Animation -->
            <div class="relative w-full max-w-md aspect-[3/4] perspective-1000 cursor-pointer mb-8 group" onclick="triggerDefaultDraw()">
                <div id="card-inner" class="w-full h-full relative transform-style-3d transition-transform duration-700 shadow-2xl rounded-3xl">
                    
                    <!-- Card Back (Unflipped State) -->
                    <div id="card-back" class="absolute inset-0 w-full h-full rounded-3xl bg-gradient-to-br from-indigo-600 via-purple-600 to-pink-500 text-white p-8 flex flex-col justify-between items-center text-center backface-hidden shadow-xl border-4 border-white/20">
                        <div class="w-full flex justify-between items-center opacity-80">
                            <i class="fa-solid fa-sparkles text-xl"></i>
                            <span class="text-xs tracking-widest uppercase font-semibold">Teacher Rainbow Cards</span>
                            <i class="fa-solid fa-sparkles text-xl"></i>
                        </div>
                        <div class="flex flex-col items-center space-y-4">
                            <div class="w-24 h-24 rounded-full bg-white/10 backdrop-blur-md flex items-center justify-center border border-white/30 group-hover:scale-105 transition-transform duration-300">
                                <i class="fa-solid fa-hand-sparkles text-4xl text-yellow-200"></i>
                            </div>
                            <div>
                                <h3 class="text-2xl font-bold tracking-wide mb-1">Draw Today's Guidance</h3>
                                <p class="text-sm text-purple-100 font-light">Click a color button or tap this card to receive your daily inspiration</p>
                            </div>
                        </div>
                        <div class="w-full py-3 bg-white/20 backdrop-blur-sm rounded-xl text-sm font-semibold tracking-wide border border-white/20 group-hover:bg-white/30 transition-colors">
                            Click to Flip Card ✨
                        </div>
                    </div>

                    <!-- Card Front (Flipped State) -->
                    <div id="card-front" class="absolute inset-0 w-full h-full rounded-3xl bg-white p-6 sm:p-8 flex flex-col justify-between backface-hidden rotate-y-180 shadow-2xl border-4 border-slate-100 overflow-y-auto">
                        <div class="flex justify-between items-center border-b pb-3">
                            <!-- Category and Color Tag -->
                            <span id="display-cat-badge" class="px-3.5 py-1 rounded-full text-xs font-semibold tracking-wider flex items-center gap-1.5 shadow-sm">
                                <span id="display-dot" class="w-2.5 h-2.5 rounded-full"></span> 
                                <span id="display-cat-name">Category Name</span>
                            </span>
                            <div class="flex items-center gap-2">
                                <!-- Favorite Heart Button on Drawn Card -->
                                <button id="display-fav-btn" onclick="event.stopPropagation(); toggleFavoriteCurrentCard()" class="w-8 h-8 rounded-full bg-slate-50 hover:bg-rose-50 text-slate-400 hover:text-rose-500 flex items-center justify-center transition-colors">
                                    <i class="fa-regular fa-heart text-sm" id="display-fav-icon"></i>
                                </button>
                                <span id="display-card-id" class="text-xs text-slate-400 font-mono">#01</span>
                            </div>
                        </div>

                        <!-- Card Content: English Primary, Chinese Secondary -->
                        <div class="my-auto py-4 text-center space-y-4">
                            <i class="fa-solid fa-quote-left text-indigo-300 text-3xl mb-1 block"></i>
                            <!-- English Primary Quote -->
                            <h2 id="display-quote-en" class="text-xl sm:text-2xl font-bold text-slate-800 leading-relaxed">
                                Loading...
                            </h2>
                            <!-- Chinese Secondary Quote underneath -->
                            <p id="display-quote-zh" class="text-sm sm:text-base font-medium text-slate-500 italic">
                                載入中...
                            </p>
                        </div>

                        <div class="pt-3 border-t flex items-center justify-between text-xs text-slate-400">
                            <span>Click 'Random Draw' to explore more</span>
                            <span class="text-indigo-500 font-medium">Teacher's Rainbow Cards</span>
                        </div>
                    </div>

                </div>
            </div>

            <!-- Action Buttons -->
            <div class="flex flex-wrap justify-center gap-3">
                <button onclick="drawCard('all')" class="px-6 py-3 rounded-2xl bg-gradient-to-r from-indigo-600 to-purple-600 text-white font-semibold shadow-lg shadow-indigo-200 hover:shadow-indigo-300 hover:scale-105 active:scale-95 transition-all flex items-center gap-2">
                    <i class="fa-solid fa-dice"></i> Draw Another Card
                </button>
                <button id="btn-note" onclick="openNoteModal()" class="px-5 py-3 rounded-2xl bg-white hover:bg-slate-50 text-slate-700 font-semibold shadow border border-slate-200 transition-all flex items-center gap-2 disabled:opacity-50 disabled:cursor-not-allowed" disabled>
                    <i class="fa-solid fa-pen-nib text-indigo-500"></i> Add Reflection Note
                </button>
            </div>
        </section>

        <!-- 2. History & Notes Tab -->
        <section id="tab-history" class="w-full hidden">
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6 gap-4">
                <div>
                    <h2 class="text-2xl font-bold text-slate-800">Card History & Reflection Notes</h2>
                    <p class="text-sm text-slate-500">Review your drawn cards and keep track of your mindful growth.</p>
                </div>
                <div class="flex gap-2">
                    <button onclick="exportHistory()" class="px-4 py-2 rounded-xl bg-white border border-slate-200 text-slate-600 text-sm font-medium hover:bg-slate-50 transition-all shadow-sm">
                        <i class="fa-solid fa-download mr-1"></i> Export Records (.txt)
                    </button>
                    <button onclick="clearHistory()" class="px-4 py-2 rounded-xl bg-rose-50 border border-rose-200 text-rose-600 text-sm font-medium hover:bg-rose-100 transition-all">
                        <i class="fa-solid fa-trash-can mr-1"></i> Clear History
                    </button>
                </div>
            </div>

            <div id="history-list" class="grid grid-cols-1 md:grid-cols-2 gap-4"></div>

            <div id="history-empty" class="text-center py-16 hidden">
                <div class="w-20 h-20 bg-slate-100 rounded-full flex items-center justify-center mx-auto mb-4 text-slate-400 text-2xl">
                    <i class="fa-solid fa-box-open"></i>
                </div>
                <h3 class="text-lg font-bold text-slate-700 mb-1">No drawing history yet</h3>
                <p class="text-sm text-slate-500 mb-4">Go to 'Daily Draw' to draw your first inspirational card!</p>
                <button onclick="switchTab('draw')" class="px-5 py-2.5 rounded-xl bg-indigo-600 text-white font-medium text-sm shadow-md">
                    Go to Draw
                </button>
            </div>
        </section>

        <!-- 3. Card Library Tab -->
        <section id="tab-library" class="w-full hidden">
            <div class="mb-6 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                <div>
                    <h2 class="text-2xl font-bold text-slate-800">Complete Card Library (32 Cards)</h2>
                    <p class="text-sm text-slate-500">Explore all positive affirmation statements designed across four color energies.</p>
                </div>
                <!-- Search Box -->
                <div class="relative w-full md:w-72">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none text-slate-400">
                        <i class="fa-solid fa-magnifying-glass"></i>
                    </span>
                    <input type="text" id="library-search" oninput="filterLibrary()" placeholder="Search keyword..." class="w-full pl-9 pr-4 py-2 rounded-xl bg-white border border-slate-200 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 shadow-sm">
                </div>
            </div>

            <!-- Library Grid -->
            <div id="library-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4"></div>
        </section>

    </main>

    <!-- Favorites Modal / Drawer -->
    <div id="favorites-modal" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-2xl w-full p-6 shadow-2xl border border-slate-100 max-h-[85vh] flex flex-col transform transition-all">
            <div class="flex justify-between items-center mb-4 pb-3 border-b">
                <h3 class="text-lg font-bold text-slate-800 flex items-center gap-2">
                    <i class="fa-solid fa-heart text-rose-500"></i> Favorite Quotes (<span id="fav-modal-count">0</span>)
                </h3>
                <button onclick="closeFavoritesModal()" class="w-8 h-8 rounded-full bg-slate-100 text-slate-500 hover:bg-slate-200 flex items-center justify-center transition-colors">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div id="favorites-modal-list" class="overflow-y-auto space-y-3 pr-2 flex-grow">
                <!-- Dynamically populated favorite quotes -->
            </div>
        </div>
    </div>

    <!-- Reflection Note Modal -->
    <div id="note-modal" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-lg w-full p-6 shadow-2xl border border-slate-100 transform transition-all">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-lg font-bold text-slate-800 flex items-center gap-2">
                    <i class="fa-solid fa-pen-nib text-indigo-600"></i> Teaching Reflection Note
                </h3>
                <button onclick="closeNoteModal()" class="w-8 h-8 rounded-full bg-slate-100 text-slate-500 hover:bg-slate-200 flex items-center justify-center transition-colors">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div class="mb-4 bg-slate-50 p-3 rounded-2xl border border-slate-200">
                <p id="modal-quote-preview" class="text-sm font-semibold text-slate-700 italic">"Quote preview..."</p>
            </div>
            <div class="mb-4">
                <label class="block text-xs font-semibold text-slate-500 mb-1.5">Record your thoughts or classroom application ideas:</label>
                <textarea id="note-input" rows="4" class="w-full p-3 rounded-2xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm text-slate-700 placeholder:text-slate-400 resize-none" placeholder="e.g., Today the class was lively; drawing this card reminded me to take a deep breath and guide students with warmth..."></textarea>
            </div>
            <div class="flex justify-end gap-2">
                <button onclick="closeNoteModal()" class="px-4 py-2 rounded-xl bg-slate-100 text-slate-600 font-medium text-sm hover:bg-slate-200 transition-colors">
                    Cancel
                </button>
                <button onclick="saveNote()" class="px-5 py-2 rounded-xl bg-indigo-600 text-white font-medium text-sm hover:bg-indigo-700 shadow-md transition-all">
                    Save Note
                </button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-6 right-6 bg-slate-900 text-white px-5 py-3 rounded-2xl shadow-2xl z-50 text-sm font-medium transform translate-y-20 opacity-0 transition-all duration-300 flex items-center gap-2">
        <i class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-msg">Successfully saved!</span>
    </div>

    <!-- Footer -->
    <footer class="w-full py-6 text-center text-xs text-slate-400 border-t bg-white/40 mt-12">
        <p>Teacher's Rainbow Cards Online 🌈 Inspiring Educators Worldwide</p>
    </footer>

    <!-- Application Script & 32 Cards Database -->
    <script>
        // 32 Teacher Rainbow Cards Database (English Primary, Chinese Secondary, NO guide text)
        const rainbowCardsData = [
            // Yellow: Joy & Vitality (8 cards)
            { id: "Y01", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "My enthusiasm and smile are the warmest light in the classroom.", quoteZh: "我的熱情與笑容，是教室裡最溫暖的光芒。" },
            { id: "Y02", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "Every small step of progress is worth celebrating out loud.", quoteZh: "每一個小小的進步，都值得我們大聲慶祝。" },
            { id: "Y03", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "I radiate confidence and vitality, infusing the class with positive energy.", quoteZh: "我散發著自信與活力，為課堂注入滿滿的正向能量。" },
            { id: "Y04", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "Play and laughter are the best catalysts for meaningful learning.", quoteZh: "遊戲與笑聲是最好的學習催化劑。" },
            { id: "Y05", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "I am creative, transforming ordinary lessons into engaging experiences.", quoteZh: "我充滿創造力，能將平凡的課程變得生動有趣。" },
            { id: "Y06", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "Today, I choose to welcome every child with gratitude and anticipation.", quoteZh: "今天，我選擇用感恩與期待的心情迎接每一位孩子。" },
            { id: "Y07", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "My sense of humor eases tension, bringing a joyful atmosphere.", quoteZh: "我的幽默感能化解緊張，帶領班級走向輕鬆愉快的氛圍。" },
            { id: "Y08", cat: "yellow", catName: "Yellow · Joy & Vitality", colorCode: "bg-yellow-400", textColor: "text-yellow-800", bgColor: "bg-yellow-50", borderColor: "border-yellow-300", quoteEn: "Education is a beautiful encounter; I enjoy every moment of abundance.", quoteZh: "教育是一場美好的相遇，我享受當下的每一刻豐盛。" },

            // Blue: Calm & Trust (8 cards)
            { id: "B01", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "Amidst chaos and noise, I possess inner peace and anchoring strength.", quoteZh: "在混亂與喧鬧中，我擁有內在的平靜與定錨力量。" },
            { id: "B02", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "I trust the timeline of student growth; everyone blooms in their season.", quoteZh: "我選擇信任學生成長的時程，每個人都在自己的花期綻放。" },
            { id: "B03", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "Listening is more powerful than preaching; I step into student hearts with empathy.", quoteZh: "傾聽比說教更有力量，我用同理心走入學生的內心。" },
            { id: "B04", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "My words carry a healing power that is both gentle and firm.", quoteZh: "我的言語帶有溫柔且堅定的療癒力量。" },
            { id: "B05", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "Empowering students through trust allows them to try and learn from mistakes.", quoteZh: "放手讓學生去嘗試與犯錯，信任是最好的授權。" },
            { id: "B06", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "I accept each child's uniqueness without limiting them with standard answers.", quoteZh: "我接納每個孩子的獨特性，不急著用標準答案限制他們。" },
            { id: "B07", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "Patience and gentleness bridge connection; trust is our best guide.", quoteZh: "在對話中保持耐心與溫柔，信任是師生最好的橋樑。" },
            { id: "B08", cat: "blue", catName: "Blue · Calm & Trust", colorCode: "bg-sky-400", textColor: "text-sky-800", bgColor: "bg-sky-50", borderColor: "border-sky-300", quoteEn: "My mind is clear like still water, perceiving true student needs.", quoteZh: "我的心靈如止水般清明，能清晰洞察學生的真實需求。" },

            // Red: Passion & Courage (8 cards)
            { id: "R01", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "I have the courage to face classroom challenges and grow resilient.", quoteZh: "我有勇氣面對教學現場的挑戰，並在每一次嘗試中變得更堅韌。" },
            { id: "R02", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "My leadership and persistence ignite the fire of exploration in students.", quoteZh: "我的領導與堅持，正默默點燃學生心中的探索之火。" },
            { id: "R03", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "I bravely break old frameworks, injecting innovation into education.", quoteZh: "我勇敢打破舊有框架，為教育注入創新與改變。" },
            { id: "R04", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "I have enough passion to warm every weary soul on this journey.", quoteZh: "我擁有足夠的熱忱，能溫暖每一顆疲憊的心靈。" },
            { id: "R05", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "When facing conflict, I maintain integrity, fairness, and courage.", quoteZh: "面對衝突與挑戰時，我保持正直、公正與勇氣。" },
            { id: "R06", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "Stepping out of my comfort zone breaks barriers and opens new paths.", quoteZh: "我不怕跨出舒適圈，每一次改變都是突破自我的機會。" },
            { id: "R07", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "When doubts arise, I firmly believe in the value of my education.", quoteZh: "當質疑聲出現時，我堅信自己教育的信念與價值。" },
            { id: "R08", cat: "red", catName: "Red · Passion & Courage", colorCode: "bg-rose-400", textColor: "text-rose-800", bgColor: "bg-rose-50", borderColor: "border-rose-300", quoteEn: "Kind and firm leadership guides the classroom toward warm order.", quoteZh: "我有足夠的魄力與愛心，帶領班級走向溫馨而有規矩的方向。" },

            // Green: Growth & Healing (8 cards)
            { id: "G01", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "Taking care of my mind and body is the most responsible role model.", quoteZh: "照顧好自己的身心，是我對學生最溫柔且負責任的示範。" },
            { id: "G02", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "Allowing myself occasional rest; growth is a resilient oasis path.", quoteZh: "允許自己偶爾犯錯與休息，成長是一條充滿韌性的綠洲小徑。" },
            { id: "G03", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "Nature and meditation are my endless sources of inspiration and energy.", quoteZh: "大自然與靜心，是我源源不絕的靈感與能量泉源。" },
            { id: "G04", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "I find balance in work, letting both career and life shine brightly.", quoteZh: "我在工作中找到平衡，工作與生活皆能綻放光彩。" },
            { id: "G05", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "Every day is a new beginning; I possess infinite self-healing capacity.", quoteZh: "每一天都是新的開始，我擁有無限的自我修復能力。" },
            { id: "G06", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "Releasing perfectionism, I love my authentic self right now.", quoteZh: "放下過度的完美主義，愛自己現在的真實模樣。" },
            { id: "G07", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "Quiet time after work is my best spiritual and mental recharge.", quoteZh: "下班後的安靜時光，是我給自己最好的心靈充電。" },
            { id: "G08", cat: "green", catName: "Green · Growth & Healing", colorCode: "bg-emerald-400", textColor: "text-emerald-800", bgColor: "bg-emerald-50", borderColor: "border-emerald-300", quoteEn: "I allow myself to feel tired, and I rise to embrace hope anew.", quoteZh: "我允許自己疲憊，也允許自己重新站起來擁抱希望。" }
        ];

        let isFlipped = false;
        let currentCard = null;
        let favoriteIds = JSON.parse(localStorage.getItem('teacher_english_favorite_ids')) || [];
        let historyList = JSON.parse(localStorage.getItem('teacher_english_rainbow_history')) || [];
        let noteModalTarget = null;

        window.addEventListener('DOMContentLoaded', () => {
            updateFavoritesBadge();
            renderLibrary();
            updateHistoryUI();
        });

        // Tab Switching
        function switchTab(tabName) {
            document.getElementById('tab-draw').classList.add('hidden');
            document.getElementById('tab-history').classList.add('hidden');
            document.getElementById('tab-library').classList.add('hidden');

            document.getElementById('nav-draw').className = "px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 text-slate-600 hover:text-indigo-600 flex items-center gap-1.5";
            document.getElementById('nav-history').className = "px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 text-slate-600 hover:text-indigo-600 flex items-center gap-1.5";
            document.getElementById('nav-library').className = "px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 text-slate-600 hover:text-indigo-600 flex items-center gap-1.5";

            document.getElementById(`tab-${tabName}`).classList.remove('hidden');
            document.getElementById(`nav-${tabName}`).className = "px-3 py-1.5 sm:px-4 sm:py-2 rounded-lg transition-all duration-200 bg-white text-indigo-600 shadow-sm flex items-center gap-1.5";
        }

        function triggerDefaultDraw() {
            drawCard('all');
        }

        // Draw Card Logic (Random or Color-specific)
        function drawCard(category) {
            let pool = rainbowCardsData;
            if (category !== 'all') {
                pool = rainbowCardsData.filter(c => c.cat === category);
            }

            const randomIndex = Math.floor(Math.random() * pool.length);
            currentCard = pool[randomIndex];

            // Set front card content (English primary, Chinese secondary)
            document.getElementById('display-quote-en').innerText = `"${currentCard.quoteEn}"`;
            document.getElementById('display-quote-zh').innerText = `「${currentCard.quoteZh}」`;
            document.getElementById('display-card-id').innerText = `#${currentCard.id}`;
            document.getElementById('display-cat-name').innerText = currentCard.catName;
            
            const dot = document.getElementById('display-dot');
            dot.className = `w-2.5 h-2.5 rounded-full ${currentCard.colorCode}`;

            const badge = document.getElementById('display-cat-badge');
            badge.className = `px-3.5 py-1 rounded-full text-xs font-semibold tracking-wider flex items-center gap-1.5 ${currentCard.bgColor} ${currentCard.textColor} border ${currentCard.borderColor} shadow-sm`;

            // Update heart icon state on drawn card
            updateCurrentCardFavoriteUI();

            // 3D Flip Animation
            const cardInner = document.getElementById('card-inner');
            cardInner.style.transform = 'rotateY(180deg)';
            isFlipped = true;

            // Enable action button
            document.getElementById('btn-note').removeAttribute('disabled');

            // Confetti effect
            confetti({
                particleCount: 85,
                spread: 75,
                origin: { y: 0.6 }
            });

            addToHistory(currentCard);
        }

        function updateCurrentCardFavoriteUI() {
            if (!currentCard) return;
            const favIcon = document.getElementById('display-fav-icon');
            const isFav = favoriteIds.includes(currentCard.id);
            if (isFav) {
                favIcon.className = "fa-solid fa-heart text-rose-500 text-sm";
            } else {
                favIcon.className = "fa-regular fa-heart text-slate-400 text-sm";
            }
        }

        function toggleFavoriteCurrentCard() {
            if (!currentCard) return;
            const index = favoriteIds.indexOf(currentCard.id);
            if (index > -1) {
                favoriteIds.splice(index, 1);
                showToast('Removed from favorites');
            } else {
                favoriteIds.push(currentCard.id);
                showToast('Added to favorites');
            }
            localStorage.setItem('teacher_english_favorite_ids', JSON.stringify(favoriteIds));
            updateFavoritesBadge();
            updateCurrentCardFavoriteUI();
            renderLibrary();
            updateHistoryUI();
        }

        function toggleFavoriteCardById(cardId) {
            const index = favoriteIds.indexOf(cardId);
            if (index > -1) {
                favoriteIds.splice(index, 1);
                showToast('Removed from favorites');
            } else {
                favoriteIds.push(cardId);
                showToast('Added to favorites');
            }
            localStorage.setItem('teacher_english_favorite_ids', JSON.stringify(favoriteIds));
            updateFavoritesBadge();
            updateCurrentCardFavoriteUI();
            renderLibrary();
            updateHistoryUI();
            if (!document.getElementById('favorites-modal').classList.contains('hidden')) {
                renderFavoritesModalList();
            }
        }

        function updateFavoritesBadge() {
            document.getElementById('favorites-badge').innerText = favoriteIds.length;
        }

        // Favorites Modal Control
        function openFavoritesModal() {
            renderFavoritesModalList();
            document.getElementById('favorites-modal').classList.remove('hidden');
        }

        function closeFavoritesModal() {
            document.getElementById('favorites-modal').classList.add('hidden');
        }

        function renderFavoritesModalList() {
            const container = document.getElementById('favorites-modal-list');
            document.getElementById('fav-modal-count').innerText = favoriteIds.length;

            if (favoriteIds.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-12 text-slate-400">
                        <i class="fa-regular fa-heart text-4xl mb-2 block text-slate-300"></i>
                        <p class="text-sm">No favorite quotes yet. Click the heart icon on any card to save it here!</p>
                    </div>
                `;
                return;
            }

            let html = '';
            favoriteIds.forEach(id => {
                const card = rainbowCardsData.find(c => c.id === id);
                if (!card) return;
                html += `
                    <div class="bg-slate-50/80 rounded-2xl p-4 border border-slate-200/80 flex flex-col justify-between hover:bg-white transition-all shadow-sm">
                        <div class="flex justify-between items-center mb-2">
                            <span class="px-3 py-0.5 rounded-full text-xs font-semibold ${card.bgColor} ${card.textColor} border ${card.borderColor} flex items-center gap-1.5">
                                <span class="w-2 h-2 rounded-full ${card.colorCode}"></span> ${card.catName}
                            </span>
                            <div class="flex items-center gap-3">
                                <span class="text-xs text-slate-400 font-mono">#${card.id}</span>
                                <button onclick="toggleFavoriteCardById('${card.id}')" class="text-rose-500 hover:text-slate-400 transition-colors" title="Remove from favorites">
                                    <i class="fa-solid fa-heart"></i>
                                </button>
                            </div>
                        </div>
                        <h4 class="font-bold text-slate-800 text-sm sm:text-base mb-1">"${card.quoteEn}"</h4>
                        <p class="text-xs text-slate-500 italic">「${card.quoteZh}」</p>
                    </div>
                `;
            });
            container.innerHTML = html;
        }

        // Add to History
        function addToHistory(card) {
            const historyItem = {
                historyId: Date.now(),
                cardId: card.id,
                quoteEn: card.quoteEn,
                quoteZh: card.quoteZh,
                catName: card.catName,
                colorCode: card.colorCode,
                bgColor: card.bgColor,
                textColor: card.textColor,
                borderColor: card.borderColor,
                date: new Date().toLocaleString('en-US', { hour12: false }),
                note: ''
            };

            historyList.unshift(historyItem);
            localStorage.setItem('teacher_english_rainbow_history', JSON.stringify(historyList));
            updateHistoryUI();
        }

        // Update History UI
        function updateHistoryUI() {
            const container = document.getElementById('history-list');
            const emptyState = document.getElementById('history-empty');
            const badge = document.getElementById('history-badge');

            badge.innerText = historyList.length;

            if (historyList.length === 0) {
                container.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');
            let html = '';

            historyList.forEach(item => {
                const isFav = favoriteIds.includes(item.cardId);
                html += `
                    <div class="glass-panel rounded-3xl p-6 shadow-sm border border-slate-100 flex flex-col justify-between hover:shadow-md transition-shadow">
                        <div>
                            <div class="flex justify-between items-center mb-3">
                                <span class="px-3 py-1 rounded-full text-xs font-semibold ${item.bgColor} ${item.textColor} border ${item.borderColor} flex items-center gap-1.5">
                                    <span class="w-2 h-2 rounded-full ${item.colorCode}"></span> ${item.catName}
                                </span>
                                <span class="text-xs text-slate-400 font-mono">${item.date}</span>
                            </div>
                            <h3 class="text-base font-bold text-slate-800 mb-1">"${item.quoteEn}"</h3>
                            <p class="text-xs text-slate-500 mb-4 italic">「${item.quoteZh}」</p>
                            
                            ${item.note ? `
                                <div class="mb-4 bg-amber-50/70 border border-amber-200/60 p-3 rounded-xl text-xs text-slate-700">
                                    <p class="font-bold text-amber-800 mb-1 flex items-center gap-1"><i class="fa-solid fa-pen-nib"></i> Reflection Note:</p>
                                    <p>${item.note}</p>
                                </div>
                            ` : ''}
                        </div>
                        <div class="flex justify-between items-center pt-3 border-t text-xs">
                            <button onclick="toggleFavoriteCardById('${item.cardId}')" class="flex items-center gap-1 font-medium transition-colors ${isFav ? 'text-rose-600' : 'text-slate-400 hover:text-slate-600'}">
                                <i class="${isFav ? 'fa-solid' : 'fa-regular'} fa-heart"></i> ${isFav ? 'Favorited' : 'Favorite'}
                            </button>
                            <div class="flex items-center gap-2">
                                <button onclick="openNoteModalForHistory(${item.historyId})" class="px-3 py-1.5 rounded-xl bg-indigo-50 text-indigo-600 hover:bg-indigo-100 font-medium transition-colors">
                                    <i class="fa-solid fa-pen mr-1"></i> ${item.note ? 'Edit Note' : 'Add Note'}
                                </button>
                                <button onclick="deleteHistoryItem(${item.historyId})" class="text-slate-400 hover:text-rose-600 p-1.5 transition-colors" title="Delete">
                                    <i class="fa-solid fa-trash-can"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                `;
            });

            container.innerHTML = html;
        }

        function deleteHistoryItem(historyId) {
            historyList = historyList.filter(h => h.historyId !== historyId);
            localStorage.setItem('teacher_english_rainbow_history', JSON.stringify(historyList));
            updateHistoryUI();
            showToast('Record deleted');
        }

        function clearHistory() {
            if (historyList.length === 0) return;
            historyList = [];
            localStorage.removeItem('teacher_english_rainbow_history');
            updateHistoryUI();
            showToast('All records cleared');
        }

        function exportHistory() {
            if (historyList.length === 0) {
                showToast('No records to export');
                return;
            }
            let text = "--- Teacher's Rainbow Cards & Notes History ---\n\n";
            historyList.forEach((h, index) => {
                text += `[${index + 1}] ${h.date} - ${h.catName}\n`;
                text += `English: "${h.quoteEn}"\n`;
                text += `Chinese: 「${h.quoteZh}」\n`;
                if (h.note) text += `Note: ${h.note}\n`;
                text += `----------------------------------------\n\n`;
            });

            const blob = new Blob([text], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `Teachers_Rainbow_Cards_History_${new Date().toISOString().slice(0,10)}.txt`;
            a.click();
            showToast('History text file exported successfully');
        }

        function openNoteModal() {
            if (!currentCard || historyList.length === 0) return;
            noteModalTarget = historyList[0].historyId;
            document.getElementById('modal-quote-preview').innerText = `"${currentCard.quoteEn}"`;
            document.getElementById('note-input').value = historyList[0].note || '';
            document.getElementById('note-modal').classList.remove('hidden');
        }

        function openNoteModalForHistory(historyId) {
            noteModalTarget = historyId;
            const item = historyList.find(h => h.historyId === historyId);
            if (item) {
                document.getElementById('modal-quote-preview').innerText = `"${item.quoteEn}"`;
                document.getElementById('note-input').value = item.note || '';
                document.getElementById('note-modal').classList.remove('hidden');
            }
        }

        function closeNoteModal() {
            document.getElementById('note-modal').classList.add('hidden');
            noteModalTarget = null;
            document.getElementById('note-input').value = '';
        }

        function saveNote() {
            if (!noteModalTarget) return;
            const noteText = document.getElementById('note-input').value.trim();
            const item = historyList.find(h => h.historyId === noteModalTarget);
            if (item) {
                item.note = noteText;
                localStorage.setItem('teacher_english_rainbow_history', JSON.stringify(historyList));
                updateHistoryUI();
                showToast('Note saved successfully!');
            }
            closeNoteModal();
        }

        // Render Card Library
        function renderLibrary(filterKeyword = '') {
            const grid = document.getElementById('library-grid');
            let html = '';

            const keyword = filterKeyword.toLowerCase();
            const filteredCards = rainbowCardsData.filter(card => {
                return card.quoteEn.toLowerCase().includes(keyword) ||
                       card.quoteZh.toLowerCase().includes(keyword) ||
                       card.catName.toLowerCase().includes(keyword) ||
                       card.id.toLowerCase().includes(keyword);
            });

            filteredCards.forEach(card => {
                const isFav = favoriteIds.includes(card.id);
                html += `
                    <div class="glass-panel rounded-3xl p-5 shadow-sm border border-slate-100 flex flex-col justify-between hover:shadow-md transition-shadow">
                        <div>
                            <div class="flex justify-between items-center mb-3">
                                <span class="px-3 py-1 rounded-full text-xs font-semibold ${card.bgColor} ${card.textColor} border ${card.borderColor} flex items-center gap-1.5">
                                    <span class="w-2 h-2 rounded-full ${card.colorCode}"></span> ${card.catName}
                                </span>
                                <div class="flex items-center gap-2">
                                    <button onclick="toggleFavoriteCardById('${card.id}')" class="w-7 h-7 rounded-full bg-slate-50 hover:bg-rose-50 ${isFav ? 'text-rose-500' : 'text-slate-400'} flex items-center justify-center transition-colors">
                                        <i class="${isFav ? 'fa-solid' : 'fa-regular'} fa-heart text-xs"></i>
                                    </button>
                                    <span class="text-xs text-slate-400 font-mono">#${card.id}</span>
                                </div>
                            </div>
                            <h4 class="font-bold text-slate-800 text-sm sm:text-base mb-1">"${card.quoteEn}"</h4>
                            <p class="text-xs text-slate-500 italic">「${card.quoteZh}」</p>
                        </div>
                    </div>
                `;
            });

            if (filteredCards.length === 0) {
                grid.innerHTML = `<div class="col-span-3 text-center py-12 text-slate-400">No matching rainbow cards found.</div>`;
            } else {
                grid.innerHTML = html;
            }
        }

        function filterLibrary() {
            const query = document.getElementById('library-search').value;
            renderLibrary(query);
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
```
eof
