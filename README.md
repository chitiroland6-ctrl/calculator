```html
<!DOCTYPE html>
<html lang="en" class="h-full dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modern Interactive Calculator</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        calc: {
                            bg: '#0f172a',
                            card: '#1e293b',
                            display: '#020617',
                            btn: '#334155',
                            btnHover: '#475569',
                            op: '#38bdf8',
                            opHover: '#0284c7',
                            accent: '#10b981',
                            accentHover: '#059669'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        ::-webkit-scrollbar {
            width: 4px;
            height: 4px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #475569;
            border-radius: 9999px;
        }
        .btn-press {
            touch-action: manipulation;
            user-select: none;
            transition: transform 0.08s ease, background-color 0.15s ease;
        }
        .btn-press:active {
            transform: scale(0.92);
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 font-sans min-h-full flex items-center justify-center p-2 sm:p-4">

    <div class="w-full max-w-4xl bg-calc-card border border-slate-800 rounded-3xl shadow-2xl overflow-hidden flex flex-col md:flex-row min-h-[560px] max-h-[92vh]">
        
        <!-- Main Calculator Section -->
        <div class="flex-1 flex flex-col justify-between p-4 sm:p-6 border-b md:border-b-0 md:border-r border-slate-800">
            
            <div class="flex justify-between items-center mb-3">
                <div class="flex items-center gap-2">
                    <span class="w-2.5 h-2.5 rounded-full bg-emerald-500"></span>
                    <span class="text-xs font-semibold tracking-wider text-slate-400 uppercase">Calculator App</span>
                </div>
                <div class="flex gap-2">
                    <button id="toggle-history" class="md:hidden text-slate-400 hover:text-white p-2 rounded-xl bg-calc-btn hover:bg-calc-btnHover transition" title="Toggle History">
                        <i class="fa-solid fa-clock-rotate-left text-sm"></i>
                    </button>
                    <button id="sound-toggle" class="text-slate-400 hover:text-white p-2 rounded-xl bg-calc-btn hover:bg-calc-btnHover transition" title="Toggle Sound">
                        <i id="sound-icon" class="fa-solid fa-volume-high text-sm"></i>
                    </button>
                </div>
            </div>

            <div class="bg-calc-display rounded-2xl p-4 sm:p-5 mb-4 flex flex-col justify-end items-end shadow-inner border border-slate-800/80 min-h-[110px] overflow-hidden">
                <div id="expression-display" class="text-xs sm:text-sm text-slate-400 h-6 overflow-x-auto whitespace-nowrap w-full text-right font-mono transition-all">
                    <!-- Dynamic calculation expression -->
                </div>
                <div id="main-display" class="text-3xl sm:text-5xl font-semibold tracking-tight text-white overflow-x-auto whitespace-nowrap w-full text-right font-mono mt-1">
                    0
                </div>
            </div>

            <div class="grid grid-cols-4 gap-2.5 sm:gap-3 flex-1">
                <!-- Row 1 -->
                <button data-action="clear" class="btn-press font-semibold text-base sm:text-lg rounded-2xl bg-rose-950/40 text-rose-400 hover:bg-rose-900/60 border border-rose-900/40 flex items-center justify-center p-3 sm:p-4">AC</button>
                <button data-action="backspace" class="btn-press font-semibold text-base sm:text-lg rounded-2xl bg-calc-btn text-slate-300 hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">
                    <i class="fa-solid fa-delete-left"></i>
                </button>
                <button data-action="percent" class="btn-press font-semibold text-base sm:text-lg rounded-2xl bg-calc-btn text-slate-300 hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">%</button>
                <button data-action="operator" data-val="/" class="btn-press font-semibold text-lg sm:text-xl rounded-2xl bg-sky-950/50 text-sky-400 hover:bg-sky-900/60 border border-sky-800/40 flex items-center justify-center p-3 sm:p-4">÷</button>

                <!-- Row 2 -->
                <button data-action="number" data-val="7" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">7</button>
                <button data-action="number" data-val="8" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">8</button>
                <button data-action="number" data-val="9" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">9</button>
                <button data-action="operator" data-val="*" class="btn-press font-semibold text-lg sm:text-xl rounded-2xl bg-sky-950/50 text-sky-400 hover:bg-sky-900/60 border border-sky-800/40 flex items-center justify-center p-3 sm:p-4">×</button>

                <!-- Row 3 -->
                <button data-action="number" data-val="4" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">4</button>
                <button data-action="number" data-val="5" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">5</button>
                <button data-action="number" data-val="6" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">6</button>
                <button data-action="operator" data-val="-" class="btn-press font-semibold text-lg sm:text-xl rounded-2xl bg-sky-950/50 text-sky-400 hover:bg-sky-900/60 border border-sky-800/40 flex items-center justify-center p-3 sm:p-4">−</button>

                <!-- Row 4 -->
                <button data-action="number" data-val="1" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">1</button>
                <button data-action="number" data-val="2" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">2</button>
                <button data-action="number" data-val="3" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">3</button>
                <button data-action="operator" data-val="+" class="btn-press font-semibold text-lg sm:text-xl rounded-2xl bg-sky-950/50 text-sky-400 hover:bg-sky-900/60 border border-sky-800/40 flex items-center justify-center p-3 sm:p-4">+</button>

                <!-- Row 5 -->
                <button data-action="toggle-sign" class="btn-press font-semibold text-base sm:text-lg rounded-2xl bg-calc-btn text-slate-300 hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">±</button>
                <button data-action="number" data-val="0" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">0</button>
                <button data-action="decimal" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-calc-btn text-white hover:bg-calc-btnHover flex items-center justify-center p-3 sm:p-4">.</button>
                <button data-action="equals" class="btn-press font-semibold text-xl sm:text-2xl rounded-2xl bg-emerald-600 text-white hover:bg-emerald-500 shadow-lg shadow-emerald-900/30 flex items-center justify-center p-3 sm:p-4">=</button>
            </div>
        </div>

        <div id="history-panel" class="w-full md:w-80 bg-calc-card p-4 sm:p-6 flex flex-col justify-between hidden md:flex border-t md:border-t-0 border-slate-800">
            <div>
                <div class="flex justify-between items-center mb-4 pb-3 border-b border-slate-800">
                    <h3 class="text-xs font-semibold text-slate-300 uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-clock-rotate-left text-sky-400"></i>
                        History
                    </h3>
                    <button id="clear-history" class="text-xs text-slate-400 hover:text-rose-400 transition flex items-center gap-1">
                        <i class="fa-solid fa-trash-can text-xs"></i>
                        Clear
                    </button>
                </div>

                <!-- History items log container -->
                <div id="history-list" class="space-y-2.5 overflow-y-auto max-h-[340px] pr-1">
                    <p id="empty-history" class="text-xs text-slate-500 text-center py-8 italic">No previous calculations</p>
                </div>
            </div>

            <div class="mt-4 pt-3 border-t border-slate-800/80 text-[11px] text-slate-500 text-center">
                Tap history items to load results back into the calculator.
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            let currentInput = '0';
            let previousInput = '';
            let operator = null;
            let waitingForOperand = false;
            let history = [];
            let soundEnabled = true;

            const mainDisplay = document.getElementById('main-display');
            const expressionDisplay = document.getElementById('expression-display');
            const historyList = document.getElementById('history-list');
            const emptyHistory = document.getElementById('empty-history');
            const clearHistoryBtn = document.getElementById('clear-history');
            const toggleHistoryBtn = document.getElementById('toggle-history');
            const historyPanel = document.getElementById('history-panel');
            const soundToggleBtn = document.getElementById('sound-toggle');
            const soundIcon = document.getElementById('sound-icon');

            const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            
            function playClickSound(freq = 550) {
                if (!soundEnabled) return;
                try {
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
                    gain.gain.setValueAtTime(0.04, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.04);
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    osc.start();
                    osc.stop(audioCtx.currentTime + 0.04);
                } catch (e) {}
            }

            function formatNumber(num) {
                if (num === 'Error' || num === 'Infinity' || isNaN(num)) return num;
                const number = parseFloat(num);
                if (Math.abs(number) > 1e11 || (Math.abs(number) < 1e-6 && number !== 0)) {
                    return number.toExponential(4);
                }
                const parts = num.toString().split('.');
                parts[0] = parseInt(parts[0], 10).toLocaleString('en-US');
                return parts.join('.');
            }

            function updateDisplay() {
                mainDisplay.textContent = formatNumber(currentInput);
                let expr = '';
                if (previousInput !== '') {
                    expr += `${formatNumber(previousInput)} ${getOperatorSymbol(operator)}`;
                }
                expressionDisplay.textContent = expr;
            }

            function getOperatorSymbol(op) {
                switch(op) {
                    case '+': return '+';
                    case '-': return '−';
                    case '*': return '×';
                    case '/': return '÷';
                    default: return '';
                }
            }

            function calculate(a, b, op) {
                const num1 = parseFloat(a);
                const num2 = parseFloat(b);
                if (isNaN(num1) || isNaN(num2)) return 0;

                switch (op) {
                    case '+': return num1 + num2;
                    case '-': return num1 - num2;
                    case '*': return num1 * num2;
                    case '/': return num2 === 0 ? 'Error' : num1 / num2;
                    default: return num2;
                }
            }

            function handleNumber(digit) {
                playClickSound(500);
                if (waitingForOperand) {
                    currentInput = digit;
                    waitingForOperand = false;
                } else {
                    currentInput = currentInput === '0' ? digit : currentInput + digit;
                }
                updateDisplay();
            }

            function handleDecimal() {
                playClickSound(550);
                if (waitingForOperand) {
                    currentInput = '0.';
                    waitingForOperand = false;
                } else if (!currentInput.includes('.')) {
                    currentInput += '.';
                }
                updateDisplay();
            }

            function handleOperator(nextOperator) {
                playClickSound(650);
                if (currentInput === 'Error') return;

                if (operator && waitingForOperand) {
                    operator = nextOperator;
                    updateDisplay();
                    return;
                }

                if (previousInput === '') {
                    previousInput = currentInput;
                } else if (operator) {
                    const result = calculate(previousInput, currentInput, operator);
                    if (result === 'Error') {
                        currentInput = 'Error';
                        previousInput = '';
                        operator = null;
                        updateDisplay();
                        return;
                    }
                    currentInput = String(result);
                    previousInput = currentInput;
                }

                waitingForOperand = true;
                operator = nextOperator;
                updateDisplay();
            }

            function handleEquals() {
                playClickSound(800);
                if (!operator || previousInput === '' || currentInput === 'Error') return;

                const result = calculate(previousInput, currentInput, operator);
                const resultString = String(result);

                addHistoryItem(previousInput, currentInput, operator, resultString);

                expressionDisplay.textContent = `${formatNumber(previousInput)} ${getOperatorSymbol(operator)} ${formatNumber(currentInput)} =`;
                currentInput = resultString;
                previousInput = '';
                operator = null;
                waitingForOperand = true;

                mainDisplay.textContent = formatNumber(currentInput);
            }

            function handleClear() {
                playClickSound(300);
                currentInput = '0';
                previousInput = '';
                operator = null;
                waitingForOperand = false;
                updateDisplay();
            }

            function handleBackspace() {
                playClickSound(400);
                if (waitingForOperand || currentInput === 'Error') return;
                currentInput = currentInput.length > 1 ? currentInput.slice(0, -1) : '0';
                updateDisplay();
            }

            function handlePercent() {
                playClickSound(600);
                if (currentInput === 'Error') return;
                const val = parseFloat(currentInput);
                currentInput = String(val / 100);
                updateDisplay();
            }

            function handleToggleSign() {
                playClickSound(600);
                if (currentInput === 'Error' || currentInput === '0') return;
                currentInput = String(parseFloat(currentInput) * -1);
                updateDisplay();
            }

            function addHistoryItem(prev, curr, op, result) {
                if (result === 'Error') return;
                history.unshift({
                    expression: `${formatNumber(prev)} ${getOperatorSymbol(op)} ${formatNumber(curr)}`,
                    result: formatNumber(result),
                    rawResult: result
                });
                renderHistory();
            }

            function renderHistory() {
                if (history.length === 0) {
                    emptyHistory.classList.remove('hidden');
                    historyList.innerHTML = '';
                    historyList.appendChild(emptyHistory);
                    return;
                }

                emptyHistory.classList.add('hidden');
                historyList.innerHTML = '';

                history.forEach((item) => {
                    const div = document.createElement('div');
                    div.className = 'p-2.5 rounded-xl bg-calc-display/80 hover:bg-calc-btn cursor-pointer transition border border-slate-800/60 group';
                    div.innerHTML = `
                        <div class="text-xs text-slate-400 group-hover:text-slate-300 font-mono">${item.expression}</div>
                        <div class="text-sm font-semibold text-white font-mono text-right">= ${item.result}</div>
                    `;
                    div.addEventListener('click', () => {
                        playClickSound(550);
                        currentInput = item.rawResult;
                        waitingForOperand = false;
                        updateDisplay();
                    });
                    historyList.appendChild(div);
                });
            }

            clearHistoryBtn.addEventListener('click', () => {
                playClickSound(300);
                history = [];
                renderHistory();
            });

            toggleHistoryBtn.addEventListener('click', () => {
                historyPanel.classList.toggle('hidden');
            });

            soundToggleBtn.addEventListener('click', () => {
                soundEnabled = !soundEnabled;
                soundIcon.className = soundEnabled ? 'fa-solid fa-volume-high text-sm' : 'fa-solid fa-volume-xmark text-sm';
            });

            document.querySelectorAll('button[data-action]').forEach(button => {
                button.addEventListener('click', (e) => {
                    const target = e.currentTarget;
                    const action = target.dataset.action;
                    const val = target.dataset.val;

                    switch (action) {
                        case 'number': handleNumber(val); break;
                        case 'decimal': handleDecimal(); break;
                        case 'operator': handleOperator(val); break;
                        case 'equals': handleEquals(); break;
                        case 'clear': handleClear(); break;
                        case 'backspace': handleBackspace(); break;
                        case 'percent': handlePercent(); break;
                        case 'toggle-sign': handleToggleSign(); break;
                    }
                });
            });

            document.addEventListener('keydown', (e) => {
                if (e.key >= '0' && e.key <= '9') handleNumber(e.key);
                else if (e.key === '.') handleDecimal();
                else if (e.key === '+' || e.key === '-' || e.key === '*' || e.key === '/') handleOperator(e.key);
                else if (e.key === 'Enter' || e.key === '=') { e.preventDefault(); handleEquals(); }
                else if (e.key === 'Backspace') handleBackspace();
                else if (e.key === 'Escape') handleClear();
                else if (e.key === '%') handlePercent();
            });

            updateDisplay();
        });
    </script>
</body>
</html>
```# calculator
