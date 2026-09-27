
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciamento de Calor Residual Planetário - Civilização Tipo 1</title>
    <!-- Tailwind CSS para Estilização Moderna -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome para Ícones Científicos e Futuristas -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Orbitron & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Orbitron:wght@400;600;800;900&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #05070f;
            color: #e2e8f0;
            overflow-x: hidden;
        }
        .font-orbitron { font-family: 'Orbitron', sans-serif; }
        
        /* Efeitos de Glassmorphism Sci-Fi */
        .glass-panel {
            background: rgba(13, 19, 36, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(56, 189, 248, 0.15);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.5);
        }
        
        .glass-panel-glow {
            box-shadow: 0 0 20px rgba(56, 189, 248, 0.2);
            border: 1px solid rgba(56, 189, 248, 0.3);
        }

        /* Styling Customizado para Inputs Slider */
        input[type=range] {
            -webkit-appearance: none;
            background: #1e293b;
            border-radius: 8px;
            height: 6px;
        }
        input[type=range]::-webkit-slider-thumb {
            -webkit-appearance: none;
            height: 18px;
            width: 18px;
            border-radius: 50%;
            background: #38bdf8;
            cursor: pointer;
            box-shadow: 0 0 10px #38bdf8;
            transition: all 0.2s ease;
        }
        input[type=range]::-webkit-slider-thumb:hover {
            transform: scale(1.2);
            background: #7dd3fc;
        }

        /* Animações de Alertas e Pulsos */
        @keyframes pulse-red {
            0%, 100% { box-shadow: 0 0 15px rgba(239, 68, 68, 0.4); border-color: rgba(239, 68, 68, 0.8); }
            50% { box-shadow: 0 0 35px rgba(239, 68, 68, 0.8); border-color: rgba(239, 68, 68, 1); }
        }
        .alert-critical {
            animation: pulse-red 1.2s infinite;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #0b0f19; }
        ::-webkit-scrollbar-thumb { background: #1e293b; border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: #38bdf8; }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between p-2 md:p-4 bg-slate-950 text-slate-100">

    <!-- CABEÇALHO DA APLICAÇÃO -->
    <header class="w-full glass-panel rounded-2xl p-4 mb-4 border-b border-cyan-500/20 flex flex-col md:flex-row justify-between items-center gap-4">
        <div class="flex items-center gap-3">
            <div class="p-3 bg-cyan-500/10 border border-cyan-400/30 rounded-xl text-cyan-400 text-2xl">
                <i class="fa-solid me-1 fa-atom animate-spin-slow"></i>
            </div>
            <div>
                <h1 class="font-orbitron font-bold text-lg md:text-xl text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-sky-200 to-indigo-400 tracking-wider">
                    KARDASHEV TIPO-1: DISSIPAÇÃO TÉRMICA
                </h1>
                <p class="text-xs text-slate-400">Gerenciamento da Segunda Lei da Termodinâmica e Escala Planetária</p>
            </div>
        </div>

        <!-- Indicador Rápido de Status Global -->
        <div class="flex items-center gap-3 bg-slate-900/80 px-4 py-2 rounded-xl border border-slate-800">
            <div id="statusIndicatorDot" class="w-3 h-3 rounded-full bg-emerald-400 animate-pulse"></div>
            <span id="statusIndicatorText" class="font-orbitron text-xs md:text-sm font-semibold text-emerald-400">SISTEMA EM EQUILÍBRIO</span>
        </div>

        <!-- Botoes de Ação Rápida (Sons e Manual) -->
        <div class="flex items-center gap-2">
            <button id="btnAudioToggle" class="px-3 py-2 bg-slate-800/80 hover:bg-slate-700 text-slate-300 hover:text-cyan-400 border border-slate-700 rounded-lg text-xs font-semibold flex items-center gap-2 transition-all">
                <i id="audioIcon" class="fa-solid fa-volume-xmark"></i>
                <span id="audioText">Áudio OFF</span>
            </button>
            <button id="btnOpenManual" class="px-3 py-2 bg-cyan-500/20 hover:bg-cyan-500/30 text-cyan-300 border border-cyan-500/40 rounded-lg text-xs font-semibold flex items-center gap-2 transition-all">
                <i class="fa-solid fa-book-bookmark"></i>
                <span>Manual Técnico</span>
            </button>
        </div>
    </header>

    <!-- CONTEÚDO PRINCIPAL (GRID RESPONSIVO) -->
    <main class="grid grid-cols-1 lg:grid-cols-12 gap-4 flex-grow">
        
        <!-- VISUALIZADOR PRINCIPAL (CANVAS 2D) -->
        <section class="lg:col-span-8 flex flex-col gap-3">
            <div class="relative w-full h-[450px] md:h-[580px] glass-panel rounded-2xl overflow-hidden border border-slate-800 flex flex-col">
                <!-- Overlay de HUD Superior do Canvas -->
                <div class="absolute top-3 left-3 right-3 z-10 flex justify-between items-center pointer-events-none">
                    <div class="bg-slate-950/80 backdrop-blur-md px-3 py-1.5 rounded-lg border border-slate-800 text-xs text-cyan-300 font-orbitron flex items-center gap-2">
                        <span class="w-2 h-2 rounded-full bg-cyan-400 animate-ping"></span>
                        VISÃO TRANSVERSAL EXO-ATMOSFÉRICA
                    </div>
                    <div class="bg-slate-950/80 backdrop-blur-md px-3 py-1.5 rounded-lg border border-slate-800 text-xs font-orbitron text-slate-300">
                        FPS: <span id="fpsCounter" class="text-emerald-400">60</span>
                    </div>
                </div>

                <!-- Canvas principal 2D -->
                <canvas id="thermalCanvas" class="w-full h-full cursor-crosshair bg-slate-950"></canvas>

                <!-- HUD Inferior Overlay (Informações de Feixes Orbitais e Oceanos) -->
                <div class="absolute bottom-3 left-3 right-3 z-10 flex justify-between items-end pointer-events-none">
                    <div class="bg-slate-950/80 backdrop-blur-md p-2.5 rounded-xl border border-slate-800/80 text-xs space-y-1">
                        <div class="text-slate-400 font-semibold text-[10px] uppercase">Radiadores Orbitais Ativos</div>
                        <div class="text-sky-300 font-orbitron flex items-center gap-1.5">
                            <i class="fa-solid fa-satellite text-cyan-400"></i>
                            <span id="canvasOrbitalBeamPower">0.0 PW</span> Feixe Dissipativo Space-Ray
                        </div>
                    </div>
                    <div class="bg-slate-950/80 backdrop-blur-md p-2.5 rounded-xl border border-slate-800/80 text-xs space-y-1 text-right">
                        <div class="text-slate-400 font-semibold text-[10px] uppercase">Absorção Oceanos Profundos</div>
                        <div class="text-blue-400 font-orbitron flex items-center gap-1.5 justify-end">
                            <span id="canvasOceanSinkPower">0.0 PW</span> Sumidouro Geotérmico
                            <i class="fa-solid fa-water text-blue-400"></i>
                        </div>
                    </div>
                </div>
            </div>

            <!-- PRESETS RÁPIDOS DE CENÁRIOS DE TIPO-1 -->
            <div class="glass-panel p-3 rounded-xl border border-slate-800 flex flex-wrap items-center justify-between gap-2">
                <span class="text-xs text-slate-400 font-semibold uppercase tracking-wider pl-1">
                    <i class="fa-solid fa-sliders text-cyan-400 mr-1"></i> Presets Termodinâmicos:
                </span>
                <div class="flex flex-wrap gap-2">
                    <button id="presetBalanced" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-xs font-medium text-slate-200 rounded-lg transition-all border border-slate-700">
                        🌱 Equilíbrio Kardashev (100 PW)
                    </button>
                    <button id="presetSurge" class="px-3 py-1.5 bg-amber-500/20 hover:bg-amber-500/30 text-xs font-medium text-amber-300 rounded-lg transition-all border border-amber-500/30">
                        ⚡ Surto Produtivo (400 PW)
                    </button>
                    <button id="presetCrisis" class="px-3 py-1.5 bg-rose-500/20 hover:bg-rose-500/30 text-xs font-medium text-rose-300 rounded-lg transition-all border border-rose-500/30">
                        🔥 Crise de Superaquecimento
                    </button>
                    <button id="presetSpaceRadiator" class="px-3 py-1.5 bg-sky-500/20 hover:bg-sky-500/30 text-xs font-medium text-sky-300 rounded-lg transition-all border border-sky-500/30">
                        🚀 Dissipação Orbital Máxima
                    </button>
                </div>
            </div>
        </section>

        <!-- CONTROLES E DASHBOARD DE MÉTRICAS -->
        <section class="lg:col-span-4 flex flex-col gap-4">
            
            <!-- PAINEL DE MÉTRICAS TERMODINÂMICAS -->
            <div class="glass-panel p-4 rounded-2xl border border-slate-800 flex flex-col gap-3">
                <h2 class="font-orbitron text-xs font-bold text-slate-300 uppercase tracking-wider border-b border-slate-800 pb-2 flex justify-between items-center">
                    <span>Telemetria Térmica Global</span>
                    <i class="fa-solid fa-chart-line text-cyan-400"></i>
                </h2>

                <!-- Anomalia Térmica Destacada -->
                <div id="thermalAnomalyCard" class="bg-slate-900/90 p-3.5 rounded-xl border border-slate-800 flex justify-between items-center transition-all">
                    <div>
                        <div class="text-[11px] text-slate-400 font-semibold uppercase">Anomalia Térmica Atm.</div>
                        <div class="text-xs text-slate-500">Temperatura Média Baseline: 14.0 °C</div>
                    </div>
                    <div class="text-right">
                        <div id="tempAnomalyValue" class="font-orbitron font-extrabold text-2xl text-emerald-400">
                            +0.00 °C
                        </div>
                        <div id="totalTempAbs" class="text-xs font-mono text-slate-400">14.00 °C Absoluto</div>
                    </div>
                </div>

                <!-- Medidores em Grid de 2 Colunas -->
                <div class="grid grid-cols-2 gap-2">
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400 font-medium">Calor Residual Gerado</div>
                        <div id="metricHeatGenerated" class="font-orbitron font-bold text-sm text-rose-400 mt-1">0.0 PW</div>
                        <div class="text-[9px] text-slate-500">Q = P_tot × (1 - η)</div>
                    </div>
                    <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800">
                        <div class="text-[10px] text-slate-400 font-medium">Dissipação Total Ativa</div>
                        <div id="metricHeatDissipated" class="font-orbitron font-bold text-sm text-cyan-400 mt-1">0.0 PW</div>
                        <div class="text-[9px] text-slate-500">Radiadores + Oceanos</div>
                    </div>
                </div>

                <!-- Índice de Estabilidade Ecológica e Barra de Progresso -->
                <div class="bg-slate-900/60 p-3 rounded-xl border border-slate-800 space-y-2">
                    <div class="flex justify-between items-center text-xs">
                        <span class="text-slate-400 font-semibold">Índice de Estabilidade Ecológica (ESI)</span>
                        <span id="esiValue" class="font-orbitron font-bold text-emerald-400">100.0%</span>
                    </div>
                    <div class="w-full h-2.5 bg-slate-950 rounded-full overflow-hidden p-0.5 border border-slate-800">
                        <div id="esiBar" class="h-full bg-gradient-to-r from-emerald-500 to-cyan-400 rounded-full transition-all duration-300" style="width: 100%;"></div>
                    </div>
                </div>

                <!-- Risco de Superaquecimento Planetário -->
                <div class="bg-slate-900/60 p-2.5 rounded-xl border border-slate-800 flex justify-between items-center">
                    <span class="text-xs text-slate-400 font-semibold">Nível de Risco Térmico:</span>
                    <span id="riskBadge" class="px-2.5 py-1 rounded-lg text-xs font-orbitron font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/30">
                        NOMINAL
                    </span>
                </div>
            </div>

            <!-- PAINEL DE CONTROLES DE ENGENHARIA -->
            <div class="glass-panel p-4 rounded-2xl border border-slate-800 flex flex-col gap-4">
                <h2 class="font-orbitron text-xs font-bold text-slate-300 uppercase tracking-wider border-b border-slate-800 pb-2 flex justify-between items-center">
                    <span>Parâmetros de Operação Tipo-1</span>
                    <i class="fa-solid fa-sliders text-cyan-400"></i>
                </h2>

                <!-- Control 1: Consumo Energético Total (PW) -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs">
                        <label for="sliderEnergy" class="text-slate-300 font-medium">Consumo Energético Global</label>
                        <span id="valEnergy" class="font-orbitron text-cyan-400 font-bold">100 Petawatts</span>
                    </div>
                    <input type="range" id="sliderEnergy" min="10" max="1000" step="10" value="100" class="w-full">
                    <p class="text-[10px] text-slate-500">Demanda energética total de megacidades e computação quântica global.</p>
                </div>

                <!-- Control 2: Eficiência Termodinâmica η (%) -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs">
                        <label for="sliderEfficiency" class="text-slate-300 font-medium">Eficiência Termodinâmica (η)</label>
                        <span id="valEfficiency" class="font-orbitron text-emerald-400 font-bold">60%</span>
                    </div>
                    <input type="range" id="sliderEfficiency" min="20" max="98" step="1" value="60" class="w-full">
                    <p class="text-[10px] text-slate-500">Porcentagem de energia convertida em trabalho útil sem gerar calor residual bruto.</p>
                </div>

                <!-- Control 3: Potência Radiadores Orbitais -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs">
                        <label for="sliderRadiators" class="text-slate-300 font-medium">Radiadores Orbitais Exo-Atmosféricos</label>
                        <span id="valRadiators" class="font-orbitron text-sky-400 font-bold">40 Petawatts</span>
                    </div>
                    <input type="range" id="sliderRadiators" min="0" max="500" step="5" value="40" class="w-full">
                    <p class="text-[10px] text-slate-500">Matriz de mega-radiadores na órbita baixa expelindo calor em feixes infravermelhos.</p>
                </div>

                <!-- Control 4: Absorção Sinks Oceânicos Profundos -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs">
                        <label for="sliderOcean" class="text-slate-300 font-medium">Sumidouros Térmicos Oceânicos</label>
                        <span id="valOcean" class="font-orbitron text-blue-400 font-bold">15 Petawatts</span>
                    </div>
                    <input type="range" id="sliderOcean" min="0" max="250" step="5" value="15" class="w-full">
                    <p class="text-[10px] text-slate-500">Troca de calor via fluidos refrigerantes conduzidos às profundezas marinhas.</p>
                </div>

                <!-- Control 5: Reciclagem Termoelétrica -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs">
                        <label for="sliderThermoelectric" class="text-slate-300 font-medium">Reciclagem Termoelétrica Seebeck</label>
                        <span id="valThermoelectric" class="font-orbitron text-amber-400 font-bold">15% Recuperado</span>
                    </div>
                    <input type="range" id="sliderThermoelectric" min="0" max="60" step="1" value="15" class="w-full">
                    <p class="text-[10px] text-slate-500">Captura de calor desperdiçado reaproveitado via gradiente de estado sólido.</p>
                </div>
            </div>
        </section>
    </main>

    <!-- MODAL DO MANUAL TÉCNICO EXPLICATIVO -->
    <div id="manualModal" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-md hidden flex items-center justify-center p-4">
        <div class="glass-panel w-full max-w-3xl max-h-[85vh] rounded-2xl border border-cyan-500/30 flex flex-col overflow-hidden shadow-2xl">
            <!-- Cabeçalho do Modal -->
            <div class="p-4 border-b border-slate-800 flex justify-between items-center bg-slate-900/80">
                <div class="flex items-center gap-2 text-cyan-400 font-orbitron font-bold text-base">
                    <i class="fa-solid fa-microchip"></i>
                    <span>MANUAL TÉCNICO: SEGUNDA LEI & ESCALA KARDASHEV TIPO-1</span>
                </div>
                <button id="btnCloseManual" class="text-slate-400 hover:text-slate-100 text-xl px-2">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Corpo de Texto do Modal com Scroll -->
            <div class="p-6 overflow-y-auto space-y-6 text-xs md:text-sm text-slate-300 leading-relaxed">
                <section class="space-y-2">
                    <h3 class="text-cyan-300 font-orbitron font-bold text-sm uppercase">1. O Dilema Termodinâmico do Tipo 1</h3>
                    <p>
                        A Escala de Kardashev classifica uma civilização do **Tipo 1** como aquela capaz de aproveitar e consumir toda a energia incidente em seu planeta natal (aproximadamente $10^{16}$ a $10^{17}$ Watts, ou 100 a 1000 Petawatts).
                    </p>
                    <p>
                        Contudo, a **Segunda Lei da Termodinâmica** impõe uma limitação estrita: *qualquer conversão de energia gera calor residual não aproveitável (entropia)*. Mesmo com eficiência ultra-avançada ($\eta$), o calor bruto dissipado $Q_{residual} = P \cdot (1 - \eta)$ se acumula no sistema fechado da atmosfera terrestre, ameaçando provocar um efeito estufa descontrolado por acoplamento térmico direto.
                    </p>
                </section>

                <section class="space-y-2">
                    <h3 class="text-cyan-300 font-orbitron font-bold text-sm uppercase">2. Formulação Física da Simulação</h3>
                    <div class="bg-slate-950 p-3 rounded-xl border border-slate-800 font-mono text-xs text-sky-300 space-y-1">
                        <div>• Calor Residual Bruto: Q_bruto = P_total × (1 - η)</div>
                        <div>• Calor Reciclado: Q_reciclado = Q_bruto × R_termoelétrica</div>
                        <div>• Calor Residual Líquido: Q_liquido = Q_bruto - Q_reciclado</div>
                        <div>• Radiatividade Natural (Stefan-Boltzmann): P_rad = ε·σ·A·T⁴</div>
                        <div>• Balanço de Dissipação: ΔQ = Q_liquido - (Q_natural + Q_radiadores_orbitais + Q_sumidouros_oceanicos)</div>
                        <div>• Variação Térmica Atm: d(ΔT)/dt = ΔQ / C_capacidade_termica_planetaria</div>
                    </div>
                </section>

                <section class="space-y-2">
                    <h3 class="text-cyan-300 font-orbitron font-bold text-sm uppercase">3. Tecnologias de Dissipação Térmica em Escala Global</h3>
                    <ul class="list-disc pl-5 space-y-1 text-slate-400">
                        <li><strong class="text-slate-200">Radiadores Orbitais Exo-Atmosféricos:</strong> Conjuntos de satélites fora da atmosfera que convertem o calor conduzido da superfície em feixes laser/infravermelhos coerentes disparados diretamente para o espaço profundo, ultrapassando a barreira radiativa estufa.</li>
                        <li><strong class="text-slate-200">Sumidouros Oceânicos Profundos:</strong> Encanamento térmico megaglobal canalizando calor para crosta oceânica profunda e poços geotérmicos basálticos.</li>
                        <li><strong class="text-slate-200">Geradores Termoelétricos de Estado Sólido (Seebeck):</strong> Recicladores avançados que capturam o gradiente térmico imediato nas saídas de máquinas e computadores quanticos convertendo 15% a 60% de volta em eletricidade.</li>
                    </ul>
                </section>

                <section class="space-y-2">
                    <h3 class="text-cyan-300 font-orbitron font-bold text-sm uppercase">4. Limites Ecológicos Toleráveis</h3>
                    <p>
                        Para a biosfera terrestre suportar a transição Tipo 1, a **Anomalia Térmica ($\Delta T$)** deve ser mantida obrigatoriamente abaixo de $+1.5^\circ C$. Valores acima de $+3.0^\circ C$ acionam riscos críticos ecológicos, e acima de $+7.0^\circ C$ deflagram o colapso térmico estufa com desoxigenação dos oceanos.
                    </p>
                </section>
            </div>

            <!-- Rodapé do Modal -->
            <div class="p-4 border-t border-slate-800 bg-slate-900/80 flex justify-end">
                <button id="btnConfirmManual" class="px-4 py-2 bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-orbitron font-bold text-xs rounded-xl transition-all">
                    ENTENDIDO - INICIAR SIMULAÇÃO
                </button>
            </div>
        </div>
    </div>

    <script>
        /* ===================================================================
         * MOTOR DE SIMULAÇÃO TERMODINÂMICA E AUDIO SINTETIZADO (WEB AUDIO API)
         * =================================================================== */

        // ESTADO GLOBAL DA SIMULAÇÃO
        const state = {
            energyPW: 100,            // Consumo em Petawatts (10 a 1000)
            efficiency: 0.60,         // Eficiência Termodinâmica η (0.20 a 0.98)
            orbitalRadiatorsPW: 40,   // Potência Dissipada por Radiadores (0 a 500)
            oceanSinksPW: 15,         // Absorção Oceânica (0 a 250)
            thermoelectricRecycle: 0.15, // Reciclagem (0.0 a 0.60)
            
            // Variáveis Físicas Calculadas
            grossWasteHeatPW: 0,
            recycledHeatPW: 0,
            netWasteHeatPW: 0,
            dissipatedHeatPW: 0,
            heatBalancePW: 0,
            
            // Temperatura e Estabilidade
            baselineTemp: 14.0,       // °C
            tempAnomaly: 0.0,         // ΔT em °C
            esi: 100.0,               // Ecological Stability Index %
            riskLevel: 'NOMINAL',      // NOMINAL, CAUTION, CRITICAL, RUNAWAY
            
            // Histórico para Gráfico On-Canvas
            historyLength: 120,
            tempHistory: [],
            
            // Controle de Audio
            audioEnabled: false,
            audioCtx: null,
            humOscillator: null,
            humGain: null,
            alarmOscillator: null,
            alarmGain: null,
            lastAlarmTime: 0
        };

        // SINTETIZADOR DE ÁUDIO NATIVO (WEB AUDIO API)
        function initAudio() {
            if (state.audioCtx) return;
            try {
                const AudioCtx = window.AudioContext || window.webkitAudioContext;
                state.audioCtx = new AudioCtx();

                // Oscilador de zumbido térmico/hum de reator orbital
                state.humOscillator = state.audioCtx.createOscillator();
                state.humGain = state.audioCtx.createGain();
                
                state.humOscillator.type = 'sawtooth';
                state.humOscillator.frequency.setValueAtTime(55, state.audioCtx.currentTime); // 55Hz Low Hum
                
                // Filtro Passa-Baixa para suavizar o zumbido
                const filter = state.audioCtx.createBiquadFilter();
                filter.type = 'lowpass';
                filter.frequency.setValueAtTime(180, state.audioCtx.currentTime);

                state.humGain.gain.setValueAtTime(0.01, state.audioCtx.currentTime);

                state.humOscillator.connect(filter);
                filter.connect(state.humGain);
                state.humGain.connect(state.audioCtx.destination);
                state.humOscillator.start();

            } catch(e) {
                console.warn("Navegador não suporta Web Audio API automaticamente", e);
            }
        }

        function updateAudioDynamics() {
            if (!state.audioEnabled || !state.audioCtx) return;

            // Ajusta o pitch do hum de acordo com a carga de calor
            const heatRatio = Math.min(2.0, state.netWasteHeatPW / 100.0);
            const targetFreq = 40 + (heatRatio * 60);
            state.humOscillator.frequency.setTargetAtTime(targetFreq, state.audioCtx.currentTime, 0.2);

            // Alarme Sonoro se o Risco for Crítico ou Estufa
            if ((state.riskLevel === 'CRITICAL' || state.riskLevel === 'RUNAWAY') && Date.now() - state.lastAlarmTime > 1500) {
                playWarningBeep();
                state.lastAlarmTime = Date.now();
            }
        }

        function playWarningBeep() {
            if (!state.audioEnabled || !state.audioCtx) return;
            const osc = state.audioCtx.createOscillator();
            const gain = state.audioCtx.createGain();

            osc.type = 'sine';
            osc.frequency.setValueAtTime(state.riskLevel === 'RUNAWAY' ? 880 : 587.33, state.audioCtx.currentTime);

            gain.gain.setValueAtTime(0.05, state.audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.001, state.audioCtx.currentTime + 0.4);

            osc.connect(gain);
            gain.connect(state.audioCtx.destination);

            osc.start();
            osc.stop(state.audioCtx.currentTime + 0.4);
        }

        function playBeamLaserSound() {
            if (!state.audioEnabled || !state.audioCtx) return;
            const osc = state.audioCtx.createOscillator();
            const gain = state.audioCtx.createGain();

            osc.type = 'triangle';
            osc.frequency.setValueAtTime(220, state.audioCtx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(880, state.audioCtx.currentTime + 0.2);

            gain.gain.setValueAtTime(0.04, state.audioCtx.currentTime);
            gain.gain.linearRampToValueAtTime(0.001, state.audioCtx.currentTime + 0.25);

            osc.connect(gain);
            gain.connect(state.audioCtx.destination);

            osc.start();
            osc.stop(state.audioCtx.currentTime + 0.25);
        }

        // MOTOR DE FÍSICA TERMODINÂMICA PLANETÁRIA
        function updateThermodynamics(deltaTime) {
            // 1. Calor Residual Bruto: Q = P_tot * (1 - η)
            state.grossWasteHeatPW = state.energyPW * (1.0 - state.efficiency);

            // 2. Reciclagem Termoelétrica
            state.recycledHeatPW = state.grossWasteHeatPW * state.thermoelectricRecycle;

            // 3. Calor Residual Líquido injetado no ambiente
            state.netWasteHeatPW = state.grossWasteHeatPW - state.recycledHeatPW;

            // 4. Dissipação Térmica Natural (Emissão Infravermelha Stefan-Boltzmann aproximada)
            // Baseline do planeta equilibra ~40 PW naturais sem anomalia.
            const naturalRadiationPW = 30.0 * Math.pow(1.0 + (state.tempAnomaly / 30.0), 4);

            // 5. Dissipação Artificial Total (Radiadores Orbitais + Oceanos)
            state.dissipatedHeatPW = state.orbitalRadiatorsPW + state.oceanSinksPW + naturalRadiationPW;

            // 6. Balanço Térmico Líquido (ΔQ)
            state.heatBalancePW = state.netWasteHeatPW - state.dissipatedHeatPW;

            // 7. Equação Diferencial de Temperatura Atmosférica d(ΔT)/dt
            // Capacidade térmica global representada pela constante C = 400.0 PW·s / °C
            const planetHeatCapacity = 400.0;
            const dTemp = (state.heatBalancePW / planetHeatCapacity) * deltaTime;

            state.tempAnomaly += dTemp;

            // Limite inferior e dissipação lenta no vácuo
            if (state.tempAnomaly < -2.0) state.tempAnomaly = -2.0;

            // 8. Cálculo do ESI (Índice de Estabilidade Ecológica)
            // Baseline 100% em ΔT = 0, cai a 0% em ΔT = +10.0 °C
            if (state.tempAnomaly <= 0) {
                state.esi = 100.0;
            } else {
                state.esi = Math.max(0, 100.0 - (state.tempAnomaly / 10.0) * 100.0);
            }

            // 9. Determinação do Nível de Risco
            if (state.tempAnomaly < 1.0) {
                state.riskLevel = 'NOMINAL';
            } else if (state.tempAnomaly < 3.0) {
                state.riskLevel = 'CAUTION';
            } else if (state.tempAnomaly < 7.0) {
                state.riskLevel = 'CRITICAL';
            } else {
                state.riskLevel = 'RUNAWAY';
            }

            // Registrar Histórico para o Gráfico
            if (state.tempHistory.length >= state.historyLength) {
                state.tempHistory.shift();
            }
            state.tempHistory.push(state.tempAnomaly);
        }

        // REGISTRO DE PARTÍCULAS E ELEMENTOS VISUAIS
        const canvas = document.getElementById('thermalCanvas');
        const ctx = canvas.getContext('2d');

        let particles = [];
        let orbitalAngle = 0;

        function resizeCanvas() {
            const rect = canvas.parentElement.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
        }

        // Criar Partículas de Calor Residual ou Feixes
        function createHeatParticle(x, y, targetType) {
            particles.push({
                x: x,
                y: y,
                vx: (Math.random() - 0.5) * 0.8,
                vy: -Math.random() * 1.5 - 0.5,
                size: Math.random() * 2.5 + 1.5,
                life: 1.0,
                decay: Math.random() * 0.015 + 0.008,
                targetType: targetType // 'atmosphere', 'ocean', 'recycled', 'beam'
            });
        }

        function updateAndDrawParticles() {
            for (let i = particles.length - 1; i >= 0; i--) {
                const p = particles[i];
                p.x += p.vx;
                p.y += p.vy;
                p.life -= p.decay;

                if (p.life <= 0) {
                    particles.splice(i, 1);
                    continue;
                }

                // Renderizar cor de acordo com o tipo
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                if (p.targetType === 'recycled') {
                    ctx.fillStyle = `rgba(52, 211, 153, ${p.life})`; // Verde-esmeralda
                } else if (p.targetType === 'ocean') {
                    ctx.fillStyle = `rgba(56, 189, 248, ${p.life})`; // Azul
                } else if (p.targetType === 'beam') {
                    ctx.fillStyle = `rgba(192, 132, 252, ${p.life})`; // Roxo exo-orbital
                } else {
                    ctx.fillStyle = `rgba(248, 113, 113, ${p.life})`; // Vermelho/Laranja calor
                }
                ctx.fill();
            }
        }

        // DESENHAR PLANETA, CROSTA, CIDADE, ATMOSFERA E RADIADORES
        function drawScene() {
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height * 1.35; // Centro da curvatura da Terra
            const planetRadius = height * 0.95;

            // 1. Limpar Fundo (Espaço Sideral Profundo com Estrelas)
            ctx.fillStyle = '#030712';
            ctx.fillRect(0, 0, width, height);

            // Estrelas Fundo Estático
            ctx.fillStyle = 'rgba(255, 255, 255, 0.3)';
            for (let i = 0; i < 40; i++) {
                const sx = (i * 137.5) % width;
                const sy = (i * 91.3) % (height * 0.4);
                ctx.fillRect(sx, sy, 1.5, 1.5);
            }

            // 2. Camada da Atmosfera Radiativa (Muda de cor conforme Anomalia Térmica ΔT)
            const atmosRadius = planetRadius + 70;
            let atmosColor1, atmosColor2;

            if (state.tempAnomaly < 1.0) {
                atmosColor1 = 'rgba(56, 189, 248, 0.25)'; // Cyan equilibrado
                atmosColor2 = 'rgba(14, 165, 233, 0.05)';
            } else if (state.tempAnomaly < 3.0) {
                atmosColor1 = 'rgba(251, 191, 36, 0.35)'; // Amber/Amarelo alerta
                atmosColor2 = 'rgba(217, 119, 6, 0.08)';
            } else if (state.tempAnomaly < 7.0) {
                atmosColor1 = 'rgba(239, 68, 68, 0.45)'; // Vermelho Crítico
                atmosColor2 = 'rgba(185, 28, 28, 0.12)';
            } else {
                atmosColor1 = 'rgba(217, 70, 239, 0.6)'; // Púrpura/Crimson Colapso
                atmosColor2 = 'rgba(157, 23, 77, 0.2)';
            }

            const atmosGlow = ctx.createRadialGradient(centerX, centerY, planetRadius, centerX, centerY, atmosRadius + 30);
            atmosGlow.addColorStop(0, atmosColor1);
            atmosGlow.addColorStop(0.7, atmosColor2);
            atmosGlow.addColorStop(1, 'rgba(0, 0, 0, 0)');

            ctx.beginPath();
            ctx.arc(centerX, centerY, atmosRadius + 30, 0, Math.PI * 2);
            ctx.fillStyle = atmosGlow;
            ctx.fill();

            // 3. Oceano e Crosta Terrestre (Curva)
            const planetGlow = ctx.createRadialGradient(centerX, centerY, planetRadius - 80, centerX, centerY, planetRadius);
            planetGlow.addColorStop(0, '#0284c7'); // Azul Oceano
            planetGlow.addColorStop(0.85, '#0f172a'); // Crosta escura
            planetGlow.addColorStop(1, '#1e293b');

            ctx.beginPath();
            ctx.arc(centerX, centerY, planetRadius, 0, Math.PI * 2);
            ctx.fillStyle = planetGlow;
            ctx.fill();

            // Linha do Horizonte Terrestre
            ctx.strokeStyle = '#38bdf8';
            ctx.lineWidth = 1.5;
            ctx.stroke();

            // 4. Desenhar Megacidades Energizadas (Nódulos com Luzes Pulsantes)
            const cityCount = 7;
            const cityAngles = [-0.4, -0.28, -0.15, 0, 0.15, 0.28, 0.4];

            cityAngles.forEach((angle, idx) => {
                const cx = centerX + Math.sin(angle) * planetRadius;
                const cy = centerY - Math.cos(angle) * planetRadius;

                // Nódulo Urbano
                ctx.beginPath();
                ctx.arc(cx, cy, 5, 0, Math.PI * 2);
                ctx.fillStyle = '#f59e0b'; // Amarelo Megacidade
                ctx.fill();

                // Brilho da Cidade
                ctx.beginPath();
                ctx.arc(cx, cy, 10, 0, Math.PI * 2);
                ctx.fillStyle = 'rgba(245, 158, 11, 0.2)';
                ctx.fill();

                // Gerar Partículas de Calor Residual nas Cidades
                if (Math.random() < (state.energyPW / 200.0)) {
                    const isRecycled = Math.random() < state.thermoelectricRecycle;
                    createHeatParticle(cx + (Math.random() - 0.5) * 10, cy - 5, isRecycled ? 'recycled' : 'atmosphere');
                }
            });

            // 5. Circuito Troca Térmica Sinks Oceânicos (Tubo Submerso)
            const oceanX = centerX - Math.sin(0.32) * planetRadius;
            const oceanY = centerY - Math.cos(0.32) * planetRadius;

            ctx.beginPath();
            ctx.arc(oceanX, oceanY + 25, 18, 0, Math.PI * 2);
            ctx.strokeStyle = '#0284c7';
            ctx.lineWidth = 2;
            ctx.stroke();
            ctx.fillStyle = 'rgba(2, 132, 199, 0.3)';
            ctx.fill();

            if (state.oceanSinksPW > 0 && Math.random() < 0.6) {
                createHeatParticle(oceanX + (Math.random() - 0.5) * 20, oceanY + 20, 'ocean');
            }

            // 6. Radiadores Orbitais Exo-Atmosféricos e Feixes Dissipativos
            orbitalAngle += 0.003;
            const radiatorCount = 3;
            const orbitRadius = planetRadius + 95;

            for (let i = 0; i < radiatorCount; i++) {
                const radAngle = orbitalAngle + (i * (Math.PI * 2 / radiatorCount)) - 1.5;
                const rx = centerX + Math.sin(radAngle) * orbitRadius;
                const ry = centerY - Math.cos(radAngle) * orbitRadius;

                // Só desenhar satélites se estiverem na parte superior visível
                if (ry < centerY - 100) {
                    // Desenhar Satélite Radiador
                    ctx.save();
                    ctx.translate(rx, ry);
                    ctx.rotate(radAngle);

                    // Corpos e Paineis Radiadores
                    ctx.fillStyle = '#e2e8f0';
                    ctx.fillRect(-6, -3, 12, 6);

                    ctx.fillStyle = '#38bdf8'; // Painel Sol/Térmico
                    ctx.fillRect(-18, -2, 10, 4);
                    ctx.fillRect(8, -2, 10, 4);

                    ctx.restore();

                    // Disparo do Feixe Térmico Infravermelho para o Espaço Sideral
                    if (state.orbitalRadiatorsPW > 0) {
                        const beamLength = 120 + (state.orbitalRadiatorsPW / 500.0) * 100;
                        const bx = rx + Math.sin(radAngle) * beamLength;
                        const by = ry - Math.cos(radAngle) * beamLength;

                        // Gradiente do Feixe
                        const beamGrad = ctx.createLinearGradient(rx, ry, bx, by);
                        beamGrad.addColorStop(0, 'rgba(192, 132, 252, 0.9)');
                        beamGrad.addColorStop(0.5, 'rgba(168, 85, 247, 0.5)');
                        beamGrad.addColorStop(1, 'rgba(168, 85, 247, 0)');

                        ctx.beginPath();
                        ctx.moveTo(rx, ry);
                        ctx.lineTo(bx, by);
                        ctx.strokeStyle = beamGrad;
                        ctx.lineWidth = Math.min(12, 2 + (state.orbitalRadiatorsPW / 35.0));
                        ctx.stroke();

                        // Partículas de Energia no Feixe
                        if (Math.random() < 0.7) {
                            createHeatParticle(rx, ry, 'beam');
                        }
                    }
                }
            }

            // Atualizar e renderizar partículas acumuladas
            updateAndDrawParticles();

            // 7. Renderizar Gráfico Histórico da Anomalia Térmica On-Canvas
            drawCanvasTemperatureGraph(width - 210, 20, 190, 85);
        }

        // GRÁFICO HISTÓRICO EMBUTIDO NO CANVAS
        function drawCanvasTemperatureGraph(x, y, w, h) {
            // Fundo do Painel do Gráfico
            ctx.fillStyle = 'rgba(11, 15, 25, 0.85)';
            ctx.strokeStyle = 'rgba(56, 189, 248, 0.2)';
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.roundRect(x, y, w, h, 8);
            ctx.fill();
            ctx.stroke();

            // Título do Gráfico
            ctx.font = '9px Orbitron, sans-serif';
            ctx.fillStyle = '#94a3b8';
            ctx.fillText('HISTÓRICO TEMPERATURA ΔT', x + 8, y + 14);

            // Linha Guia de Limite Seguro (+1.5°C)
            const safeY = y + h - 15 - ((1.5 / 10.0) * (h - 25));
            ctx.strokeStyle = 'rgba(52, 211, 153, 0.4)';
            ctx.setLineDash([2, 2]);
            ctx.beginPath();
            ctx.moveTo(x + 5, safeY);
            ctx.lineTo(x + w - 5, safeY);
            ctx.stroke();
            ctx.setLineDash([]); // Reset dash

            // Plotagem do Gráfico
            if (state.tempHistory.length < 2) return;

            ctx.beginPath();
            const stepX = (w - 10) / (state.historyLength - 1);

            for (let i = 0; i < state.tempHistory.length; i++) {
                const temp = state.tempHistory[i];
                // Escala Y: 0°C na base, +10°C no topo
                const clampedTemp = Math.max(-1.0, Math.min(10.0, temp));
                const py = (y + h - 10) - ((clampedTemp / 10.0) * (h - 25));
                const px = (x + 5) + (i * stepX);

                if (i === 0) ctx.moveTo(px, py);
                else ctx.lineTo(px, py);
            }

            // Cor da Linha do Gráfico dinâmica
            if (state.tempAnomaly < 1.0) ctx.strokeStyle = '#34d399';
            else if (state.tempAnomaly < 3.0) ctx.strokeStyle = '#fbbf24';
            else ctx.strokeStyle = '#f87171';

            ctx.lineWidth = 1.8;
            ctx.stroke();
        }

        // SINCRONIZAÇÃO DA INTERFACE DOM
        function updateDOM() {
            // Atualizar valores textuais dos sliders
            document.getElementById('valEnergy').innerText = `${state.energyPW} Petawatts`;
            document.getElementById('valEfficiency').innerText = `${Math.round(state.efficiency * 100)}%`;
            document.getElementById('valRadiators').innerText = `${state.orbitalRadiatorsPW} Petawatts`;
            document.getElementById('valOcean').innerText = `${state.oceanSinksPW} Petawatts`;
            document.getElementById('valThermoelectric').innerText = `${Math.round(state.thermoelectricRecycle * 100)}% Recuperado`;

            // Canvas HUD text
            document.getElementById('canvasOrbitalBeamPower').innerText = `${state.orbitalRadiatorsPW.toFixed(1)} PW`;
            document.getElementById('canvasOceanSinkPower').innerText = `${state.oceanSinksPW.toFixed(1)} PW`;

            // Painel de Métricas
            const anomalyElem = document.getElementById('tempAnomalyValue');
            const sign = state.tempAnomaly >= 0 ? '+' : '';
            anomalyElem.innerText = `${sign}${state.tempAnomaly.toFixed(2)} °C`;
            
            document.getElementById('totalTempAbs').innerText = `${(state.baselineTemp + state.tempAnomaly).toFixed(2)} °C Absoluto`;
            document.getElementById('metricHeatGenerated').innerText = `${state.netWasteHeatPW.toFixed(1)} PW`;
            document.getElementById('metricHeatDissipated').innerText = `${state.dissipatedHeatPW.toFixed(1)} PW`;

            // ESI Bar
            document.getElementById('esiValue').innerText = `${state.esi.toFixed(1)}%`;
            const esiBar = document.getElementById('esiBar');
            esiBar.style.width = `${state.esi}%`;

            // Cores do ESI e Anomalia
            if (state.tempAnomaly < 1.0) {
                anomalyElem.className = 'font-orbitron font-extrabold text-2xl text-emerald-400';
                esiBar.className = 'h-full bg-gradient-to-r from-emerald-500 to-cyan-400 rounded-full transition-all duration-300';
            } else if (state.tempAnomaly < 3.0) {
                anomalyElem.className = 'font-orbitron font-extrabold text-2xl text-amber-400';
                esiBar.className = 'h-full bg-gradient-to-r from-amber-500 to-yellow-400 rounded-full transition-all duration-300';
            } else {
                anomalyElem.className = 'font-orbitron font-extrabold text-2xl text-rose-500 animate-pulse';
                esiBar.className = 'h-full bg-gradient-to-r from-rose-600 to-red-500 rounded-full transition-all duration-300';
            }

            // Badges de Risco
            const riskBadge = document.getElementById('riskBadge');
            const statusDot = document.getElementById('statusIndicatorDot');
            const statusText = document.getElementById('statusIndicatorText');
            const anomalyCard = document.getElementById('thermalAnomalyCard');

            if (state.riskLevel === 'NOMINAL') {
                riskBadge.className = 'px-2.5 py-1 rounded-lg text-xs font-orbitron font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/30';
                riskBadge.innerText = 'NOMINAL (SEGURO)';
                statusDot.className = 'w-3 h-3 rounded-full bg-emerald-400 animate-pulse';
                statusText.innerText = 'SISTEMA EM EQUILÍBRIO';
                statusText.className = 'font-orbitron text-xs md:text-sm font-semibold text-emerald-400';
                anomalyCard.classList.remove('alert-critical');
            } else if (state.riskLevel === 'CAUTION') {
                riskBadge.className = 'px-2.5 py-1 rounded-lg text-xs font-orbitron font-bold bg-amber-500/20 text-amber-400 border border-amber-500/30';
                riskBadge.innerText = 'ATENÇÃO TÉRMICA';
                statusDot.className = 'w-3 h-3 rounded-full bg-amber-400 animate-ping';
                statusText.innerText = 'AQUECIMENTO ATMOSFÉRICO';
                statusText.className = 'font-orbitron text-xs md:text-sm font-semibold text-amber-400';
                anomalyCard.classList.remove('alert-critical');
            } else if (state.riskLevel === 'CRITICAL') {
                riskBadge.className = 'px-2.5 py-1 rounded-lg text-xs font-orbitron font-bold bg-rose-500/20 text-rose-400 border border-rose-500/30';
                riskBadge.innerText = 'RISCO CRÍTICO ECOLÓGICO';
                statusDot.className = 'w-3 h-3 rounded-full bg-rose-500 animate-ping';
                statusText.innerText = 'ALERTA DE SOBRECARGA';
                statusText.className = 'font-orbitron text-xs md:text-sm font-semibold text-rose-400';
                anomalyCard.classList.add('alert-critical');
            } else {
                riskBadge.className = 'px-2.5 py-1 rounded-lg text-xs font-orbitron font-bold bg-purple-500/20 text-purple-300 border border-purple-500/40 animate-pulse';
                riskBadge.innerText = 'COLAPSO TERMODINÂMICO';
                statusDot.className = 'w-3 h-3 rounded-full bg-purple-500 animate-bounce';
                statusText.innerText = 'EFEITO ESTUFA UNSTOPPABLE';
                statusText.className = 'font-orbitron text-xs md:text-sm font-semibold text-purple-400';
                anomalyCard.classList.add('alert-critical');
            }
        }

        // EVENT LISTENERS DOS SLIDERS
        document.getElementById('sliderEnergy').addEventListener('input', (e) => {
            state.energyPW = parseFloat(e.target.value);
            initAudio();
        });
        document.getElementById('sliderEfficiency').addEventListener('input', (e) => {
            state.efficiency = parseFloat(e.target.value) / 100.0;
            initAudio();
        });
        document.getElementById('sliderRadiators').addEventListener('input', (e) => {
            const oldVal = state.orbitalRadiatorsPW;
            state.orbitalRadiatorsPW = parseFloat(e.target.value);
            if (state.orbitalRadiatorsPW > oldVal) playBeamLaserSound();
            initAudio();
        });
        document.getElementById('sliderOcean').addEventListener('input', (e) => {
            state.oceanSinksPW = parseFloat(e.target.value);
            initAudio();
        });
        document.getElementById('sliderThermoelectric').addEventListener('input', (e) => {
            state.thermoelectricRecycle = parseFloat(e.target.value) / 100.0;
            initAudio();
        });

        // PRESETS RÁPIDOS
        document.getElementById('presetBalanced').addEventListener('click', () => {
            applyPreset(100, 70, 30, 10, 20);
        });
        document.getElementById('presetSurge').addEventListener('click', () => {
            applyPreset(400, 60, 100, 30, 15);
        });
        document.getElementById('presetCrisis').addEventListener('click', () => {
            applyPreset(850, 35, 20, 10, 5);
        });
        document.getElementById('presetSpaceRadiator').addEventListener('click', () => {
            applyPreset(600, 65, 380, 120, 30);
        });

        function applyPreset(energy, eff, rad, ocean, thermo) {
            state.energyPW = energy;
            state.efficiency = eff / 100.0;
            state.orbitalRadiatorsPW = rad;
            state.oceanSinksPW = ocean;
            state.thermoelectricRecycle = thermo / 100.0;

            document.getElementById('sliderEnergy').value = energy;
            document.getElementById('sliderEfficiency').value = eff;
            document.getElementById('sliderRadiators').value = rad;
            document.getElementById('sliderOcean').value = ocean;
            document.getElementById('sliderThermoelectric').value = thermo;

            playBeamLaserSound();
            initAudio();
        }

        // ÁUDIO TOGGLE
        const btnAudio = document.getElementById('btnAudioToggle');
        btnAudio.addEventListener('click', () => {
            state.audioEnabled = !state.audioEnabled;
            if (state.audioEnabled) {
                initAudio();
                if (state.audioCtx && state.audioCtx.state === 'suspended') {
                    state.audioCtx.resume();
                }
                document.getElementById('audioIcon').className = 'fa-solid fa-volume-high text-cyan-400';
                document.getElementById('audioText').innerText = 'Áudio ON';
            } else {
                if (state.humGain) state.humGain.gain.setValueAtTime(0, state.audioCtx.currentTime);
                document.getElementById('audioIcon').className = 'fa-solid fa-volume-xmark';
                document.getElementById('audioText').innerText = 'Áudio OFF';
            }
        });

        // MODAL
        const modal = document.getElementById('manualModal');
        document.getElementById('btnOpenManual').addEventListener('click', () => modal.classList.remove('hidden'));
        document.getElementById('btnCloseManual').addEventListener('click', () => modal.classList.add('hidden'));
        document.getElementById('btnConfirmManual').addEventListener('click', () => {
            modal.classList.add('hidden');
            initAudio();
        });

        // LOOP PRINCIPAL DA SIMULAÇÃO (60 FPS)
        let lastTime = performance.now();
        let frameCount = 0;
        let fpsTimer = 0;

        function gameLoop(currentTime) {
            const deltaTime = Math.min(0.1, (currentTime - lastTime) / 1000.0);
            lastTime = currentTime;

            // Medidor de FPS
            frameCount++;
            fpsTimer += deltaTime;
            if (fpsTimer >= 1.0) {
                document.getElementById('fpsCounter').innerText = frameCount;
                frameCount = 0;
                fpsTimer = 0;
            }

            // Atualizar Física Termodinâmica
            updateThermodynamics(deltaTime);

            // Atualizar Efeitos Sonoros Dinâmicos
            updateAudioDynamics();

            // Atualizar Renders no Canvas
            drawScene();

            // Sincronizar DOM
            updateDOM();

            requestAnimationFrame(gameLoop);
        }

        // INICIALIZAÇÃO DA APLICAÇÃO
        window.addEventListener('resize', resizeCanvas);
        window.onload = function() {
            resizeCanvas();
            requestAnimationFrame(gameLoop);
        };
    </script>
</body>
</html>
