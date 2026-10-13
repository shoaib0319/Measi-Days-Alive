<!DOCTYPE html>
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Measi Days Alive - Vibrant Life Tracker</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        neonPink: '#ff007f',
                        neonPurple: '#7b2cbf',
                        neonCyan: '#00f5d4',
                        neonOrange: '#ff5722',
                        neonYellow: '#ffee32',
                        darkBg: '#090a10',
                    },
                    animation: {
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'float': 'float 5s ease-in-out infinite',
                        'spin-slow': 'spin 12s linear infinite',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-12px)' },
                        }
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts Outfit -->
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    
    <style>
        body {
            font-family: 'Outfit', sans-serif;
            background: #090a10;
            background-image: 
                radial-gradient(circle at 15% 15%, rgba(255, 0, 127, 0.18) 0%, transparent 45%),
                radial-gradient(circle at 85% 85%, rgba(0, 245, 212, 0.18) 0%, transparent 45%),
                radial-gradient(circle at 50% 50%, rgba(123, 44, 191, 0.15) 0%, transparent 55%),
                radial-gradient(circle at 80% 20%, rgba(255, 87, 34, 0.12) 0%, transparent 40%);
            background-attachment: fixed;
            min-height: 100vh;
        }
        .glass-card {
            background: rgba(15, 17, 26, 0.75);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .gradient-text {
            background: linear-gradient(135deg, #00f5d4 0%, #ff007f 50%, #ffee32 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .gradient-border {
            position: relative;
            border-radius: 1.5rem;
            background: linear-gradient(135deg, #ff007f, #7b2cbf, #00f5d4, #ffee32);
            padding: 2px;
        }
        .gradient-border-inner {
            background: #0d0e17;
            border-radius: calc(1.5rem - 2px);
        }
        .progress-bar-fill {
            background: linear-gradient(90deg, #ff007f, #7b2cbf, #00f5d4);
            transition: width 1s ease-in-out;
        }
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #090a10;
        }
        ::-webkit-scrollbar-thumb {
            background: #252838;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #ff007f;
        }
    </style>
</head>
<body class="text-slate-100 flex flex-col items-center justify-center p-3 sm:p-6 md:p-8 min-h-screen">

    <header class="text-center mb-6 sm:mb-10 max-w-3xl w-full animate-float mt-4">
        <div class="inline-flex items-center gap-2 mb-3 px-5 py-1.5 rounded-full bg-gradient-to-r from-neonPink/20 via-neonPurple/20 to-neonCyan/20 border border-neonPink/40 text-xs sm:text-sm font-extrabold tracking-widest uppercase text-neonCyan shadow-lg backdrop-blur-md">
            <span>✨</span>
            <span>COSMIC LIFE CHRONICLE</span>
            <span>✨</span>
        </div>
        <h1 class="text-4xl sm:text-6xl md:text-7xl font-black tracking-tight mb-3 drop-shadow-lg">
            Measi <span class="gradient-text">Days Alive</span>
        </h1>
        <p class="text-slate-300 text-sm sm:text-base max-w-xl mx-auto font-light leading-relaxed">
            Track your precise existence down to the exact second and celebrate your biological and cosmic milestone metrics in real-time.
        </p>
    </header>

    <main class="w-full max-w-4xl glass-card rounded-3xl p-5 sm:p-8 md:p-10 shadow-2xl relative overflow-hidden transition-all duration-300 border border-slate-800">
        <!-- Background Ambient Color Glows -->
        <div class="absolute -top-28 -right-28 w-60 h-60 bg-neonPink/20 rounded-full blur-3xl pointer-events-none"></div>
        <div class="absolute -bottom-28 -left-28 w-60 h-60 bg-neonCyan/20 rounded-full blur-3xl pointer-events-none"></div>

        <div class="relative z-10 grid grid-cols-1 md:grid-cols-12 gap-4 mb-8">
            <div class="md:col-span-5">
                <label for="dob" class="block text-xs font-bold uppercase tracking-wider text-neonCyan mb-2">Date of Birth</label>
                <input type="date" id="dob" class="w-full bg-slate-900/90 border border-slate-700 rounded-2xl px-4 py-3.5 text-slate-100 focus:outline-none focus:border-neonCyan focus:ring-2 focus:ring-neonCyan/20 transition-all text-base cursor-pointer">
            </div>
            <div class="md:col-span-4">
                <label for="birthTime" class="block text-xs font-bold uppercase tracking-wider text-neonPink mb-2">Time of Birth (Optional)</label>
                <input type="time" id="birthTime" value="00:00" class="w-full bg-slate-900/90 border border-slate-700 rounded-2xl px-4 py-3.5 text-slate-100 focus:outline-none focus:border-neonPink focus:ring-2 focus:ring-neonPink/20 transition-all text-base cursor-pointer">
            </div>
            <div class="md:col-span-3 flex items-end">
                <button id="calculateBtn" onclick="calculateLife()" class="w-full py-3.5 rounded-2xl bg-gradient-to-r from-neonPink via-neonPurple to-neonCyan text-white font-extrabold text-base shadow-xl shadow-neonPink/30 hover:shadow-neonCyan/50 hover:scale-[1.02] active:scale-[0.98] transition-all duration-200 flex items-center justify-center gap-2 group cursor-pointer">
                    <span>Calculate</span>
                    <svg class="w-5 h-5 group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M13 7l5 5m0 0l-5 5m5-5H6"></path></svg>
                </button>
            </div>
        </div>

        <div id="resultsContainer" class="hidden space-y-8 animate-fadeIn relative z-10">
            
            <!-- Main Days & Live Seconds Banner -->
            <div class="gradient-border p-[2px]">
                <div class="gradient-border-inner p-6 sm:p-8 text-center relative overflow-hidden">
                    <div class="absolute inset-0 bg-gradient-to-r from-neonPink/10 via-neonPurple/10 to-neonCyan/10 pointer-events-none"></div>
                    
                    <div class="flex items-center justify-center gap-2 mb-2">
                        <span class="inline-block w-2.5 h-2.5 rounded-full bg-neonCyan animate-ping"></span>
                        <span class="text-xs sm:text-sm font-bold uppercase tracking-widest text-slate-400">Total Exact Days Alive</span>
                    </div>

                    <div id="totalDays" class="text-5xl sm:text-7xl md:text-8xl font-black gradient-text tracking-tight mb-2 drop-shadow-md">0</div>
                    <div id="exactTimeAge" class="text-slate-200 text-sm sm:text-base font-semibold mb-4">0 years, 0 months, 0 days</div>
                    
                    <!-- Realtime Ticking Counter Badge -->
                    <div class="inline-flex items-center gap-2 bg-slate-900/90 border border-slate-700/80 px-4 py-2 rounded-xl text-xs sm:text-sm font-mono text-neonYellow shadow-inner">
                        <span class="text-slate-400">⚡ Live Ticking Seconds:</span>
                        <span id="liveSeconds" class="font-extrabold text-neonYellow">0</span>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <!-- Exact Units Grid -->
                <div class="glass-card rounded-2xl p-5 border border-slate-800">
                    <div class="flex items-center justify-between mb-4">
                        <h3 class="text-xs font-bold uppercase tracking-wider text-neonCyan">Full Unit Spectrum</h3>
                        <span class="p-1.5 rounded-lg bg-neonCyan/20 text-neonCyan text-xs">⏳</span>
                    </div>
                    <div class="grid grid-cols-3 gap-2 text-center">
                        <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                            <span id="unitYears" class="text-xl sm:text-2xl font-black text-neonCyan block">0</span>
                            <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Years</span>
                        </div>
                        <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                            <span id="unitMonths" class="text-xl sm:text-2xl font-black text-neonPink block">0</span>
                            <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Months</span>
                        </div>
                        <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                            <span id="unitWeeks" class="text-xl sm:text-2xl font-black text-neonYellow block">0</span>
                            <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Weeks</span>
                        </div>
                    </div>
                    <div class="grid grid-cols-3 gap-2 text-center mt-2">
                        <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                            <span id="unitDays" class="text-xl sm:text-2xl font-black text-neonOrange block">0</span>
                            <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Days</span>
                        </div>
                        <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                            <span id="unitHours" class="text-xl sm:text-2xl font-black text-neonPurple block">0</span>
                            <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Hours</span>
                        </div>
                        <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                            <span id="unitMinutes" class="text-xl sm:text-2xl font-black text-emerald-400 block">0</span>
                            <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Minutes</span>
                        </div>
                    </div>
                </div>

                <!-- Birthday Countdown -->
                <div class="glass-card rounded-2xl p-5 border border-slate-800 flex flex-col justify-between">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-xs font-bold uppercase tracking-wider text-neonPink">Next Birthday Countdown</h3>
                            <span class="p-1.5 rounded-lg bg-neonPink/20 text-neonPink text-xs">🎂</span>
                        </div>
                        <div class="grid grid-cols-3 gap-2 text-center">
                            <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                                <span id="nextBdayMonths" class="text-2xl sm:text-3xl font-black text-neonPink block">0</span>
                                <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Months</span>
                            </div>
                            <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                                <span id="nextBdayDays" class="text-2xl sm:text-3xl font-black text-neonCyan block">0</span>
                                <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Days</span>
                            </div>
                            <div class="bg-slate-900/80 p-3 rounded-xl border border-slate-800">
                                <span id="nextBdayHours" class="text-2xl sm:text-3xl font-black text-neonYellow block">0</span>
                                <span class="text-[10px] sm:text-xs text-slate-400 font-semibold uppercase">Hours</span>
                            </div>
                        </div>
                    </div>
                    
                    <button onclick="triggerConfetti()" class="w-full mt-4 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 text-neonYellow border border-neonYellow/30 font-bold text-xs uppercase tracking-wider transition-all flex items-center justify-center gap-2 cursor-pointer">
                        <span>🎉 Celebrate Milestone Now</span>
                    </button>
                </div>
            </div>

            <div>
                <h3 class="text-xs font-bold uppercase tracking-wider text-slate-400 mb-4 flex items-center gap-2">
                    <span>🚀 Biological & Environmental Life Metrics</span>
                </h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <!-- Heartbeats -->
                    <div class="glass-card rounded-2xl p-4 border border-slate-800/80 hover:border-neonPink/40 transition-colors group">
                        <div class="flex items-center gap-2.5 mb-2">
                            <div class="p-2 rounded-xl bg-neonPink/10 text-neonPink group-hover:scale-110 transition-transform animate-pulse">💓</div>
                            <span class="text-[11px] font-bold text-slate-400 uppercase">Heartbeats</span>
                        </div>
                        <div id="statHeartbeats" class="text-lg sm:text-xl font-black text-slate-100 font-mono">0</div>
                    </div>

                    <!-- Breaths Taken -->
                    <div class="glass-card rounded-2xl p-4 border border-slate-800/80 hover:border-neonCyan/40 transition-colors group">
                        <div class="flex items-center gap-2.5 mb-2">
                            <div class="p-2 rounded-xl bg-neonCyan/10 text-neonCyan group-hover:scale-110 transition-transform">🫁</div>
                            <span class="text-[11px] font-bold text-slate-400 uppercase">Breaths Taken</span>
                        </div>
                        <div id="statBreaths" class="text-lg sm:text-xl font-black text-slate-100 font-mono">0</div>
                    </div>

                    <!-- Sleep Hours -->
                    <div class="glass-card rounded-2xl p-4 border border-slate-800/80 hover:border-neonPurple/40 transition-colors group">
                        <div class="flex items-center gap-2.5 mb-2">
                            <div class="p-2 rounded-xl bg-neonPurple/10 text-neonPurple group-hover:scale-110 transition-transform">💤</div>
                            <span class="text-[11px] font-bold text-slate-400 uppercase">Sleep Hours (~33%)</span>
                        </div>
                        <div id="statSleep" class="text-lg sm:text-xl font-black text-slate-100 font-mono">0</div>
                    </div>

                    <!-- Food Consumed -->
                    <div class="glass-card rounded-2xl p-4 border border-slate-800/80 hover:border-neonYellow/40 transition-colors group">
                        <div class="flex items-center gap-2.5 mb-2">
                            <div class="p-2 rounded-xl bg-neonYellow/10 text-neonYellow group-hover:scale-110 transition-transform">🍕</div>
                            <span class="text-[11px] font-bold text-slate-400 uppercase">Food Consumed (~kg)</span>
                        </div>
                        <div id="statFood" class="text-lg sm:text-xl font-black text-slate-100 font-mono">0</div>
                    </div>
                </div>
            </div>

            <div class="glass-card rounded-2xl p-5 border border-slate-800">
                <h3 class="text-xs font-bold uppercase tracking-wider text-slate-400 mb-4 flex items-center gap-2">
                    <span>🏆 Major Life Milestones Progress</span>
                </h3>
                
                <div class="space-y-4">
                    <!-- 10,000 Days Milestone -->
                    <div>
                        <div class="flex justify-between text-xs font-bold mb-1">
                            <span class="text-slate-300">10,000 Days Milestone</span>
                            <span id="milestone10kText" class="text-neonCyan">0%</span>
                        </div>
                        <div class="w-full bg-slate-900 rounded-full h-2.5 overflow-hidden border border-slate-800">
                            <div id="milestone10kBar" class="progress-bar-fill h-full w-0"></div>
                        </div>
                    </div>

                    <!-- 20,000 Days Milestone -->
                    <div>
                        <div class="flex justify-between text-xs font-bold mb-1">
                            <span class="text-slate-300">20,000 Days Milestone</span>
                            <span id="milestone20kText" class="text-neonPink">0%</span>
                        </div>
                        <div class="w-full bg-slate-900 rounded-full h-2.5 overflow-hidden border border-slate-800">
                            <div id="milestone20kBar" class="progress-bar-fill h-full w-0"></div>
                        </div>
                    </div>

                    <!-- Century Goal (100 Years) -->
                    <div>
                        <div class="flex justify-between text-xs font-bold mb-1">
                            <span class="text-slate-300">100 Years Century Milestone</span>
                            <span id="milestone100yText" class="text-neonYellow">0%</span>
                        </div>
                        <div class="w-full bg-slate-900 rounded-full h-2.5 overflow-hidden border border-slate-800">
                            <div id="milestone100yBar" class="progress-bar-fill h-full w-0"></div>
                        </div>
                    </div>
                </div>
            </div>

        </div>

        <div id="emptyState" class="text-center py-12 text-slate-500">
            <div class="text-5xl mb-3 animate-bounce">🎂</div>
            <p class="text-base font-semibold text-slate-400">Select your date & time of birth above to launch <span class="text-neonCyan">Measi Days Alive</span>!</p>
        </div>
    </main>

    <!-- Footer -->
    <footer class="mt-8 text-center text-xs text-slate-500 font-medium">
        Measi Days Alive &copy; Live Cosmic Chronometer
    </footer>

    <script>
        let liveTimerInterval = null;

        // Set maximum selectable date to today
        const dobInput = document.getElementById('dob');
        const today = new Date();
        dobInput.max = today.toISOString().split('T')[0];
        
        // Default DOB: 25 years ago
        const defaultDob = new Date();
        defaultDob.setFullYear(defaultDob.getFullYear() - 25);
        dobInput.value = defaultDob.toISOString().split('T')[0];

        function triggerConfetti() {
            if (typeof confetti === 'function') {
                confetti({
                    particleCount: 120,
                    spread: 80,
                    origin: { y: 0.6 },
                    colors: ['#ff007f', '#7b2cbf', '#00f5d4', '#ffee32', '#ff5722']
                });
            }
        }

        function formatNumber(num) {
            return new Intl.NumberFormat().format(num);
        }

        function calculateLife() {
            const dobVal = dobInput.value;
            const timeVal = document.getElementById('birthTime').value || "00:00";

            if (!dobVal) {
                alertUser('Please select your date of birth.');
                return;
            }

            const [hours, minutes] = timeVal.split(':').map(Number);
            const birthDate = new Date(dobVal);
            birthDate.setHours(hours || 0, minutes || 0, 0, 0);

            const now = new Date();

            if (birthDate > now) {
                alertUser('Date and time of birth cannot be in the future!');
                return;
            }

            // Clear previous real-time timer if running
            if (liveTimerInterval) clearInterval(liveTimerInterval);

            // Function to update calculations in real-time
            function updateCounters() {
                const currentNow = new Date();
                const diffMs = Math.max(0, currentNow - birthDate);

                const totalSeconds = Math.floor(diffMs / 1000);
                const totalMinutes = Math.floor(totalSeconds / 60);
                const totalHours = Math.floor(totalMinutes / 60);
                const totalDays = Math.floor(totalHours / 24);
                const totalWeeks = Math.floor(totalDays / 7);

                // Exact Years, Months, Days breakdown
                let years = currentNow.getFullYear() - birthDate.getFullYear();
                let months = currentNow.getMonth() - birthDate.getMonth();
                let days = currentNow.getDate() - birthDate.getDate();

                if (days < 0) {
                    months--;
                    const prevMonth = new Date(currentNow.getFullYear(), currentNow.getMonth(), 0);
                    days += prevMonth.getDate();
                }
                if (months < 0) {
                    years--;
                    months += 12;
                }

                const totalMonths = (years * 12) + months;

                // Fun biological estimates
                const approxHeartbeats = Math.floor(totalMinutes * 75); // ~75 bpm average
                const approxBreaths = Math.floor(totalMinutes * 16);     // ~16 breaths per min
                const sleepHours = Math.floor(totalHours * 0.33);         // ~1/3 of life slept
                const foodConsumedKg = Math.floor(totalDays * 1.8);       // ~1.8 kg food per day

                // Next Birthday calculation
                const currentYear = currentNow.getFullYear();
                let nextBday = new Date(currentYear, birthDate.getMonth(), birthDate.getDate(), hours || 0, minutes || 0);
                if (nextBday < currentNow) {
                    nextBday.setFullYear(currentYear + 1);
                }

                const bdayDiffMs = nextBday - currentNow;
                const bdayDiffDays = Math.floor(bdayDiffMs / (1000 * 60 * 60 * 24));
                const bdayMonths = Math.floor(bdayDiffDays / 30);
                const bdayDays = bdayDiffDays % 30;
                const bdayHours = Math.floor((bdayDiffMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));

                // Milestones percentages
                const pct10k = Math.min(100, ((totalDays / 10000) * 100)).toFixed(1);
                const pct20k = Math.min(100, ((totalDays / 20000) * 100)).toFixed(1);
                const pct100y = Math.min(100, ((years / 100) * 100)).toFixed(1);

                // Update DOM elements
                document.getElementById('totalDays').textContent = formatNumber(totalDays);
                document.getElementById('exactTimeAge').textContent = `${years} Years, ${months} Months, ${days} Days Old`;
                document.getElementById('liveSeconds').textContent = formatNumber(totalSeconds);

                // Unit breakdowns
                document.getElementById('unitYears').textContent = formatNumber(years);
                document.getElementById('unitMonths').textContent = formatNumber(totalMonths);
                document.getElementById('unitWeeks').textContent = formatNumber(totalWeeks);
                document.getElementById('unitDays').textContent = formatNumber(totalDays);
                document.getElementById('unitHours').textContent = formatNumber(totalHours);
                document.getElementById('unitMinutes').textContent = formatNumber(totalMinutes);

                // Birthday countdown
                document.getElementById('nextBdayMonths').textContent = Math.max(0, bdayMonths);
                document.getElementById('nextBdayDays').textContent = Math.max(0, bdayDays);
                document.getElementById('nextBdayHours').textContent = Math.max(0, bdayHours);

                // Stats
                document.getElementById('statHeartbeats').textContent = formatNumber(approxHeartbeats);
                document.getElementById('statBreaths').textContent = formatNumber(approxBreaths);
                document.getElementById('statSleep').textContent = formatNumber(sleepHours) + ' hrs';
                document.getElementById('statFood').textContent = formatNumber(foodConsumedKg) + ' kg';

                // Milestones
                document.getElementById('milestone10kText').textContent = pct10k + '%';
                document.getElementById('milestone10kBar').style.width = pct10k + '%';

                document.getElementById('milestone20kText').textContent = pct20k + '%';
                document.getElementById('milestone20kBar').style.width = pct20k + '%';

                document.getElementById('milestone100yText').textContent = pct100y + '%';
                document.getElementById('milestone100yBar').style.width = pct100y + '%';
            }

            // Execute immediately and set up 1 second interval
            updateCounters();
            liveTimerInterval = setInterval(updateCounters, 1000);

            // Toggle view visibility
            document.getElementById('emptyState').classList.add('hidden');
            document.getElementById('resultsContainer').classList.remove('hidden');

            // Trigger celebration confetti
            triggerConfetti();
        }

        // Custom alert modal replace standard browser alert
        function alertUser(msg) {
            const existing = document.getElementById('customAlertModal');
            if (existing) existing.remove();

            const modal = document.createElement('div');
            modal.id = 'customAlertModal';
            modal.className = 'fixed inset-0 bg-black/80 backdrop-blur-md flex items-center justify-center z-50 p-4 animate-fadeIn';
            modal.innerHTML = `
                <div class="glass-card border border-neonPink/40 max-w-sm w-full p-6 rounded-3xl text-center shadow-2xl">
                    <div class="text-4xl mb-3">⚠️</div>
                    <h3 class="text-lg font-bold text-white mb-2">Attention</h3>
                    <p class="text-slate-300 text-sm mb-6">${msg}</p>
                    <button onclick="document.getElementById('customAlertModal').remove()" class="w-full py-3 rounded-xl bg-gradient-to-r from-neonPink to-neonPurple text-white font-extrabold shadow-lg hover:opacity-90 transition-opacity">Got It</button>
                </div>
            `;
            document.body.appendChild(modal);
        }

        // Initial calculation on page load
        window.addEventListener('DOMContentLoaded', () => {
            calculateLife();
        });
    </script>
</body>
</html>
