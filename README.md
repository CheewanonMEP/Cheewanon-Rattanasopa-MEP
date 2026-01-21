<html lang="th" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>คณิตศาสตร์การเงิน ป.5</title>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
        body {
            box-sizing: border-box;
            font-family: 'Prompt', sans-serif;
        }
        
        .coin-icon {
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .result-card {
            animation: slideIn 0.5s ease-out;
        }
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes rocketLeft {
            0% {
                bottom: -20%;
            }
            50% {
                bottom: 40%;
            }
            100% {
                bottom: 110%;
            }
        }
        
        @keyframes rocketRight {
            0% {
                bottom: -20%;
            }
            50% {
                bottom: 35%;
            }
            100% {
                bottom: 110%;
            }
        }
    </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full overflow-auto">
  <div id="app" class="w-full h-full"></div>
  <script>
        const defaultConfig = {
            background_color: '#87CEEB',
            surface_color: '#ffffff',
            text_color: '#1e3a8a',
            primary_action_color: '#3b82f6',
            secondary_action_color: '#2563eb',
            font_family: 'Prompt',
            font_size: 16,
            app_title: '💰 คณิตศาสตร์การเงิน',
            subtitle: 'เรียนรู้การออมและการใช้จ่ายอย่างฉลาด',
            creator: 'ผู้สร้าง: เด็กชาย ชีวานนท์ รัตนโสภา',
            saving_title: '🐷 คำนวณการออมเงิน',
            spending_title: '🛒 คำนวณการใช้จ่าย',
            calculate_button: 'คำนวณ'
        };

        let config = { ...defaultConfig };

        function createApp() {
            const app = document.getElementById('app');
            
            const fontStack = `${config.font_family}, Arial, sans-serif`;
            const baseSize = config.font_size;
            
            app.style.backgroundColor = config.background_color;
            app.style.fontFamily = fontStack;
            app.style.minHeight = '100%';
            
            app.innerHTML = `
                <div class="w-full px-6 py-8" style="position: relative;">
                    <!-- Sun -->
                    <div style="position: absolute; top: 20px; right: 40px;">
                        <svg width="100" height="100" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                            <!-- Sun rays -->
                            <line x1="50" y1="10" x2="50" y2="20" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="75" y1="15" x2="70" y2="23" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="90" y1="35" x2="82" y2="40" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="90" y1="60" x2="82" y2="55" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="75" y1="80" x2="70" y2="72" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="50" y1="85" x2="50" y2="75" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="25" y1="80" x2="30" y2="72" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="10" y1="60" x2="18" y2="55" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="10" y1="35" x2="18" y2="40" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <line x1="25" y1="15" x2="30" y2="23" stroke="#FDB813" stroke-width="3" stroke-linecap="round"/>
                            <!-- Sun circle -->
                            <circle cx="50" cy="47" r="22" fill="#FFD700"/>
                            <circle cx="50" cy="47" r="18" fill="#FDB813"/>
                        </svg>
                    </div>
                    
                    <!-- Clouds -->
                    <div style="position: absolute; top: 60px; left: 80px; opacity: 0.9;">
                        <svg width="120" height="60" viewBox="0 0 120 60" xmlns="http://www.w3.org/2000/svg">
                            <ellipse cx="30" cy="35" rx="25" ry="20" fill="#ffffff"/>
                            <ellipse cx="55" cy="30" rx="30" ry="25" fill="#ffffff"/>
                            <ellipse cx="85" cy="35" rx="28" ry="22" fill="#ffffff"/>
                            <ellipse cx="60" cy="40" rx="35" ry="20" fill="#ffffff"/>
                        </svg>
                    </div>
                    
                    <div style="position: absolute; top: 150px; right: 150px; opacity: 0.85;">
                        <svg width="100" height="50" viewBox="0 0 100 50" xmlns="http://www.w3.org/2000/svg">
                            <ellipse cx="25" cy="30" rx="20" ry="16" fill="#ffffff"/>
                            <ellipse cx="45" cy="25" rx="25" ry="20" fill="#ffffff"/>
                            <ellipse cx="70" cy="30" rx="23" ry="18" fill="#ffffff"/>
                            <ellipse cx="50" cy="35" rx="30" ry="16" fill="#ffffff"/>
                        </svg>
                    </div>
                    
                    <div style="position: absolute; bottom: 180px; left: 120px; opacity: 0.8;">
                        <svg width="90" height="45" viewBox="0 0 90 45" xmlns="http://www.w3.org/2000/svg">
                            <ellipse cx="20" cy="28" rx="18" ry="14" fill="#ffffff"/>
                            <ellipse cx="40" cy="23" rx="22" ry="18" fill="#ffffff"/>
                            <ellipse cx="62" cy="28" rx="20" ry="15" fill="#ffffff"/>
                            <ellipse cx="45" cy="32" rx="25" ry="14" fill="#ffffff"/>
                        </svg>
                    </div>
                    
                    <!-- Left Rocket -->
                    <div style="position: absolute; left: 10%; animation: rocketLeft 8s ease-in-out infinite;">
                        <svg width="80" height="120" viewBox="0 0 80 120" xmlns="http://www.w3.org/2000/svg">
                            <defs>
                                <linearGradient id="rocketBody" x1="0%" y1="0%" x2="100%" y2="0%">
                                    <stop offset="0%" style="stop-color:#E74C3C;stop-opacity:1" />
                                    <stop offset="50%" style="stop-color:#C0392B;stop-opacity:1" />
                                    <stop offset="100%" style="stop-color:#E74C3C;stop-opacity:1" />
                                </linearGradient>
                                <linearGradient id="flame" x1="0%" y1="0%" x2="0%" y2="100%">
                                    <stop offset="0%" style="stop-color:#FFA500;stop-opacity:1" />
                                    <stop offset="50%" style="stop-color:#FF6347;stop-opacity:1" />
                                    <stop offset="100%" style="stop-color:#FFD700;stop-opacity:0.8" />
                                </linearGradient>
                            </defs>
                            
                            <!-- Flames -->
                            <ellipse cx="40" cy="95" rx="8" ry="15" fill="url(#flame)" opacity="0.9">
                                <animate attributeName="ry" values="15;20;15" dur="0.5s" repeatCount="indefinite"/>
                            </ellipse>
                            <ellipse cx="40" cy="100" rx="6" ry="12" fill="#FFD700" opacity="0.8">
                                <animate attributeName="ry" values="12;16;12" dur="0.4s" repeatCount="indefinite"/>
                            </ellipse>
                            
                            <!-- Rocket body -->
                            <rect x="25" y="30" width="30" height="60" fill="url(#rocketBody)" rx="3"/>
                            
                            <!-- Nose cone -->
                            <path d="M 25 30 L 40 5 L 55 30 Z" fill="#E74C3C"/>
                            <path d="M 30 30 L 40 10 L 50 30 Z" fill="#C0392B"/>
                            
                            <!-- Window -->
                            <circle cx="40" cy="20" r="6" fill="#87CEEB" opacity="0.8"/>
                            <circle cx="40" cy="20" r="4" fill="#5DADE2"/>
                            
                            <!-- Body windows -->
                            <circle cx="40" cy="45" r="4" fill="#34495E" opacity="0.7"/>
                            <circle cx="40" cy="60" r="4" fill="#34495E" opacity="0.7"/>
                            
                            <!-- Fins -->
                            <path d="M 25 70 L 15 90 L 25 85 Z" fill="#3498DB"/>
                            <path d="M 55 70 L 65 90 L 55 85 Z" fill="#3498DB"/>
                            
                            <!-- Details -->
                            <rect x="25" y="50" width="30" height="2" fill="#34495E" opacity="0.5"/>
                            <rect x="25" y="75" width="30" height="2" fill="#34495E" opacity="0.5"/>
                        </svg>
                    </div>
                    
                    <!-- Right Rocket -->
                    <div style="position: absolute; right: 10%; animation: rocketRight 8s ease-in-out infinite;">
                        <svg width="80" height="120" viewBox="0 0 80 120" xmlns="http://www.w3.org/2000/svg">
                            <!-- Flames -->
                            <ellipse cx="40" cy="95" rx="8" ry="15" fill="url(#flame)" opacity="0.9">
                                <animate attributeName="ry" values="15;20;15" dur="0.5s" repeatCount="indefinite"/>
                            </ellipse>
                            <ellipse cx="40" cy="100" rx="6" ry="12" fill="#FFD700" opacity="0.8">
                                <animate attributeName="ry" values="12;16;12" dur="0.4s" repeatCount="indefinite"/>
                            </ellipse>
                            
                            <!-- Rocket body -->
                            <rect x="25" y="30" width="30" height="60" fill="url(#rocketBody)" rx="3"/>
                            
                            <!-- Nose cone -->
                            <path d="M 25 30 L 40 5 L 55 30 Z" fill="#E74C3C"/>
                            <path d="M 30 30 L 40 10 L 50 30 Z" fill="#C0392B"/>
                            
                            <!-- Window -->
                            <circle cx="40" cy="20" r="6" fill="#87CEEB" opacity="0.8"/>
                            <circle cx="40" cy="20" r="4" fill="#5DADE2"/>
                            
                            <!-- Body windows -->
                            <circle cx="40" cy="45" r="4" fill="#34495E" opacity="0.7"/>
                            <circle cx="40" cy="60" r="4" fill="#34495E" opacity="0.7"/>
                            
                            <!-- Fins -->
                            <path d="M 25 70 L 15 90 L 25 85 Z" fill="#3498DB"/>
                            <path d="M 55 70 L 65 90 L 55 85 Z" fill="#3498DB"/>
                            
                            <!-- Details -->
                            <rect x="25" y="50" width="30" height="2" fill="#34495E" opacity="0.5"/>
                            <rect x="25" y="75" width="30" height="2" fill="#34495E" opacity="0.5"/>
                        </svg>
                    </div>
                    
                    <!-- Header -->
                    <div class="text-center mb-8" style="position: relative; z-index: 10;">
                        <h1 id="main-title" class="font-bold mb-2" style="font-size: ${baseSize * 2}px; color: ${config.text_color}; font-family: ${fontStack};">
                            ${config.app_title}
                        </h1>
                        <p id="subtitle" class="font-medium" style="font-size: ${baseSize * 1.1}px; color: ${config.text_color}; font-family: ${fontStack};">
                            ${config.subtitle}
                        </p>
                    </div>

                    <!-- Main Content Grid -->
                    <div class="max-w-5xl mx-auto grid md:grid-cols-2 gap-6" style="position: relative; z-index: 10;">
                        <!-- Saving Calculator -->
                        <div class="rounded-3xl shadow-lg p-6" style="background-color: ${config.surface_color};">
                            <div class="text-center mb-4">
                                <div class="coin-icon inline-block" style="font-size: ${baseSize * 3}px;">🐷</div>
                                <h2 id="saving-title" class="font-bold mt-2" style="font-size: ${baseSize * 1.4}px; color: ${config.text_color}; font-family: ${fontStack};">
                                    ${config.saving_title}
                                </h2>
                            </div>
                            
                            <div class="space-y-4">
                                <div>
                                    <label class="block font-medium mb-2" style="font-size: ${baseSize}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        เงินออมเริ่มต้น (บาท)
                                    </label>
                                    <input type="number" id="initial-saving" value="500" min="0" 
                                        class="w-full px-4 py-3 rounded-xl border-2 focus:outline-none focus:ring-2"
                                        style="font-size: ${baseSize}px; color: ${config.text_color}; border-color: ${config.primary_action_color}; font-family: ${fontStack};">
                                </div>
                                
                                <div>
                                    <label class="block font-medium mb-2" style="font-size: ${baseSize}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        ออมเพิ่มต่อสัปดาห์ (บาท)
                                    </label>
                                    <input type="number" id="weekly-saving" value="50" min="0"
                                        class="w-full px-4 py-3 rounded-xl border-2 focus:outline-none focus:ring-2"
                                        style="font-size: ${baseSize}px; color: ${config.text_color}; border-color: ${config.primary_action_color}; font-family: ${fontStack};">
                                </div>
                                
                                <div>
                                    <label class="block font-medium mb-2" style="font-size: ${baseSize}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        จำนวนสัปดาห์
                                    </label>
                                    <input type="number" id="weeks" value="10" min="1"
                                        class="w-full px-4 py-3 rounded-xl border-2 focus:outline-none focus:ring-2"
                                        style="font-size: ${baseSize}px; color: ${config.text_color}; border-color: ${config.primary_action_color}; font-family: ${fontStack};">
                                </div>
                                
                                <button id="calc-saving" class="w-full py-3 rounded-xl font-bold shadow-md hover:shadow-lg transition-all transform hover:scale-105"
                                    style="background-color: ${config.primary_action_color}; color: white; font-size: ${baseSize * 1.1}px; font-family: ${fontStack};">
                                    ${config.calculate_button}
                                </button>
                                
                                <div id="saving-result" class="hidden result-card rounded-xl p-4 text-center" style="background-color: ${config.background_color};">
                                    <p class="font-medium mb-2" style="font-size: ${baseSize * 0.9}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        เงินออมทั้งหมด
                                    </p>
                                    <p id="saving-amount" class="font-bold" style="font-size: ${baseSize * 2}px; color: ${config.primary_action_color}; font-family: ${fontStack};">
                                        0 บาท
                                    </p>
                                </div>
                            </div>
                        </div>

                        <!-- Spending Calculator -->
                        <div class="rounded-3xl shadow-lg p-6" style="background-color: ${config.surface_color};">
                            <div class="text-center mb-4">
                                <div class="coin-icon inline-block" style="font-size: ${baseSize * 3}px;">🛒</div>
                                <h2 id="spending-title" class="font-bold mt-2" style="font-size: ${baseSize * 1.4}px; color: ${config.text_color}; font-family: ${fontStack};">
                                    ${config.spending_title}
                                </h2>
                            </div>
                            
                            <div class="space-y-4">
                                <div>
                                    <label class="block font-medium mb-2" style="font-size: ${baseSize}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        เงินที่มี (บาท)
                                    </label>
                                    <input type="number" id="total-money" value="1000" min="0"
                                        class="w-full px-4 py-3 rounded-xl border-2 focus:outline-none focus:ring-2"
                                        style="font-size: ${baseSize}px; color: ${config.text_color}; border-color: ${config.secondary_action_color}; font-family: ${fontStack};">
                                </div>
                                
                                <div>
                                    <label class="block font-medium mb-2" style="font-size: ${baseSize}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        ราคาของที่ต้องการซื้อ (บาท)
                                    </label>
                                    <input type="number" id="item-price" value="250" min="0"
                                        class="w-full px-4 py-3 rounded-xl border-2 focus:outline-none focus:ring-2"
                                        style="font-size: ${baseSize}px; color: ${config.text_color}; border-color: ${config.secondary_action_color}; font-family: ${fontStack};">
                                </div>
                                
                                <div>
                                    <label class="block font-medium mb-2" style="font-size: ${baseSize}px; color: ${config.text_color}; font-family: ${fontStack};">
                                        จำนวนชิ้น
                                    </label>
                                    <input type="number" id="quantity" value="2" min="1"
                                        class="w-full px-4 py-3 rounded-xl border-2 focus:outline-none focus:ring-2"
                                        style="font-size: ${baseSize}px; color: ${config.text_color}; border-color: ${config.secondary_action_color}; font-family: ${fontStack};">
                                </div>
                                
                                <button id="calc-spending" class="w-full py-3 rounded-xl font-bold shadow-md hover:shadow-lg transition-all transform hover:scale-105"
                                    style="background-color: ${config.secondary_action_color}; color: white; font-size: ${baseSize * 1.1}px; font-family: ${fontStack};">
                                    ${config.calculate_button}
                                </button>
                                
                                <div id="spending-result" class="hidden result-card rounded-xl p-4" style="background-color: ${config.background_color};">
                                    <div class="text-center mb-2">
                                        <p class="font-medium" style="font-size: ${baseSize * 0.9}px; color: ${config.text_color}; font-family: ${fontStack};">
                                            ราคารวม
                                        </p>
                                        <p id="total-price" class="font-bold" style="font-size: ${baseSize * 1.5}px; color: ${config.secondary_action_color}; font-family: ${fontStack};">
                                            0 บาท
                                        </p>
                                    </div>
                                    <div id="can-buy" class="text-center p-3 rounded-lg font-bold" style="font-size: ${baseSize}px; font-family: ${fontStack};">
                                    </div>
                                    <div id="remaining" class="text-center mt-2" style="font-size: ${baseSize * 0.85}px; color: ${config.text_color}; font-family: ${fontStack};">
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            `;

            // Add event listeners
            document.getElementById('calc-saving').addEventListener('click', calculateSaving);
            document.getElementById('calc-spending').addEventListener('click', calculateSpending);
        }

        function calculateSaving() {
            const initial = parseFloat(document.getElementById('initial-saving').value) || 0;
            const weekly = parseFloat(document.getElementById('weekly-saving').value) || 0;
            const weeks = parseFloat(document.getElementById('weeks').value) || 0;
            
            const total = initial + (weekly * weeks);
            
            const resultDiv = document.getElementById('saving-result');
            const amountText = document.getElementById('saving-amount');
            
            amountText.textContent = total.toLocaleString('th-TH') + ' บาท';
            resultDiv.classList.remove('hidden');
        }

        function calculateSpending() {
            const totalMoney = parseFloat(document.getElementById('total-money').value) || 0;
            const itemPrice = parseFloat(document.getElementById('item-price').value) || 0;
            const quantity = parseFloat(document.getElementById('quantity').value) || 0;
            
            const totalPrice = itemPrice * quantity;
            
            const resultDiv = document.getElementById('spending-result');
            const totalPriceText = document.getElementById('total-price');
            const canBuyDiv = document.getElementById('can-buy');
            const remainingDiv = document.getElementById('remaining');
            
            totalPriceText.textContent = totalPrice.toLocaleString('th-TH') + ' บาท';
            
            if (totalMoney >= totalPrice) {
                const remaining = totalMoney - totalPrice;
                canBuyDiv.style.backgroundColor = config.secondary_action_color;
                canBuyDiv.style.color = 'white';
                canBuyDiv.textContent = '✓ ซื้อได้!';
                remainingDiv.textContent = 'เงินเหลือ: ' + remaining.toLocaleString('th-TH') + ' บาท';
            } else {
                const shortage = totalPrice - totalMoney;
                canBuyDiv.style.backgroundColor = '#ef4444';
                canBuyDiv.style.color = 'white';
                canBuyDiv.textContent = '✗ เงินไม่พอ';
                remainingDiv.textContent = 'ต้องมีเงินเพิ่มอีก: ' + shortage.toLocaleString('th-TH') + ' บาท';
            }
            
            resultDiv.classList.remove('hidden');
        }

        async function onConfigChange(newConfig) {
            config = { ...newConfig };
            
            const fontStack = `${config.font_family}, Arial, sans-serif`;
            const baseSize = config.font_size;
            
            // Update colors
            const app = document.getElementById('app');
            if (app) {
                app.style.backgroundColor = config.background_color;
                app.style.fontFamily = fontStack;
            }
            
            // Update text content
            const mainTitle = document.getElementById('main-title');
            if (mainTitle) {
                mainTitle.textContent = config.app_title;
                mainTitle.style.fontSize = `${baseSize * 2}px`;
                mainTitle.style.color = config.text_color;
                mainTitle.style.fontFamily = fontStack;
            }
            
            const subtitle = document.getElementById('subtitle');
            if (subtitle) {
                subtitle.textContent = config.subtitle;
                subtitle.style.fontSize = `${baseSize * 1.1}px`;
                subtitle.style.color = config.text_color;
                subtitle.style.fontFamily = fontStack;
            }
            
            const creator = document.getElementById('creator');
            if (creator) {
                creator.textContent = config.creator;
                creator.style.fontSize = `${baseSize * 0.9}px`;
                creator.style.color = config.text_color;
                creator.style.fontFamily = fontStack;
            }
            
            const savingTitle = document.getElementById('saving-title');
            if (savingTitle) {
                savingTitle.textContent = config.saving_title;
                savingTitle.style.fontSize = `${baseSize * 1.4}px`;
                savingTitle.style.color = config.text_color;
                savingTitle.style.fontFamily = fontStack;
            }
            
            const spendingTitle = document.getElementById('spending-title');
            if (spendingTitle) {
                spendingTitle.textContent = config.spending_title;
                spendingTitle.style.fontSize = `${baseSize * 1.4}px`;
                spendingTitle.style.color = config.text_color;
                spendingTitle.style.fontFamily = fontStack;
            }
            
            // Update buttons
            const calcSavingBtn = document.getElementById('calc-saving');
            if (calcSavingBtn) {
                calcSavingBtn.textContent = config.calculate_button;
                calcSavingBtn.style.backgroundColor = config.primary_action_color;
                calcSavingBtn.style.fontSize = `${baseSize * 1.1}px`;
                calcSavingBtn.style.fontFamily = fontStack;
            }
            
            const calcSpendingBtn = document.getElementById('calc-spending');
            if (calcSpendingBtn) {
                calcSpendingBtn.textContent = config.calculate_button;
                calcSpendingBtn.style.backgroundColor = config.secondary_action_color;
                calcSpendingBtn.style.fontSize = `${baseSize * 1.1}px`;
                calcSpendingBtn.style.fontFamily = fontStack;
            }
        }

        if (window.elementSdk) {
            window.elementSdk.init({
                defaultConfig: defaultConfig,
                onConfigChange: onConfigChange,
                mapToCapabilities: (config) => ({
                    recolorables: [
                        {
                            get: () => config.background_color || defaultConfig.background_color,
                            set: (value) => {
                                config.background_color = value;
                                window.elementSdk.setConfig({ background_color: value });
                            }
                        },
                        {
                            get: () => config.surface_color || defaultConfig.surface_color,
                            set: (value) => {
                                config.surface_color = value;
                                window.elementSdk.setConfig({ surface_color: value });
                            }
                        },
                        {
                            get: () => config.text_color || defaultConfig.text_color,
                            set: (value) => {
                                config.text_color = value;
                                window.elementSdk.setConfig({ text_color: value });
                            }
                        },
                        {
                            get: () => config.primary_action_color || defaultConfig.primary_action_color,
                            set: (value) => {
                                config.primary_action_color = value;
                                window.elementSdk.setConfig({ primary_action_color: value });
                            }
                        },
                        {
                            get: () => config.secondary_action_color || defaultConfig.secondary_action_color,
                            set: (value) => {
                                config.secondary_action_color = value;
                                window.elementSdk.setConfig({ secondary_action_color: value });
                            }
                        }
                    ],
                    borderables: [],
                    fontEditable: {
                        get: () => config.font_family || defaultConfig.font_family,
                        set: (value) => {
                            config.font_family = value;
                            window.elementSdk.setConfig({ font_family: value });
                        }
                    },
                    fontSizeable: {
                        get: () => config.font_size || defaultConfig.font_size,
                        set: (value) => {
                            config.font_size = value;
                            window.elementSdk.setConfig({ font_size: value });
                        }
                    }
                }),
                mapToEditPanelValues: (config) => new Map([
                    ['app_title', config.app_title || defaultConfig.app_title],
                    ['subtitle', config.subtitle || defaultConfig.subtitle],
                    ['creator', config.creator || defaultConfig.creator],
                    ['saving_title', config.saving_title || defaultConfig.saving_title],
                    ['spending_title', config.spending_title || defaultConfig.spending_title],
                    ['calculate_button', config.calculate_button || defaultConfig.calculate_button]
                ])
            });
        }

        createApp();
    </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9c1342f530ffa1b0',t:'MTc2ODk2MTI4My4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
