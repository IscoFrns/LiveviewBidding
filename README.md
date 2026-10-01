# LiveviewBidding
Website untuk melihat live Bidding Penjualan Aset Kami
<!DOCTYPE html>
<html lang="id" class="h-full bg-[#0857C3] text-slate-800">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live View Bidding - Portal Lelang Mobil</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Font Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            500: '#71c5e8',
                            600: '#0857C3',
                            700: '#064299',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0857C3;
        }
        ::-webkit-scrollbar-thumb {
            background: #94a3b8;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #64748b;
        }
    </style>
</head>
<body class="h-full flex flex-col font-sans antialiased selection:bg-[#71c5e8] selection:text-slate-900 bg-[#0857C3]">

    <!-- Header / Navigation Panel -->
    <header class="sticky top-0 z-40 bg-white shadow-lg border-b border-slate-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3.5 flex items-center justify-between gap-4">
            <!-- Brand Logo & Main Header -->
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-[#0857C3] flex items-center justify-center text-white font-black text-xl shadow-md">
                    <i class="fa-solid fa-gavel"></i>
                </div>
                <div>
                    <h1 class="font-extrabold text-xl tracking-tight text-slate-900 flex items-center gap-2">
                        Live View Bidding
                        <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-red-100 text-red-600 border border-red-200">
                            <span class="w-2 h-2 rounded-full bg-red-500 mr-1.5 animate-ping"></span> LIVE
                        </span>
                    </h1>
                    <p class="text-xs text-slate-500">Portal Pemantauan Lelang Mobil Real-Time</p>
                </div>
            </div>

            <!-- Client Status Badge -->
            <div class="bg-slate-100 px-3.5 py-1.5 rounded-xl border border-slate-200 text-xs font-semibold text-slate-700 flex items-center gap-2">
                <span class="w-2 h-2 rounded-full bg-emerald-500"></span>
                <span>Akses Pemantau (View Only)</span>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">
        
        <!-- Info Banner Panel -->
        <div class="bg-white border border-slate-200 rounded-2xl p-4 shadow-xl flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="p-2.5 rounded-xl bg-blue-50 text-[#0857C3] border border-blue-200">
                    <i class="fa-solid fa-circle-info text-lg"></i>
                </div>
                <div>
                    <h3 class="text-sm font-bold text-slate-900">Informasi Pemantauan Lelang</h3>
                    <p class="text-xs text-slate-600">Halaman ini diperbarui secara langsung. Silakan pantau perkembangan harga penawaran unit impian Anda.</p>
                </div>
            </div>
            <div class="flex items-center gap-2 text-xs text-slate-600 bg-slate-100 px-3 py-1.5 rounded-xl border border-slate-200 font-medium whitespace-nowrap">
                <i class="fa-regular fa-clock text-[#0857C3]"></i> Status Sistem: <span class="text-emerald-600 font-bold">Terhubung</span>
            </div>
        </div>

        <!-- Search, Filter & Layout Controls Panel -->
        <div class="bg-white rounded-2xl p-4 border border-slate-200 shadow-xl flex flex-col md:flex-row gap-4 items-center justify-between">
            <!-- Search Input -->
            <div class="relative w-full md:w-96">
                <div class="absolute inset-y-0 left-0 pl-3.5 flex items-center pointer-events-none text-slate-400">
                    <i class="fa-solid fa-magnifying-glass"></i>
                </div>
                <input type="text" id="searchInput" oninput="filterCars()" placeholder="Cari Plat No (B 1234 ABC) / Model..." class="w-full pl-10 pr-4 py-2.5 bg-slate-50 border border-slate-300 rounded-xl text-sm text-slate-900 placeholder-slate-400 focus:outline-none focus:border-[#0857C3] focus:ring-1 focus:ring-[#0857C3] transition-colors">
            </div>

            <!-- Filters -->
            <div class="flex flex-wrap items-center gap-3 w-full md:w-auto justify-between md:justify-end">
                <div class="flex items-center gap-2">
                    <label class="text-xs text-slate-600 font-semibold whitespace-nowrap"><i class="fa-solid fa-filter text-slate-400"></i> Status:</label>
                    <select id="statusFilter" onchange="filterCars()" class="bg-slate-50 border border-slate-300 text-xs text-slate-800 font-medium rounded-xl px-3 py-2.5 focus:outline-none focus:border-[#0857C3]">
                        <option value="ALL">Semua Status</option>
                        <option value="LIVE">LIVE Bidding</option>
                        <option value="HOT">HOT Bid 🔥</option>
                        <option value="ENDED">Lelang Selesai</option>
                        <option value="SOLD">TERJUAL (Sold)</option>
                    </select>
                </div>

                <div class="flex items-center gap-2">
                    <label class="text-xs text-slate-600 font-semibold whitespace-nowrap"><i class="fa-solid fa-arrow-down-short-wide text-slate-400"></i> Urutan:</label>
                    <select id="sortFilter" onchange="filterCars()" class="bg-slate-50 border border-slate-300 text-xs text-slate-800 font-medium rounded-xl px-3 py-2.5 focus:outline-none focus:border-[#0857C3]">
                        <option value="newest">Terbaru Ditambahkan</option>
                        <option value="price-high">Harga Tertinggi</option>
                        <option value="price-low">Harga Terendah</option>
                    </select>
                </div>

                <!-- View Switcher -->
                <div class="flex bg-slate-100 p-1 rounded-xl border border-slate-200">
                    <button id="viewGridBtn" onclick="setSwitchView('grid')" class="p-2 rounded-lg text-white bg-[#0857C3] shadow-sm transition-colors" title="Grid View">
                        <i class="fa-solid fa-border-all"></i>
                    </button>
                    <button id="viewListBtn" onclick="setSwitchView('list')" class="p-2 rounded-lg text-slate-500 hover:text-slate-800 transition-colors" title="List View">
                        <i class="fa-solid fa-list"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Car List Display Container -->
        <div id="carContainer" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5 transition-all"></div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden flex-col items-center justify-center py-16 text-center bg-white rounded-2xl border border-slate-200 shadow-xl">
            <div class="w-16 h-16 rounded-full bg-slate-100 flex items-center justify-center text-slate-400 mb-3 text-2xl">
                <i class="fa-solid fa-car-side"></i>
            </div>
            <h3 class="text-slate-800 font-bold text-lg">Tidak Ada Mobil Ditemukan</h3>
            <p class="text-slate-500 text-xs max-w-sm mt-1">Coba sesuaikan kata kunci pencarian atau filter Anda untuk menemukan unit kendaraan.</p>
        </div>
    </main>

    <script>
        // Initial Data Vehicles
        const INITIAL_CARS = [
            {
                id: 'car-101',
                model: 'Toyota Innova Zenix 2.0 Q HV Modelista 2023',
                nopol: 'B 1892 SSX',
                km: '15.000 km',
                stnkDate: '10/2026',
                openBid: 580000000,
                currentBid: 605000000,
                status: 'HOT',
                image: 'https://images.unsplash.com/photo-1552519507-da3b142c6e3d?auto=format&fit=crop&w=800&q=80',
                totalBids: 12,
                updatedAt: new Date().getTime()
            },
            {
                id: 'car-102',
                model: 'Honda CR-V 1.5 Turbo Prestige Black Edition 2022',
                nopol: 'B 2341 TGR',
                km: '28.500 km',
                stnkDate: 'Pajak Panjang 08/2025',
                openBid: 490000000,
                currentBid: 512000000,
                status: 'LIVE',
                image: 'https://images.unsplash.com/photo-1533473359331-0135ef1b58bf?auto=format&fit=crop&w=800&q=80',
                totalBids: 8,
                updatedAt: new Date().getTime()
            },
            {
                id: 'car-103',
                model: 'Mitsubishi Pajero Sport 2.4 Dakar Ultimate 4x2 2021',
                nopol: 'D 1102 AB',
                km: '42.000 km',
                stnkDate: 'Desember 2025',
                openBid: 475000000,
                currentBid: 495000000,
                status: 'LIVE',
                image: 'https://images.unsplash.com/photo-1541899481282-d53bffe3c35d?auto=format&fit=crop&w=800&q=80',
                totalBids: 5,
                updatedAt: new Date().getTime()
            },
            {
                id: 'car-104',
                model: 'Hyundai Ioniq 5 Signature Long Range 2022',
                nopol: 'B 888 EV',
                km: '12.300 km',
                stnkDate: '05/2027',
                openBid: 620000000,
                currentBid: 660000000,
                status: 'HOT',
                image: 'https://images.unsplash.com/photo-1563720223185-11003d516935?auto=format&fit=crop&w=800&q=80',
                totalBids: 19,
                updatedAt: new Date().getTime()
            }
        ];

        let cars = [];
        let currentLayout = 'grid';

        window.onload = function() {
            loadCarsFromStorage();
            renderCars();
        };

        function loadCarsFromStorage() {
            const stored = localStorage.getItem('autobid_cars_data');
            if (stored) {
                try {
                    cars = JSON.parse(stored);
                } catch(e) {
                    cars = [...INITIAL_CARS];
                }
            } else {
                cars = [...INITIAL_CARS];
            }
        }

        function formatIDR(amount) {
            return new Intl.NumberFormat('id-ID', {
                style: 'currency',
                currency: 'IDR',
                maximumFractionDigits: 0
            }).format(amount);
        }

        function setSwitchView(view) {
            currentLayout = view;
            const gridBtn = document.getElementById('viewGridBtn');
            const listBtn = document.getElementById('viewListBtn');
            const container = document.getElementById('carContainer');

            if (view === 'grid') {
                gridBtn.className = 'p-2 rounded-lg text-white bg-[#0857C3] shadow-sm transition-colors';
                listBtn.className = 'p-2 rounded-lg text-slate-500 hover:text-slate-800 transition-colors';
                container.className = 'grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5 transition-all';
            } else {
                listBtn.className = 'p-2 rounded-lg text-white bg-[#0857C3] shadow-sm transition-colors';
                gridBtn.className = 'p-2 rounded-lg text-slate-500 hover:text-slate-800 transition-colors';
                container.className = 'flex flex-col gap-4 transition-all';
            }

            renderCars();
        }

        function getStatusBadgeHTML(status) {
            switch (status) {
                case 'LIVE':
                    return `<span class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold bg-emerald-100 text-emerald-700 border border-emerald-300 shadow-sm">
                        <span class="w-2 h-2 rounded-full bg-emerald-500 mr-1.5 animate-pulse"></span> LIVE
                    </span>`;
                case 'HOT':
                    return `<span class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold bg-amber-100 text-amber-700 border border-amber-300 shadow-sm">
                        <i class="fa-solid fa-fire text-amber-500 mr-1"></i> HOT BID
                    </span>`;
                case 'ENDED':
                    return `<span class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold bg-slate-100 text-slate-600 border border-slate-300">
                        <i class="fa-solid fa-clock-rotate-left mr-1"></i> Selesai
                    </span>`;
                case 'SOLD':
                    return `<span class="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold bg-purple-100 text-purple-700 border border-purple-300">
                        <i class="fa-solid fa-check-circle mr-1"></i> TERJUAL
                    </span>`;
                default:
                    return '';
            }
        }

        function renderCars(dataToRender = null) {
            const container = document.getElementById('carContainer');
            const emptyState = document.getElementById('emptyState');
            const targetData = dataToRender || getFilteredAndSortedCars();

            if (targetData.length === 0) {
                container.innerHTML = '';
                emptyState.classList.remove('hidden');
                emptyState.classList.add('flex');
                return;
            } else {
                emptyState.classList.add('hidden');
                emptyState.classList.remove('flex');
            }

            let html = '';

            targetData.forEach(car => {
                const isGrid = currentLayout === 'grid';
                
                if (isGrid) {
                    html += `
                    <div class="bg-white border border-slate-200 hover:border-blue-300 rounded-2xl overflow-hidden shadow-xl flex flex-col justify-between transition-all duration-300 hover:shadow-2xl hover:-translate-y-1 group">
                        <div>
                            <div class="relative h-48 w-full bg-slate-100 overflow-hidden">
                                <img src="${car.image}" alt="${car.model}" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105" onerror="this.src='https://placehold.co/600x400/0857C3/ffffff?text=Foto+Kendaraan'">
                                <div class="absolute top-3 left-3">
                                    ${getStatusBadgeHTML(car.status)}
                                </div>
                                <div class="absolute top-3 right-3 bg-white/95 backdrop-blur-md px-2.5 py-1 rounded-lg border border-slate-200 text-slate-900 font-mono text-xs font-extrabold shadow-sm">
                                    ${car.nopol}
                                </div>
                            </div>

                            <div class="p-5">
                                <h3 class="font-bold text-base text-slate-900 line-clamp-2 leading-snug group-hover:text-[#0857C3] transition-colors" title="${car.model}">
                                    ${car.model}
                                </h3>

                                <!-- Badges KM & STNK Date (Free Text) -->
                                <div class="mt-2.5 flex items-center gap-2 flex-wrap">
                                    <span class="inline-flex items-center gap-1 bg-slate-100 border border-slate-200 px-2 py-0.5 rounded-md text-[11px] font-semibold text-slate-700">
                                        <i class="fa-solid fa-gauge-high text-[#0857C3]"></i> ${car.km || 'N/A'}
                                    </span>
                                    <span class="inline-flex items-center gap-1 bg-slate-100 border border-slate-200 px-2 py-0.5 rounded-md text-[11px] font-semibold text-slate-700">
                                        <i class="fa-solid fa-calendar-check text-[#0857C3]"></i> STNK: ${car.stnkDate || 'N/A'}
                                    </span>
                                </div>

                                <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between text-xs text-slate-500">
                                    <span>Harga Open Bid:</span>
                                    <span class="font-mono text-slate-700 font-bold">${formatIDR(car.openBid)}</span>
                                </div>

                                <div class="mt-2 p-3 bg-slate-50 rounded-xl border border-slate-200 flex flex-col justify-center">
                                    <div class="flex items-center justify-between">
                                        <span class="text-[11px] font-bold uppercase tracking-wider text-slate-500 flex items-center gap-1">
                                            <i class="fa-solid fa-chart-line text-[#0857C3]"></i> Penawaran Tertinggi
                                        </span>
                                        <span class="text-[10px] text-slate-400 font-mono font-medium">${car.totalBids || 0} Update</span>
                                    </div>
                                    <div class="text-xl font-black text-[#0857C3] font-mono mt-0.5">
                                        ${formatIDR(car.currentBid)}
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    `;
                } else {
                    html += `
                    <div class="bg-white border border-slate-200 hover:border-blue-300 rounded-2xl p-4 shadow-md flex flex-col md:flex-row items-center justify-between gap-4 transition-all duration-300 hover:shadow-xl">
                        <div class="flex items-center gap-4 w-full md:w-auto">
                            <div class="relative h-20 w-32 shrink-0 rounded-xl bg-slate-100 overflow-hidden border border-slate-200">
                                <img src="${car.image}" alt="${car.model}" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/600x400/0857C3/ffffff?text=Foto'">
                            </div>

                            <div class="space-y-1">
                                <div class="flex items-center gap-2 flex-wrap">
                                    ${getStatusBadgeHTML(car.status)}
                                    <span class="bg-slate-100 px-2 py-0.5 rounded border border-slate-200 text-slate-800 font-mono text-xs font-bold">
                                        ${car.nopol}
                                    </span>
                                </div>
                                <h3 class="font-bold text-sm text-slate-900">${car.model}</h3>
                                <div class="flex items-center gap-2 text-xs text-slate-500">
                                    <span>KM: <strong class="text-slate-700">${car.km || '-'}</strong></span>
                                    <span>•</span>
                                    <span>STNK: <strong class="text-slate-700">${car.stnkDate || '-'}</strong></span>
                                </div>
                            </div>
                        </div>

                        <div class="flex flex-col sm:flex-row items-center gap-4 w-full md:w-auto justify-end">
                            <div class="bg-slate-50 px-4 py-2 rounded-xl border border-slate-200 text-right w-full sm:w-auto">
                                <span class="text-[10px] uppercase font-bold text-slate-500 block">Penawaran Terbaru</span>
                                <span class="text-lg font-black text-[#0857C3] font-mono">
                                    ${formatIDR(car.currentBid)}
                                </span>
                            </div>
                        </div>
                    </div>
                    `;
                }
            });

            container.innerHTML = html;
        }

        function getFilteredAndSortedCars() {
            const searchKeyword = document.getElementById('searchInput').value.toLowerCase().trim();
            const statusVal = document.getElementById('statusFilter').value;
            const sortVal = document.getElementById('sortFilter').value;

            return cars.filter(car => {
                const matchesSearch = car.model.toLowerCase().includes(searchKeyword) || car.nopol.toLowerCase().includes(searchKeyword);
                const matchesStatus = (statusVal === 'ALL') || (car.status === statusVal);
                return matchesSearch && matchesStatus;
            }).sort((a, b) => {
                if (sortVal === 'price-high') return b.currentBid - a.currentBid;
                if (sortVal === 'price-low') return a.currentBid - b.currentBid;
                return b.updatedAt - a.updatedAt;
            });
        }

        function filterCars() {
            renderCars();
        }
    </script>
</body>
</html>
