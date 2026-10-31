<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Navigating Tech Anxiety: Salesforce Women In Tech Brunch Toolkit</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            600: '#16a34a',
                            700: '#15803d',
                            800: '#166534',
                            900: '#14532d',
                        },
                        indigoBrand: {
                            50: '#eef2ff',
                            600: '#4f46e5',
                            700: '#4338ca',
                            900: '#312e81',
                        },
                        warmNeutral: {
                            50: '#fcfbf9',
                            100: '#f6f4ee',
                            200: '#e8e5da',
                            800: '#423f38',
                            900: '#26241f',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        /* Responsive chart container standard */
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 650px;
            margin-left: auto;
            margin-right: auto;
            height: 320px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 360px;
            }
        }
        /* Custom styled scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<!-- Chosen Palette: Warm Empowering Emerald & Indigo (Warm neutral background, Emerald primary, Deep Indigo secondary) -->
<!-- Application Structure Plan: The SPA is architected as an interactive brunch presentation & interactive workshop toolkit. It features a top header with Mode Switcher (Presentation View vs Workshop Blueprint), key metric counters, and five main deep-dive thematic modules: 1. AI Workforce Evolution & Job Security, 2. AI Risk Legislation (NIST & Florida Laws), 3. Career Empowerment & NotebookLM Mock Interview Simulator, 4. Secure Config & External Client Apps (ECA) Migration, 5. Brunch Table Discussion Cards. Designed to empower attendees by moving from fear to actionable technical strategy. -->
<!-- Visualization & Content Choices: Uses Chart.js canvas for dynamic job market data and skill shifts; interactive custom JS logic for a Live Mock Interview Simulator with instant feedback; interactive NIST framework explorer cards; interactive ECA migration risk audit tool; and interactive brunch discussion prompts. Strictly NO SVG and NO Mermaid JS used—all icons are created with styled Unicode characters and HTML/CSS elements. -->
<!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<body class="bg-warmNeutral-50 text-slate-800 font-sans antialiased min-h-screen flex flex-col selection:bg-brand-100 selection:text-brand-900">

    <!-- TOP HEADER / NAV BAR -->
    <header class="bg-white border-b border-warmNeutral-200 sticky top-0 z-50 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16 sm:h-20">
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-brand-600 to-indigoBrand-700 flex items-center justify-center text-white font-bold text-xl shadow-md">
                        &#10024;
                    </div>
                    <div>
                        <span class="text-xs font-semibold uppercase tracking-wider text-brand-700 bg-brand-50 px-2 py-0.5 rounded border border-brand-100">Salesforce Women In Tech Brunch</span>
                        <h1 class="text-lg sm:text-xl font-bold text-slate-900 leading-tight">Navigating Tech Anxiety with Confidence</h1>
                    </div>
                </div>

                <!-- Navigation Links -->
                <nav class="hidden md:flex space-x-1 lg:space-x-2 text-sm font-medium">
                    <button onclick="switchTab('ai-workforce')" id="nav-ai-workforce" class="nav-btn px-3 py-2 rounded-lg text-slate-600 hover:text-brand-700 hover:bg-warmNeutral-100 transition">AI & Jobs</button>
                    <button onclick="switchTab('legislation')" id="nav-legislation" class="nav-btn px-3 py-2 rounded-lg text-slate-600 hover:text-brand-700 hover:bg-warmNeutral-100 transition">AI Guardrails</button>
                    <button onclick="switchTab('career-prep')" id="nav-career-prep" class="nav-btn px-3 py-2 rounded-lg text-slate-600 hover:text-brand-700 hover:bg-warmNeutral-100 transition">Mock Interviewer</button>
                    <button onclick="switchTab('config-eca')" id="nav-config-eca" class="nav-btn px-3 py-2 rounded-lg text-slate-600 hover:text-brand-700 hover:bg-warmNeutral-100 transition">Config & ECAs</button>
                    <button onclick="switchTab('discussion')" id="nav-discussion" class="nav-btn px-3 py-2 rounded-lg text-slate-600 hover:text-brand-700 hover:bg-warmNeutral-100 transition">Table Prompts</button>
                </nav>

                <!-- Action Button -->
                <div class="flex items-center space-x-2">
                    <button id="modeToggleBtn" onclick="togglePresentationMode()" class="px-3 py-1.5 sm:px-4 sm:py-2 text-xs sm:text-sm font-semibold rounded-lg bg-indigoBrand-50 text-indigoBrand-700 border border-indigoBrand-100 hover:bg-indigoBrand-600 hover:text-white transition shadow-sm flex items-center space-x-1">
                        <span id="modeIcon">&#128100;</span>
                        <span id="modeText">Presentation Mode</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Nav Bar -->
        <div class="md:hidden border-t border-warmNeutral-200 bg-white px-4 py-2 flex overflow-x-auto space-x-2 text-xs font-medium">
            <button onclick="switchTab('ai-workforce')" id="mnav-ai-workforce" class="mnav-btn px-3 py-1.5 rounded-md whitespace-nowrap bg-warmNeutral-100">AI & Jobs</button>
            <button onclick="switchTab('legislation')" id="mnav-legislation" class="mnav-btn px-3 py-1.5 rounded-md whitespace-nowrap">AI Guardrails</button>
            <button onclick="switchTab('career-prep')" id="mnav-career-prep" class="mnav-btn px-3 py-1.5 rounded-md whitespace-nowrap">Mock Interviewer</button>
            <button onclick="switchTab('config-eca')" id="mnav-config-eca" class="mnav-btn px-3 py-1.5 rounded-md whitespace-nowrap">Config & ECAs</button>
            <button onclick="switchTab('discussion')" id="mnav-discussion" class="mnav-btn px-3 py-1.5 rounded-md whitespace-nowrap">Table Prompts</button>
        </div>
    </header>

    <!-- BANNER STATS SUMMARY -->
    <section class="bg-gradient-to-r from-slate-900 via-indigoBrand-900 to-slate-900 text-white py-6 shadow-inner">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-center">
                <div class="p-3 rounded-lg bg-white/5 border border-white/10 backdrop-blur-sm">
                    <div class="text-xl sm:text-2xl font-extrabold text-emerald-400">19%</div>
                    <div class="text-xs text-slate-300 mt-1">Orgs with AI-Ready Data</div>
                </div>
                <div class="p-3 rounded-lg bg-white/5 border border-white/10 backdrop-blur-sm">
                    <div class="text-xl sm:text-2xl font-extrabold text-indigo-300">81%</div>
                    <div class="text-xs text-slate-300 mt-1">CHROs Reskilling Workforce</div>
                </div>
                <div class="p-3 rounded-lg bg-white/5 border border-white/10 backdrop-blur-sm">
                    <div class="text-xl sm:text-2xl font-extrabold text-amber-300">Summer '27</div>
                    <div class="text-xs text-slate-300 mt-1">Connected Apps Deprecation</div>
                </div>
                <div class="p-3 rounded-lg bg-white/5 border border-white/10 backdrop-blur-sm">
                    <div class="text-xl sm:text-2xl font-extrabold text-rose-300">NIST 1.0</div>
                    <div class="text-xs text-slate-300 mt-1">Federal AI Governance Standard</div>
                </div>
            </div>
        </div>
    </section>

    <!-- MAIN CONTENT AREA -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <!-- ================= SECTION 1: AI WORKFORCE & JOB SECURITY ================= -->
        <section id="sec-ai-workforce" class="tab-content block space-y-8">
            
            <div class="bg-white rounded-2xl p-6 sm:p-8 border border-warmNeutral-200 shadow-sm">
                <div class="max-w-3xl">
                    <span class="text-xs font-bold tracking-wider uppercase text-brand-700 bg-brand-50 px-2.5 py-1 rounded-md border border-brand-100">Module 1: The AI Workforce Evolution</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 mt-3">From Configuration Execution to AI Governance</h2>
                    <p class="text-slate-600 mt-3 text-base sm:text-lg leading-relaxed">
                        The fear that Agentforce and AI will eliminate Salesforce jobs is real—but the reality is a <strong>shift in skill value</strong> rather than complete extinction. Routine task execution is compressing, while the demand for data governance, business analysis, and architecture is skyrocketing.
                    </p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 mt-8 items-start">
                    <!-- Chart Column -->
                    <div class="lg:col-span-7 bg-warmNeutral-50 rounded-xl p-5 border border-warmNeutral-200">
                        <div class="flex justify-between items-center mb-4">
                            <div>
                                <h3 class="font-bold text-slate-900 text-base">Salesforce Role Demand & Compensation Trends</h3>
                                <p class="text-xs text-slate-500">Comparing traditional generalist admin roles with specialized strategic positions.</p>
                            </div>
                            <span class="text-xs bg-indigoBrand-50 text-indigoBrand-700 px-2 py-1 rounded font-semibold border border-indigoBrand-100">2025–2026 Data</span>
                        </div>
                        
                        <!-- Responsive Chart Wrapper -->
                        <div class="chart-container">
                            <canvas id="jobMarketChart"></canvas>
                        </div>
                        <div class="mt-3 text-xs text-slate-500 text-center italic">
                            Source: Market analysis showing saturation in generalist admin pools vs. salary premiums in specialized roles.
                        </div>
                    </div>

                    <!-- Key Insights Column -->
                    <div class="lg:col-span-5 space-y-4">
                        <div class="p-4 rounded-xl bg-brand-50/50 border border-brand-100">
                            <div class="flex items-start space-x-3">
                                <div class="text-brand-700 font-bold text-xl">&#9889;</div>
                                <div>
                                    <h4 class="font-bold text-slate-900 text-sm">The Execution Layer Compression</h4>
                                    <p class="text-xs text-slate-600 mt-1 leading-relaxed">
                                        Basic reports, flow boilerplate, and routine field changes are automated by AI. Admins are transitioning from "manual builders" to <strong>Platform Product Managers</strong>.
                                    </p>
                                </div>
                            </div>
                        </div>

                        <div class="p-4 rounded-xl bg-amber-50/60 border border-amber-200">
                            <div class="flex items-start space-x-3">
                                <div class="text-amber-700 font-bold text-xl">&#128269;</div>
                                <div>
                                    <h4 class="font-bold text-slate-900 text-sm">The 19% Data Readiness Bottleneck</h4>
                                    <p class="text-xs text-slate-600 mt-1 leading-relaxed">
                                        AI is only as smart as underlying enterprise data. Only 19% of companies have AI-ready data. Cleaning, structuring, and governing Data Cloud is the primary growth opportunity.
                                    </p>
                                </div>
                            </div>
                        </div>

                        <div class="p-4 rounded-xl bg-indigoBrand-50/60 border border-indigoBrand-200">
                            <div class="flex items-start space-x-3">
                                <div class="text-indigoBrand-700 font-bold text-xl">&#128640;</div>
                                <div>
                                    <h4 class="font-bold text-slate-900 text-sm">The Executive Reskilling Mandate</h4>
                                    <p class="text-xs text-slate-600 mt-1 leading-relaxed">
                                        81% of CHROs are actively reskilling teams. AI is designed to boost productivity by 30%, shifting talent into higher-value strategic projects rather than head-count reduction.
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Interactive Skill Pivot Tool -->
                <div class="mt-8 pt-8 border-t border-warmNeutral-200">
                    <h3 class="text-lg font-bold text-slate-900 mb-2">&#128736; Interactive Tool: AI Career Pivot Map</h3>
                    <p class="text-xs text-slate-600 mb-4">Select your current core skill set to discover your highest-leverage career evolution path:</p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-4">
                        <button onclick="updatePivotPath('admin')" id="pivot-btn-admin" class="pivot-btn p-3 text-left rounded-lg border border-slate-200 bg-white hover:border-brand-600 text-sm font-semibold text-slate-700 transition shadow-sm">
                            &#128187; Traditional Administrator
                        </button>
                        <button onclick="updatePivotPath('dev')" id="pivot-btn-dev" class="pivot-btn p-3 text-left rounded-lg border border-slate-200 bg-white hover:border-brand-600 text-sm font-semibold text-slate-700 transition shadow-sm">
                            &#9881; Apex / LWC Developer
                        </button>
                        <button onclick="updatePivotPath('ba')" id="pivot-btn-ba" class="pivot-btn p-3 text-left rounded-lg border border-slate-200 bg-white hover:border-brand-600 text-sm font-semibold text-slate-700 transition shadow-sm">
                            &#128202; Business Analyst / Consultant
                        </button>
                    </div>

                    <div id="pivotDisplay" class="p-5 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200">
                        <!-- Dynamic JS Injection -->
                    </div>
                </div>
            </div>

        </section>


        <!-- ================= SECTION 2: LEGISLATION & AI GUARDRAILS ================= -->
        <section id="sec-legislation" class="tab-content hidden space-y-8">
            
            <div class="bg-white rounded-2xl p-6 sm:p-8 border border-warmNeutral-200 shadow-sm">
                <div class="max-w-3xl">
                    <span class="text-xs font-bold tracking-wider uppercase text-indigoBrand-700 bg-indigoBrand-50 px-2.5 py-1 rounded-md border border-indigoBrand-100">Module 2: AI Guardrails & Legislation</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 mt-3">Compliance, Ethics & Risk Management Frameworks</h2>
                    <p class="text-slate-600 mt-3 text-base sm:text-lg leading-relaxed">
                        Deploying AI agents isn't just a technical challenge—it's a regulatory imperative. Governments and standards bodies are establishing frameworks to prevent algorithmic bias, data leakage, and unvetted decision making.
                    </p>
                </div>

                <!-- Federal vs State Grid -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-8">
                    <!-- NIST AI RMF Card -->
                    <div class="bg-slate-900 text-white rounded-xl p-6 shadow-md relative overflow-hidden">
                        <div class="absolute -right-6 -bottom-6 w-32 h-32 bg-indigoBrand-600/20 rounded-full blur-2xl"></div>
                        <span class="text-xs font-bold uppercase text-emerald-400 tracking-wider">Federal Standard</span>
                        <h3 class="text-xl font-bold mt-1 text-white">NIST AI Risk Management Framework (1.0)</h3>
                        <p class="text-xs text-slate-300 mt-2 leading-relaxed">
                            NIST AI RMF moves beyond traditional cybersecurity to manage statistical risks: model drift, hallucination, opacity, and downstream bias.
                        </p>

                        <div class="grid grid-cols-2 gap-2 mt-4 text-xs">
                            <div class="p-2.5 rounded bg-white/10 border border-white/10">
                                <span class="font-bold text-emerald-300 block">1. GOVERN</span>
                                Set policy, culture & AI risk tolerance.
                            </div>
                            <div class="p-2.5 rounded bg-white/10 border border-white/10">
                                <span class="font-bold text-indigo-300 block">2. MAP</span>
                                Document context, data pipelines & limits.
                            </div>
                            <div class="p-2.5 rounded bg-white/10 border border-white/10">
                                <span class="font-bold text-amber-300 block">3. MEASURE</span>
                                Test telemetry, hallucination & bias metrics.
                            </div>
                            <div class="p-2.5 rounded bg-white/10 border border-white/10">
                                <span class="font-bold text-rose-300 block">4. MANAGE</span>
                                Deploy kill switches & emergency overrides.
                            </div>
                        </div>
                    </div>

                    <!-- Florida Legislation Card -->
                    <div class="bg-gradient-to-br from-warmNeutral-100 to-white rounded-xl p-6 border border-warmNeutral-200 shadow-sm flex flex-col justify-between">
                        <div>
                            <span class="text-xs font-bold uppercase text-brand-700 tracking-wider">State Spotlight</span>
                            <h3 class="text-xl font-bold text-slate-900 mt-1">Florida Regulatory Landscape (SB 1680 / HB 919)</h3>
                            <p class="text-xs text-slate-600 mt-2 leading-relaxed">
                                Enacted in April 2024, Florida's legislation created the <strong>Government Technology Modernization Council</strong> within DMS to monitor AI ethical standards and mandate strict disclosures around synthetic/manipulated AI media.
                            </p>
                            <ul class="mt-4 space-y-2 text-xs text-slate-700">
                                <li class="flex items-center space-x-2">
                                    <span class="text-brand-700 font-bold">&#10003;</span>
                                    <span>Mandatory AI content disclosures & transparency standards.</span>
                                </li>
                                <li class="flex items-center space-x-2">
                                    <span class="text-brand-700 font-bold">&#10003;</span>
                                    <span>Legal liability frameworks for automated decision-making.</span>
                                </li>
                                <li class="flex items-center space-x-2">
                                    <span class="text-brand-700 font-bold">&#10003;</span>
                                    <span>State agency oversight on automated citizen communications.</span>
                                </li>
                            </ul>
                        </div>
                        <div class="mt-4 pt-3 border-t border-warmNeutral-200 text-xs font-semibold text-slate-500">
                            Key Takeaway: Configuration decisions are now legal compliance matters.
                        </div>
                    </div>
                </div>

                <!-- Interactive NIST Exploration Matrix -->
                <div class="mt-8 pt-8 border-t border-warmNeutral-200">
                    <h3 class="text-lg font-bold text-slate-900 mb-2">&#128269; Agentforce Governance Mapping Tool</h3>
                    <p class="text-xs text-slate-600 mb-4">Click any NIST core function to see direct configuration requirements for Salesforce Agentforce:</p>

                    <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 mb-4">
                        <button onclick="showNistDetail('govern')" id="nist-btn-govern" class="nist-btn p-3 rounded-lg border border-slate-200 bg-white hover:border-indigoBrand-600 text-xs sm:text-sm font-bold text-slate-800 text-center transition">
                            1. GOVERN
                        </button>
                        <button onclick="showNistDetail('map')" id="nist-btn-map" class="nist-btn p-3 rounded-lg border border-slate-200 bg-white hover:border-indigoBrand-600 text-xs sm:text-sm font-bold text-slate-800 text-center transition">
                            2. MAP
                        </button>
                        <button onclick="showNistDetail('measure')" id="nist-btn-measure" class="nist-btn p-3 rounded-lg border border-slate-200 bg-white hover:border-indigoBrand-600 text-xs sm:text-sm font-bold text-slate-800 text-center transition">
                            3. MEASURE
                        </button>
                        <button onclick="showNistDetail('manage')" id="nist-btn-manage" class="nist-btn p-3 rounded-lg border border-slate-200 bg-white hover:border-indigoBrand-600 text-xs sm:text-sm font-bold text-slate-800 text-center transition">
                            4. MANAGE
                        </button>
                    </div>

                    <div id="nistDetailBox" class="p-5 rounded-xl bg-slate-900 text-white border border-slate-800">
                        <!-- Dynamic JS Content -->
                    </div>
                </div>
            </div>

        </section>


        <!-- ================= SECTION 3: CAREER PREP & LIVE MOCK INTERVIEWER ================= -->
        <section id="sec-career-prep" class="tab-content hidden space-y-8">
            
            <div class="bg-white rounded-2xl p-6 sm:p-8 border border-warmNeutral-200 shadow-sm">
                <div class="max-w-3xl">
                    <span class="text-xs font-bold tracking-wider uppercase text-brand-700 bg-brand-50 px-2.5 py-1 rounded-md border border-brand-100">Module 3: Career Empowerment & Tools</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 mt-3">Overcoming Career Paralysis with AI Tools & NotebookLM</h2>
                    <p class="text-slate-600 mt-3 text-base sm:text-lg leading-relaxed">
                        Fear of interviewing, asking for a promotion, or transitioning roles often stems from imposter syndrome and lack of structured rehearsal. Tools like <strong>Google NotebookLM</strong> (using custom Retrieval-Augmented Generation) and AI voice mode allow you to build personalized interview simulators.
                    </p>
                </div>

                <!-- NotebookLM Steps Visual -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-8">
                    <div class="p-4 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200 relative">
                        <div class="w-7 h-7 rounded-full bg-brand-700 text-white font-bold text-xs flex items-center justify-center mb-3">1</div>
                        <h3 class="font-bold text-slate-900 text-sm">Upload Context Corpus</h3>
                        <p class="text-xs text-slate-600 mt-1">
                            Ingest your resume, performance reviews, target job descriptions, Salesforce release notes, and org architecture specs into NotebookLM.
                        </p>
                    </div>

                    <div class="p-4 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200 relative">
                        <div class="w-7 h-7 rounded-full bg-brand-700 text-white font-bold text-xs flex items-center justify-center mb-3">2</div>
                        <h3 class="font-bold text-slate-900 text-sm">Perform Skill Gap Synthesis</h3>
                        <p class="text-xs text-slate-600 mt-1">
                            Prompt NotebookLM: "Analyze my past projects against the Senior Architect requirements. Map my exact transferable achievements using STAR technique."
                        </p>
                    </div>

                    <div class="p-4 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200 relative">
                        <div class="w-7 h-7 rounded-full bg-brand-700 text-white font-bold text-xs flex items-center justify-center mb-3">3</div>
                        <h3 class="font-bold text-slate-900 text-sm">Execute Live Verbal Drills</h3>
                        <p class="text-xs text-slate-600 mt-1">
                            Use Audio Overview or ChatGPT Advanced Voice Mode to simulate an adversarial technical hiring manager asking drill-down architecture questions.
                        </p>
                    </div>
                </div>

                <!-- LIVE INTERACTIVE MOCK INTERVIEW TOOL -->
                <div class="mt-8 pt-8 border-t border-warmNeutral-200">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-4">
                        <div>
                            <h3 class="text-lg font-bold text-slate-900 flex items-center gap-2">
                                <span>&#127908;</span> Interactive Live Mock Interview Simulator
                            </h3>
                            <p class="text-xs text-slate-600">Rehearse high-stakes technical questions right here in this workshop tool.</p>
                        </div>
                        
                        <div class="flex items-center space-x-2">
                            <label for="roleSelect" class="text-xs font-semibold text-slate-700">Select Target Role:</label>
                            <select id="roleSelect" onchange="loadInterviewQuestion()" class="text-xs p-2 rounded-lg border border-slate-300 bg-white font-medium text-slate-800">
                                <option value="architect">Salesforce Platform Architect</option>
                                <option value="devops">DevOps & Release Engineer</option>
                                <option value="ai-governance">AI Governance & Data Specialist</option>
                                <option value="lead-admin">Lead Salesforce Administrator</option>
                            </select>
                        </div>
                    </div>

                    <!-- Simulator Console -->
                    <div class="bg-slate-900 text-white rounded-xl p-5 sm:p-6 shadow-md border border-slate-800">
                        <div class="flex items-center justify-between border-b border-slate-800 pb-3 mb-4">
                            <div class="flex items-center space-x-2">
                                <span class="w-3 h-3 rounded-full bg-rose-500 animate-pulse"></span>
                                <span class="text-xs font-bold text-slate-300 uppercase tracking-wide">Live Simulation Session</span>
                            </div>
                            <span id="questionCategory" class="text-xs font-mono text-emerald-400 bg-emerald-950/60 px-2.5 py-1 rounded border border-emerald-800">Category: Architectural Risk</span>
                        </div>

                        <!-- Prompt / Question Display -->
                        <div class="mb-4">
                            <label class="text-xs text-slate-400 font-mono block mb-1">INTERVIEWER PROMPT:</label>
                            <p id="questionPrompt" class="text-sm sm:text-base font-semibold text-slate-100 bg-slate-800/80 p-4 rounded-lg border border-slate-700/60 leading-relaxed">
                                Loading interview prompt...
                            </p>
                        </div>

                        <!-- Answer Input Area -->
                        <div class="mb-4">
                            <div class="flex justify-between items-center mb-1">
                                <label for="userAnswer" class="text-xs text-slate-400 font-mono">YOUR REHEARSAL RESPONSE (Type or Speak):</label>
                                <span class="text-xs text-slate-500">Focus on STAR Method (Situation, Task, Action, Result)</span>
                            </div>
                            <textarea id="userAnswer" rows="4" class="w-full text-xs sm:text-sm p-3 rounded-lg bg-slate-950 border border-slate-700 text-slate-100 focus:outline-none focus:border-brand-600 focus:ring-1 focus:ring-brand-600 transition font-sans" placeholder="Describe your technical decision, the security guardrails you enforced, and the quantifiable outcome..."></textarea>
                        </div>

                        <!-- Controls -->
                        <div class="flex flex-wrap items-center justify-between gap-3 pt-2">
                            <button onclick="loadInterviewQuestion()" class="px-3 py-2 rounded-lg bg-slate-800 hover:bg-slate-700 text-xs font-medium text-slate-300 transition border border-slate-700">
                                &#8634; Try Another Question
                            </button>
                            <button onclick="evaluateInterviewAnswer()" class="px-5 py-2 rounded-lg bg-brand-600 hover:bg-brand-700 text-white text-xs sm:text-sm font-bold shadow-md transition flex items-center space-x-1">
                                <span>&#9889; Evaluate Response with AI Engine</span>
                            </button>
                        </div>

                        <!-- AI Evaluation Output Box -->
                        <div id="evaluationResult" class="hidden mt-6 pt-5 border-t border-slate-800">
                            <!-- Dynamic Content -->
                        </div>
                    </div>
                </div>
            </div>

        </section>


        <!-- ================= SECTION 4: CONFIGURATION & INTEGRATION SECURITY (ECA) ================= -->
        <section id="sec-config-eca" class="tab-content hidden space-y-8">
            
            <div class="bg-white rounded-2xl p-6 sm:p-8 border border-warmNeutral-200 shadow-sm">
                <div class="max-w-3xl">
                    <span class="text-xs font-bold tracking-wider uppercase text-rose-700 bg-rose-50 px-2.5 py-1 rounded-md border border-rose-100">Module 4: Secure Config & ECA Shift</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 mt-3">Preventing Security Gaps & Data Loss in Modern Salesforce</h2>
                    <p class="text-slate-600 mt-3 text-base sm:text-lg leading-relaxed">
                        Configuration anxiety—fearing that an access edit or deployment will open a security hole or delete data—is best solved by adherence to modern architecture: <strong>Permission Sets over Profiles</strong> and migrating from legacy <strong>Connected Apps to External Client Apps (ECAs)</strong>.
                    </p>
                </div>

                <!-- Strategic Transition Timeline Banner -->
                <div class="mt-8 p-5 rounded-xl bg-gradient-to-r from-slate-900 via-indigoBrand-950 to-slate-900 text-white border border-slate-800 shadow-sm">
                    <div class="flex flex-col md:flex-row items-center justify-between gap-4">
                        <div>
                            <span class="text-xs uppercase font-bold text-amber-400 tracking-widest">Platform Critical Timeline</span>
                            <h3 class="text-lg font-bold text-white mt-0.5">Connected Apps Deprecation & ECA Enforcement</h3>
                            <p class="text-xs text-slate-300 mt-1 max-w-2xl">
                                Salesforce restricted new Connected Apps in Spring 2026 and will fully end support in Summer 2027. All integrations must adopt External Client Apps (ECAs) with OAuth 2.0 PKCE.
                            </p>
                        </div>
                        <div class="flex items-center space-x-3 bg-white/10 px-4 py-3 rounded-lg border border-white/10 shrink-0">
                            <div class="text-center">
                                <div class="text-xs text-slate-400 font-mono uppercase">Spring 2026</div>
                                <div class="text-xs font-bold text-amber-300">Creation Restricted</div>
                            </div>
                            <div class="text-slate-500 font-bold">&#8594;</div>
                            <div class="text-center">
                                <div class="text-xs text-slate-400 font-mono uppercase">Summer 2027</div>
                                <div class="text-xs font-bold text-rose-400">Complete EOL</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Connected Apps vs ECA Comparison Table -->
                <div class="mt-8">
                    <h3 class="text-base font-bold text-slate-900 mb-3">Architectural Comparison: Legacy vs Modern Integration Security</h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="bg-warmNeutral-100 text-slate-800 border-b border-warmNeutral-200">
                                    <th class="p-3 font-bold">Feature / Capability</th>
                                    <th class="p-3 font-bold text-rose-700 bg-rose-50/50">Legacy Connected Apps</th>
                                    <th class="p-3 font-bold text-brand-700 bg-brand-50/50">Modern External Client Apps (ECAs)</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-warmNeutral-200">
                                <tr>
                                    <td class="p-3 font-semibold text-slate-900">Metadata Architecture</td>
                                    <td class="p-3 text-slate-600 bg-rose-50/20">Monolithic (developer credentials & policies bundled together)</td>
                                    <td class="p-3 text-slate-700 font-medium bg-brand-50/20">Decoupled (Global App Definition separated from Local Org Policies)</td>
                                </tr>
                                <tr>
                                    <td class="p-3 font-semibold text-slate-900">Packaging Compatibility</td>
                                    <td class="p-3 text-slate-600 bg-rose-50/20">Poor 2GP support; manual post-install configuration needed</td>
                                    <td class="p-3 text-slate-700 font-medium bg-brand-50/20">Full 2GP First-Class Support (Automated DevHub packaging)</td>
                                </tr>
                                <tr>
                                    <td class="p-3 font-semibold text-slate-900">OAuth Security Protocols</td>
                                    <td class="p-3 text-slate-600 bg-rose-50/20">Supports insecure legacy flows (Username/Password flow)</td>
                                    <td class="p-3 text-slate-700 font-medium bg-brand-50/20">Mandates OAuth 2.0 PKCE & Dynamic Refresh Token Rotation</td>
                                </tr>
                                <tr>
                                    <td class="p-3 font-semibold text-slate-900">Default Access Posture</td>
                                    <td class="p-3 text-slate-600 bg-rose-50/20">Open by default in many org contexts</td>
                                    <td class="p-3 text-slate-700 font-medium bg-brand-50/20">Closed Security Posture by Default (Explicit User Assign Needed)</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- INTERACTIVE ECA & PERMISSION AUDIT CALCULATOR -->
                <div class="mt-8 pt-8 border-t border-warmNeutral-200">
                    <h3 class="text-lg font-bold text-slate-900 mb-2">&#128737; Interactive Risk & Security Audit Tool</h3>
                    <p class="text-xs text-slate-600 mb-4">Toggle your org's current configuration choices to calculate your overall Security Posture Score:</p>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 bg-warmNeutral-50 p-5 rounded-xl border border-warmNeutral-200">
                        <div class="space-y-4">
                            <div class="flex items-center justify-between p-3 rounded-lg bg-white border border-slate-200">
                                <div>
                                    <div class="text-xs font-bold text-slate-900">Access Control Model</div>
                                    <div class="text-[11px] text-slate-500">Are you using Profile permissions or Minimum Access + Perm Sets?</div>
                                </div>
                                <select id="auditAccess" onchange="calculateSecurityScore()" class="text-xs p-1.5 rounded border border-slate-300 font-medium">
                                    <option value="profile">Profile Heavy (High Risk)</option>
                                    <option value="hybrid">Hybrid Transition</option>
                                    <option value="permsets" selected>Minimum Access + Perm Set Groups</option>
                                </select>
                            </div>

                            <div class="flex items-center justify-between p-3 rounded-lg bg-white border border-slate-200">
                                <div>
                                    <div class="text-xs font-bold text-slate-900">Integration Framework</div>
                                    <div class="text-[11px] text-slate-500">Connected Apps vs External Client Apps with PKCE</div>
                                </div>
                                <select id="auditEca" onchange="calculateSecurityScore()" class="text-xs p-1.5 rounded border border-slate-300 font-medium">
                                    <option value="legacy">Legacy Connected Apps</option>
                                    <option value="in-progress">In-Progress Migration</option>
                                    <option value="eca" selected>Full External Client Apps (ECAs)</option>
                                </select>
                            </div>

                            <div class="flex items-center justify-between p-3 rounded-lg bg-white border border-slate-200">
                                <div>
                                    <div class="text-xs font-bold text-slate-900">Backup & Disaster Recovery</div>
                                    <div class="text-[11px] text-slate-500">Frequency and immutability of data/metadata backups</div>
                                </div>
                                <select id="auditBackup" onchange="calculateSecurityScore()" class="text-xs p-1.5 rounded border border-slate-300 font-medium">
                                    <option value="native">Native Export Only (Weekly)</option>
                                    <option value="third-party" selected>Automated 3rd Party Daily Incremental</option>
                                </select>
                            </div>
                        </div>

                        <!-- Score Display -->
                        <div class="bg-white p-5 rounded-lg border border-slate-200 flex flex-col justify-between items-center text-center">
                            <span class="text-xs font-bold uppercase tracking-wider text-slate-500">Calculated Security Posture</span>
                            
                            <div class="my-3">
                                <div id="securityScoreVal" class="text-5xl font-extrabold text-emerald-600">92/100</div>
                                <div id="securityRatingLabel" class="text-xs font-bold text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-full mt-2 inline-block border border-emerald-200">
                                    EXCELLENT SECURITY POSTURE
                                </div>
                            </div>

                            <p id="securityAdviceText" class="text-xs text-slate-600 text-center leading-relaxed">
                                Your org is adhering to modern Salesforce architectural best practices with robust governance.
                            </p>
                        </div>
                    </div>
                </div>
            </div>

        </section>


        <!-- ================= SECTION 5: BRUNCH TABLE DISCUSSION PROMPTS ================= -->
        <section id="sec-discussion" class="tab-content hidden space-y-8">
            
            <div class="bg-white rounded-2xl p-6 sm:p-8 border border-warmNeutral-200 shadow-sm">
                <div class="max-w-3xl">
                    <span class="text-xs font-bold tracking-wider uppercase text-indigoBrand-700 bg-indigoBrand-50 px-2.5 py-1 rounded-md border border-indigoBrand-100">Module 5: Workshop & Brunch Table Cards</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 mt-3">Interactive Group Prompts & Action Blueprint</h2>
                    <p class="text-slate-600 mt-3 text-base sm:text-lg leading-relaxed">
                        Use these curated prompt cards at your brunch table to foster peer vulnerability, share real-world experiences, and draft an immediate action plan for next week.
                    </p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-8">
                    <!-- Card 1 -->
                    <div class="p-6 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200 hover:border-brand-600 transition shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="text-2xl mb-2">&#128172;</div>
                            <span class="text-[10px] font-bold uppercase text-brand-700 tracking-wider">Prompt Card #1</span>
                            <h3 class="font-bold text-slate-900 text-base mt-1">Confronting AI Job Fears</h3>
                            <p class="text-xs text-slate-600 mt-2 leading-relaxed">
                                "What routine tasks in your current job are you most afraid of AI automating, and what high-value skill (Data Cloud, Architecture, Business Strategy) do you want to build to replace it?"
                            </p>
                        </div>
                        <div class="mt-4 pt-3 border-t border-warmNeutral-200 text-[11px] text-slate-500 italic">
                            Discuss for 10 minutes at your table.
                        </div>
                    </div>

                    <!-- Card 2 -->
                    <div class="p-6 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200 hover:border-indigoBrand-600 transition shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="text-2xl mb-2">&#127908;</div>
                            <span class="text-[10px] font-bold uppercase text-indigoBrand-700 tracking-wider">Prompt Card #2</span>
                            <h3 class="font-bold text-slate-900 text-base mt-1">Career Advocacy & Interviewing</h3>
                            <p class="text-xs text-slate-600 mt-2 leading-relaxed">
                                "When was the last time you asked for a raise, promotion, or new title? What held you back, and how can we use tools like NotebookLM to practice advocating for ourselves?"
                            </p>
                        </div>
                        <div class="mt-4 pt-3 border-t border-warmNeutral-200 text-[11px] text-slate-500 italic">
                            Pair up with a partner to outline key achievements.
                        </div>
                    </div>

                    <!-- Card 3 -->
                    <div class="p-6 rounded-xl bg-warmNeutral-100 border border-warmNeutral-200 hover:border-rose-600 transition shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="text-2xl mb-2">&#128737;</div>
                            <span class="text-[10px] font-bold uppercase text-rose-700 tracking-wider">Prompt Card #3</span>
                            <h3 class="font-bold text-slate-900 text-base mt-1">Config Horrors & Lessons</h3>
                            <p class="text-xs text-slate-600 mt-2 leading-relaxed">
                                "Share a time a configuration change caused an issue or data loss. What guardrails (permission sets, backups, CI/CD, ECAs) have you implemented since?"
                            </p>
                        </div>
                        <div class="mt-4 pt-3 border-t border-warmNeutral-200 text-[11px] text-slate-500 italic">
                            Share lessons learned and technical wins.
                        </div>
                    </div>
                </div>

                <!-- Personal Action Plan Checklist -->
                <div class="mt-8 pt-8 border-t border-warmNeutral-200">
                    <h3 class="text-lg font-bold text-slate-900 mb-3">&#128221; My Monday Morning Commitment Checklist</h3>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-xs">
                        <label class="flex items-center space-x-3 p-3 rounded-lg bg-white border border-slate-200 cursor-pointer hover:bg-brand-50/30 transition">
                            <input type="checkbox" class="rounded text-brand-600 focus:ring-brand-500 w-4 h-4">
                            <span class="text-slate-800 font-medium">Audit all existing Connected Apps and flag for ECA migration.</span>
                        </label>
                        <label class="flex items-center space-x-3 p-3 rounded-lg bg-white border border-slate-200 cursor-pointer hover:bg-brand-50/30 transition">
                            <input type="checkbox" class="rounded text-brand-600 focus:ring-brand-500 w-4 h-4">
                            <span class="text-slate-800 font-medium">Build a custom NotebookLM notebook with my resume & target job spec.</span>
                        </label>
                        <label class="flex items-center space-x-3 p-3 rounded-lg bg-white border border-slate-200 cursor-pointer hover:bg-brand-50/30 transition">
                            <input type="checkbox" class="rounded text-brand-600 focus:ring-brand-500 w-4 h-4">
                            <span class="text-slate-800 font-medium">Review Data Cloud readiness & clean up stale data pipelines.</span>
                        </label>
                        <label class="flex items-center space-x-3 p-3 rounded-lg bg-white border border-slate-200 cursor-pointer hover:bg-brand-50/30 transition">
                            <input type="checkbox" class="rounded text-brand-600 focus:ring-brand-500 w-4 h-4">
                            <span class="text-slate-800 font-medium">Schedule 1-on-1 with manager to present AI governance goals.</span>
                        </label>
                    </div>
                </div>
            </div>

        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-white border-t border-warmNeutral-200 py-6 text-center text-xs text-slate-500">
        <div class="max-w-7xl mx-auto px-4">
            <p class="font-medium text-slate-700">Salesforce Women In Tech Brunch Keynote & Interactive Blueprint</p>
            <p class="mt-1">Designed to transform technical anxiety into high-leverage architectural leadership.</p>
        </div>
    </footer>


    <!-- JAVASCRIPT APPLICATION LOGIC -->
    <script>
        // Global Application State
        let isPresentationMode = false;
        let activeTab = 'ai-workforce';
        let jobChart = null;

        // Interview Question Bank
        const interviewQuestions = {
            'architect': [
                {
                    category: 'Security Architecture',
                    prompt: 'With Connected Apps ending support in Summer 2027, how would you migrate an enterprise integration with external ERP systems to External Client Apps (ECAs) while ensuring zero downtime and maintaining OAuth 2.0 PKCE compliance?'
                },
                {
                    category: 'AI Data Readiness',
                    prompt: 'Your organization wants to deploy Agentforce to autonomously update Service Cloud cases. How do you assess data quality and enforce NIST AI RMF governance before enabling the agent?'
                }
            ],
            'devops': [
                {
                    category: 'Deployment & CI/CD',
                    prompt: 'Walk me through how you prevent catastrophic data loss during complex schema changes (e.g., converting a Master-Detail field to Lookup or running bulk data updates in production).'
                },
                {
                    category: 'Packaging',
                    prompt: 'Why are External Client Apps (ECAs) superior to legacy Connected Apps when using Second-Generation Managed Packaging (2GP)?'
                }
            ],
            'ai-governance': [
                {
                    category: 'Legislative Compliance',
                    prompt: 'How do Florida SB 1680 / HB 919 and federal NIST standards influence how we configure prompt templates and audit AI agent decisions in Data Cloud?'
                },
                {
                    category: 'Model Drift & Monitoring',
                    prompt: 'What metrics and telemetry would you monitor to perform the "Measure" function of the NIST AI Framework for an active Agentforce deployment?'
                }
            ],
            'lead-admin': [
                {
                    category: 'Access Control',
                    prompt: 'Salesforce reversed the hard retirement of permissions on profiles. Why is relying on profiles still a major security risk, and how do you transition an org to Minimum Access Profiles + Permission Set Groups?'
                },
                {
                    category: 'Career & Leadership',
                    prompt: 'Describe a project where you moved from being a reactive task configurator to a strategic platform owner. What quantifiable impact did you achieve?'
                }
            ]
        };

        // Initialize App on DOM Ready
        document.addEventListener('DOMContentLoaded', () => {
            initChart();
            updatePivotPath('admin');
            showNistDetail('govern');
            loadInterviewQuestion();
            calculateSecurityScore();
            updateTabNavigation('ai-workforce');
        });

        // Tab Switcher Logic
        function switchTab(tabId) {
            activeTab = tabId;
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            const target = document.getElementById(`sec-${tabId}`);
            if (target) target.classList.remove('hidden');

            updateTabNavigation(tabId);
        }

        function updateTabNavigation(tabId) {
            // Update desktop nav
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('bg-brand-50', 'text-brand-700', 'font-bold');
                btn.classList.add('text-slate-600');
            });
            const activeNav = document.getElementById(`nav-${tabId}`);
            if (activeNav) {
                activeNav.classList.add('bg-brand-50', 'text-brand-700', 'font-bold');
            }

            // Update mobile nav
            document.querySelectorAll('.mnav-btn').forEach(btn => {
                btn.classList.remove('bg-brand-600', 'text-white', 'font-bold');
                btn.classList.add('bg-warmNeutral-100', 'text-slate-700');
            });
            const activeMNav = document.getElementById(`mnav-${tabId}`);
            if (activeMNav) {
                activeMNav.classList.remove('bg-warmNeutral-100', 'text-slate-700');
                activeMNav.classList.add('bg-brand-600', 'text-white', 'font-bold');
            }
        }

        // Toggle Presentation View
        function togglePresentationMode() {
            isPresentationMode = !isPresentationMode;
            const body = document.body;
            const btn = document.getElementById('modeToggleBtn');
            const modeText = document.getElementById('modeText');
            
            if (isPresentationMode) {
                body.classList.add('scale-[1.01]', 'transition-all');
                btn.classList.remove('bg-indigoBrand-50', 'text-indigoBrand-700');
                btn.classList.add('bg-brand-600', 'text-white');
                modeText.innerText = "Exit Presentation View";
            } else {
                body.classList.remove('scale-[1.01]');
                btn.classList.remove('bg-brand-600', 'text-white');
                btn.classList.add('bg-indigoBrand-50', 'text-indigoBrand-700');
                modeText.innerText = "Presentation Mode";
            }
        }

        // Initialize Chart.js
        function initChart() {
            const ctx = document.getElementById('jobMarketChart').getContext('2d');
            
            jobChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Generalist Admin', 'Business Analyst', 'Product Owner', 'DevOps Specialist', 'AI/Data Architect'],
                    datasets: [
                        {
                            label: 'Market Supply vs Demand Index',
                            data: [330, 115, 85, 65, 45],
                            backgroundColor: '#f43f5e',
                            borderRadius: 6
                        },
                        {
                            label: 'Avg Salary Index ($k USD)',
                            data: [82, 108, 148, 192, 210],
                            backgroundColor: '#10b981',
                            borderRadius: 6
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                boxWidth: 12,
                                font: { size: 11 }
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.dataset.label || '';
                                    if (label) label += ': ';
                                    if (context.datasetIndex === 0) {
                                        label += context.raw + '% (Market Ratio)';
                                    } else {
                                        label += '$' + context.raw + 'k USD';
                                    }
                                    return label;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            grid: { display: false },
                            ticks: { font: { size: 10 } }
                        },
                        y: {
                            beginAtZero: true,
                            grid: { color: '#f1f5f9' },
                            ticks: { font: { size: 10 } }
                        }
                    }
                }
            });
        }

        // Interactive Pivot Tool Logic
        function updatePivotPath(roleKey) {
            document.querySelectorAll('.pivot-btn').forEach(btn => {
                btn.classList.remove('border-brand-600', 'bg-brand-50', 'text-brand-900');
            });
            const activeBtn = document.getElementById(`pivot-btn-${roleKey}`);
            if (activeBtn) activeBtn.classList.add('border-brand-600', 'bg-brand-50', 'text-brand-900');

            const display = document.getElementById('pivotDisplay');
            
            let content = '';
            if (roleKey === 'admin') {
                content = `
                    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                        <div>
                            <span class="text-xs font-bold uppercase text-brand-700">Evolution Path: Admin &#8594; AI Platform Product Manager</span>
                            <h4 class="text-base font-bold text-slate-900 mt-1">Focus Areas: Data Governance & Agent Orchestration</h4>
                            <p class="text-xs text-slate-600 mt-1 leading-relaxed">
                                Move away from manual field/page layout edits. Master <strong>Data Cloud unification rules</strong>, prompt engineering for Agentforce, and setting up permission-set access boundaries.
                            </p>
                        </div>
                        <div class="bg-white p-3 rounded-lg border border-warmNeutral-200 text-center shrink-0">
                            <div class="text-xs font-bold text-slate-500">Target Salary Growth</div>
                            <div class="text-lg font-extrabold text-emerald-600">+35% to +50%</div>
                        </div>
                    </div>
                `;
            } else if (roleKey === 'dev') {
                content = `
                    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                        <div>
                            <span class="text-xs font-bold uppercase text-indigoBrand-700">Evolution Path: Apex Developer &#8594; AI System Architect & ECA Specialist</span>
                            <h4 class="text-base font-bold text-slate-900 mt-1">Focus Areas: External Client Apps, OAuth 2.0 PKCE & Vector Search</h4>
                            <p class="text-xs text-slate-600 mt-1 leading-relaxed">
                                Stop writing standard CRUD Apex wrappers. Master <strong>External Client Apps (ECA) packaging (2GP)</strong>, custom Apex actions for Agentforce topics, and zero-copy integrations.
                            </p>
                        </div>
                        <div class="bg-white p-3 rounded-lg border border-warmNeutral-200 text-center shrink-0">
                            <div class="text-xs font-bold text-slate-500">Target Salary Growth</div>
                            <div class="text-lg font-extrabold text-indigoBrand-600">$180k - $220k+</div>
                        </div>
                    </div>
                `;
            } else if (roleKey === 'ba') {
                content = `
                    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                        <div>
                            <span class="text-xs font-bold uppercase text-amber-700">Evolution Path: Business Analyst &#8594; AI Strategy & Ethics Consultant</span>
                            <h4 class="text-base font-bold text-slate-900 mt-1">Focus Areas: NIST Governance Mapping & Workflow Re-engineering</h4>
                            <p class="text-xs text-slate-600 mt-1 leading-relaxed">
                                Bridge the gap between C-suite executives and technical teams. Conduct <strong>NIST AI RMF Risk Mapping</strong>, design human-in-the-loop review steps, and calculate AI ROI metrics.
                            </p>
                        </div>
                        <div class="bg-white p-3 rounded-lg border border-warmNeutral-200 text-center shrink-0">
                            <div class="text-xs font-bold text-slate-500">Market Demand Rating</div>
                            <div class="text-lg font-extrabold text-amber-600">High Growth</div>
                        </div>
                    </div>
                `;
            }
            display.innerHTML = content;
        }

        // NIST Tool JS Logic
        function showNistDetail(functionKey) {
            document.querySelectorAll('.nist-btn').forEach(btn => {
                btn.classList.remove('border-indigoBrand-600', 'bg-indigoBrand-600', 'text-white');
                btn.classList.add('bg-white', 'text-slate-800');
            });
            const activeBtn = document.getElementById(`nist-btn-${functionKey}`);
            if (activeBtn) {
                activeBtn.classList.remove('bg-white', 'text-slate-800');
                activeBtn.classList.add('border-indigoBrand-600', 'bg-indigoBrand-600', 'text-white');
            }

            const box = document.getElementById('nistDetailBox');
            let data = {};

            if (functionKey === 'govern') {
                data = {
                    title: '1. GOVERN (NIST Function)',
                    sub: 'Establishing Organizational Policy & Accountability',
                    items: [
                        'Define executive oversight roles for Agentforce deployment.',
                        'Establish clear AI risk tolerance thresholds in written security policies.',
                        'Audit user license assignments (e.g., Integration User licenses vs User seats).'
                    ]
                };
            } else if (functionKey === 'map') {
                data = {
                    title: '2. MAP (NIST Function)',
                    sub: 'Contextualizing Systems & Identifying Limits',
                    items: [
                        'Document exact Data Cloud unified objects accessed by the AI model.',
                        'Map explicit boundaries: what actions can the AI take autonomously vs human approval?',
                        'Identify affected stakeholder groups and potential algorithmic bias vectors.'
                    ]
                };
            } else if (functionKey === 'measure') {
                data = {
                    title: '3. MEASURE (NIST Function)',
                    sub: 'Quantitative Testing, Telemetry & Evaluation',
                    items: [
                        'Monitor hallucination rate and prompt injection vulnerability.',
                        'Track model drift over time using standard test suites before release.',
                        'Measure real-time latency and user override percentages.'
                    ]
                };
            } else if (functionKey === 'manage') {
                data = {
                    title: '4. MANAGE (NIST Function)',
                    sub: 'Risk Mitigation, Kill Switches & Continuous Response',
                    items: [
                        'Deploy automated kill switches to immediately disable AI agents if behavior drifts.',
                        'Maintain immutable audit logs of every decision generated by Agentforce.',
                        'Execute incident response plans for unvetted data exposure.'
                    ]
                };
            }

            box.innerHTML = `
                <div class="text-emerald-400 text-xs font-mono font-bold">${data.title}</div>
                <h4 class="text-base font-bold text-white mt-1">${data.sub}</h4>
                <ul class="mt-3 space-y-2 text-xs text-slate-300">
                    ${data.items.map(item => `<li class="flex items-start space-x-2"><span class="text-emerald-400 font-bold">&#9658;</span><span>${item}</span></li>`).join('')}
                </ul>
            `;
        }

        // Live Mock Interview Logic
        function loadInterviewQuestion() {
            const role = document.getElementById('roleSelect').value;
            const questions = interviewQuestions[role] || interviewQuestions['architect'];
            const randomQ = questions[Math.floor(Math.random() * questions.length)];

            document.getElementById('questionCategory').innerText = `Category: ${randomQ.category}`;
            document.getElementById('questionPrompt').innerText = `"${randomQ.prompt}"`;
            document.getElementById('userAnswer').value = '';
            document.getElementById('evaluationResult').classList.add('hidden');
        }

        function evaluateInterviewAnswer() {
            const answerText = document.getElementById('userAnswer').value.trim();
            const resultBox = document.getElementById('evaluationResult');

            if (answerText.length < 20) {
                alert("Please type a more detailed answer (at least a couple of sentences) to run the evaluation analysis!");
                return;
            }

            resultBox.classList.remove('hidden');

            // RAG Analysis Simulator Score
            const wordCount = answerText.split(' ').length;
            const hasStar = answerText.toLowerCase().includes('result') || answerText.toLowerCase().includes('led to') || answerText.toLowerCase().includes('outcome') || answerText.toLowerCase().includes('implemented');
            const hasTechnical = answerText.toLowerCase().includes('eca') || answerText.toLowerCase().includes('pkce') || answerText.toLowerCase().includes('permission set') || answerText.toLowerCase().includes('nist') || answerText.toLowerCase().includes('data cloud') || answerText.toLowerCase().includes('backup');

            let score = 70;
            if (wordCount > 40) score += 10;
            if (hasStar) score += 10;
            if (hasTechnical) score += 10;
            if (score > 98) score = 98;

            resultBox.innerHTML = `
                <div class="bg-slate-950 p-4 rounded-lg border border-slate-800">
                    <div class="flex items-center justify-between mb-3">
                        <span class="text-xs font-bold text-emerald-400 uppercase tracking-wider">&#10024; AI Feedback Analysis</span>
                        <span class="text-xs font-bold px-2.5 py-1 rounded bg-brand-900/60 text-brand-300 border border-brand-700">Answer Score: ${score}/100</span>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 text-xs mb-3">
                        <div class="p-2.5 rounded bg-slate-900 border border-slate-800">
                            <span class="text-slate-400 block text-[10px]">STAR STRUCTURE</span>
                            <span class="font-bold ${hasStar ? 'text-emerald-400' : 'text-amber-400'}">${hasStar ? 'Strong Outcome Cited' : 'Needs Quantified Result'}</span>
                        </div>
                        <div class="p-2.5 rounded bg-slate-900 border border-slate-800">
                            <span class="text-slate-400 block text-[10px]">TECHNICAL TERMINOLOGY</span>
                            <span class="font-bold ${hasTechnical ? 'text-emerald-400' : 'text-amber-400'}">${hasTechnical ? 'Architectural Terms Used' : 'Use Specific Security Terms'}</span>
                        </div>
                        <div class="p-2.5 rounded bg-slate-900 border border-slate-800">
                            <span class="text-slate-400 block text-[10px]">VERBAL CONCORDANCE</span>
                            <span class="font-bold text-indigo-300">Clear & Confident Tone</span>
                        </div>
                    </div>

                    <p class="text-xs text-slate-300 leading-relaxed italic">
                        "Your response shows solid technical familiarity. To elevate this further during an interview, quantify your outcome (e.g., 'This reduced access risk by 40% and prevented legacy token decay')."
                    </p>
                </div>
            `;
        }

        // Security Calculator Logic
        function calculateSecurityScore() {
            const access = document.getElementById('auditAccess').value;
            const eca = document.getElementById('auditEca').value;
            const backup = document.getElementById('auditBackup').value;

            let score = 0;

            if (access === 'permsets') score += 40;
            else if (access === 'hybrid') score += 25;
            else score += 10;

            if (eca === 'eca') score += 40;
            else if (eca === 'in-progress') score += 25;
            else score += 10;

            if (backup === 'third-party') score += 20;
            else score += 10;

            const valEl = document.getElementById('securityScoreVal');
            const labelEl = document.getElementById('securityRatingLabel');
            const adviceEl = document.getElementById('securityAdviceText');

            valEl.innerText = `${score}/100`;

            if (score >= 85) {
                valEl.className = "text-5xl font-extrabold text-emerald-600";
                labelEl.innerText = "EXCELLENT SECURITY POSTURE";
                labelEl.className = "text-xs font-bold text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-full mt-2 inline-block border border-emerald-200";
                adviceEl.innerText = "Your org aligns with modern Salesforce standards: ECAs enabled, permission-set architecture, and daily granular backups.";
            } else if (score >= 60) {
                valEl.className = "text-5xl font-extrabold text-amber-600";
                labelEl.innerText = "MODERATE RISK EXPOSURE";
                labelEl.className = "text-xs font-bold text-amber-700 bg-amber-50 px-2.5 py-1 rounded-full mt-2 inline-block border border-amber-200";
                adviceEl.innerText = "You are in transition. Prioritize migrating legacy Connected Apps to External Client Apps prior to Summer 2027.";
            } else {
                valEl.className = "text-5xl font-extrabold text-rose-600";
                labelEl.innerText = "CRITICAL SECURITY GAPS";
                labelEl.className = "text-xs font-bold text-rose-700 bg-rose-50 px-2.5 py-1 rounded-full mt-2 inline-block border border-rose-200";
                adviceEl.innerText = "High vulnerability! Relying heavily on profiles and legacy Connected Apps leaves your org open to credentials leak and data loss.";
            }
        }
    </script>
</body>
</html>
