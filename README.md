<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ұстаздың AI құралдары</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700;800;900&family=Inter:wght@300;400;500;600;700;800&display=swap');
        body {
            font-family: 'Montserrat', 'Inter', sans-serif;
        }
        .ambient-glow-1 {
            background: radial-gradient(circle, rgba(99, 102, 241, 0.15) 0%, rgba(255, 255, 255, 0) 70%);
        }
        .ambient-glow-2 {
            background: radial-gradient(circle, rgba(139, 92, 246, 0.12) 0%, rgba(255, 255, 255, 0) 70%);
        }
        .custom-scrollbar::-webkit-scrollbar {
            height: 6px;
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: transparent;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
    </style>
</head>
<body class="bg-[#f8fafc] text-slate-800 min-h-screen pb-16 relative overflow-x-hidden">

    <!-- Декоративті артқы фон шұғылалары (Ambient Glow) -->
    <div class="absolute top-0 left-1/4 w-[600px] h-[600px] ambient-glow-1 pointer-events-none -z-10 rounded-full blur-3xl"></div>
    <div class="absolute top-1/3 right-1/4 w-[500px] h-[500px] ambient-glow-2 pointer-events-none -z-10 rounded-full blur-3xl"></div>

    <!-- Хабарлама терезесі (Toast) -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-10 opacity-0 pointer-events-none transition-all duration-300 flex items-center gap-3 bg-slate-900 text-white px-5 py-4 rounded-2xl shadow-xl border border-slate-800">
        <span id="toastIcon" class="p-1 rounded-lg bg-emerald-500/10">
            <!-- Белгіше серпінді түрде қойылады -->
        </span>
        <span id="toastMessage" class="text-sm font-semibold tracking-wide">Сәтті орындалды!</span>
    </div>

    <!-- Басқы контейнер -->
    <div class="max-w-6xl mx-auto px-4 sm:px-6">
        
        <!-- Хедер / Тақырып бөлімі -->
        <header class="py-12 border-b border-slate-200/80 mb-10 flex flex-col md:flex-row md:items-center md:justify-between gap-6">
            <div class="space-y-2">
                <div class="inline-flex items-center gap-2 px-3 py-1 bg-indigo-50 border border-indigo-100 rounded-full text-indigo-700 text-xs font-bold uppercase tracking-wider">
                    ✨ Ұстаздар Порталы
                </div>
                <h1 class="text-3xl sm:text-4xl lg:text-5xl font-extrabold text-slate-950 tracking-tight leading-none">
                    Ұстаздың <br class="hidden sm:inline"><span class="text-indigo-600 bg-gradient-to-r from-indigo-600 via-violet-600 to-purple-600 bg-clip-text text-transparent">AI құралдары</span>
                </h1>
                <p class="text-slate-500 text-base sm:text-lg max-w-xl font-medium">
                    Мұғалімдердің тиімді жұмыс істеуіне қажетті бұлттық платформалар мен жасанды интеллект құралдарының бірыңғай жинағы.
                </p>
            </div>
            
            <div class="flex flex-wrap gap-3 items-center">
                <!-- Админ батырмалары (тек сәтті кіргенде көрінеді) -->
                <div id="adminPanelControls" class="hidden flex items-center gap-3">
                    <div class="flex gap-2 bg-white p-1.5 rounded-2xl border border-slate-200 shadow-sm">
                        <button onclick="exportData()" title="Сайттарды файлға сақтау" class="p-2 text-slate-500 hover:text-indigo-600 hover:bg-indigo-50 rounded-xl transition-all">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path></svg>
                        </button>
                        <button onclick="triggerImport()" title="Файлдан сайттарды жүктеу" class="p-2 text-slate-500 hover:text-indigo-600 hover:bg-indigo-50 rounded-xl transition-all">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path></svg>
                        </button>
                        <button onclick="openResetModal()" title="Бастапқы қалпына келтіру" class="p-2 text-slate-500 hover:text-amber-600 hover:bg-amber-50 rounded-xl transition-all">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4 4v5h.582m15.356 2A8.001 8.001 0 1121.21 7.89H18.5"></path></svg>
                        </button>
                        <input type="file" id="importFile" class="hidden" accept=".json" onchange="importData(event)">
                    </div>

                    <button onclick="openModal()" class="inline-flex items-center justify-center gap-2 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-700 hover:to-violet-700 text-white font-bold px-5 py-3 rounded-2xl shadow-lg shadow-indigo-600/10 active:scale-[0.98] transition-all">
                        <svg class="w-4.5 h-4.5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"></path></svg>
                        Сайт қосу
                    </button>
                </div>

                <!-- Админ кіру/шығу батырмалары -->
                <button id="adminLoginBtn" onclick="openAdminAuthModal()" class="inline-flex items-center justify-center gap-2 bg-slate-800 hover:bg-slate-900 text-white font-bold px-5 py-3 rounded-2xl shadow-md active:scale-[0.98] transition-all text-sm">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path></svg>
                    Админ режимі
                </button>
                <button id="adminLogoutBtn" onclick="logoutAdmin()" class="hidden inline-flex items-center justify-center gap-2 bg-rose-600 hover:bg-rose-700 text-white font-bold px-5 py-3 rounded-2xl shadow-md active:scale-[0.98] transition-all text-sm">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path></svg>
                    Шығу
                </button>
            </div>
        </header>

        <!-- ================= БӨЛІМ: МЕНІҢ AI ҚҰРАЛДАРЫМ ================= -->
        <section class="mb-14">
            <div class="flex items-center justify-between mb-6">
                <div class="flex items-center gap-3">
                    <div class="p-2.5 bg-violet-600 text-white rounded-xl shadow-md shadow-violet-600/10">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 113.536 0V21h2v-4.757"></path>
                        </svg>
                    </div>
                    <div>
                        <h2 class="text-2xl font-extrabold text-slate-900 tracking-tight">Менің AI құралдарым</h2>
                        <p class="text-xs text-slate-400 font-medium">Жеке ұсынылған жасанды интеллект ресурстарыңыздың басты жинағы</p>
                    </div>
                </div>
            </div>
            
            <div id="aiSitesGrid" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Осы жерге AI сайттары нақты уақытта бұлттық базадан шығады -->
            </div>
        </section>

        <!-- Сәнді бөлгіш сызық -->
        <div class="relative py-4 mb-10">
            <div class="absolute inset-0 flex items-center" aria-hidden="true">
                <div class="w-full border-t border-slate-200/80"></div>
            </div>
            <div class="relative flex justify-center">
                <span class="bg-[#f8fafc] px-4 text-slate-400 text-xs font-bold tracking-widest uppercase">Қосымша ресурстар</span>
            </div>
        </div>

        <!-- ================= ҚОСЫМША БӨЛІМДЕР ================= -->
        <section>
            <!-- Бөлімдер тақырыбы мен іздеу жүйесі -->
            <div class="flex flex-col lg:flex-row gap-6 items-start lg:items-center justify-between mb-8">
                <div>
                    <h2 class="text-xl font-extrabold text-slate-900 tracking-tight">Қосымша пайдалы платформалар</h2>
                    <p class="text-xs text-slate-400 font-medium">Санаттар бойынша жүйеленген ресурстар жиынтығы</p>
                </div>
                
                <!-- Іздеу жолағы -->
                <div class="relative w-full lg:w-96 group">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 pointer-events-none text-slate-400 group-focus-within:text-indigo-500 transition-colors">
                        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
                    </span>
                    <input type="text" id="searchInput" oninput="filterAndSearch()" placeholder="Қосымша платформалардан іздеу..." class="w-full pl-11 pr-4 py-3 bg-white border border-slate-200 rounded-2xl focus:outline-none focus:ring-4 focus:ring-indigo-100 focus:border-indigo-500 transition-all text-sm font-medium shadow-sm">
                </div>
            </div>

            <!-- Санаттар бойынша фильтр (Пиллдер стилі) -->
            <div class="flex gap-2 overflow-x-auto pb-3 mb-8 custom-scrollbar" id="filterContainer">
                <button onclick="setFilter('fav')" id="btn-fav" class="filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl text-slate-600 bg-white border border-slate-200 hover:bg-slate-50 transition-all duration-200 flex items-center gap-1.5">
                    <span class="text-amber-500">⭐</span> Таңдаулылар
                </button>
                <button onclick="setFilter('method')" id="btn-method" class="filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl bg-indigo-600 text-white shadow-md shadow-indigo-600/10 transition-all duration-200">Әдістемелік құралдар & Сабақтар</button>
                <button onclick="setFilter('test')" id="btn-test" class="filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl text-slate-600 bg-white border border-slate-200 hover:bg-slate-50 transition-all duration-200">Тесттер & Ойындар</button>
                <button onclick="setFilter('design')" id="btn-design" class="filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl text-slate-600 bg-white border border-slate-200 hover:bg-slate-50 transition-all duration-200">Дизайн & Презентация</button>
                <button onclick="setFilter('interactive')" id="btn-interactive" class="filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl text-slate-600 bg-white border border-slate-200 hover:bg-slate-50 transition-all duration-200">Интерактивті тақта & Құралдар</button>
            </div>

            <!-- Басқа сайттар кестесі / Грид -->
            <div id="otherSitesGrid" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Санаттарға байланысты басқа сайттар осында көрсетіледі -->
            </div>

            <!-- Бос күй (Empty State) -->
            <div id="emptyState" class="hidden text-center py-20 bg-white rounded-3xl border border-dashed border-slate-300">
                <div class="p-4 bg-slate-50 inline-block rounded-2xl mb-4">
                    <svg class="w-12 h-12 text-slate-300 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0a2 2 0 01-2 2H6a2 2 0 01-2-2m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4"></path></svg>
                </div>
                <h3 class="text-xl font-extrabold text-slate-700">Бұл санат бос немесе ештеңе табылмады</h3>
                <p class="text-slate-400 text-sm mt-1 max-w-sm mx-auto font-medium">Сайт қосып көріңіз немесе іздеу сөзін өзгертіңіз.</p>
            </div>
        </section>

        <!-- Футер -->
        <footer class="mt-20 pt-8 border-t border-slate-200 text-center text-slate-400 text-xs">
            <p class="font-semibold text-slate-500">© 2026 Ұстаздың AI құралдары білім беру порталы</p>
            <p class="mt-1">Сілтемелер мен жазбалар бұлтты базада және браузер жадында қауіпсіз сақталады.</p>
        </footer>
    </div>

    <!-- ================= ЖЕЗЕЛ ЖАЗБАЛАР (STICKY NOTES) ВИДЖЕТІ ================= -->
    <div class="fixed bottom-6 left-6 z-40 flex flex-col items-start">
        <!-- Блокнот терезесі -->
        <div id="stickyNotesPanel" class="w-72 bg-amber-50 rounded-3xl border border-amber-200 shadow-2xl p-5 mb-3 hidden transform translate-y-4 opacity-0 transition-all duration-300">
            <div class="flex items-center justify-between mb-3 border-b border-amber-200/60 pb-2">
                <span class="text-sm font-bold text-amber-900 flex items-center gap-1.5">
                    📝 Жедел жазбалар
                </span>
                <button onclick="toggleStickyNotes()" class="text-amber-700 hover:text-amber-950 p-1 hover:bg-amber-100/50 rounded-lg transition-all">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            <textarea id="quickNotesText" oninput="saveNotes()" rows="6" placeholder="Сабақ барысына қажетті ескертулерді немесе жедел көшіретін сілтемелерді осында жазыңыз..." class="w-full bg-transparent resize-none text-xs font-semibold text-amber-950 placeholder-amber-700/50 border-none focus:outline-none focus:ring-0 leading-relaxed"></textarea>
            <div class="text-[10px] text-amber-700/60 text-right mt-1 font-semibold italic">автоматты түрде сақталады</div>
        </div>
        
        <!-- Жедел жазбалар іске қосу батырмасы -->
        <button onclick="toggleStickyNotes()" class="w-12 h-12 bg-amber-400 hover:bg-amber-500 text-amber-950 rounded-full shadow-lg hover:shadow-xl hover:scale-105 active:scale-95 transition-all flex items-center justify-center border border-amber-300">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
        </button>
    </div>

    <!-- ================= МОДАЛЬДІ ТЕРЕЗЕ: САЙТ ҚОСУ / ӨҢДЕУ ================= -->
    <div id="modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm hidden transition-all duration-300">
        <div class="bg-white rounded-3xl shadow-2xl w-full max-w-md transform transition-all scale-95 duration-300 border border-slate-100" id="modalContent">
            <div class="px-6 py-5 border-b border-slate-100 flex items-center justify-between">
                <h3 id="modalTitle" class="text-xl font-extrabold text-slate-900">Жаңа сайт қосу</h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-slate-600 rounded-xl p-1.5 hover:bg-slate-50 transition-all">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            
            <form id="siteForm" onsubmit="saveSite(event)" class="p-6 space-y-4">
                <input type="hidden" id="editId">
                
                <div>
                    <label class="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-2">Сайт атауы *</label>
                    <input type="text" id="siteName" required placeholder="Мысалы: ChatGPT немесе BilimLand" class="w-full px-4 py-3 border border-slate-200 rounded-2xl focus:outline-none focus:ring-4 focus:ring-indigo-100 focus:border-indigo-500 transition-all text-sm font-semibold">
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-2">Сілтеме (URL) *</label>
                    <input type="url" id="siteUrl" required placeholder="https://example.com" class="w-full px-4 py-3 border border-slate-200 rounded-2xl focus:outline-none focus:ring-4 focus:ring-indigo-100 focus:border-indigo-500 transition-all text-sm font-semibold">
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-2">Санат *</label>
                    <select id="siteCategory" required class="w-full px-4 py-3 border border-slate-200 bg-white rounded-2xl focus:outline-none focus:ring-4 focus:ring-indigo-100 focus:border-indigo-500 transition-all text-sm font-bold">
                        <option value="ai">Менің AI құралдарым</option>
                        <option value="method">Әдістемелік құралдар & Сабақтар</option>
                        <option value="test">Тесттер & Ойындар</option>
                        <option value="design">Дизайн & Презентация</option>
                        <option value="interactive">Интерактивті тақта & платформалар</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-2">Қысқаша сипаттамасы</label>
                    <textarea id="siteDesc" rows="3" placeholder="Сайттың не үшін пайдалы екендігін қысқаша жазыңыз..." class="w-full px-4 py-3 border border-slate-200 rounded-2xl focus:outline-none focus:ring-4 focus:ring-indigo-100 focus:border-indigo-500 transition-all text-sm font-medium"></textarea>
                </div>

                <div class="flex gap-3 pt-3">
                    <button type="button" onclick="closeModal()" class="w-1/2 py-3.5 text-sm font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-2xl active:scale-[0.98] transition-all">Болдырмау</button>
                    <button type="submit" class="w-1/2 py-3.5 text-sm font-bold text-white bg-indigo-600 hover:bg-indigo-700 rounded-2xl shadow-lg shadow-indigo-600/10 active:scale-[0.98] transition-all">Сақтау</button>
                </div>
            </form>
        </div>
    </div>

    <!-- ЖЕКЕ МОДАЛЬ: ӨШІРУДІ РАСТАУ (Confirm алмастырғыш) -->
    <div id="deleteConfirmModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm hidden transition-all duration-300">
        <div class="bg-white rounded-3xl shadow-2xl w-full max-w-sm transform transition-all scale-95 duration-300 border border-slate-100 p-6 space-y-4" id="deleteModalContent">
            <div class="w-12 h-12 bg-rose-50 rounded-2xl flex items-center justify-center text-rose-600 mx-auto">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
            </div>
            <div class="text-center space-y-1">
                <h3 class="text-lg font-bold text-slate-950">Сайтты өшіру</h3>
                <p class="text-sm text-slate-500 font-medium">Бұл ресурсты тізімнен біржола өшіргіңіз келетініне сенімдісіз бе?</p>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeDeleteModal()" class="w-1/2 py-3 text-sm font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-2xl transition-all">Болдырмау</button>
                <button onclick="confirmDeleteSite()" class="w-1/2 py-3 text-sm font-bold text-white bg-rose-600 hover:bg-rose-700 rounded-2xl shadow-lg shadow-rose-600/10 transition-all">Иә, өшіру</button>
            </div>
        </div>
    </div>

    <!-- ЖЕКЕ МОДАЛЬ: БАСТАПҚЫ ҚАЛПЫНА КЕЛТІРУДІ РАСТАУ -->
    <div id="resetConfirmModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm hidden transition-all duration-300">
        <div class="bg-white rounded-3xl shadow-2xl w-full max-w-sm transform transition-all scale-95 duration-300 border border-slate-100 p-6 space-y-4" id="resetModalContent">
            <div class="w-12 h-12 bg-amber-50 rounded-2xl flex items-center justify-center text-amber-600 mx-auto">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4 4v5h.582m15.356 2A8.001 8.001 0 1121.21 7.89H18.5"></path></svg>
            </div>
            <div class="text-center space-y-1">
                <h3 class="text-lg font-bold text-slate-950">Бастапқы күйге келтіру</h3>
                <p class="text-sm text-slate-500 font-medium">Барлық өзгерістер мен өшірілген әдепкі сайттар қалпына келтіріледі. Сенімдісіз бе?</p>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeResetModal()" class="w-1/2 py-3 text-sm font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-2xl transition-all">Болдырмау</button>
                <button onclick="confirmResetAll()" class="w-1/2 py-3 text-sm font-bold text-white bg-amber-500 hover:bg-amber-600 rounded-2xl shadow-lg shadow-amber-500/10 transition-all">Иә, қалпына келтіру</button>
            </div>
        </div>
    </div>

    <!-- ================= STREAMING_CHUNK:Preparing modal custom admin password window... ================= -->
    <!-- ЖЕКЕ МОДАЛЬ: АДМИН АВТОРИЗАЦИЯСЫ -->
    <div id="adminAuthModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm hidden transition-all duration-300">
        <div class="bg-white rounded-3xl shadow-2xl w-full max-w-sm transform transition-all scale-95 duration-300 border border-slate-100 p-6 space-y-4" id="adminModalContent">
            <div class="w-12 h-12 bg-indigo-50 rounded-2xl flex items-center justify-center text-indigo-600 mx-auto">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path></svg>
            </div>
            <div class="text-center space-y-1">
                <h3 class="text-lg font-bold text-slate-950">Администратор ретінде кіру</h3>
                <p class="text-sm text-slate-500 font-medium">Сайттарды басқару үшін құпия сөзді енгізіңіз</p>
            </div>
            <div>
                <input type="password" id="adminPasswordInput" placeholder="Құпия сөзді жазыңыз" class="w-full px-4 py-3 border border-slate-200 rounded-2xl focus:outline-none focus:ring-4 focus:ring-indigo-100 focus:border-indigo-500 transition-all text-sm font-semibold text-center">
                <p id="adminAuthError" class="text-xs text-rose-500 font-semibold text-center mt-2 hidden">Қате құпия сөз! Қайта көріңіз.</p>
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeAdminAuthModal()" class="w-1/2 py-3 text-sm font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-2xl transition-all">Болдырмау</button>
                <button onclick="checkAdminPassword()" class="w-1/2 py-3 text-sm font-bold text-white bg-indigo-600 hover:bg-indigo-700 rounded-2xl shadow-lg shadow-indigo-600/10 transition-all">Кіру</button>
            </div>
        </div>
    </div>

    <!-- JavaScript логикасы -->
    <script>
        // Негізгі бастапқы әдепкі ресурстар
        const defaultSites = [
            // Әдістемелік құралдар және Сабақтар
            { id: 'def-ai-1', name: 'ChatGPT', url: 'https://chatgpt.com', desc: 'Сабақ жоспарларын құруға, мәтіндерді дайындауға және шығармашылық идеялар жинақтауға арналған әмбебап AI көмекші.', category: 'method', isDefault: true },
            { id: 'def-ai-2', name: 'Gemini', url: 'https://gemini.google.com', desc: 'Google әзірлеген, сабақ материалдарын іздеуге, мәтіндерді аударуға және күрделі сұрақтарға жауап алуға көмектесетін интеллектуалды серіктес.', category: 'method', isDefault: true },
            { id: 'def-m-1', name: 'BilimLand', url: 'https://bilimland.kz', desc: 'Қазақстандық ірі білім беру платформасы. Сабақтар, бейнероликтер мен интерактивті тапсырмалардың үлкен базасы.', category: 'method', isDefault: true },
            { id: 'def-m-2', name: 'Kundelik.kz', url: 'https://kundelik.kz', desc: 'Қазақстан мектептеріне арналған бірыңғай электрондық күнделіктер мен журналдар жүйесі.', category: 'method', isDefault: true },
            { id: 'def-m-3', name: 'Daryn.online', url: 'https://daryn.online', desc: 'Мектеп оқушыларына арналған қазақша бейнесабақтар, интерактивті тапсырмалар мен дайындық курстары бар танымал отандық платформа.', category: 'method', isDefault: true },
            { id: 'def-m-4', name: 'Opiq.kz', url: 'https://opiq.kz', desc: 'Қазақстан мектеп бағдарламасына сай бекітілген интерактивті электронды оқулықтардың ресми жинағы.', category: 'method', isDefault: true },
            { id: 'def-m-5', name: 'Google Classroom', url: 'https://classroom.google.com', desc: 'Тапсырмалар таратуға, бағалауға және сыныппен қашықтан кері байланыс орнатуға арналған Google тегін сервисі.', category: 'method', isDefault: true },
            
            // Тесттер & Ойындар
            { id: 'def-1', name: 'Quizizz', url: 'https://quizizz.com', desc: 'Сыныпта немесе үй тапсырмасы ретінде ойын түрінде интерактивті викториналар мен тесттер өткізу платформасы.', category: 'test', isDefault: true },
            { id: 'def-3', name: 'Kahoot!', url: 'https://kahoot.com', desc: 'Оқушылардың жылдамдығы мен білімін тексеретін, жарыс түріндегі викториналар ұйымдастыру құралы.', category: 'test', isDefault: true },
            { id: 'def-t-3', name: 'Plickers', url: 'https://plickers.com', desc: 'Оқушыларда интернет немесе смартфон болмаса да, қағаз карточкаларды камерамен сканерлеу арқылы лезде тест алу құралы.', category: 'test', isDefault: true },
            
            // Дизайн & Презентация
            { id: 'def-ai-3', name: 'Gamma App', url: 'https://gamma.app', desc: 'Жасанды интеллект көмегімен презентацияларды, құжаттарды және веб-парақшаларды бірнеше секундта көркем етіп жасау құралы.', category: 'design', isDefault: true },
            { id: 'def-2', name: 'Canva', url: 'https://www.canva.com', desc: 'Презентациялар, көрнекіліктер, дипломдар мен оқу парақшаларын кәсіби деңгейде безендіруге арналған құрал.', category: 'design', isDefault: true },
            { id: 'def-d-2', name: 'Genially', url: 'https://genially.com', desc: 'Интерактивті презентациялар, виртуалды ойындар мен қызықты инфографикалар дайындауға арналған керемет платформа.', category: 'design', isDefault: true },

            // Интерактивті тақта & платформалар
            { id: 'def-4', name: 'Padlet', url: 'https://padlet.com', desc: 'Оқушылармен бірлесе суреттер, сілтемелер мен пікірлер алмасуға арналған виртуалды тақта.', category: 'interactive', isDefault: true },
            { id: 'def-5', name: 'LearningApps', url: 'https://learningapps.org', desc: 'Сабаққа арналған дайын шағын ойындар, сөзжұмбақтар мен сәйкестендіру тапсырмаларының жинағы.', category: 'interactive', isDefault: true },
            { id: 'def-6', name: 'Wordwall', url: 'https://wordwall.net', desc: 'Әртүрлі үлгідегі интерактивті ойындар, кроссвордтар мен тапсырмалар құрастыруға арналған ресурс.', category: 'interactive', isDefault: true },
            { id: 'def-i-4', name: 'Classroomscreen', url: 'https://classroomscreen.com', desc: 'Сабақ барысында экранға шығарып қоюға арналған пайдалы виджеттер: таймер, шу деңгейін өлшегіш, кездейсоқ таңдау.', category: 'interactive', isDefault: true },
            { id: 'def-i-5', name: 'Nearpod', url: 'https://nearpod.com', desc: 'Мұғалімнің слайдтарын оқушы смартфонына жіберіп, нақты уақытта сұрақ қойып, жауабын бақылауға арналған платформа.', category: 'interactive', isDefault: true },
            { id: 'def-i-6', name: 'PhET Simulations', url: 'https://phet.colorado.edu/kk/', desc: 'Жаратылыстану бағытындағы (физика, химия, биология, математика) сабақтарға арналған интерактивті ғылыми зертханалық симуляциялар жинағы.', category: 'interactive', isDefault: true }
        ];

        let userSites = [];
        let favoriteIds = [];
        let currentFilter = 'method';
        let siteIdToDelete = null;
        let isAdminActive = false; // Тек құпия сөз енгізілгенде белсенді болады

        window.onload = function() {
            // Қосымша және әдепкі сайттарды жүктеу
            const savedSites = localStorage.getItem('teacher_user_sites');
            if (savedSites) {
                try { 
                    userSites = JSON.parse(savedSites); 
                } catch(e) { 
                    userSites = [...defaultSites]; 
                }
            } else {
                userSites = [...defaultSites];
                localStorage.setItem('teacher_user_sites', JSON.stringify(userSites));
            }

            // Таңдаулыларды жүктеу
            const savedFavs = localStorage.getItem('teacher_fav_ids');
            if (savedFavs) {
                try { favoriteIds = JSON.parse(savedFavs); } catch(e) { favoriteIds = []; }
            }

            // Жедел жазбаларды жүктеу
            const savedNotes = localStorage.getItem('teacher_quick_notes');
            if (savedNotes) {
                document.getElementById('quickNotesText').value = savedNotes;
            }

            // Админ күйін тексеру (браузер жабылып-ашылса да сақталуы үшін)
            const savedAdmin = sessionStorage.getItem('is_admin_active');
            if (savedAdmin === 'true') {
                isAdminActive = true;
                updateAdminUI();
            }

            renderSites();
        };

        // Админ режим терезесін ашу
        function openAdminAuthModal() {
            document.getElementById('adminPasswordInput').value = "";
            document.getElementById('adminAuthError').classList.add('hidden');
            
            const modal = document.getElementById('adminAuthModal');
            const modalContent = document.getElementById('adminModalContent');
            modal.classList.remove('hidden');
            setTimeout(() => {
                modalContent.classList.remove('scale-95');
                modalContent.classList.add('scale-100');
            }, 50);
        }

        // Админ режим терезесін жабу
        function closeAdminAuthModal() {
            const modal = document.getElementById('adminAuthModal');
            const modalContent = document.getElementById('adminModalContent');
            modalContent.classList.remove('scale-100');
            modalContent.classList.add('scale-95');
            setTimeout(() => {
                modal.classList.add('hidden');
            }, 150);
        }

        // Құпия сөзді тексеру
        function checkAdminPassword() {
            const pwd = document.getElementById('adminPasswordInput').value;
            // ҚҰПИЯ СӨЗ ОСЫ ЖЕРДЕ БЕЛГІЛЕНГЕН: admin123
            if (pwd === "admin123") {
                isAdminActive = true;
                sessionStorage.setItem('is_admin_active', 'true');
                showToast("Администратор режимі белсенді!", "success");
                updateAdminUI();
                closeAdminAuthModal();
                renderSites();
            } else {
                document.getElementById('adminAuthError').classList.remove('hidden');
            }
        }

        // Админнен шығу
        function logoutAdmin() {
            isAdminActive = false;
            sessionStorage.removeItem('is_admin_active');
            showToast("Администратор режимінен шықтыңыз", "edit");
            updateAdminUI();
            renderSites();
        }

        // Админ интерфейсін жаңарту
        function updateAdminUI() {
            const adminPanel = document.getElementById('adminPanelControls');
            const loginBtn = document.getElementById('adminLoginBtn');
            const logoutBtn = document.getElementById('adminLogoutBtn');

            if (isAdminActive) {
                adminPanel.classList.remove('hidden');
                loginBtn.classList.add('hidden');
                logoutBtn.classList.remove('hidden');
            } else {
                adminPanel.classList.add('hidden');
                loginBtn.classList.remove('hidden');
                logoutBtn.classList.add('hidden');
            }
        }

        // Тізімді құру және экранға шығару
        function renderSites() {
            const aiGrid = document.getElementById('aiSitesGrid');
            const otherGrid = document.getElementById('otherSitesGrid');
            const emptyState = document.getElementById('emptyState');
            const searchVal = document.getElementById('searchInput').value.toLowerCase();
            
            // 1. AI құралдары (тек іздеуге сәйкес келгендері)
            const aiSites = userSites.filter(site => {
                const matchesSearch = site.name.toLowerCase().includes(searchVal) || 
                                      (site.desc && site.desc.toLowerCase().includes(searchVal));
                return site.category === 'ai' && matchesSearch;
            });

            // 2. Басқа сайттар (санаттар және іздеу сөзі бойынша)
            const otherSites = userSites.filter(site => {
                const matchesSearch = site.name.toLowerCase().includes(searchVal) || 
                                      (site.desc && site.desc.toLowerCase().includes(searchVal));
                
                let matchesFilter = false;
                if (currentFilter === 'fav') {
                    matchesFilter = favoriteIds.includes(site.id);
                } else {
                    matchesFilter = site.category === currentFilter;
                }
                
                return site.category !== 'ai' && matchesFilter && matchesSearch;
            });

            // Санаттар бойынша стильдер
            const categories = {
                'ai': { label: 'Менің AI', color: 'bg-violet-50 text-violet-700 border-violet-100' },
                'method': { label: 'Әдістемелік құрал', color: 'bg-indigo-50 text-indigo-700 border-indigo-100' },
                'test': { label: 'Тест & Ойын', color: 'bg-emerald-50 text-emerald-700 border-emerald-100' },
                'design': { label: 'Дизайн & Слайд', color: 'bg-purple-50 text-purple-700 border-purple-100' },
                'interactive': { label: 'Интерактивті құрал', color: 'bg-sky-50 text-sky-700 border-sky-100' }
            };

            // Карточка құрастыру HTML
            const createCardHTML = (site) => {
                const cat = categories[site.category] || { label: 'Басқа', color: 'bg-slate-50 text-slate-700 border-slate-100' };
                const isStarred = favoriteIds.includes(site.id);
                
                let domain = "";
                try {
                    domain = new URL(site.url).hostname;
                } catch(e) {
                    domain = "";
                }
                const faviconUrl = domain ? `https://www.google.com/s2/favicons?sz=64&domain=${domain}` : '';

                const isAI = site.category === 'ai';
                const cardStyle = isAI 
                    ? 'border-violet-100 hover:border-violet-300 hover:shadow-violet-600/5 bg-gradient-to-b from-white to-violet-50/10' 
                    : 'border-slate-100 hover:border-indigo-200 hover:shadow-indigo-600/5 bg-white';

                // Админ болса өңдеу/өшіру батырмаларын көрсету, болмаса жасыру
                const actionControls = isAdminActive ? `
                    <div class="flex gap-1.5">
                        <button onclick="editSite('${site.id}')" class="text-slate-400 hover:text-amber-600 hover:bg-amber-50 p-2 rounded-xl transition-all" title="Өңдеу">
                            <svg class="w-4.5 h-4.5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
                        </button>
                        <button onclick="openDeleteModal('${site.id}')" class="text-slate-400 hover:text-rose-600 hover:bg-rose-50 p-2 rounded-xl transition-all" title="Өшіру">
                            <svg class="w-4.5 h-4.5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                        </button>
                    </div>
                ` : '';

                return `
                    <div class="${cardStyle} p-6 rounded-3xl border shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 flex flex-col justify-between relative group">
                        <div>
                            <!-- Үстіңгі детальдар -->
                            <div class="flex items-center justify-between mb-5">
                                <div class="w-11 h-11 rounded-2xl bg-slate-50 flex items-center justify-center overflow-hidden border border-slate-100 shadow-inner group-hover:scale-105 transition-transform duration-300">
                                    ${faviconUrl ? 
                                        `<img src="${faviconUrl}" alt="${site.name}" class="w-6 h-6 object-contain" onerror="this.src='data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\' fill=\'none\' viewBox=\'0 0 24 24\' stroke=\'%236366f1\'><path stroke-linecap=\'round\' stroke-linejoin=\'round\' stroke-width=\'2\' d=\'M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9\'/></svg>'">` 
                                        : 
                                        `<svg class="w-5 h-5 text-indigo-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9"></path></svg>`
                                    }
                                </div>
                                <div class="flex items-center gap-2">
                                    <!-- Таңдаулы батырмасы -->
                                    <button onclick="toggleFavorite('${site.id}')" title="${isStarred ? 'Таңдаулылардан жою' : 'Таңдаулыларға қосу'}" class="p-2 rounded-xl border ${isStarred ? 'bg-amber-50 border-amber-200 text-amber-500 hover:bg-amber-100' : 'bg-slate-50 border-slate-100 text-slate-400 hover:text-amber-500 hover:bg-amber-50'} transition-all duration-200">
                                        <svg class="w-4 h-4 fill-current" viewBox="0 0 20 20"><path d="M10 15l-5.878 3.09 1.123-6.545L.489 6.91l6.572-.955L10 0l2.939 5.955 6.572.955-4.756 4.635 1.123 6.545z"/></svg>
                                    </button>
                                    <span class="px-3 py-1 rounded-xl text-xs font-bold border ${cat.color} tracking-wide">
                                        ${cat.label}
                                    </span>
                                </div>
                            </div>

                            <!-- Аты мен сипаттамасы -->
                            <h3 class="text-lg font-bold text-slate-900 group-hover:text-indigo-600 transition-colors duration-200">${site.name}</h3>
                            <p class="text-slate-500 text-sm mt-2 mb-6 line-clamp-3 font-semibold leading-relaxed">${site.desc || 'Қосымша сипаттама енгізілмеген.'}</p>
                        </div>

                        <!-- Әрекеттер -->
                        <div class="flex items-center justify-between pt-4 border-t border-slate-100 mt-auto">
                            <a href="${site.url}" target="_blank" class="inline-flex items-center gap-1.5 text-sm font-bold text-indigo-600 hover:text-indigo-800 transition-colors">
                                Сайтқа өту
                                <svg class="w-4 h-4 transform group-hover:translate-x-0.5 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path></svg>
                            </a>

                            ${actionControls}
                        </div>
                    </div>
                `;
            };

            // AI тізімі
            if (aiSites.length === 0) {
                aiGrid.innerHTML = `
                    <div class="col-span-full text-center py-10 bg-slate-50 rounded-3xl text-slate-400 text-sm border-2 border-dashed border-slate-200">
                        <svg class="w-10 h-10 mx-auto mb-3 text-slate-300" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M12 9v3m0 0v3m0-3h3m-3 0H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                        <p class="font-bold text-slate-600">Мұнда әлі сіз қосқан AI құралдары жоқ.</p>
                        ${isAdminActive ? 
                          '<p class="text-slate-400 text-xs mt-1">Оларды қосу үшін жоғарғы оң жақтағы <strong>"Сайт қосу"</strong> батырмасын басыңыз!</p>' : 
                          '<p class="text-slate-400 text-xs mt-1">Администратор жаңа ресурстар қосқанда осында пайда болады.</p>'}
                    </div>
                `;
            } else {
                aiGrid.innerHTML = aiSites.map(createCardHTML).join('');
            }

            // Басқа сайттар кестесі
            if (otherSites.length === 0) {
                otherGrid.innerHTML = '';
                emptyState.classList.remove('hidden');
            } else {
                emptyState.classList.add('hidden');
                otherGrid.innerHTML = otherSites.map(createCardHTML).join('');
            }
        }

        // Фильтр белсендіру
        function setFilter(filterType) {
            currentFilter = filterType;
            
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.className = "filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl text-slate-600 bg-white border border-slate-200 hover:bg-slate-50 transition-all duration-200";
                if (btn.id === 'btn-fav') {
                    btn.className = "filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl text-slate-600 bg-white border border-slate-200 hover:bg-slate-50 transition-all duration-200 flex items-center gap-1.5";
                }
            });

            const activeBtn = document.getElementById(`btn-${filterType}`);
            if (activeBtn) {
                if (filterType === 'fav') {
                    activeBtn.className = "filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl bg-indigo-600 text-white shadow-md shadow-indigo-600/10 transition-all duration-200 flex items-center gap-1.5";
                } else {
                    activeBtn.className = "filter-btn shrink-0 px-5 py-2.5 text-xs font-bold rounded-xl bg-indigo-600 text-white shadow-md shadow-indigo-600/10 transition-all duration-200";
                }
            }

            renderSites();
        }

        // Сүзгілеу мен іздеу
        function filterAndSearch() {
            renderSites();
        }

        // Таңдаулыларды ауыстырып қосу
        function toggleFavorite(id) {
            if (favoriteIds.includes(id)) {
                favoriteIds = favoriteIds.filter(favId => favId !== id);
                showToast("Таңдаулылардан алынды", "edit");
            } else {
                favoriteIds.push(id);
                showToast("Таңдаулыларға қосылды", "success");
            }
            localStorage.setItem('teacher_fav_ids', JSON.stringify(favoriteIds));
            renderSites();
        }

        // Жедел жазбалар терезесін ашу/жабу
        function toggleStickyNotes() {
            const panel = document.getElementById('stickyNotesPanel');
            if (panel.classList.contains('hidden')) {
                panel.classList.remove('hidden');
                setTimeout(() => {
                    panel.classList.remove('translate-y-4', 'opacity-0');
                    panel.classList.add('translate-y-0', 'opacity-100');
                }, 50);
            } else {
                panel.classList.remove('translate-y-0', 'opacity-100');
                panel.classList.add('translate-y-4', 'opacity-0');
                setTimeout(() => {
                    panel.classList.add('hidden');
                }, 300);
            }
        }

        // Жазбаларды автоматты сақтау
        function saveNotes() {
            const val = document.getElementById('quickNotesText').value;
            localStorage.setItem('teacher_quick_notes', val);
        }

        // Қосқан сайттарды файл ретінде экспорттау (JSON)
        function exportData() {
            if (userSites.length === 0) {
                showToast("Экспорттайтын жаңа сайттар жоқ!", "delete");
                return;
            }
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(userSites));
            const dlAnchorElem = document.createElement('a');
            dlAnchorElem.setAttribute("href", dataStr);
            dlAnchorElem.setAttribute("download", "ustaz_resources_backup.json");
            document.body.appendChild(dlAnchorElem);
            dlAnchorElem.click();
            dlAnchorElem.remove();
            showToast("Сайттар файлға сәтті сақталды!", "success");
        }

        // Импорт терезесін іске қосу
        function triggerImport() {
            document.getElementById('importFile').click();
        }

        // Файлдан сайттарды импорттау
        function importData(e) {
            const file = e.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(evt) {
                try {
                    const imported = JSON.parse(evt.target.result);
                    if (Array.isArray(imported)) {
                        userSites = imported;
                        localStorage.setItem('teacher_user_sites', JSON.stringify(userSites));
                        renderSites();
                        showToast("Сайттар сәтті қалпына келтірілді!", "success");
                    } else {
                        showToast("Файл форматы дұрыс емес!", "delete");
                    }
                } catch(err) {
                    showToast("Файлды оқу мүмкін болмады!", "delete");
                }
                e.target.value = ""; // Тазалау
            };
            reader.readAsText(file);
        }

        // Қалпына келтіру модалін ашу
        function openResetModal() {
            const modal = document.getElementById('resetConfirmModal');
            const modalContent = document.getElementById('resetModalContent');
            modal.classList.remove('hidden');
            setTimeout(() => {
                modalContent.classList.remove('scale-95');
                modalContent.classList.add('scale-100');
            }, 50);
        }

        // Қалпына келтіру модалін жабу
        function closeResetModal() {
            const modal = document.getElementById('resetConfirmModal');
            const modalContent = document.getElementById('resetModalContent');
            modalContent.classList.remove('scale-100');
            modalContent.classList.add('scale-95');
            setTimeout(() => {
                modal.classList.add('hidden');
            }, 150);
        }

        // Толықтай әдепкі күйге қалпына келтіру
        function confirmResetAll() {
            userSites = [...defaultSites];
            favoriteIds = [];
            localStorage.setItem('teacher_user_sites', JSON.stringify(userSites));
            localStorage.setItem('teacher_fav_ids', JSON.stringify(favoriteIds));
            renderSites();
            showToast("Бастапқы сайттар қалпына келтірілді!", "success");
            closeResetModal();
        }

        // Модал терезені ашу
        function openModal(editId = null) {
            const modal = document.getElementById('modal');
            const modalContent = document.getElementById('modalContent');
            const form = document.getElementById('siteForm');
            const modalTitle = document.getElementById('modalTitle');
            
            form.reset();
            document.getElementById('editId').value = '';
            
            if (editId) {
                modalTitle.textContent = "Сайтты өңдеу";
                const target = userSites.find(s => s.id === editId);
                if (target) {
                    document.getElementById('editId').value = target.id;
                    document.getElementById('siteName').value = target.name;
                    document.getElementById('siteUrl').value = target.url;
                    document.getElementById('siteCategory').value = target.category;
                    document.getElementById('siteDesc').value = target.desc || '';
                }
            } else {
                modalTitle.textContent = "Жаңа сайт қосу";
            }

            modal.classList.remove('hidden');
            setTimeout(() => {
                modalContent.classList.remove('scale-95');
                modalContent.classList.add('scale-100');
            }, 50);
        }

        // Модальді жабу
        function closeModal() {
            const modal = document.getElementById('modal');
            const modalContent = document.getElementById('modalContent');
            
            modalContent.classList.remove('scale-100');
            modalContent.classList.add('scale-95');
            setTimeout(() => {
                modal.classList.add('hidden');
            }, 150);
        }

        // Жеке Растау Модалін ашу (Confirm алмастырғышы)
        function openDeleteModal(id) {
            siteIdToDelete = id;
            const modal = document.getElementById('deleteConfirmModal');
            const modalContent = document.getElementById('deleteModalContent');

            modal.classList.remove('hidden');
            setTimeout(() => {
                modalContent.classList.remove('scale-95');
                modalContent.classList.add('scale-100');
            }, 50);
        }

        // Растау Модалін жабу
        function closeDeleteModal() {
            const modal = document.getElementById('deleteConfirmModal');
            const modalContent = document.getElementById('deleteModalContent');
            
            modalContent.classList.remove('scale-100');
            modalContent.classList.add('scale-95');
            setTimeout(() => {
                modal.classList.add('hidden');
                siteIdToDelete = null;
            }, 150);
        }

        // Расталған соң өшіруді аяқтау
        function confirmDeleteSite() {
            if (siteIdToDelete) {
                // Таңдаулылардан да өшіру
                favoriteIds = favoriteIds.filter(fId => fId !== siteIdToDelete);
                localStorage.setItem('teacher_fav_ids', JSON.stringify(favoriteIds));

                userSites = userSites.filter(site => site.id !== siteIdToDelete);
                localStorage.setItem('teacher_user_sites', JSON.stringify(userSites));
                showToast("Ресурс сәтті өшірілді", "delete");
                renderSites();
            }
            closeDeleteModal();
        }

        // Сайт мәліметтерін жадқа жазу
        function saveSite(e) {
            e.preventDefault();

            const editId = document.getElementById('editId').value;
            const name = document.getElementById('siteName').value.trim();
            const url = document.getElementById('siteUrl').value.trim();
            const category = document.getElementById('siteCategory').value;
            const desc = document.getElementById('siteDesc').value.trim();

            if (editId) {
                userSites = userSites.map(site => {
                    if (site.id === editId) {
                        return { ...site, name, url, category, desc };
                    }
                    return site;
                });
                showToast("Ресурс сәтті өзгертілді!", "edit");
            } else {
                const newSite = {
                    id: 'user-' + Date.now(),
                    name,
                    url,
                    category,
                    desc,
                    isDefault: false
                };
                userSites.push(newSite);
                showToast("Жаңа ресурс сәтті қосылды!", "add");
            }

            localStorage.setItem('teacher_user_sites', JSON.stringify(userSites));
            renderSites();
            closeModal();
        }

        // Өңдеу режимін іске қосу
        function editSite(id) {
            openModal(id);
        }

        // Сәнді Toast көрсету жүйесі
        function showToast(message, type = "success") {
            const toast = document.getElementById('toast');
            const toastMessage = document.getElementById('toastMessage');
            const toastIcon = document.getElementById('toastIcon');

            toastMessage.textContent = message;

            if (type === 'delete') {
                toastIcon.className = "p-1.5 rounded-xl bg-rose-500/10 text-rose-500";
                toastIcon.innerHTML = `<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>`;
            } else if (type === 'edit') {
                toastIcon.className = "p-1.5 rounded-xl bg-amber-500/10 text-amber-500";
                toastIcon.innerHTML = `<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"></path></svg>`;
            } else {
                toastIcon.className = "p-1.5 rounded-xl bg-emerald-500/10 text-emerald-500";
                toastIcon.innerHTML = `<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"></path></svg>`;
            }

            toast.classList.remove('translate-y-10', 'opacity-0', 'pointer-events-none');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-10', 'opacity-0', 'pointer-events-none');
            }, 3000);
        }
    </script>
</body>
</html>
