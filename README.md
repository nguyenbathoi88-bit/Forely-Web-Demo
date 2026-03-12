<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Forely - Đấu trí & Nhận thưởng</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #f1f5f9;
            color: #0f172a;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        .safe-area-bottom {
            padding-bottom: env(safe-area-inset-bottom);
        }

        /* Logic hiển thị Tab */
        .tab-content {
            display: none;
            animation: slideUp 0.3s ease-out;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Hiệu ứng Gacha */
        .gacha-shake {
            animation: shake 0.5s cubic-bezier(.36,.07,.19,.97) both infinite;
        }

        @keyframes shake {
            10%, 90% { transform: translate3d(-1px, 0, 0); }
            20%, 80% { transform: translate3d(2px, 0, 0); }
            30%, 50%, 70% { transform: translate3d(-4px, 0, 0); }
            40%, 60% { transform: translate3d(4px, 0, 0); }
        }

        .gradient-brand {
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
        }

        .market-card {
            transition: transform 0.2s;
        }
        .market-card:active {
            transform: scale(0.98);
        }

        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
    </style>
</head>
<body class="max-w-md mx-auto bg-white min-h-screen shadow-2xl relative overflow-x-hidden">

    <!-- PHẦN 1: KHUNG XƯƠNG & HEADER (CORE LAYOUT) -->
    <header class="sticky top-0 z-50 bg-white/80 backdrop-blur-md border-b border-slate-100 px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-2">
            <div class="w-8 h-8 gradient-brand rounded-lg flex items-center justify-center text-white font-black text-xl">F</div>
            <span class="font-extrabold text-xl tracking-tight">FORELY</span>
        </div>
        <div class="bg-indigo-50 px-3 py-1.5 rounded-full flex items-center gap-2 border border-indigo-100 transition-transform duration-200" id="fp-container">
            <span class="text-indigo-600 font-bold text-sm" id="global-fp">2,450</span>
            <span class="text-xs font-bold text-indigo-400">FP</span>
        </div>
    </header>

    <main class="pb-24 pt-4 px-4 overflow-y-auto no-scrollbar">

        <!-- PHẦN 2: SÀN ĐẤU TRÍ (MARKET FEED) -->
        <div id="tab-home" class="tab-content active space-y-6">
            <!-- AI Summary Block -->
            <div class="bg-slate-900 rounded-2xl p-5 text-white relative overflow-hidden">
                <div class="absolute -right-4 -top-4 w-24 h-24 bg-indigo-500/20 rounded-full blur-2xl"></div>
                <div class="relative z-10">
                    <p class="text-xs font-bold text-indigo-400 uppercase tracking-widest mb-1">AI Insights • Gemini 1.5</p>
                    <h2 class="text-lg font-bold leading-tight mb-2 italic">"Vàng SJC đang hạ nhiệt sau đấu thầu, nhưng VN-Index vẫn kẹt tại mốc 1250..."</h2>
                    <p class="text-[11px] text-slate-400">Dựa trên 45 tin tức mới nhất từ CafeF & VnExpress.</p>
                </div>
            </div>

            <div class="space-y-4">
                <h3 class="font-bold text-slate-800 flex items-center justify-between px-1">
                    Thị trường nóng hổi
                    <span class="text-xs text-indigo-600 font-medium">Xem tất cả</span>
                </h3>

                <!-- Market Card -->
                <div class="market-card bg-white border border-slate-200 rounded-2xl p-4 shadow-sm space-y-4">
                    <div class="flex justify-between items-start">
                        <span class="bg-amber-100 text-amber-700 text-[10px] font-bold px-2 py-0.5 rounded uppercase">Kinh tế</span>
                        <div class="flex items-center gap-1 text-rose-500 text-xs font-bold">
                            <span class="animate-pulse">⏳</span> 02:45:12
                        </div>
                    </div>
                    <h4 class="font-bold text-slate-800 leading-tight">VN-Index có vượt mốc 1.300 điểm vào cuối phiên Thứ Sáu tuần này?</h4>
                    
                    <div class="flex gap-3">
                        <button onclick="openPredictModal('VN-Index', 'CÓ', '3.2x')" class="flex-1 py-3 rounded-xl border-2 border-indigo-600 text-indigo-600 font-bold hover:bg-indigo-50 transition-colors">
                            CÓ (3.2x)
                        </button>
                        <button onclick="openPredictModal('VN-Index', 'KHÔNG', '1.4x')" class="flex-1 py-3 rounded-xl border-2 border-orange-500 text-orange-500 font-bold hover:bg-orange-50 transition-colors">
                            KHÔNG (1.4x)
                        </button>
                    </div>

                    <div class="pt-2">
                        <div class="flex justify-between text-[10px] font-bold text-slate-400 mb-1">
                            <span>PHE CÓ: 28%</span>
                            <span>PHE KHÔNG: 72%</span>
                        </div>
                        <div class="w-full h-1.5 bg-slate-100 rounded-full overflow-hidden flex">
                            <div class="h-full bg-indigo-500" style="width: 28%"></div>
                            <div class="h-full bg-orange-400" style="width: 72%"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- PHẦN 3: BRAND ZONE (MISSION SYSTEM) -->
        <div id="tab-brand" class="tab-content space-y-6">
            <div class="border-b border-slate-100 pb-4">
                <h2 class="text-2xl font-black text-slate-900">Brand Zone</h2>
                <p class="text-sm text-slate-500">Làm nhiệm vụ, nhận FP bảo chứng bởi nhãn hàng.</p>
            </div>

            <div class="space-y-4">
                <div class="bg-white border border-slate-200 rounded-2xl p-4 flex gap-4 items-center">
                    <div class="w-14 h-14 bg-blue-50 rounded-xl flex items-center justify-center shrink-0 border border-blue-100">
                        <span class="text-2xl">🥛</span>
                    </div>
                    <div class="flex-grow">
                        <h4 class="font-bold text-sm">Vinamilk: Ý tưởng bao bì</h4>
                        <p class="text-[11px] text-slate-500">Khảo sát Gen Z • 3 phút</p>
                    </div>
                    <button onclick="simulateSurvey(500)" class="bg-indigo-600 text-white px-4 py-2 rounded-xl text-xs font-bold shadow-lg shadow-indigo-200">
                        +500 FP
                    </button>
                </div>

                <div class="bg-white border border-slate-200 rounded-2xl p-4 flex gap-4 items-center">
                    <div class="w-14 h-14 bg-orange-50 rounded-xl flex items-center justify-center shrink-0 border border-orange-100">
                        <span class="text-2xl">🛍️</span>
                    </div>
                    <div class="flex-grow">
                        <h4 class="font-bold text-sm">Shopee: Review xu hướng</h4>
                        <p class="text-[11px] text-slate-500">Xem video • 1 phút</p>
                    </div>
                    <button onclick="simulateSurvey(200)" class="bg-indigo-600 text-white px-4 py-2 rounded-xl text-xs font-bold shadow-lg shadow-indigo-200">
                        +200 FP
                    </button>
                </div>
            </div>
        </div>

        <!-- PHẦN 4: GAME HÓA - GACHA & GUILDS (GAMIFICATION) -->
        <div id="tab-gacha" class="tab-content space-y-8">
            <div class="text-center space-y-2">
                <h2 class="text-2xl font-black text-slate-900">Hộp Quà May Mắn</h2>
                <p class="text-sm text-slate-500 px-10">Dùng 500 FP mở hộp quà may mắn. Cơ hội nổ Voucher Shopee!</p>
            </div>

            <div class="relative flex justify-center py-10">
                <div id="gacha-box" class="w-48 h-48 gradient-brand rounded-3xl shadow-2xl flex items-center justify-center text-6xl relative z-10 transition-transform cursor-pointer">
                    🎁
                    <div class="absolute inset-0 bg-white/20 rounded-3xl animate-pulse"></div>
                </div>
            </div>

            <button id="btn-spin" onclick="spinGacha()" class="w-full py-4 gradient-brand text-white font-black rounded-2xl shadow-xl shadow-indigo-200 text-lg active:scale-95 transition-transform">
                MỞ 1 LẦN (500 FP)
            </button>
        </div>

        <div id="tab-guild" class="tab-content space-y-6">
            <h2 class="text-2xl font-black text-slate-900">Bang Hội</h2>
            <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                <div class="p-4 flex items-center gap-4 border-b border-slate-100">
                    <span class="text-amber-500 font-black text-lg">1</span>
                    <div class="w-10 h-10 gradient-brand rounded-full flex items-center justify-center text-white font-bold">🐺</div>
                    <div class="flex-grow">
                        <h4 class="font-bold text-sm text-slate-800">Sói Già Phố Wall</h4>
                        <p class="text-[10px] text-slate-400">452 thành viên</p>
                    </div>
                    <p class="font-black text-indigo-600">852.4k</p>
                </div>
            </div>
        </div>

        <!-- PHẦN 5: VÍ CÁ NHÂN & PHÂN TÍCH (PROFILE & WALLET) -->
        <div id="tab-profile" class="tab-content space-y-6">
            <div class="flex items-center gap-4">
                <div class="w-20 h-20 rounded-3xl gradient-brand flex items-center justify-center text-4xl text-white shadow-xl shadow-indigo-200">
                    🦊
                </div>
                <div>
                    <h2 class="text-xl font-black text-slate-900">Hoàng Long <span class="text-xs bg-indigo-100 text-indigo-600 px-2 py-0.5 rounded-full ml-1 font-bold">Lv. 12</span></h2>
                    <p class="text-sm text-slate-500 font-mono">UUID: 8a2f-91b3-4c5d</p>
                </div>
            </div>

            <div class="bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
                <h3 class="font-bold text-slate-800 text-sm mb-4">Hiệu suất Đấu trí (7 ngày)</h3>
                <div class="h-40 w-full">
                    <canvas id="profileChart"></canvas>
                </div>
            </div>
            
            <div class="space-y-4">
                <h3 class="font-bold text-slate-800 text-sm">Nhật ký giao dịch</h3>
                <div class="bg-white p-4 rounded-2xl border border-slate-200 flex justify-between items-center">
                    <div class="flex gap-3 items-center">
                        <div class="w-8 h-8 bg-emerald-50 text-emerald-600 rounded-full flex items-center justify-center text-xs">💰</div>
                        <p class="text-xs font-bold">Thắng dự báo VN-Index</p>
                    </div>
                    <span class="text-emerald-500 font-black text-sm">+850 FP</span>
                </div>
            </div>
        </div>
    </main>

    <!-- MODALS & NAVIGATION SYSTEM -->
    <div id="predict-modal" class="fixed inset-0 z-[100] bg-slate-900/60 backdrop-blur-sm flex items-end justify-center hidden">
        <div class="bg-white w-full max-w-md rounded-t-3xl p-6 space-y-6">
            <div class="flex justify-between items-center">
                <h3 class="font-black text-xl" id="modal-title">Bảo vệ nhận định</h3>
                <button onclick="closeModal('predict-modal')" class="text-slate-400 text-2xl">&times;</button>
            </div>
            <input type="number" id="predict-amount" class="w-full bg-slate-100 p-4 rounded-xl font-black text-2xl text-center outline-none" value="100">
            <button onclick="confirmPrediction()" class="w-full py-4 gradient-brand text-white font-black rounded-2xl shadow-xl">XÁC NHẬN BẢO VỆ</button>
        </div>
    </div>

    <!-- Bottom Tab Bar Navigation -->
    <nav class="fixed bottom-0 left-0 right-0 max-w-md mx-auto bg-white/95 backdrop-blur-lg border-t border-slate-100 px-4 py-2 flex justify-between items-center z-[90] safe-area-bottom">
        <button onclick="switchTab('home')" id="nav-btn-home" class="flex flex-col items-center gap-1 flex-1 text-indigo-600 transition-all">
            <span class="text-xl">📊</span>
            <span class="text-[10px] font-bold uppercase tracking-tight">Đấu trí</span>
        </button>
        <button onclick="switchTab('brand')" id="nav-btn-brand" class="flex flex-col items-center gap-1 flex-1 text-slate-400 transition-all">
            <span class="text-xl">🏢</span>
            <span class="text-[10px] font-bold uppercase tracking-tight">Brands</span>
        </button>
        <button onclick="switchTab('gacha')" id="nav-btn-gacha" class="flex flex-col items-center gap-1 flex-1 text-slate-400 transition-all -translate-y-4">
            <div class="w-14 h-14 gradient-brand rounded-full flex items-center justify-center text-white shadow-xl shadow-indigo-300 border-4 border-white">
                <span class="text-2xl">🎁</span>
            </div>
        </button>
        <button onclick="switchTab('guild')" id="nav-btn-guild" class="flex flex-col items-center gap-1 flex-1 text-slate-400 transition-all">
            <span class="text-xl">🛡️</span>
            <span class="text-[10px] font-bold uppercase tracking-tight">Bang</span>
        </button>
        <button onclick="switchTab('profile')" id="nav-btn-profile" class="flex flex-col items-center gap-1 flex-1 text-slate-400 transition-all">
            <span class="text-xl">👤</span>
            <span class="text-[10px] font-bold uppercase tracking-tight">Ví</span>
        </button>
    </nav>

    <!-- LOGIC & STATE MANAGEMENT -->
    <script>
        let userFP = 2450;
        let profileChart = null;

        // Quản lý Tab Navigation
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.getElementById('tab-' + tabId).classList.add('active');
            document.querySelectorAll('nav button').forEach(btn => btn.classList.replace('text-indigo-600', 'text-slate-400'));
            document.getElementById('nav-btn-' + tabId).classList.replace('text-slate-400', 'text-indigo-600');
            if (tabId === 'profile') initChart();
        }

        // Logic Điểm FP
        function updateFP(amount) {
            userFP += amount;
            const display = document.getElementById('global-fp');
            display.innerText = userFP.toLocaleString();
            const container = document.getElementById('fp-container');
            container.classList.add('scale-110');
            setTimeout(() => container.classList.remove('scale-110'), 200);
        }

        // Logic Dự báo
        function openPredictModal(title, option, roi) {
            document.getElementById('modal-title').innerText = title;
            document.getElementById('predict-modal').classList.remove('hidden');
        }

        function confirmPrediction() {
            const amount = parseInt(document.getElementById('predict-amount').value);
            if (amount > userFP) {
                showSimpleMessage('Không đủ điểm!');
                return;
            }
            updateFP(-amount);
            closeModal('predict-modal');
            showSimpleMessage('Đã đặt cược!');
        }

        // Logic Gacha
        function spinGacha() {
            if (userFP < 500) {
                showSimpleMessage('Cần 500 FP!');
                return;
            }
            updateFP(-500);
            const box = document.getElementById('gacha-box');
            box.classList.add('gacha-shake');
            setTimeout(() => {
                box.classList.remove('gacha-shake');
                showSimpleMessage('Chúc mừng! Bạn trúng quà (Demo)');
            }, 2000);
        }

        // Khởi tạo biểu đồ Profile
        function initChart() {
            if (profileChart) return;
            const ctx = document.getElementById('profileChart').getContext('2d');
            profileChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['T2', 'T3', 'T4', 'T5', 'T6', 'T7', 'CN'],
                    datasets: [{
                        data: [1200, 1900, 1500, 2400, 1800, 3200, 2450],
                        borderColor: '#4f46e5',
                        backgroundColor: 'rgba(79, 70, 229, 0.1)',
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: { y: { display: false }, x: { grid: { display: false } } }
                }
            });
        }

        function closeModal(id) { document.getElementById(id).classList.add('hidden'); }

        function showSimpleMessage(msg) {
            const toast = document.createElement('div');
            toast.className = 'fixed top-20 left-1/2 -translate-x-1/2 bg-slate-900 text-white px-6 py-3 rounded-2xl text-xs font-bold z-[200] shadow-2xl';
            toast.innerText = msg;
            document.body.appendChild(toast);
            setTimeout(() => toast.remove(), 2000);
        }

        function simulateSurvey(p) {
            showSimpleMessage('Đang thực hiện khảo sát...');
            setTimeout(() => updateFP(p), 1500);
        }
    </script>
</body>
</html>
