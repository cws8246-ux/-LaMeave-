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
        
        /* --- Graph Styles for Animation --- */
        .bar-chart-bar {
            transition: height 1.5s ease-out;
            height: 0; 
        }

        /* --- Touch Reaction Styles (NEW) --- */
        .reaction-animation {
            transition: transform 0.1s ease-out, background-color 0.3s, box-shadow 0.3s;
        }
        /* 클릭/터치 시 적용될 스타일 */
        .reacted {
            transform: scale(0.95);
            /* CTA 버튼의 경우, 눌렸을 때 색상을 약간 어둡게 유지 */
            background-color: #d14008 !important; 
            box-shadow: 0 0 5px rgba(255, 94, 30, 0.5);
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
                <!-- RESERVE BUTTON: reaction-animation 클래스 추가 및 ID 부여 -->
                <a id="navReserveBtn" 
                   href="https://booking.naver.com/booking/13/bizes/374029/items/3508163?area=pll&lang=ko&startDate=2025-12-08&theme=place" target="_blank" 
                   class="reaction-animation bg-[#ff5e1e] text-white text-xs font-bold px-6 py-3 rounded-none hover:bg-[#d14008] transition tracking-widest">
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

    <!-- Hero Section -->
    <section id="philosophy" class="relative h-screen flex items-center justify-center overflow-hidden bg-[#0f0f0f]">
        <div class="relative z-10 text-center px-6 max-w-5xl mx-auto animate-fade-in pt-20"> 
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

    <!-- Philosophy Grid -->
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

    <!-- The Difference (Comparison Data - NUMBERS EMPHASIZED) -->
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
                            <div class="absolute -top-16 left-1/2 -translate-x-1/2 text-white text-xs font-medium bg-gray-900 px-2 py-1 rounded-full opacity-0 group-hover:opacity-100 transition whitespace-nowrap">일반 PT (50분)</div>
                            <div class="absolute -top-8 left-1/2 -translate-x-1/2 text-gray-500 text-sm font-bold opacity-0 group-hover:opacity-100 transition">45%</div>
                            <div class="bar-chart-bar bg-gradient-to-t from-gray-800 to-gray-600 w-full mx-auto rounded-t-sm" data-target-percent="45"></div>
                            <p class="text-center text-gray-500 text-xs mt-4 tracking-widest uppercase editable-text" data-field="label_pt" contenteditable="false">1:1 PT</p>
                        </div>
                        
                        <!-- LaMeave Bar (Emphasized for EMS + Therapy) -->
                        <div class="w-24 group relative">
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

                <!-- Graph 2: Number Focus (Simplified from Circle Graph) -->
                <div class="glass-panel p-10 rounded-sm hover:border-[#ff5e1e]/30 transition duration-500">
                    <h3 class="text-xl text-white font-light mb-16 border-l-2 border-[#ff5e1e] pl-4 editable-text" data-field="graph2_title" contenteditable="false">
                        체질 개선 완성도 및 지속성
                    </h3>
                    
                    <div class="flex justify-around items-start text-center">
                        <!-- Data Point: Normal PT -->
                        <div class="w-1/2">
                            <div class="text-6xl font-serif text-gray-500 font-bold mb-2 editable-text" data-field="pt_percent" contenteditable="false">30%</div>
                            <p class="text-gray-500 text-sm tracking-widest uppercase">Normal PT</p>
                            <p class="text-xs text-gray-700 mt-2 editable-text" data-field="pt_label_desc" contenteditable="false">단기 효과</p>
                        </div>
                        
                        <!-- Data Point: LaMeave (Emphasized) -->
                        <div class="w-1/2">
                            <div class="text-8xl font-serif text-[#ff5e1e] font-bold mb-2 editable-text" data-field="lameave_percent" contenteditable="false">95%</div>
                            <p class="text-[#ff5e1e] text-sm tracking-widest uppercase font-bold">LaMeave</p>
                            <p class="text-xs text-gray-400 mt-2 editable-text" data-field="meave_label_desc" contenteditable="false">근본적 체질 개선</p>
                        </div>
                    </div>

                    <p class="text-xs text-gray-500 mt-10 text-right italic editable-text" data-field="graph2_note" contenteditable="false">*8가지 패턴 관리 및 항상성 회복 기준</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Program Flow (Vertical Luxury Timeline) -->
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

    <!-- Exclusive Features -->
    <section class="py-32 bg-[#121212]">
        <div class="max-w-7xl mx-auto px-6">
            <h2 class="font-serif text-3xl md:text-4xl text-white text-center mb-20 editable-text" data-field="feat_title" contenteditable="false">Exclusive Amenities</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <!-- Item 1: EMS Training (Lightning Bolt SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat1_title" contenteditable="false">EMS Training</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat1_desc" contenteditable="false">20분으로 6시간 효과를 내는<br>초밀도 근육 자극</p>
                </div>
                
                <!-- Item 2: White Tanning (Shine/Star SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M5 3s.34.42.5.5c.24.23.44.43.7.67M22 12h-4m-7-7V2.5M10 20.5V22M20 18l-2-2M18 6l-2 2M6 18l2-2M6 6l2 2" />
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 17a5 5 0 100-10 5 5 0 000 10z" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat2_title" contenteditable="false">White Tanning</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat2_desc" contenteditable="false">피부 톤 개선과 탄력을 위한<br>프리미엄 뷰티 솔루션</p>
                </div>
                
                <!-- Item 3: Phantom Recovery (Comfort/Check SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                             <path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m5.617 1.258a11.94 11.94 0 01-5.714 4.04M2.572 15.176a11.941 11.941 0 005.617 1.258m-5.617-1.258l-.05.05m0-.05l.05-.05M2 12h1m18 0h1m-1 0a9 9 0 10-18 0z" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat3_title" contenteditable="false">Phantom Recovery</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat3_desc" contenteditable="false">바디프랜드 팬텀으로<br>완벽한 전신 피로 해소</p>
                </div>
                
                <!-- Item 4: Data Tracking (Bar Chart SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m-4-8h8m-8 4h8m-8-8h8m-8 12h8m-8 4h8" />
                            <rect x="3" y="10" width="18" height="11" rx="2" ry="2" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat4_title" contenteditable="false">Data Tracking</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat4_desc" contenteditable="false">매 회차 정밀 분석을 통한<br>개인 맞춤형 로드맵</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-black py-24 border-t border-gray-900">
        <div class="max-w-5xl mx-auto px-6 text-center">
            <h2 class="font-serif text-4xl text-white mb-8 editable-text" data-field="footer_cta" contenteditable="false">Begin Your Journey</h2>
            <p class="text-gray-400 mb-12 editable-text" data-field="footer_sub" contenteditable="false">진정한 변화를 위한 첫 걸음, 라 미브와 함께하세요.</p>
            
            <!-- FOOTER BUTTON: reaction-animation 클래스 추가 및 ID 부여 -->
            <a id="footerReserveBtn" 
               href="https://booking.naver.com/booking/13/bizes/374029/items/3508163?area=pll&lang=ko&startDate=2025-12-08&theme=place" target="_blank" 
               class="reaction-animation inline-block border border-[#ff5e1e] text-[#ff5e1e] px-10 py-4 hover:bg-[#ff5e1e] hover:text-white transition duration-300 tracking-widest uppercase text-sm mb-16">
                Book Consultation
            </a>

            <div class="border-t border-gray-900 pt-12">
                <p class="text-gray-600 text-sm mb-6">인천 서구 중봉대로586번길 15 청연 프라자 906호</p>
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
        const navReserveBtn = document.getElementById('navReserveBtn');
        const footerReserveBtn = document.getElementById('footerReserveBtn');
        const root = document.documentElement;
        
        const PASSWORD = '8246';

        // --- Core Functions ---

        // Function to animate the bar chart (Graph 1 only)
        const initializeGraphs = () => {
            document.querySelectorAll('.bar-chart-bar').forEach(bar => {
                const percent = parseInt(bar.dataset.targetPercent);
                requestAnimationFrame(() => {
                    bar.style.height = `${percent}%`;
                });
            });
        };

        // Function to apply the press reaction (NEW)
        const applyReaction = (element) => {
            element.classList.add('reacted');
            // 100ms 후 복원
            setTimeout(() => {
                element.classList.remove('reacted');
            }, 100); 
        };

        // Function to set up mobile/desktop reaction listeners (NEW)
        const setupButtonReaction = (buttonElement) => {
            if (!buttonElement) return;

            // 1. Touchstart (모바일 터치 시작 시 즉시 반응)
            buttonElement.addEventListener('touchstart', (event) => {
                // event.preventDefault(); // 링크 이동을 위해 기본 동작 방지 안 함
                applyReaction(buttonElement);
            }, { passive: true }); // passive: true로 스크롤 성능 향상

            // 2. Click (데스크톱 마우스 클릭)
            // Note: 모바일에서는 touchstart -> touchend -> click 순으로 발생하지만,
            // 터치 반응은 이미 touchstart에서 처리했으므로, click은 데스크톱용으로만 기능적으로 사용됩니다.
            buttonElement.addEventListener('click', (event) => {
                // 터치 기기에서는 이미 반응했으므로, 여기서는 딜레이가 있는 click에 대해서만 반응을 추가합니다.
                applyReaction(buttonElement);
            });

            // 3. 마우스 다운/업 (데스크톱에서의 미세한 반응 개선)
            buttonElement.addEventListener('mousedown', () => {
                 buttonElement.classList.add('reacted');
            });
            buttonElement.addEventListener('mouseup', () => {
                 buttonElement.classList.remove('reacted');
            });
            buttonElement.addEventListener('mouseleave', () => {
                 buttonElement.classList.remove('reacted');
            });
        };


        // --- Event Listeners and Initializers ---

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

            // Initialize Graph Animations
            initializeGraphs();

            // Initialize Button Reactions (NEW)
            setupButtonReaction(navReserveBtn);
            setupButtonReaction(footerReserveBtn);
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
<!DOCTYPE html>
<html lang="ko" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LaMeave | High-End Wellness Lounge</title>
    <!-- Tailwind CSS CDN 로드 -->
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
        
        /* --- Progress Bar Styles for Animation (New) --- */
        .progress-bar-fill {
            transition: width 1.5s ease-out;
            width: 0%; /* Initial state for animation */
        }
        
        /* --- Touch Reaction Styles (모바일/클릭 반응) --- */
        .reaction-animation {
            transition: transform 0.1s ease-out, background-color 0.3s, box-shadow 0.3s;
        }
        .reacted {
            transform: scale(0.95);
            background-color: #d14008 !important; 
            box-shadow: 0 0 5px rgba(255, 94, 30, 0.5);
        }

        /* --- Animations: Fade In from Bottom --- */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
            animation: fadeIn 1s ease-out forwards;
            opacity: 0; /* Ensures elements start hidden */
        }

        /* Scrollbar styles remain the same */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg-dark); }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--accent-hermes); }

        /* Editable Text Styles */
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
    </style>
</head>
<body class="relative">

    <!-- Navbar: Floating & Transparent -->
    <!-- Nav bar is intentionally not animated to be immediately visible -->
    <nav class="fixed w-full z-50 transition-all duration-300 bg-black/80 backdrop-blur-md border-b border-white/5">
        <div class="max-w-7xl mx-auto px-6 h-20 flex justify-between items-center">
            <!-- Logo -->
            <a href="#" class="text-2xl md:text-3xl font-luxury tracking-widest text-white">
                LA<span class="text-[#ff5e1e]">MEAVE</span>
            </a>

            <!-- Desktop Menu -->
            <div class="hidden md:flex space-x-12 text-sm font-medium tracking-widest text-gray-400">
                <a href="#philosophy" class="hover:text-[#ff5e1e] transition-colors">OUR VISION</a>
                <a href="#difference" class="hover:text-[#ff5e1e] transition-colors">THE DIFFERENCE</a>
                <a href="#program" class="hover:text-[#ff5e1e] transition-colors">PROGRAM FLOW</a>
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
                <!-- RESERVE BUTTON: 모바일 반응성 적용 -->
                <a id="navReserveBtn" 
                   href="https://booking.naver.com/booking/13/bizes/374029/items/3508163?area=pll&lang=ko&startDate=2025-12-08&theme=place" target="_blank" 
                   class="reaction-animation bg-[#ff5e1e] text-white text-xs font-bold px-6 py-3 rounded-none hover:bg-[#d14008] transition tracking-widest">
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

    <!-- Hero Section -->
    <section id="philosophy" class="relative h-screen flex items-center justify-center overflow-hidden bg-[#0f0f0f]">
        <div class="relative z-10 text-center px-6 max-w-5xl mx-auto animate-fade-in pt-20"> 
            <p class="text-[#ff5e1e] font-bold tracking-[0.3em] text-sm md:text-base mb-6 uppercase editable-text" data-field="hero_subtitle" contenteditable="false">
                THE ART OF SELF-ELEVATION
            </p>
            <h1 class="font-serif text-5xl md:text-7xl lg:text-8xl text-white mb-8 leading-tight editable-text" data-field="hero_title" contenteditable="false">
                나를 가장 높은 곳으로,<br>최상의 <span class="text-[#dfa67b]">EXPERIENCE</span>, 라 미브
            </h1>
            <div class="w-20 h-[1px] bg-[#dfa67b] mx-auto mb-8"></div>
            <p class="text-gray-200 text-lg md:text-2xl font-light leading-relaxed mb-12 editable-text" data-field="hero_desc" contenteditable="false">
                단순한 관리를 넘어, 몸과 마음의 조화(Harmony)를 통해 본질적인 아름다움을 회복하는 <span class="text-white font-normal">PRESTIGE WELLNESS LOUNGE</span>.
            </p>
        </div>
        
        <!-- Scroll Indicator -->
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 animate-bounce">
            <span class="text-gray-500 text-xs tracking-widest">SCROLL DOWN</span>
        </div>
    </section>

    <!-- Philosophy Grid (애니메이션 추가) -->
    <section class="py-24 px-6 bg-[#0f0f0f]">
        <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-0 divide-y md:divide-y-0 md:divide-x divide-gray-800 border-t border-b border-gray-800">
            <!-- La -->
            <div class="p-12 text-center group hover:bg-[#151515] transition duration-500 animate-fade-in" style="animation-delay: 0.2s;">
                <span class="font-serif text-6xl text-gray-800 group-hover:text-[#dfa67b] transition duration-500 block mb-4 editable-text" data-field="la_title" contenteditable="false">La</span>
                <h3 class="text-[#ff5e1e] text-xs font-bold tracking-[0.2em] mb-4 uppercase editable-text" data-field="la_sub" contenteditable="false">THE VALUE</h3>
                <p class="text-gray-300 font-light leading-relaxed editable-text" data-field="la_desc" contenteditable="false">시간의 흔적을 지우는<br>완벽한 <span class="text-white">VALUE INVESTMENT</span></p>
            </div>
            <!-- Me -->
            <div class="p-12 text-center group hover:bg-[#151515] transition duration-500 animate-fade-in" style="animation-delay: 0.4s;">
                <span class="font-serif text-6xl text-gray-800 group-hover:text-[#dfa67b] transition duration-500 block mb-4 editable-text" data-field="me_title" contenteditable="false">Me</span>
                <h3 class="text-[#ff5e1e] text-xs font-bold tracking-[0.2em] mb-4 uppercase editable-text" data-field="me_sub" contenteditable="false">MYSELF</h3>
                <p class="text-gray-300 font-light leading-relaxed editable-text" data-field="me_desc" contenteditable="false">모든 감각을 깨우는<br>철저히 <span class="text-white">PRIVATE EXPERIENCE</span></p>
            </div>
            <!-- Ave -->
            <div class="p-12 text-center group hover:bg-[#151515] transition duration-500 animate-fade-in" style="animation-delay: 0.6s;">
                <span class="font-serif text-6xl text-gray-800 group-hover:text-[#dfa67b] transition duration-500 block mb-4 editable-text" data-field="ave_title" contenteditable="false">Ave</span>
                <h3 class="text-[#ff5e1e] text-xs font-bold tracking-[0.2em] mb-4 uppercase editable-text" data-field="ave_sub" contenteditable="false">ELEVATION</h3>
                <p class="text-gray-300 font-light leading-relaxed editable-text" data-field="ave_desc" contenteditable="false">한계를 초월하여 나를<br>새롭게 정의하는 <span class="text-white">MOMENT</span></p>
            </div>
        </div>
    </section>

    <!-- The Difference (Comparison Data - 직선형 그래프 통일) -->
    <section id="difference" class="py-32 bg-[#121212] relative">
        <div class="max-w-7xl mx-auto px-6">
            <div class="text-center mb-24 animate-fade-in"> <!-- 타이틀 애니메이션 추가 -->
                <h2 class="font-serif text-4xl md:text-5xl text-white mb-6 editable-text" data-field="diff_main_title" contenteditable="false">THE <span class="text-[#ff5e1e]">OVERWHELMING</span> DIFFERENCE</h2>
                <p class="text-gray-300 max-w-2xl mx-auto editable-text" data-field="diff_main_desc" contenteditable="false">
                    평범한 노력으로는 닿을 수 없는 '엘리베이션'. 라 미브는 **PREMIUM EMS THERAPY**와 **정밀 진단 시스템**으로 차원이 다른 효율을 약속합니다.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-start">
                
                <!-- Graph 1: 운동 효율 비교 (애니메이션 추가) -->
                <div class="glass-panel p-8 rounded-sm hover:border-[#ff5e1e]/30 transition duration-500 animate-fade-in" style="animation-delay: 0.2s;">
                    <h3 class="text-xl text-white font-light mb-8 border-l-2 border-[#ff5e1e] pl-4 editable-text" data-field="graph1_title" contenteditable="false">
                        MAXIMIZED TIME DENSITY <span class="text-[#dfa67b] text-sm font-luxury ml-2">(운동 효율)</span>
                    </h3>
                    
                    <div class="space-y-6">
                        <!-- 일반 PT -->
                        <div class="space-y-2">
                            <div class="flex justify-between items-center text-sm">
                                <span class="text-gray-400 editable-text" data-field="label_pt" contenteditable="false">Normal 1:1 PT (50 min)</span>
                                <span class="text-gray-500 font-bold">45%</span>
                            </div>
                            <div class="w-full h-2 bg-gray-800 rounded-full overflow-hidden">
                                <div class="progress-bar-fill h-full bg-gray-600 rounded-full" data-target-percent="45"></div>
                            </div>
                        </div>

                        <!-- LaMeave (EMS & Therapy) -->
                        <div class="space-y-2">
                            <div class="flex justify-between items-center text-sm">
                                <span class="text-[#ff5e1e] font-bold editable-text" data-field="label_meave" contenteditable="false">LaMeave EMS & Therapy (70 min)</span>
                                <span class="text-[#ff5e1e] font-bold">85%</span>
                            </div>
                            <div class="w-full h-2 bg-gray-800 rounded-full overflow-hidden shadow-lg shadow-[#ff5e1e]/10">
                                <div class="progress-bar-fill h-full bg-gradient-to-r from-[#8B3A15] to-[#ff5e1e] rounded-full" data-target-percent="85"></div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 설명 텍스트 -->
                    <div class="mt-8 p-4 bg-[#1a1a1a] border-l-4 border-[#ff5e1e] shadow-lg">
                        <p class="text-sm font-bold text-[#ff5e1e] mb-1">⚡ 20 MIN EMS = 6 HOURS EFFECT</p>
                        <p class="text-xs text-gray-400">EMS 트레이닝으로 시간 밀도를 극대화하고, 순환 테라피가 결합되어 차원이 다른 결과를 창출합니다.</p>
                    </div>
                    
                    <p class="text-xs text-gray-500 mt-6 text-right italic editable-text" data-field="graph1_note" contenteditable="false">*Based on 20-min EMS training and combined therapy synergy</p>
                </div>

                <!-- Graph 2: 근본 개선 비교 (애니메이션 추가) -->
                <div class="glass-panel p-8 rounded-sm hover:border-[#ff5e1e]/30 transition duration-500 animate-fade-in" style="animation-delay: 0.4s;">
                    <h3 class="text-xl text-white font-light mb-8 border-l-2 border-[#ff5e1e] pl-4 editable-text" data-field="graph2_title" contenteditable="false">
                        SUSTAINABLE BEAUTY DESIGN <span class="text-[#dfa67b] text-sm font-luxury ml-2">(근본 개선)</span>
                    </h3>
                    
                    <div class="space-y-6">
                         <!-- 단기 효과 -->
                        <div class="space-y-2">
                            <div class="flex justify-between items-center text-sm">
                                <span class="text-gray-400 editable-text" data-field="pt_label_desc" contenteditable="false">General Care (Temporary Effect)</span>
                                <span class="text-gray-500 font-bold">30%</span>
                            </div>
                            <div class="w-full h-2 bg-gray-800 rounded-full overflow-hidden">
                                <div class="progress-bar-fill h-full bg-gray-600 rounded-full" data-target-percent="30"></div>
                            </div>
                        </div>

                        <!-- LaMeave 근본 개선 -->
                        <div class="space-y-2">
                            <div class="flex justify-between items-center text-sm">
                                <span class="text-[#ff5e1e] font-bold editable-text" data-field="meave_label_desc" contenteditable="false">LaMeave (Fundamental Improvement)</span>
                                <span class="text-[#ff5e1e] font-bold">95%</span>
                            </div>
                            <div class="w-full h-2 bg-gray-800 rounded-full overflow-hidden shadow-lg shadow-[#ff5e1e]/10">
                                <div class="progress-bar-fill h-full bg-gradient-to-r from-[#8B3A15] to-[#ff5e1e] rounded-full" data-target-percent="95"></div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 설명 텍스트 -->
                    <div class="mt-8 p-4 bg-[#1a1a1a] border-l-4 border-[#ff5e1e] shadow-lg">
                        <p class="text-sm font-bold text-[#ff5e1e] mb-1">✓ 8 PATTERN MANAGEMENT</p>
                        <p class="text-xs text-gray-400">일시적인 감량이 아닌, 고객의 체질과 체형 패턴을 근본적으로 개선하여 유지 가능한 아름다움을 설계합니다.</p>
                    </div>

                    <p class="text-xs text-gray-500 mt-6 text-right italic editable-text" data-field="graph2_note" contenteditable="false">*Based on 8-pattern management and homeostasis recovery</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Program Flow (Vertical Luxury Timeline) (애니메이션 추가) -->
    <section id="program" class="py-32 bg-[#0f0f0f]">
        <div class="max-w-4xl mx-auto px-6">
            <div class="text-center mb-20 animate-fade-in"> <!-- 타이틀 애니메이션 추가 -->
                <span class="text-[#dfa67b] text-sm tracking-[0.3em] uppercase block mb-3 editable-text" data-field="flow_super" contenteditable="false">THE ULTIMATE 70-MINUTE PROTOCOL</span>
                <h2 class="font-serif text-4xl text-white editable-text" data-field="flow_title" contenteditable="false">MASTER THERAPIST의 <span class="text-[#ff5e1e]">PRESTIGE CARE</span> FLOW</h2>
            </div>

            <div class="space-y-4">
                <!-- Step 1 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default animate-fade-in" style="animation-delay: 0.2s;">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">01</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step1_title" contenteditable="false">PRIVATE WELCOME RITUAL</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step1_desc" contenteditable="false">오직 고객님만을 위한 공간에서 최상의 컨디션 준비</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 2 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default animate-fade-in" style="animation-delay: 0.4s;">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">02</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step2_title" contenteditable="false">PRECISE INBODY & PATTERN DIAGNOSIS</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step2_desc" contenteditable="false">8가지 체형/체질 데이터 분석</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 3 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default animate-fade-in" style="animation-delay: 0.6s;">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">03</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step3_title" contenteditable="false">SIGNATURE ELEVATION THERAPY</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step3_desc" contenteditable="false">막힌 순환을 열고 독소를 배출하는 근본 테라피</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 4 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default animate-fade-in" style="animation-delay: 0.8s;">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">04</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step4_title" contenteditable="false">FRENCH LIFTING</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step4_desc" contenteditable="false">바디 탄력 및 라인 컨투어링</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
                <!-- Step 5 -->
                <div class="group flex items-center p-6 border-b border-gray-800 hover:bg-[#151515] hover:border-[#ff5e1e] transition duration-300 cursor-default animate-fade-in" style="animation-delay: 1.0s;">
                    <span class="text-3xl font-serif text-gray-700 group-hover:text-[#ff5e1e] mr-8 transition duration-300">05</span>
                    <div class="flex-1">
                        <h4 class="text-xl text-white font-light mb-1 editable-text" data-field="step5_title" contenteditable="false">DOCTOR'S THERAPY</h4>
                        <p class="text-sm text-gray-400 font-light editable-text" data-field="step5_desc" contenteditable="false">근육 이완 및 최종 회복 마무리</p>
                    </div>
                    <span class="text-2xl text-gray-700 group-hover:text-[#ff5e1e] transition">→</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Exclusive Features (애니메이션 추가) -->
    <section class="py-32 bg-[#121212]">
        <div class="max-w-7xl mx-auto px-6">
            <h2 class="font-serif text-3xl md:text-4xl text-white text-center mb-20 editable-text animate-fade-in" data-field="feat_title" contenteditable="false" style="animation-delay: 0.1s;">EXCLUSIVE FEATURES at LaMeave</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <!-- Item 1: EMS Training (Lightning Bolt SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500 animate-fade-in" style="animation-delay: 0.3s;">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat1_title" contenteditable="false">THE POWER OF 20 MINUTES</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat1_desc" contenteditable="false">미세 전류를 통해 몸의 깊은 곳까지 깨우는 초밀도 근육 강화 시스템</p>
                </div>
                
                <!-- Item 2: White Tanning (Shine/Star SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500 animate-fade-in" style="animation-delay: 0.5s;">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M5 3s.34.42.5.5c.24.23.44.43.7.67M22 12h-4m-7-7V2.5M10 20.5V22M20 18l-2-2M18 6l-2 2M6 18l2-2M6 6l2 2" />
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 17a5 5 0 100-10 5 5 0 000 10z" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat2_title" contenteditable="false">TONE UP & ELASTICITY RENEWAL</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat2_desc" contenteditable="false">피부 세포 활성화를 통한 화사한 톤과 탱탱한 탄력 회복</p>
                </div>
                
                <!-- Item 3: Phantom Recovery (Comfort/Check SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500 animate-fade-in" style="animation-delay: 0.7s;">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                             <path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m5.617 1.258a11.94 11.94 0 01-5.714 4.04M2.572 15.176a11.941 11.941 0 005.617 1.258m-5.617-1.258l-.05.05m0-.05l.05-.05M2 12h1m18 0h1m-1 0a9 9 0 10-18 0z" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat3_title" contenteditable="false">PHANTOM RECOVERY</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat3_desc" contenteditable="false">바디프랜드 팬텀으로<br>완벽한 전신 피로 해소</p>
                </div>
                
                <!-- Item 4: Data Tracking (Bar Chart SVG) -->
                <div class="text-center p-8 border border-gray-800 hover:border-[#dfa67b] transition duration-500 animate-fade-in" style="animation-delay: 0.9s;">
                    <div class="text-4xl text-[#dfa67b] mb-6 inline-block">
                        <svg class="w-8 h-8 mx-auto" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m-4-8h8m-8 4h8m-8-8h8m-8 12h8m-8 4h8" />
                            <rect x="3" y="10" width="18" height="11" rx="2" ry="2" />
                        </svg>
                    </div>
                    <h4 class="text-lg text-white font-bold mb-3 editable-text" data-field="feat4_title" contenteditable="false">DATA TRACKING</h4>
                    <p class="text-sm text-gray-400 leading-relaxed editable-text" data-field="feat4_desc" contenteditable="false">매 회차 정밀 분석을 통한<br>개인 맞춤형 로드맵</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-black py-24 border-t border-gray-900">
        <div class="max-w-5xl mx-auto px-6 text-center animate-fade-in" style="animation-delay: 0.1s;"> <!-- 애니메이션 추가 -->
            <h2 class="font-serif text-4xl text-white mb-8 editable-text" data-field="footer_cta" contenteditable="false">BEGIN YOUR <span class="text-[#ff5e1e]">NEW JOURNEY</span> at LaMeave</h2>
            <p class="text-gray-400 mb-12 editable-text" data-field="footer_sub" contenteditable="false">'나'를 가장 빛나게 만들 궁극의 변화. 지금, 프레스티지 컨설팅을 예약하세요.</p>
            
            <!-- FOOTER BUTTON: 모바일 반응성 적용 -->
            <a id="footerReserveBtn" 
               href="https://booking.naver.com/booking/13/bizes/374029/items/3508163?area=pll&lang=ko&startDate=2025-12-08&theme=place" target="_blank" 
               class="reaction-animation inline-block border border-[#ff5e1e] text-[#ff5e1e] px-10 py-4 hover:bg-[#ff5e1e] hover:text-white transition duration-300 tracking-widest uppercase text-sm mb-16">
                BOOK CONSULTATION
            </a>

            <div class="border-t border-gray-900 pt-12">
                <p class="text-gray-600 text-sm mb-6">인천 서구 중봉대로586번길 15 청연 프라자 906호</p>
                <p class="text-gray-700 text-xs tracking-widest">© 2025 LAMEAVE. ALL RIGHTS RESERVED.</p>
            </div>
        </div>
    </footer>

    <!-- Logic Script (터치 반응 로직 포함) -->
    <script>
        const settingsBtn = document.getElementById('settings-btn');
        const settingsModal = document.getElementById('settings-modal');
        const closeModalBtn = document.getElementById('close-modal');
        const fontSizeSlider = document.getElementById('font-size-slider');
        const editPasswordInput = document.getElementById('edit-password');
        const activateEditBtn = document.getElementById('activate-edit-btn');
        const passwordMessage = document.getElementById('password-message');
        const saveBtn = document.getElementById('save-btn');
        const navReserveBtn = document.getElementById('navReserveBtn');
        const footerReserveBtn = document.getElementById('footerReserveBtn');
        const root = document.documentElement;
        
        const PASSWORD = '8246'; // 관리자 편집 모드 비밀번호

        // --- Core Functions ---

        // Progress Bar 애니메이션 (직선형 막대 그래프 애니메이션)
        const initializeGraphs = () => {
            document.querySelectorAll('.progress-bar-fill').forEach(bar => {
                const percent = bar.dataset.targetPercent;
                // 애니메이션 적용을 위해 0ms 지연 후 width 설정
                setTimeout(() => {
                    bar.style.width = `${percent}%`;
                }, 10); // 작은 지연으로 CSS transition이 적용되게 함
            });
        };

        // 버튼 눌림 반응을 적용하는 함수 (모바일/클릭 공통)
        const applyReaction = (element) => {
            element.classList.add('reacted');
            setTimeout(() => {
                element.classList.remove('reacted');
            }, 100); 
        };

        // 버튼에 모바일 터치 및 마우스 반응 리스너를 설정하는 함수
        const setupButtonReaction = (buttonElement) => {
            if (!buttonElement) return;

            // 1. touchstart (모바일 터치 시작 시 즉시 반응)
            buttonElement.addEventListener('touchstart', (event) => {
                applyReaction(buttonElement);
            }, { passive: true });

            // 2. click (데스크톱 마우스 클릭 시 반응)
            buttonElement.addEventListener('click', (event) => {
                applyReaction(buttonElement);
            });

            // 3. mousedown/mouseup (데스크톱 환경에서 더 즉각적인 반응을 위해)
            buttonElement.addEventListener('mousedown', () => {
                 buttonElement.classList.add('reacted');
            });
            buttonElement.addEventListener('mouseup', () => {
                 buttonElement.classList.remove('reacted');
            });
            buttonElement.addEventListener('mouseleave', () => {
                 buttonElement.classList.remove('reacted');
            });
        };


        // --- Event Listeners and Initializers ---

        document.addEventListener('DOMContentLoaded', () => {
            // 저장된 콘텐츠 복원
            document.querySelectorAll('.editable-text').forEach(el => {
                const saved = localStorage.getItem(el.dataset.field);
                if (saved) el.innerHTML = saved;
            });
            // 저장된 폰트 크기 복원
            const savedSize = localStorage.getItem('fontSizeScale');
            if (savedSize) {
                root.style.setProperty('--font-size-scale', savedSize);
                fontSizeSlider.value = savedSize;
            }

            // 그래프 애니메이션 초기화 (새로운 직선형 그래프에 맞춰 업데이트)
            initializeGraphs();

            // 버튼 터치 반응 초기화
            setupButtonReaction(navReserveBtn);
            setupButtonReaction(footerReserveBtn);
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
            alert('모든 변경 사항이 저장되었습니다.');
        });
    </script>
</body>
</html>
