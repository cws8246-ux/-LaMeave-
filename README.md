<!DOCTYPE html>
<html lang="ko" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LaMeave | High-End Wellness Lounge</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Fonts: Cinzel (Classic Luxury), Playfair Display (Elegant), Noto Sans KR (Modern) -->
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Playfair+Display:ital,wght@0,400..900;1,400..900&family=Noto+Sans+KR:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        /* --- Premium Dark Theme Variables --- */
        :root {
            --bg-dark: #0f0f0f;
            --bg-card: #1a1a1a;
            --text-main: #ffffff; /* Increased contrast to pure white */
            --text-muted: #c0c0c0; /* Brighter muted text */
            --accent-orange: #dfa67b; /* Muted Gold/Orange for luxury */
            --accent-hermes: #ff5e1e; /* Vibrant Hermes Orange for CTA */
            --border-color: rgba(223, 166, 123, 0.2);
            --default-font-base: 16px;
            --font-size-scale: 1.0;
        }

        body {
            font-family: 'Noto Sans KR', sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-main);
            font-size: calc(var(--default-font-base) * var(--font-size-scale));
            overflow-x: hidden;
            word-break: keep-all;
        }

        /* --- Typography Classes --- */
        .font-luxury { font-family: 'Cinzel', serif; }
        .font-serif { font-family: 'Playfair Display', serif; }
        
        /* Contrast Improvement: Brighter text for better visibility */
        .text-gray-500 { color: #A0A0A0; } /* Adjusted standard gray for body text */
        .text-gray-400 { color: #C0C0C0; } /* Adjusted lighter gray for descriptions */

        /* --- Component Styles --- */
        .glass-panel {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        /* --- Graph Styles for Animation (IMPORTANT: height: 0 for smooth transition) --- */
        .bar-chart-bar {
            transition: height 1.5s ease-out;
            height: 0; /* Initial state for animation */
        }
        .progress-ring-circle {
            transition: stroke-dashoffset 1.5s ease-in-out;
            transform: rotate(-90deg);
            transform-origin: 50% 50%;
            /* Initial state for animation, will be set by JS */
            stroke-dashoffset: 1000; 
        }

        /* --- Editable Content Styles --- */
        .editable-text {
            border-bottom: 1px dashed transparent;
            transition: all 0.3s;
        }
        [contenteditable="true"] {
            border-bottom: 1px dashed var(--accent-hermes);
            background: rgba(255, 94, 30, 0.1);
            outline: none;
            padding: 2px 4px;
        }

        /* --- Animations & Scrollbar remain the same --- */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
            animation: fadeIn 1s ease-out forwards;
        }
        .delay-100 { animation-delay: 0.2s; }
        .delay-200 { animation-delay: 0.4s; }
        .delay-300 { animation-delay: 0.6s; }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg-dark); }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--accent-hermes); }
    </style>
</head>
<body class="relative">

    <!-- Navbar: Floating & Transparent -->
    <nav class="fixed w-full z-50 transition-all duration-300 bg-black/80 backdrop-blur-md border-b border-white/5">
        <div class="max-w-7xl mx-auto px-6 h-20 flex justify-between items-center">
            <!-- Logo -->
            <a href="#" class="text-2xl md:text-3xl font-luxury tracking-widest text-white">
                LA<span class="text-[#ff5e1e]">MEAVE</span>
            </a>

            <!-- Desktop Menu -->
            <div class="hidden md:flex space-x-12 text-sm font-medium tracking-widest text-gray-400">
                <a href="#philosophy" class="hover:text-[#ff5e1e] transition-colors">PHILOSOPHY</a>
                <a href="#difference" class="hover:text-[#ff5e1e] transition-colors">DIFFERENCE</a>
                <a href="#program" class="hover:text-[#ff5e1e] transition-colors">PROGRAM</a>
                <a href="#membership" class="hover:text-[#ff5e1e] transition-colors">MEMBERSHIP</a>
            </div>

            <!-- Controls -->
            <div class="flex items-center space-x-4">
                <button id="settings-btn" class="text-xs text-gray-400 hover:text-white border border-gray-600 px-3 py-1 rounded uppercase tracking-wider transition">
                    Settings
                </button>
                <button id="save-btn" class="hidden text-xs bg-green-900 text-green-100 px-3 py-1 rounded uppercase tracking-wider hover:bg-green-800 transition">
                    Save Changes
                </button>
                <a href="https://map.naver.com/p/search/%EC%B2%AD%EB%9D%98%ED%83%9C%EB%8B%9C/place/1491238486" target="_blank" class="bg-[#ff5e1e] text-white text-xs font-bold px-6 py-3 rounded-none hover:bg-[#d14008] transition tracking-widest">
                    RESERVE
                </a>
            </div>
        </div>
    </nav>

    <!-- Settings Modal (UNCHANGED) -->
    <div id="settings-modal" class="fixed inset-0 bg-black/90 z-[60] hidden flex items-center justify-center backdrop-blur-sm">
        <div class="bg-[#1a1a1a] border border-gray-700 p-8 max-w-md w-full shadow-2xl relative">
            <button id="close-modal" class="absolute top-4 right-4 text-gray-500 hover:text-white">✕</button>
            <h2 class="text-xl font-serif text-[#dfa67b] mb-6 tracking-wide border-b border-gray-700 pb-4">PAGE SETTINGS</h2>
            
            <!-- Font Size -->
            <div class="mb-8">
                <label class="block text-xs text-gray-400 uppercase tracking-widest mb-3">Font Size Scale</label>
                <input type="range" id="font-size-slider" min="0.8" max="1.2" step="0.05" value="1.0" class="w-full h-1 bg-gray-700 rounded-lg appearance-none cursor-pointer accent-[#ff5e1e]">
                <div class="flex justify-between text-[10px] text-gray-500 mt-2">
                    <span>Small</span>
                    <span>Default</span>
                    <span>Large</span>
                </div>
            </div>

            <!-- Admin Access -->
            <div>
                <label class="block text-xs text-gray-400 uppercase tracking-widest mb-3">Admin Edit Mode</label>
                <div class="flex gap-2">
                    <input type="password" id="edit-password" placeholder="Enter Passcode" class="flex-1 bg-black border border-gray-700 text-white px-4 py-2 text-sm focus:border-[#ff5e1e] outline-none transition">
                    <button id="activate-edit-btn" class="bg-white text-black px-4 py-2 text-xs font-bold hover:bg-gray-200 transition">UNLOCK</button>
                </div>
                <p id="password-message" class="text-xs mt-2 h-4"></p>
            </div>
        </div>
    </div>

    <!-- Hero Section (IMAGE RETAINED) -->
    <section id="philosophy" class="relative h-screen flex items-center justify-center overflow-hidden">
        <!-- Background Image with Overlay (Updated to a placeholder of a woman receiving treatment) -->
        <div class="absolute inset-0 z-0">
            <img src="https://images.unsplash.com/photo-1596700813876-03612809e0a8?q=80&w=2940&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" 
                 alt="Luxury Wellness Lounge - Woman receiving treatment" class="w-full h-full object-cover opacity-50"> <!-- Opacity slightly increased -->
            <div class="absolute inset-0 bg-gradient-to-b from-[#0f0f0f] via-transparent to-[#0f0f0f]"></div>
            <div class="absolute inset-0 bg-black/40"></div> <!-- Overlay slightly darker -->
        </div>

        <div class="relative z-10 text-center px-6 max-w-5xl mx-auto animate-fade-in">
            <p class="text-[#ff5e1e] font-bold tracking-[0.3em] text-sm md:text-base mb-6 uppercase editable-text" data-field="hero_subtitle" contenteditable="false">
                French Chic Wellness Lounge
            </p>
            <h1 class="font-serif text-5xl md:text-7xl lg:text-8xl text-white mb-8 leading-tight editable-text" data-field="hero_title" contenteditable="false">
                Elevate Me,<br>LaMeave
            </h1>
            <div class="w-20 h-[1px] bg-[#dfa67b] mx-auto mb-8"></div>
            <p class="text-gray-200 text-lg md:text-2xl font-light leading-relaxed mb-12 editable-text" data-field="hero_desc" contenteditable="false">
                내면(마음)과 외면(몸)의 균형을 되찾아,<br>
                나를 <span class="text-white font-normal">더 아름답게, 밝게, 가볍게</span> 만드는 공간.
            </p>
        </div>
        
        <!-- Scroll Indicator -->
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 animate-bounce">
            <span class="text-gray-500 text-xs tracking-widest">SCROLL</span>
        </div>
    </section>

    <!-- Philosophy Grid (TEXT CONTRAST IMPROVED) -->
    <section class="py-24 px-6 bg-[#0f0f0f]">
        <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-0 divide-y md:divide-y-0 md:divide-x divide-gray-800 border-t border-b border-gray-800">
            <!-- La -->
            <div class="p-12 text-center group hover:bg-[#151515] transition duration-500">
                <span class="font-serif text-6xl text-gray-800 group-hover:text-[#dfa67b] transition duration-500 block mb-4 editable-text" data-field="la_title" contenteditable="false">La</span>
                <h3 class="text-[#ff5e1e] text-xs font-bold tracking-[0.2em] mb-4 uppercase editable-text" data-field="la_sub" contenteditable="false">The Value</h3>
                <p class="text-gray-300 font-light leading-relaxed editable-text" data-field="la_desc" contenteditable="false">더 높은 가치를 향한<br>유일한 선택</p>
            </div>
            <!-- Me -->
            <div class="p-12 text-center group hover:bg-[#151515] transition duration-500">
                <span class="font-serif text-6xl text-gray-800 group-hover:text-[#dfa67b] transition duration-500 block mb-4 editable-text" data-field="me_title" contenteditable="false">Me</span>
                <h3 class="text-[#ff5e1e] text-xs font-bold tracking-[0.2em] mb-4 uppercase editable-text" data-field="me_sub" contenteditable="false">Myself</h3>
                <p class="text-gray-300 font-light leading-relaxed editable-text" data-field="me_desc" contenteditable="false">오직 나에게 집중하는<br>프라이빗 타임</p>
            </div>
            <!-- Ave -->
            <div class="p-12 text-center group hover:bg-[#151515] transition duration-500">
                <span class="font-serif text-6xl text-gray-800 group-hover:text-[#dfa67b] transition duration-500 block mb-4 editable-text" data-field="ave_title" contenteditable="false">Ave</span>
                <h3 class="text-[#ff5e1e] text-xs font-bold tracking-[0.2em] mb-4 uppercase editable-text" data-field="ave_sub" contenteditable="false">Elevation</h3>
                <p class="text-gray-300 font-light leading-relaxed editable-text" data-field="ave_desc" contenteditable="false">나의 아름다움을<br>가장 높이 끌어올리다</p>
            </div>
        </div>
    </section>

    <!-- The Difference (Comparison Data - EMS GRAPH IMPROVED) -->
    <section id="difference" class="py-32 bg-[#121212] relative">
        <div class="max-w-7xl mx-auto px-6">
            <div class="text-center mb-24">
                <h2 class="font-serif text-4xl md:text-5xl text-white mb-6 editable-text" data-field="diff_main_title" contenteditable="false">The Difference</h2>
                <p class="text-gray-300 max-w-2xl mx-auto editable-text" data-field="diff_main_desc" contenteditable="false">
                    일반적인 운동만으로는 도달할 수 없는 영역.<br>
                    라 미브는 데이터와 과학으로 증명된 압도적인 효율을 제공합니다.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
                <!-- Graph 1: Bar Chart (EMS Visual Emphasis) -->
                <div class="glass-panel p-10 rounded-sm hover:border-[#ff5e1e]/30 transition duration-500">
                    <h3 class="text-xl text-white font-light mb-8 border-l-2 border-[#ff5e1e] pl-4 editable-text" data-field="graph1_title" contenteditable="false">
                        EMS 트레이닝 효과: 시간 대비 극대화된 효율
                    </h3>
                    <div class="flex justify-around items-end h-64 pb-4 border-b border-gray-800 relative">
                        <!-- PT Bar -->
                        <div class="w-24 group relative">
                            <!-- New label for EMS benefit -->
                            <div class="absolute -top-16 left-1/2 -translate-x-1/2 text-white text-xs font-medium bg-gray-900 px-2 py-1 rounded-full opacity-0 group-hover:opacity-100 transition whitespace-nowrap">일반 PT (50분)</div>
                            <div class="absolute -top-8 left-1/2 -translate-x-1/2 text-gray-500 text-sm font-bold opacity-0 group-hover:opacity-100 transition">45%</div>
                            <div class="bar-chart-bar bg-gradient-to-t from-gray-800 to-gray-600 w-full mx-auto rounded-t-sm" data-target-percent="45"></div>
                            <p class="text-center text-gray-500 text-xs mt-4 tracking-widest uppercase editable-text" data-field="label_pt" contenteditable="false">1:1 PT</p>
                        </div>
                        
                        <!-- LaMeave Bar (Emphasized for EMS + Therapy) -->
                        <div class="w-24 group relative">
                            <!-- New label for EMS benefit -->
                            <div class="absolute -top-16 left-1/2 -translate-x-1/2 text-white text-xs font-medium bg-[#ff5e1e] px-2 py-1 rounded-full opacity-0 group-hover:opacity-100 transition whitespace-nowrap">EMS & 테라피 (70분)</div>
                            <div class="absolute -top-8 left-1/2 -translate-x-1/2 text-[#ff5e1e] text-lg font-bold opacity-0 group-hover:opacity-100 transition">85%</div>
                            <div class="bar-chart-bar bg-gradient-to-t from-[#8B3A15] to-[#ff5e1e] w-full mx-auto rounded-t-sm shadow-[0_0_20px_rgba(255,94,30,0.3)]" data-target-percent="85"></div>
                            <p class="text-center text-[#ff5e1e] text-xs mt-4 tracking-widest uppercase font-bold editable-text" data-field="label_meave" contenteditable="false">LaMeave</p>
                        </div>
                    </div>
                    
                    <!-- Added EMS explanatory box below the graph for strong visual context -->
                    <div class="mt-8 p-4 bg-[#1a1a1a] border-l-4 border-[#ff5e1e] shadow-lg">
                        <p class="text-sm font-bold text-[#ff5e1e] mb-1">⚡ 20분 EMS = 6시간 일반 운동 효과</p>
                        <p class="text-xs text-gray-400">라 미브는 **EMS 트레이닝**을 통해 짧은 시간 안에 깊은 근육을 자극하여 일반 PT 대비 **약 2배 높은 에너지 소모 효율**을 달성합니다. 여기에 전문가의 순환 테라피가 결합되어 결과가 극대화됩니다.</p>
                    </div>
                    
                    <p class="text-xs text-gray-500 mt-6 text-right italic editable-text" data-field="graph1_note" contenteditable="false">*20분 EMS 트레이닝 기준의 운동 효과 및 테라피 결합 시너지 반영</p>
                </div>

                <!-- Graph 2: Circular Progress (Unchanged) -->
                <div class="glass-panel p-10 rounded-sm hover:border-[#ff5e1e]/30 transition duration-500">
                    <h3 class="text-xl text-white font-light mb-8 border-l-2 border-[#ff5e1e] pl-4 editable-text" data-field="graph2_title" contenteditable="false">
                        체질 개선 완성도 및 지속성
                    </h3>
                    <div class="flex justify-around items-center h-64">
                        <!-- Circle Graph PT (data-percent for JS) -->
                        <div class="relative w-32 h-32" data-radius="60" data-percent="30">
                            <svg class="w-full h-full transform -rotate-90">
                                <circle cx="64" cy="64" r="60" stroke="#333" stroke-width="4" fill="none"></circle>
                                <circle id="pt-progress" cx="64" cy="64" r="60" stroke="#666" stroke-width="4" fill="none" stroke-dasharray="377" class="progress-ring-circle"></circle>
                            </svg>
                            <div class="absolute inset-0 flex items-center justify-center text-gray-500 font-bold text-xl editable-text" data-field="pt_percent" contenteditable="false">30%</div>
                            <p class="text-center text-gray-500 text-xs mt-4 tracking-widest uppercase absolute -bottom-8 w-full">Normal PT</p>
                        </div>
                        <!-- Circle Graph LaMeave (data-percent for JS) -->
                        <div class="relative w-40 h-40" data-radius="70" data-percent="95">
                            <svg class="w-full h-full transform -rotate-90">
                                <circle cx="80" cy="80" r="70" stroke="#333" stroke-width="6" fill="none"></circle>
                                <circle id="lameave-progress" cx="80" cy="80" r="70" stroke="#ff5e1e" stroke-width="6" fill="none" stroke-dasharray="440" class="progress-ring-circle drop-shadow-[0_0_10px_rgba(255,94,30,0.5)]"></circle>
                            </svg>
                            <div class="absolute inset-0 flex items-center justify-center text-white font-bold text-3xl editable-text" data-field="lameave_percent" contenteditable="false">95%</div>
                            <p class="text-center text-[#ff5e1e] text-xs mt-4 tracking-widest uppercase font-bold absolute -bottom-8 w-full">LaMeave</p>
                        </div>
                    </div>
                    <p class="text-xs text-gray-500 mt-10 text-right italic editable-text" data-field="graph2_note" contenteditable="false">*8가지 패턴 관리 및 항상성 회복 기준</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Program Flow (Vertical Luxury Timeline - TEXT CONTRAST IMPROVED) -->
    <section id="program" class="py-32 bg-[#0f0f0f]">
        <div class="max-w-4xl mx-auto px-6">
            <div class="text-center mb-20">
                <span class="text-[#dfa67b] text-sm tracking-[0.3em] uppercase block mb-3 editable-text" data-field="flow_super" contenteditable="false">Signature Program</span>
                <h2 class="font-serif text-4xl text-white editable-text" data-field="flow_title" contenteditable="false">70min Premium Care Flow</h2>
            </div>

            <div class="space-y-4">
                <!-- Step 1 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">01</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step1_title" contenteditable="false">웰컴 & 퍼스트 릴렉싱</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step1_desc" contenteditable="false">심신 이완 및 케어 준비</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 2 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">02</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step2_title" contenteditable="false">정밀 인바디 & 패턴 진단</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step2_desc" contenteditable="false">8가지 체형/체질 데이터 분석</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 3 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">03</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step3_title" contenteditable="false">프렌치 엘레베이션 테라피</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step3_desc" contenteditable="false">순환 극대화 및 밸런스 회복</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 4 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">04</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step4_title" contenteditable="false">프렌치 리프팅</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step4_desc" contenteditable="false">바디 탄력 및 라인 컨투어링</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 5 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">05</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step5_title" contenteditable="false">닥터 테라피</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step5_desc" contenteditable="false">근육 이완 및 최종 회복 마무리</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Exclusive Features (TEXT CONTRAST IMPROVED) -->
    <section class="py-32 bg-[#121212]">
        <div class="max-w-7xl mx-auto px-6">
            <h2 class="font-serif text-3xl md:text-4xl text-white text-center mb-20 editable-text" data-field="feat_title" contenteditable="false">Exclusive Amenities</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <!-- Item 1 -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6">⚡</div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat1_title" contenteditable="false">EMS Training</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat1_desc" contenteditable="false">20분으로 6시간 효과를 내는<br>초밀도 근육 자극</p>
                </div>
                <!-- Item 2 -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6">✨</div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat2_title" contenteditable="false">White Tanning</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat2_desc" contenteditable="false">피부 톤 개선과 탄력을 위한<br>프리미엄 뷰티 솔루션</p>
                </div>
                <!-- Item 3 -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6">🛋️</div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat3_title" contenteditable="false">Phantom Recovery</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat3_desc" contenteditable="false">바디프랜드 팬텀으로<br>완벽한 전신 피로 해소</p>
                </div>
                <!-- Item 4 -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6">📊</div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat4_title" contenteditable="false">Data Tracking</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat4_desc" contenteditable="false">매 회차 정밀 분석을 통한<br>개인 맞춤형 로드맵</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer (TEXT CONTRAST IMPROVED) -->
    <footer class="bg-black py-24 border-t border-gray-900">
        <div class="max-w-5xl mx-auto px-6 text-center">
            <h2 class="font-serif text-4xl text-white mb-8 editable-text" data-field="footer_cta" contenteditable="false">Begin Your Journey</h2>
            <p class="text-gray-400 mb-12 editable-text" data-field="footer_sub" contenteditable="false">진정한 변화를 위한 첫 걸음, 라 미브와 함께하세요.</p>
            
            <a href="https://map.naver.com/p/search/%EC%B2%AD%EB%9D%98%ED%83%9C%EB%8B%9C/place/1491238486" target="_blank" class="inline-block border border-[#ff5e1e] text-[#ff5e1e] px-10 py-4 hover:bg-[#ff5e1e] hover:text-white transition duration-300 tracking-widest uppercase text-sm mb-16">
                Book Consultation
            </a>

            <div class="border-t border-gray-900 pt-12">
                <!-- 전화번호 삭제 및 주소 마진 조정 (mb-2 -> mb-6) -->
                <p class="text-gray-600 text-sm mb-6">인천 서구 중봉대로586번길 15 청연 프라자 906호</p>
                <!-- <p class="text-gray-600 text-sm mb-6">Contact: 032-123-4567</p> <-- 삭제됨 -->
                <p class="text-gray-700 text-xs tracking-widest">© 2025 LAMEAVE. ALL RIGHTS RESERVED.</p>
            </div>
        </div>
    </footer>

    <!-- Logic Script -->
    <script>
        const settingsBtn = document.getElementById('settings-btn');
        const settingsModal = document.getElementById('settings-modal');
        const closeModalBtn = document.getElementById('close-modal');
        const fontSizeSlider = document.getElementById('font-size-slider');
        const editPasswordInput = document.getElementById('edit-password');
        const activateEditBtn = document.getElementById('activate-edit-btn');
        const passwordMessage = document.getElementById('password-message');
        const saveBtn = document.getElementById('save-btn');
        const root = document.documentElement;
        
        const PASSWORD = '8246';

        // Helper function for circular progress animation
        const setProgress = (circleId, radius, percent) => {
            const circle = document.getElementById(circleId);
            if (!circle) return;
            // The circumference calculation is based on 2*PI*r
            const circumference = 2 * Math.PI * radius;
            circle.style.strokeDasharray = `${circumference}`;
            // Calculate the offset to represent the percentage
            const offset = circumference * (1 - percent / 100);
            
            // Timeout is used to ensure the initial CSS style (stroke-dashoffset: 1000) is applied 
            // before the transition to the target offset begins for a smooth animation.
            setTimeout(() => {
                circle.style.strokeDashoffset = offset;
            }, 50); 
        };

        // Function to animate the bar and circle graphs
        const initializeGraphs = () => {
            // 1. Bar Chart Animation (FIXED: Using requestAnimationFrame for reliable animation start)
            document.querySelectorAll('.bar-chart-bar').forEach(bar => {
                const percent = parseInt(bar.dataset.targetPercent);
                
                // Use requestAnimationFrame to ensure the browser registers the initial height (0) 
                // before setting the final height for a smooth CSS transition.
                requestAnimationFrame(() => {
                    bar.style.height = `${percent}%`;
                });
            });

            // 2. Circular Progress Animation
            // PT Progress: Radius 60, Target 30%
            setProgress('pt-progress', 60, 30);
            // LaMeave Progress: Radius 70, Target 95%
            setProgress('lameave-progress', 70, 95);
        };

        // 1. Initial Load & Restore Content
        document.addEventListener('DOMContentLoaded', () => {
            // Restore Content
            document.querySelectorAll('.editable-text').forEach(el => {
                const saved = localStorage.getItem(el.dataset.field);
                if (saved) el.innerHTML = saved;
            });
            // Restore Font Size
            const savedSize = localStorage.getItem('fontSizeScale');
            if (savedSize) {
                root.style.setProperty('--font-size-scale', savedSize);
                fontSizeSlider.value = savedSize;
            }

            // Initialize Graph Animations immediately on DOMContentLoaded
            // This is critical to ensure the animation starts after the DOM is painted.
            initializeGraphs();
        });

        // 2. Settings Modal Toggle
        settingsBtn.addEventListener('click', () => settingsModal.classList.remove('hidden'));
        closeModalBtn.addEventListener('click', () => settingsModal.classList.add('hidden'));

        // 3. Font Size Logic
        fontSizeSlider.addEventListener('input', (e) => {
            const val = e.target.value;
            root.style.setProperty('--font-size-scale', val);
            localStorage.setItem('fontSizeScale', val);
        });

        // 4. Edit Mode Logic
        activateEditBtn.addEventListener('click', () => {
            if (editPasswordInput.value === PASSWORD) {
                document.querySelectorAll('.editable-text').forEach(el => el.setAttribute('contenteditable', 'true'));
                saveBtn.classList.remove('hidden');
                settingsModal.classList.add('hidden');
                editPasswordInput.value = '';
                passwordMessage.textContent = '';
                // Using a custom message box instead of alert() is recommended, but keeping simple alert() for this project's scope.
                alert('편집 모드가 활성화되었습니다. 텍스트를 클릭하여 수정하세요.');
            } else {
                passwordMessage.textContent = 'Incorrect Password';
                passwordMessage.className = 'text-xs mt-2 h-4 text-red-500';
            }
        });

        // 5. Save Logic
        saveBtn.addEventListener('click', () => {
            document.querySelectorAll('.editable-text').forEach(el => {
                localStorage.setItem(el.dataset.field, el.innerHTML);
                el.setAttribute('contenteditable', 'false');
            });
            saveBtn.classList.add('hidden');
            // Using a custom message box instead of alert() is recommended, but keeping simple alert() for this project's scope.
            alert('모든 변경 사항이 저장되었습니다.');
        });
    </script>
</body>
</html>
