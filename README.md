# web-ng-c-p-tadaaa
<!DOCTYPE html>
<html lang="vi" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hải Sản TaDaaa | Tuyệt Tác Đại Dương - Minh Vũ</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Three.js cho hiệu ứng 3D & Hạt -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <!-- Vanilla-Tilt.js cho hiệu ứng nghiêng Card 3D -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.8.0/vanilla-tilt.min.js"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,600;0,700;1,600&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <style>
        :root {
            --gold: #d4af37;
            --cyan-glow: #00f2fe;
        }
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #020813;
            color: #f8fafc;
            overflow-x: hidden;
        }
        .font-luxury {
            font-family: 'Cormorant Garamond', serif;
        }
        /* Canvas 3D Background */
        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            pointer-events: none;
        }
        /* Kính mờ cao cấp */
        .glass {
            background: rgba(6, 20, 46, 0.55);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(212, 175, 55, 0.2);
        }
        .glass-card {
            background: linear-gradient(145deg, rgba(10, 25, 55, 0.7) 0%, rgba(4, 12, 30, 0.85) 100%);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
            transform-style: preserve-3d;
        }
        .glass-card:hover {
            border-color: rgba(212, 175, 55, 0.5);
            box-shadow: 0 25px 50px rgba(0, 242, 254, 0.15);
        }
        /* Hiệu ứng chữ Vàng Kim */
        .text-gold-gradient {
            background: linear-gradient(to right, #bf953f, #fcf6ba, #b38728, #fbf5b7, #aa771c);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .btn-gold {
            background: linear-gradient(45deg, #b38728, #fcf6ba, #aa771c);
            background-size: 200% auto;
            color: #020813;
            transition: 0.5s;
        }
        .btn-gold:hover {
            background-position: right center;
            box-shadow: 0 0 25px rgba(212, 175, 55, 0.6);
            transform: translateY(-2px);
        }
        /* Nổi lên trong không gian 3D của thẻ */
        .tilt-content {
            transform: translateZ(40px);
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #020813; }
        ::-webkit-scrollbar-thumb { background: #b38728; border-radius: 4px; }
    </style>
</head>
<body class="selection:bg-amber-500 selection:text-black">

    <!-- 3D WebGL Background -->
    <canvas id="bg-canvas"></canvas>

    <!-- HEADER / NAVBAR -->
    <header class="fixed w-full top-0 z-40 glass transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <a href="#" class="flex items-center gap-3 group">
                <div class="w-11 h-11 rounded-full bg-gradient-to-tr from-amber-600 to-yellow-200 flex items-center justify-center shadow-[0_0_20px_rgba(212,175,55,0.5)] group-hover:rotate-12 transition">
                    <i class="fa-solid fa-crown text-slate-950 text-xl"></i>
                </div>
                <div>
                    <span class="font-luxury text-2xl sm:text-3xl font-bold tracking-wider text-gold-gradient block leading-none">Hải Sản TaDaaa</span>
                    <span class="text-[10px] tracking-[0.25em] text-cyan-400 uppercase block">Luxury Ocean Dining</span>
                </div>
            </a>

            <nav class="hidden md:flex space-x-8 text-sm font-medium tracking-wide">
                <a href="#home" class="text-amber-300 hover:text-white transition">TRANG CHỦ</a>
                <a href="#about" class="text-slate-300 hover:text-amber-300 transition">ĐẲNG CẤP TADAAA</a>
                <a href="#menu" class="text-slate-300 hover:text-amber-300 transition">THỰC ĐƠN THƯỢNG HẠNG</a>
                <a href="#contact" class="text-slate-300 hover:text-amber-300 transition">LIÊN HỆ</a>
            </nav>

            <div class="flex items-center gap-4">
                <a href="tel:0372360368" class="hidden lg:flex items-center gap-2 border border-amber-500/40 bg-amber-500/10 px-4 py-2 rounded-full text-xs hover:bg-amber-500/20 transition">
                    <i class="fa-solid fa-phone-volume text-amber-400 animate-pulse"></i>
                    <span>Hotline: <strong class="text-amber-300">0372.360.368</strong> (Minh Vũ)</span>
                </a>

                <button onclick="toggleCart()" class="relative p-3 rounded-full glass hover:border-amber-400 transition group">
                    <i class="fa-solid fa-bag-shopping text-amber-300 text-lg group-hover:scale-110 transition"></i>
                    <span id="cart-count" class="absolute -top-1 -right-1 w-5 h-5 rounded-full bg-red-600 text-white text-xs font-bold flex items-center justify-center shadow-lg">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- HERO SECTION -->
    <section id="home" class="relative min-h-screen flex items-center justify-center pt-20 px-4">
        <div class="max-w-7xl mx-auto grid lg:grid-cols-12 gap-12 items-center z-10">
            <div class="lg:col-span-7 space-y-6 text-center lg:text-left">
                <div class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full border border-cyan-500/30 bg-cyan-500/10 text-cyan-300 text-xs tracking-widest uppercase">
                    <span class="w-2 h-2 rounded-full bg-cyan-400 animate-ping"></span>
                    Tinh Hoa Hải Sản Tươi Sống Bậc Nhất
                </div>
                <h1 class="font-luxury text-5xl sm:text-7xl font-bold leading-tight">
                    Đánh Thức Vị Giác Từ <br>
                    <span class="text-gold-gradient italic">Đáy Đại Dương 3D</span>
                </h1>
                <p class="text-slate-300 text-base sm:text-lg max-w-2xl mx-auto lg:mx-0 font-light leading-relaxed">
                    Chào mừng đến với <strong class="text-amber-300 font-semibold">Hải Sản TaDaaa</strong>. Nơi hội tụ những tuyệt tác hải sản nhập khẩu và đánh bắt tự nhiên, được tuyển chọn trực tiếp bởi <strong class="text-white">Founder Minh Vũ</strong>. Giao hàng tận bàn trong 60 phút.
                </p>
                <div class="flex flex-wrap gap-4 justify-center lg:justify-start pt-4">
                    <a href="#menu" class="btn-gold px-8 py-4 rounded-full font-bold text-sm tracking-wider uppercase flex items-center gap-3 shadow-xl">
                        <span>Khám Phá Thực Đơn</span>
                        <i class="fa-solid fa-arrow-right"></i>
                    </a>
                    <a href="tel:0372360368" class="px-8 py-4 rounded-full glass hover:bg-white/10 font-semibold text-sm tracking-wider uppercase flex items-center gap-3 transition">
                        <i class="fa-solid fa-headset text-amber-400 text-lg"></i>
                        <span>Gọi Minh Vũ: 0372.360.368</span>
                    </a>
                </div>
                <!-- Chỉ số uy tín -->
                <div class="grid grid-cols-3 gap-4 pt-8 border-t border-white/10 max-w-lg mx-auto lg:mx-0">
                    <div>
                        <div class="font-luxury text-3xl font-bold text-amber-400">100%</div>
                        <div class="text-xs text-slate-400">Bơi sống tại hồ</div>
                    </div>
                    <div>
                        <div class="font-luxury text-3xl font-bold text-cyan-400">1 Đổi 1</div>
                        <div class="text-xs text-slate-400">Bao ăn, bao chắc thịt</div>
                    </div>
                    <div>
                        <div class="font-luxury text-3xl font-bold text-amber-400">VIP 5*</div>
                        <div class="text-xs text-slate-400">Đầu bếp chế biến</div>
                    </div>
                </div>
            </div>

            <!-- 3D Hero Showcase Card -->
            <div class="lg:col-span-5 flex justify-center">
                <div data-tilt data-tilt-max="15" data-tilt-speed="400" data-tilt-glare="true" data-tilt-max-glare="0.3" class="glass-card rounded-3xl p-6 relative w-full max-w-md cursor-pointer">
                    <div class="absolute -top-4 -right-4 bg-gradient-to-r from-red-600 to-amber-500 text-white text-xs font-bold px-4 py-2 rounded-full shadow-lg tilt-content">
                        BEST SELLER 2026
                    </div>
                    <img src="https://images.unsplash.com/photo-1559742811-822873691df8?auto=format&fit=crop&w=900&q=85" alt="Tôm Hùm Alaska" class="w-full h-72 object-cover rounded-2xl shadow-2xl mb-6 tilt-content">
                    <div class="space-y-3 tilt-content">
                        <div class="flex justify-between items-center">
                            <span class="text-xs text-cyan-400 uppercase tracking-widest">Nhập khẩu Canada</span>
                            <div class="flex text-amber-400 text-xs">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                        </div>
                        <h3 class="font-luxury text-3xl font-bold text-white">Hoàng Đế Alaska & King Crab</h3>
                        <p class="text-xs text-slate-300">Tặng kèm sốt Hoàng Kim hoặc hấp bia sả giữ trọn vị ngọt tinh khiết từ đại dương.</p>
                        <div class="pt-3 flex items-center justify-between border-t border-white/10">
                            <div>
                                <span class="text-xs text-slate-400 block">Giá ưu đãi hôm nay</span>
                                <span class="text-xl font-bold text-amber-400">1.290.000đ <small class="text-xs text-slate-400 font-normal">/kg</small></span>
                            </div>
                            <button onclick="addToCart(1)" class="btn-gold px-5 py-2.5 rounded-xl font-bold text-xs uppercase">
                                + Đặt Ngay
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ĐẲNG CẤP TADAAA SECTION -->
    <section id="about" class="py-20 px-4 relative z-10">
        <div class="max-w-7xl mx-auto">
            <div class="grid md:grid-cols-3 gap-8">
                <div data-tilt class="glass-card p-8 rounded-3xl relative overflow-hidden">
                    <div class="w-14 h-14 rounded-2xl bg-cyan-500/10 border border-cyan-400/30 flex items-center justify-center text-cyan-400 text-2xl mb-6">
                        <i class="fa-solid fa-water"></i>
                    </div>
                    <h3 class="font-luxury text-2xl font-bold text-amber-300 mb-3">Hệ Thống Bể Ngầm Lọc Oxy Chuẩn Quốc Tế</h3>
                    <p class="text-slate-300 text-sm leading-relaxed">Hải sản tại TaDaaa luôn bơi sống trong môi trường nước biển tự nhiên với nhiệt độ tiêu chuẩn từ 2°C - 18°C tùy chủng loại.</p>
                </div>
                <div data-tilt class="glass-card p-8 rounded-3xl relative overflow-hidden">
                    <div class="w-14 h-14 rounded-2xl bg-amber-500/10 border border-amber-400/30 flex items-center justify-center text-amber-400 text-2xl mb-6">
                        <i class="fa-solid fa-utensils"></i>
                    </div>
                    <h3 class="font-luxury text-2xl font-bold text-amber-300 mb-3">Đầu Bếp Thượng Hạng Chế Biến</h3>
                    <p class="text-slate-300 text-sm leading-relaxed">Hơn 15 loại sốt độc quyền: Sốt Phô Mai Trứng Muối, Sốt Ớt Singapore, Cháy Tỏi Hoàng Kim... sẵn sàng phục vụ thực khách sành ăn.</p>
                </div>
                <div data-tilt class="glass-card p-8 rounded-3xl relative overflow-hidden">
                    <div class="w-14 h-14 rounded-2xl bg-emerald-500/10 border border-emerald-400/30 flex items-center justify-center text-emerald-400 text-2xl mb-6">
                        <i class="fa-solid fa-shield-halved"></i>
                    </div>
                    <h3 class="font-luxury text-2xl font-bold text-amber-300 mb-3">Bảo Chứng Bởi Minh Vũ</h3>
                    <p class="text-slate-300 text-sm leading-relaxed">Cam kết cân đúng lượng, bao óp 1 đổi 1 tận nơi. Chỉ cần gọi <strong class="text-white">0372.360.368</strong>, mọi yêu cầu khắt khe nhất đều được đáp ứng.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- MENU & ORDERING SECTION -->
    <section id="menu" class="py-20 px-4 relative z-10">
        <div class="max-w-7xl mx-auto">
            <div class="text-center max-w-3xl mx-auto mb-12 space-y-4">
                <span class="text-cyan-400 text-xs uppercase tracking-[0.3em] font-semibold">Tuyệt Tác Ẩm Thực</span>
                <h2 class="font-luxury text-4xl sm:text-6xl font-bold text-gold-gradient">Thực Đơn Hải Sản TaDaaa</h2>
                <p class="text-slate-400 text-sm">Di chuột vào từng món ăn để cảm nhận hiệu ứng không gian 3D. Chọn món và đặt hàng trực tiếp chỉ với 1 cú chạm.</p>
            </div>

            <!-- Bộ lọc danh mục -->
            <div class="flex flex-wrap justify-center gap-3 mb-12" id="category-filters">
                <button onclick="filterMenu('all')" class="filter-btn active px-6 py-2.5 rounded-full text-xs font-bold uppercase tracking-wider btn-gold">Tất Cả Tuyệt Phẩm</button>
                <button onclick="filterMenu('nhap-khau')" class="filter-btn px-6 py-2.5 rounded-full text-xs font-bold uppercase tracking-wider glass hover:border-amber-400 transition">Hải Sản Nhập Khẩu</button>
                <button onclick="filterMenu('tuoi-song')" class="filter-btn px-6 py-2.5 rounded-full text-xs font-bold uppercase tracking-wider glass hover:border-amber-400 transition">Tươi Sống Trong Nước</button>
                <button onclick="filterMenu('combo')" class="filter-btn px-6 py-2.5 rounded-full text-xs font-bold uppercase tracking-wider glass hover:border-amber-400 transition">Combo Tiệc Hoàng Gia</button>
            </div>

            <!-- Danh sách món ăn (Render bằng JS) -->
            <div id="menu-grid" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Các thẻ 3D sẽ được tạo tự động ở đây -->
            </div>
        </div>
    </section>

    <!-- CONTACT & VIP BOOKING SECTION -->
    <section id="contact" class="py-20 px-4 relative z-10">
        <div class="max-w-5xl mx-auto glass-card rounded-3xl p-8 sm:p-12 border border-amber-500/30 relative overflow-hidden">
            <div class="grid md:grid-cols-2 gap-10 items-center">
                <div class="space-y-6">
                    <span class="px-3 py-1 rounded-full bg-amber-500/20 text-amber-300 text-xs uppercase tracking-widest">Đặt Tiệc & Giao Hàng Hỏa Tốc</span>
                    <h2 class="font-luxury text-4xl font-bold text-white">Liên Hệ Trực Tiếp <br><span class="text-gold-gradient">Founder Minh Vũ</span></h2>
                    <p class="text-slate-300 text-sm leading-relaxed">
                        Bạn cần tư vấn chọn hải sản làm quà biếu đẳng cấp, đặt tiệc gia đình hay giao nóng tận nhà? Liên hệ ngay để được phục vụ chuẩn VIP.
                    </p>
                    <div class="space-y-4 pt-2">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 rounded-xl bg-amber-500/20 border border-amber-400 flex items-center justify-center text-amber-300 text-xl">
                                <i class="fa-solid fa-phone-volume"></i>
                            </div>
                            <div>
                                <div class="text-xs text-slate-400">Hotline / Zalo 24/7</div>
                                <a href="tel:0372360368" class="text-2xl font-bold text-amber-400 hover:underline">0372.360.368 (Minh Vũ)</a>
                            </div>
                        </div>
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 rounded-xl bg-cyan-500/20 border border-cyan-400 flex items-center justify-center text-cyan-300 text-xl">
                                <i class="fa-solid fa-truck-fast"></i>
                            </div>
                            <div>
                                <div class="text-xs text-slate-400">Dịch vụ Giao Hàng</div>
                                <div class="text-base font-semibold text-white">Giao tươi sống hoặc chế biến nóng tận nơi</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Form Đặt Bàn / Tư Vấn Nhanh -->
                <form onsubmit="submitQuickVip(event)" class="glass p-6 rounded-2xl space-y-4">
                    <h3 class="font-luxury text-2xl font-bold text-amber-300 mb-2">Yêu Cầu Minh Vũ Gọi Lại</h3>
                    <div>
                        <label class="text-xs text-slate-300 block mb-1">Tên của Quý khách *</label>
                        <input type="text" id="vip-name" required placeholder="Nhập họ tên..." class="w-full px-4 py-3 rounded-xl bg-slate-900/80 border border-white/10 text-sm focus:outline-none focus:border-amber-400">
                    </div>
                    <div>
                        <label class="text-xs text-slate-300 block mb-1">Số điện thoại *</label>
                        <input type="tel" id="vip-phone" required placeholder="Nhập số điện thoại..." class="w-full px-4 py-3 rounded-xl bg-slate-900/80 border border-white/10 text-sm focus:outline-none focus:border-amber-400">
                    </div>
                    <div>
                        <label class="text-xs text-slate-300 block mb-1">Yêu cầu đặc biệt (Món ăn, giờ giao...)</label>
                        <textarea id="vip-note" rows="3" placeholder="VD: Cần 2kg Cua Hoàng Đế hấp giao lúc 19h..." class="w-full px-4 py-3 rounded-xl bg-slate-900/80 border border-white/10 text-sm focus:outline-none focus:border-amber-400"></textarea>
                    </div>
                    <button type="submit" class="w-full btn-gold py-3.5 rounded-xl font-bold text-sm uppercase tracking-wider">
                        Gửi Yêu Cầu Cho Minh Vũ
                    </button>
                </form>
            </div>
        </div>
    </section>

    <!-- FOOTER -->
    <footer class="border-t border-white/10 py-10 px-4 text-center text-xs text-slate-400 relative z-10 glass">
        <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4">
            <div>
                <span class="font-luxury text-xl font-bold text-gold-gradient">Hải Sản TaDaaa</span> — Đẳng Cấp Hải Sản Tươi Sống
            </div>
            <div>
                Điều hành & Bảo chứng chất lượng: <strong class="text-amber-300">Minh Vũ (0372.360.368)</strong>
            </div>
            <div>
                © 2026 Hải Sản TaDaaa. Interactive 3D WebGL Experience.
            </div>
        </div>
    </footer>

    <!-- SLIDE-OVER GIỎ HÀNG & ĐẶT MÓN -->
    <div id="cart-modal" class="fixed inset-0 z-50 hidden">
        <!-- Backdrop -->
        <div onclick="toggleCart()" class="absolute inset-0 bg-black/70 backdrop-blur-sm"></div>
        
        <!-- Nội dung giỏ hàng -->
        <div class="absolute right-0 top-0 h-full w-full max-w-md glass border-l border-amber-500/30 flex flex-col justify-between p-6 shadow-2xl">
            <div>
                <div class="flex justify-between items-center pb-4 border-b border-white/10">
                    <div class="flex items-center gap-2">
                        <i class="fa-solid fa-crown text-amber-400"></i>
                        <h3 class="font-luxury text-2xl font-bold text-gold-gradient">Giỏ Hàng Thượng Hạng</h3>
                    </div>
                    <button onclick="toggleCart()" class="text-slate-400 hover:text-white text-xl">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>

                <!-- Danh sách món đã chọn -->
                <div id="cart-items" class="my-4 space-y-3 max-h-[42vh] overflow-y-auto pr-1">
                    <!-- Render bằng JS -->
                </div>
            </div>

            <!-- Form thanh toán / đặt hàng -->
            <div class="border-t border-white/10 pt-4 space-y-4">
                <div class="flex justify-between items-center text-base">
                    <span class="text-slate-300">Tổng tạm tính:</span>
                    <span id="cart-total" class="text-2xl font-bold text-amber-400">0đ</span>
                </div>

                <form onsubmit="checkoutOrder(event)" class="space-y-3">
                    <input type="text" id="cust-name" required placeholder="Họ tên người nhận *" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900/90 border border-white/15 text-xs focus:border-amber-400 focus:outline-none">
                    <input type="tel" id="cust-phone" required placeholder="Số điện thoại nhận hàng *" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900/90 border border-white/15 text-xs focus:border-amber-400 focus:outline-none">
                    <input type="text" id="cust-address" required placeholder="Địa chỉ giao hàng chi tiết *" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900/90 border border-white/15 text-xs focus:border-amber-400 focus:outline-none">
                    <select id="cust-cook" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900/90 border border-white/15 text-xs text-amber-200 focus:border-amber-400 focus:outline-none">
                        <option value="Giao tươi sống về tự chế biến">🌊 Giao tươi sống (Đóng oxy chuyên dụng)</option>
                        <option value="Hấp sả / Hấp bia giữ vị ngọt">♨️ Đầu bếp Hấp sả / Hấp bia miễn phí</option>
                        <option value="Chế biến Sốt Hoàng Kim / Cháy Tỏi">🔥 Chế biến Sốt Hoàng Kim / Cháy tỏi</option>
                        <option value="Nướng phô mai / Nướng mỡ hành">🧀 Nướng Phô Mai / Nướng Mỡ Hành</option>
                    </select>
                    <button type="submit" class="w-full btn-gold py-3.5 rounded-xl font-bold text-xs uppercase tracking-wider shadow-lg flex items-center justify-center gap-2">
                        <i class="fa-solid fa-paper-plane"></i>
                        <span>Hoàn Tất Đặt Hàng (Gửi Minh Vũ)</span>
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- MODAL XÁC NHẬN ĐƠN HÀNG THÀNH CÔNG -->
    <div id="order-success-modal" class="fixed inset-0 z-50 hidden flex items-center justify-center p-4">
        <div onclick="closeSuccessModal()" class="absolute inset-0 bg-black/80 backdrop-blur-md"></div>
        <div class="glass-card max-w-md w-full rounded-3xl p-8 text-center relative z-10 border border-amber-400/50 space-y-5">
            <div class="w-20 h-20 rounded-full bg-emerald-500/20 border-2 border-emerald-400 flex items-center justify-center text-emerald-400 text-4xl mx-auto shadow-[0_0_30px_rgba(16,185,129,0.4)]">
                <i class="fa-solid fa-check"></i>
            </div>
            <h3 class="font-luxury text-3xl font-bold text-gold-gradient">Đặt Hàng Thành Công!</h3>
            <div id="order-summary-box" class="text-left text-xs bg-slate-950/80 p-4 rounded-2xl border border-white/10 space-y-1.5 text-slate-300">
                <!-- Thông tin đơn hiển thị tại đây -->
            </div>
            <p class="text-xs text-slate-300">
                Hệ thống đã ghi nhận đơn hàng. <strong class="text-amber-300">Minh Vũ (0372.360.368)</strong> sẽ liên hệ xác nhận với quý khách trong ít phút!
            </p>
            <div class="flex gap-3">
                <a href="tel:0372360368" class="flex-1 btn-gold py-3 rounded-xl font-bold text-xs uppercase flex items-center justify-center gap-2">
                    <i class="fa-solid fa-phone"></i> Gọi Ngay Minh Vũ
                </a>
                <button onclick="closeSuccessModal()" class="px-5 py-3 rounded-xl glass text-xs font-semibold hover:bg-white/10">
                    Đóng
                </button>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT: DỮ LIỆU MÓN ĂN, GIỎ HÀNG & THREE.JS 3D PARTICLES -->
    <script>
        // 1. DỮ LIỆU THỰC ĐƠN HẢI SẢN TADAAA
        const menuData = [
            {
                id: 1,
                name: "Tôm Hùm Alaska Khổng Lồ",
                category: "nhap-khau",
                price: 1290000,
                unit: "1 Kg (Size 1.5 - 3kg)",
                badge: "Best Seller",
                image: "https://images.unsplash.com/photo-1559742811-822873691df8?auto=format&fit=crop&w=800&q=80",
                desc: "Nhập khẩu trực tiếp từ vùng biển lạnh Alaska, thịt trắng ngần, giòn ngọt và gạch béo ngậy."
            },
            {
                id: 2,
                name: "Cua Hoàng Đế (King Crab) Đỏ",
                category: "nhap-khau",
                price: 2450000,
                unit: "1 Kg (Size 2 - 4kg)",
                badge: "Thượng Hạng",
                image: "https://images.unsplash.com/photo-1565680018434-b513d5e5fd47?auto=format&fit=crop&w=800&q=80",
                desc: "Vua của các loài cua biển sâu. Từng thớ thịt dày tràn ngập hương vị đại dương đẳng cấp."
            },
            {
                id: 3,
                name: "Bào Ngư Viền Xanh Úc",
                category: "nhap-khau",
                price: 950000,
                unit: "Khay 500g",
                badge: "Đại Bổ",
                image: "https://images.unsplash.com/photo-1615141982883-c7ad0e69fd62?auto=format&fit=crop&w=800&q=80",
                desc: "Thực phẩm vương giả giàu dinh dưỡng, thích hợp hầm thuốc bắc, nấu cháo hoặc sốt dầu hào."
            },
            {
                id: 4,
                name: "Cua Thịt / Cua Gạch Cà Mau",
                category: "tuoi-song",
                price: 650000,
                unit: "1 Kg (Dây không trọng lượng)",
                badge: "Bao Chắc 1 Đổi 1",
                image: "https://images.unsplash.com/photo-1553659971-f01207815844?auto=format&fit=crop&w=800&q=80",
                desc: "Tuyển chọn từng con cua Cà Mau chính gốc, gạch son tràn mai, thịt chắc ngọt tự nhiên."
            },
            {
                id: 5,
                name: "Bề Bề (Tôm Tít) Chúa Trứng",
                category: "tuoi-song",
                price: 480000,
                unit: "1 Kg (10-12 con)",
                badge: "Siêu Trứng",
                image: "https://images.unsplash.com/photo-1565557623262-b51c2513a641?auto=format&fit=crop&w=800&q=80",
                desc: "Tôm tít chúa bơi sống tại bể, bụng đầy trứng béo bùi. Ngon tuyệt đỉnh khi rang muối hoặc cháy tỏi."
            },
            {
                id: 6,
                name: "Mực Lá Đại Dương Câu Nháy",
                category: "tuoi-song",
                price: 420000,
                unit: "1 Kg",
                badge: "Tươi Trong Vắt",
                image: "https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?auto=format&fit=crop&w=800&q=80",
                desc: "Mực câu tự nhiên dày mình, da còn nhấp nháy sắc màu. Hấp gừng hoặc nướng sa tế cực phẩm."
            },
            {
                id: 7,
                name: "Hàu Sữa Pháp Fine De Claire",
                category: "nhap-khau",
                price: 390000,
                unit: "Set 6 Con VIP",
                badge: "Sashimi Chuẩn Vị",
                image: "https://images.unsplash.com/photo-1606731219412-3b1e4d6f4b6d?auto=format&fit=crop&w=800&q=80",
                desc: "Thưởng thức sống cùng chanh vàng và sốt Tabasco hoặc nướng phô mai tan chảy béo ngậy."
            },
            {
                id: 8,
                name: "Combo Hoàng Gia TaDaaa VIP 1",
                category: "combo",
                price: 1890000,
                unit: "Bàn 4 - 6 Người",
                badge: "Tiết Kiệm 300K",
                image: "https://images.unsplash.com/photo-1534422298391-e4f8c172dddb?auto=format&fit=crop&w=800&q=80",
                desc: "Gồm: 1 Tôm Hùm Bông, 2 Cua Cà Mau, 500g Ốc Hương, 500g Mực Câu & 6 Hàu Pháp nướng phô mai."
            },
            {
                id: 9,
                name: "Combo Đại Dương Thịnh Vượng",
                category: "combo",
                price: 3650000,
                unit: "Bàn 8 - 10 Người",
                badge: "Party Luxury",
                image: "https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=800&q=80",
                desc: "Trọn bộ Tôm Hùm Alaska, Chân King Crab, Bào Ngư Úc, Cá Mú Đỏ hấp Hồng Kông chế biến sẵn tận nhà."
            }
        ];

        let cart = [];

        function formatVND(amount) {
            return amount.toLocaleString('vi-VN') + 'đ';
        }

        // 2. RENDER MENU & KÍCH HOẠT HIỆU ỨNG 3D TILT
        function renderMenu(filter = 'all') {
            const grid = document.getElementById('menu-grid');
            grid.innerHTML = '';

            const filtered = filter === 'all' ? menuData : menuData.filter(item => item.category === filter);

            filtered.forEach(item => {
                const card = document.createElement('div');
                card.className = 'glass-card rounded-3xl p-5 flex flex-col justify-between relative group cursor-pointer';
                card.setAttribute('data-tilt', '');
                card.setAttribute('data-tilt-max', '12');
                card.setAttribute('data-tilt-speed', '400');
                card.setAttribute('data-tilt-glare', 'true');
                card.setAttribute('data-tilt-max-glare', '0.25');

                card.innerHTML = `
                    <div>
                        <div class="relative overflow-hidden rounded-2xl mb-4">
                            <span class="absolute top-3 left-3 z-10 bg-amber-500 text-slate-950 text-[10px] font-extrabold uppercase px-3 py-1 rounded-full shadow">
                                ${item.badge}
                            </span>
                            <img src="${item.image}" alt="${item.name}" class="w-full h-56 object-cover group-hover:scale-110 transition duration-500">
                        </div>
                        <div class="tilt-content space-y-2">
                            <span class="text-[11px] text-cyan-400 uppercase tracking-wider">${item.unit}</span>
                            <h3 class="font-luxury text-2xl font-bold text-white group-hover:text-amber-300 transition">${item.name}</h3>
                            <p class="text-xs text-slate-300 leading-relaxed line-clamp-2">${item.desc}</p>
                        </div>
                    </div>
                    <div class="pt-4 mt-4 border-t border-white/10 flex items-center justify-between tilt-content">
                        <div>
                            <span class="text-[10px] text-slate-400 block">Giá niêm yết</span>
                            <span class="text-lg font-bold text-amber-400">${formatVND(item.price)}</span>
                        </div>
                        <button onclick="addToCart(${item.id})" class="btn-gold px-4 py-2.5 rounded-xl font-bold text-xs uppercase flex items-center gap-1.5">
                            <i class="fa-solid fa-plus"></i> Chọn Món
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });

            // Khởi tạo lại hiệu ứng 3D Tilt cho các thẻ mới
            if (window.VanillaTilt) {
                VanillaTilt.init(document.querySelectorAll("#menu-grid [data-tilt]"));
            }
        }

        function filterMenu(category) {
            renderMenu(category);
            const buttons = document.querySelectorAll('#category-filters .filter-btn');
            buttons.forEach(btn => {
                btn.classList.remove('btn-gold');
                btn.classList.add('glass');
            });
            event.currentTarget.classList.remove('glass');
            event.currentTarget.classList.add('btn-gold');
        }

        // 3. QUẢN LÝ GIỎ HÀNG
        function addToCart(id) {
            const product = menuData.find(p => p.id === id);
            const existing = cart.find(item => item.id === id);
            if (existing) {
                existing.qty += 1;
            } else {
                cart.push({ ...product, qty: 1 });
            }
            updateCartUI();
            // Mở giỏ hàng báo hiệu đã thêm
            const modal = document.getElementById('cart-modal');
            if (modal.classList.contains('hidden')) {
                toggleCart();
            }
        }

        function changeQty(id, delta) {
            const item = cart.find(i => i.id === id);
            if (!item) return;
            item.qty += delta;
            if (item.qty <= 0) {
                cart = cart.filter(i => i.id !== id);
            }
            updateCartUI();
        }

        function updateCartUI() {
            const countEl = document.getElementById('cart-count');
            const itemsEl = document.getElementById('cart-items');
            const totalEl = document.getElementById('cart-total');

            const totalQty = cart.reduce((sum, i) => sum + i.qty, 0);
            const totalPrice = cart.reduce((sum, i) => sum + i.price * i.qty, 0);

            countEl.textContent = totalQty;
            totalEl.textContent = formatVND(totalPrice);

            if (cart.length === 0) {
                itemsEl.innerHTML = `<div class="text-center py-12 text-slate-400 text-xs">Giỏ hàng của quý khách đang trống.<br>Hãy chọn những tuyệt phẩm hải sản tươi ngon nhất!</div>`;
                return;
            }

            itemsEl.innerHTML = cart.map(item => `
                <div class="flex items-center justify-between gap-3 bg-slate-900/70 p-3 rounded-2xl border border-white/10">
                    <img src="${item.image}" class="w-14 h-14 rounded-xl object-cover">
                    <div class="flex-1">
                        <h4 class="text-xs font-bold text-white">${item.name}</h4>
                        <span class="text-xs text-amber-400 font-semibold">${formatVND(item.price)}</span>
                    </div>
                    <div class="flex items-center gap-2">
                        <button onclick="changeQty(${item.id}, -1)" class="w-6 h-6 rounded-lg glass text-xs flex items-center justify-center hover:bg-white/20">-</button>
                        <span class="text-xs font-bold w-4 text-center">${item.qty}</span>
                        <button onclick="changeQty(${item.id}, 1)" class="w-6 h-6 rounded-lg glass text-xs flex items-center justify-center hover:bg-white/20">+</button>
                    </div>
                </div>
            `).join('');
        }

        function toggleCart() {
            const modal = document.getElementById('cart-modal');
            modal.classList.toggle('hidden');
        }

        function checkoutOrder(e) {
            e.preventDefault();
            if (cart.length === 0) {
                alert('Quý khách vui lòng chọn ít nhất 1 món hải sản trước khi đặt hàng!');
                return;
            }
            const name = document.getElementById('cust-name').value;
            const phone = document.getElementById('cust-phone').value;
            const address = document.getElementById('cust-address').value;
            const cook = document.getElementById('cust-cook').value;
            const totalPrice = cart.reduce((sum, i) => sum + i.price * i.qty, 0);

            const itemsList = cart.map(i => `• ${i.name} (x${i.qty})`).join('<br>');

            document.getElementById('order-summary-box').innerHTML = `
                <div><strong class="text-amber-300">Khách hàng:</strong> ${name} (${phone})</div>
                <div><strong class="text-amber-300">Giao đến:</strong> ${address}</div>
                <div><strong class="text-amber-300">Yêu cầu:</strong> ${cook}</div>
                <div class="pt-2 border-t border-white/10"><strong class="text-cyan-300">Thực đơn đã đặt:</strong><br>${itemsList}</div>
                <div class="pt-2 text-sm font-bold text-amber-400">Tổng thanh toán: ${formatVND(totalPrice)}</div>
            `;

            toggleCart();
            document.getElementById('order-success-modal').classList.remove('hidden');
            cart = [];
            updateCartUI();
            e.target.reset();
        }

        function submitQuickVip(e) {
            e.preventDefault();
            const name = document.getElementById('vip-name').value;
            const phone = document.getElementById('vip-phone').value;
            const note = document.getElementById('vip-note').value || 'Tư vấn thực đơn VIP hôm nay';

            document.getElementById('order-summary-box').innerHTML = `
                <div><strong class="text-amber-300">Khách VIP:</strong> ${name}</div>
                <div><strong class="text-amber-300">Số điện thoại:</strong> ${phone}</div>
                <div><strong class="text-cyan-300">Lời nhắn cho Minh Vũ:</strong> ${note}</div>
            `;
            document.getElementById('order-success-modal').classList.remove('hidden');
            e.target.reset();
        }

        function closeSuccessModal() {
            document.getElementById('order-success-modal').classList.add('hidden');
        }

        // 4. HIỆU ỨNG ĐẠI DƯƠNG 3D & HẠT ÁNH SÁNG (THREE.JS)
        function initThreeJS() {
            const canvas = document.getElementById('bg-canvas');
            const scene = new THREE.Scene();
            scene.fog = new THREE.FogExp2(0x020813, 0.0012);

            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.z = 55;

            const renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true, antialias: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

            // Tạo Hệ Thống Hạt Đại Dương Phát Sáng (Vàng Kim & Xanh Ngọc)
            const particleCount = 1600;
            const geometry = new THREE.BufferGeometry();
            const positions = new Float32Array(particleCount * 3);
            const colors = new Float32Array(particleCount * 3);

            const colorCyan = new THREE.Color(0x00f2fe);
            const colorGold = new THREE.Color(0xfcf6ba);

            for (let i = 0; i < particleCount * 3; i += 3) {
                positions[i] = (Math.random() - 0.5) * 180;
                positions[i + 1] = (Math.random() - 0.5) * 180;
                positions[i + 2] = (Math.random() - 0.5) * 120;

                const mixedColor = Math.random() > 0.35 ? colorCyan : colorGold;
                colors[i] = mixedColor.r;
                colors[i + 1] = mixedColor.g;
                colors[i + 2] = mixedColor.b;
            }

            geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
            geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));

            const material = new THREE.PointsMaterial({
                size: 0.65,
                vertexColors: true,
                transparent: true,
                opacity: 0.85,
                blending: THREE.AdditiveBlending
            });

            const particles = new THREE.Points(geometry, material);
            scene.add(particles);

            // Tạo Quả Cầu Lưới 3D Tượng Trưng Viên Ngọc Đại Dương
            const sphereGeo = new THREE.IcosahedronGeometry(22, 2);
            const sphereMat = new THREE.MeshBasicMaterial({
                color: 0xd4af37,
                wireframe: true,
                transparent: true,
                opacity: 0.08
            });
            const oceanPearl = new THREE.Mesh(sphereGeo, sphereMat);
            scene.add(oceanPearl);

            // Tương tác di chuột 3D
            let mouseX = 0;
            let mouseY = 0;
            window.addEventListener('mousemove', (event) => {
                mouseX = (event.clientX / window.innerWidth - 0.5) * 20;
                mouseY = (event.clientY / window.innerHeight - 0.5) * 20;
            });

            // Vòng lặp Animation
            const clock = new THREE.Clock();
            function animate() {
                requestAnimationFrame(animate);
                const elapsedTime = clock.getElapsedTime();

                // Xoay nhẹ hạt và viên ngọc 3D
                particles.rotation.y = elapsedTime * 0.04;
                particles.rotation.x = Math.sin(elapsedTime * 0.1) * 0.08;

                oceanPearl.rotation.y = -elapsedTime * 0.08;
                oceanPearl.rotation.x = elapsedTime * 0.05;

                // Camera lướt mượt theo chuột
                camera.position.x += (mouseX - camera.position.x) * 0.04;
                camera.position.y += (-mouseY - camera.position.y) * 0.04;
                camera.lookAt(scene.position);

                renderer.render(scene, camera);
            }

            animate();

            // Tự động co giãn khi đổi kích thước màn hình
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
        }

        // Khởi chạy khi tải trang
        window.addEventListener('DOMContentLoaded', () => {
            renderMenu();
            updateCartUI();
            initThreeJS();
        });
    </script>
</body>
</html>
