<!DOCTYPE html>
<html lang="ko" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>학업 중단 예방 시스템 비교 분석: 한국 vs 독일</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm & Inviting -->
    <!-- Application Structure Plan: 사용자의 이해를 돕기 위해 보고서 내용을 재구성한 서사적 흐름의 SPA를 설계했습니다. [1. 서론: 문제 제시] > [2. 한국의 숙려제 분석] > [3. 독일의 Frühwarnsystem 분석] > [4. 두 시스템 비교 분석] > [5. 결론 및 제언] 순으로 구성됩니다. 각 섹션은 스크롤 또는 상단 고정 내비게이션으로 이동할 수 있습니다. 이 구조는 사용자가 전체적인 맥락을 파악하고, 각 시스템을 개별적으로 학습한 후, 상호작용적인 비교를 통해 깊이 있는 통찰을 얻고, 최종적으로 미래 방향성을 이해하도록 유도하기 위해 선택되었습니다. -->
    <!-- Visualization & Content Choices: 
        - [보고서 전체] -> Goal: Inform/Compare -> Viz: 전체 SPA 구조 -> Interaction: 스크롤 및 내비게이션 -> Justification: 복잡한 보고서 내용을 주제별로 나누어 점진적으로 이해하도록 돕습니다.
        - [독일 학업 중단율] -> Goal: Inform -> Viz: Chart.js Donut Chart & Big Number -> Interaction: Hover -> Justification: 핵심 통계를 시각적으로 강조하여 문제의 심각성을 즉각적으로 전달합니다. (NO SVG)
        - [숙려제 운영 절차] -> Goal: Organize -> Viz: HTML/CSS 순서도 -> Interaction: 없음 -> Justification: 복잡한 법적 절차를 시각적인 단계로 표현하여 사용자가 쉽게 따라갈 수 있도록 합니다. (NO SVG/Mermaid)
        - [Frühwarnsystem 핵심 지표] -> Goal: Organize/Inform -> Viz: HTML/CSS 카드 레이아웃 -> Interaction: 없음 -> Justification: EWS의 핵심 개념을 세 개의 명확한 정보 블록으로 나누어 가독성을 높입니다. (NO SVG/Mermaid)
        - [두 시스템 비교] -> Goal: Compare/Analyze -> Viz: Chart.js Radar Chart & 인터랙티브 텍스트 블록 -> Interaction: 기준 클릭 시 내용 변경 -> Justification: 레이더 차트는 다차원적 특성을 한눈에 비교하게 해주고, 인터랙티브 텍스트는 상세 비교를 깔끔하게 제공하여 사용자의 인지 부하를 줄입니다. (NO SVG)
        - [정책 제언] -> Goal: Organize/Inform -> Viz: HTML/CSS 아코디언 -> Interaction: 클릭 시 펼치기/접기 -> Justification: 최종 제언들을 간결하게 제시하고, 사용자가 관심 있는 부분만 선택하여 자세히 볼 수 있게 합니다. (NO SVG)
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body { font-family: 'Noto Sans KR', sans-serif; background-color: #F5F5F5; color: #424242; }
        .chart-container { position: relative; width: 100%; max-width: 500px; margin-left: auto; margin-right: auto; height: 300px; max-height: 400px; }
        @media (min-width: 768px) { .chart-container { height: 350px; } }
        .nav-link.active { color: #5D4037; font-weight: 700; border-bottom-color: #8D6E63; }
        .flowchart-arrow { content: '→'; color: #A1887F; font-size: 2rem; font-weight: bold; }
        .accordion-content { max-height: 0; overflow: hidden; transition: max-height 0.5s ease-in-out; }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-3">
            <div class="flex justify-between items-center">
                <h1 class="text-lg md:text-xl font-bold text-gray-800">학업 중단 예방: 한국과 독일의 접근법</h1>
                <div id="nav-menu" class="hidden md:flex space-x-8 text-sm">
                    <a href="#intro" class="nav-link border-b-2 border-transparent transition hover:text-[#5D4037]">Einleitung</a>
                    <a href="#sookryeoje" class="nav-link border-b-2 border-transparent transition hover:text-[#5D4037]">숙려제</a>
                    <a href="#ews" class="nav-link border-b-2 border-transparent transition hover:text-[#5D4037]">Frühwarnsystem</a>
                    <a href="#comparison" class="nav-link border-b-2 border-transparent transition hover:text-[#5D4037]">Vergleich</a>
                    <a href="#conclusion" class="nav-link border-b-2 border-transparent transition hover:text-[#5D4037]">Schlussfolgerung</a>
                </div>
            </div>
        </nav>
    </header>

    <main>
        <section id="intro" class="py-16 md:py-20 text-center container mx-auto px-6">
            <h2 class="text-3xl md:text-4xl font-bold mb-4">학업 중단 (*Schulabbruch*), 어떻게 막을 것인가?</h2>
            <p class="text-md md:text-lg max-w-3xl mx-auto mb-12 text-gray-600">학업 중단은 개인과 사회에 막대한 비용을 초래하는 전 세계적 과제입니다. 본 인포그래픽은 한국의 인간 중심 숙고 모델 '숙려제'와 독일의 데이터 기반 예측 시스템 '*Frühwarnsystem*'을 심층 비교하여 효과적인 예방 전략을 모색합니다.</p>
            <div class="bg-white rounded-lg shadow-md p-6 md:p-8 grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div class="chart-container h-56 md:h-auto">
                    <canvas id="dropout-chart"></canvas>
                </div>
                <div class="text-left md:text-center">
                    <h3 class="text-xl md:text-2xl font-bold mb-2">독일의 학업 중단 현황 (2022년)</h3>
                    <p class="text-5xl md:text-6xl font-bold text-[#8D6E63] mb-4">6.9%</p>
                    <p class="text-gray-600">독일의 청소년 학업 중단율은 2022년 기준 6.9%로, 여전히 많은 학생들이 정규 교육과정을 마치지 못하고 있습니다. 이는 개인과 사회에 막대한 비용을 초래하는 심각한 문제입니다.</p>
                </div>
            </div>
        </section>

        <section id="sookryeoje" class="py-16 md:py-20 bg-gray-200">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <span class="text-sm font-bold uppercase text-[#A1887F]">REAKTIVER & MENSCHENZENTRIERTER ANSATZ</span>
                    <h2 class="text-3xl md:text-4xl font-bold mt-2">한국의 학업중단 숙려제</h2>
                    <p class="text-md md:text-lg max-w-3xl mx-auto mt-4 text-gray-600">위기 징후가 나타난 학생에게 숙고의 시간(*Bedenkzeit*)을 부여하고, 인간 중심의 맞춤형 지원을 제공합니다.</p>
                </div>
                <div class="bg-white rounded-lg shadow-md p-6 md:p-8">
                     <h3 class="text-xl md:text-2xl font-bold text-center mb-8">운영 절차 (Betriebsverfahren)</h3>
                     <div class="flex flex-col md:flex-row justify-center items-center space-y-4 md:space-y-0 md:space-x-4">
                        <div class="p-4 bg-amber-50 rounded-lg text-center w-full md:w-1/3 shadow-sm border-t-4 border-[#A1887F]">
                            <p class="text-2xl font-bold text-[#8D6E63]">1</p>
                            <h4 class="font-bold mt-1">발견 및 준비</h4>
                            <p class="text-sm text-gray-600 mt-1">위기 징후 발견 또는 학생의 의사 표현 → 학업중단예방위원회 구성 및 숙려제 안내</p>
                        </div>
                        <div class="flowchart-arrow transform md:rotate-0 rotate-90"></div>
                        <div class="p-4 bg-amber-50 rounded-lg text-center w-full md:w-1/3 shadow-sm border-t-4 border-[#A1887F]">
                            <p class="text-2xl font-bold text-[#8D6E63]">2</p>
                            <h4 class="font-bold mt-1">운영 및 지원</h4>
                            <p class="text-sm text-gray-600 mt-1">최소 1주~최대 7주 숙려 기간 부여 → 맞춤형 프로그램 제공 (출석 인정)</p>
                        </div>
                        <div class="flowchart-arrow transform md:rotate-0 rotate-90"></div>
                         <div class="p-4 bg-amber-50 rounded-lg text-center w-full md:w-1/3 shadow-sm border-t-4 border-[#A1887F]">
                            <p class="text-2xl font-bold text-[#8D6E63]">3</p>
                            <h4 class="font-bold mt-1">완료 및 연계</h4>
                            <p class="text-sm text-gray-600 mt-1">학업 복귀 시 지속 관리, 학업 중단 시 학교 밖 지원센터 의무 연계</p>
                        </div>
                     </div>
                </div>
            </div>
        </section>

        <section id="ews" class="py-16 md:py-20">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <span class="text-sm font-bold uppercase text-[#A1887F]">PROAKTIVER & DATENGESTÜTZTER ANSATZ</span>
                    <h2 class="text-3xl md:text-4xl font-bold mt-2">독일의 Frühwarnsystem</h2>
                    <p class="text-md md:text-lg max-w-3xl mx-auto mt-4 text-gray-600">문제가 발생하기 전, 데이터를 통해 위험을 예측하고 선제적으로 개입합니다.</p>
                </div>
                <div class="bg-white rounded-lg shadow-md p-6 md:p-8">
                    <h3 class="text-xl md:text-2xl font-bold text-center mb-8">핵심 예측 지표: "Die ABC-Indikatoren"</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
                        <div class="p-6 bg-gray-50 rounded-lg shadow-sm">
                            <p class="text-5xl font-bold mb-2 text-[#A1887F]">A</p>
                            <h4 class="text-xl font-bold mb-2">Anwesenheit</h4>
                            <p class="text-gray-600">(출석) 만성적 결석은 학업 참여도와 학교 연결성을 보여주는 가장 강력한 지표입니다.</p>
                        </div>
                        <div class="p-6 bg-gray-50 rounded-lg shadow-sm">
                            <p class="text-5xl font-bold mb-2 text-[#A1887F]">B</p>
                            <h4 class="text-xl font-bold mb-2">Verhalten</h4>
                            <p class="text-gray-600">(행동) 징계 기록 등은 학생의 학교 환경 적응 능력과 잠재적 어려움을 반영합니다.</p>
                        </div>
                        <div class="p-6 bg-gray-50 rounded-lg shadow-sm">
                             <p class="text-5xl font-bold mb-2 text-[#A1887F]">C</p>
                            <h4 class="text-xl font-bold mb-2">Kursleistung</h4>
                            <p class="text-gray-600">(학업 성과) 주요 과목의 낙제, 낮은 학점은 미래의 학업 실패를 직접적으로 예측합니다.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="comparison" class="py-16 md:py-20 bg-gray-200">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold">숙려제 vs Frühwarnsystem: Vergleichende Analyse</h2>
                    <p class="text-md md:text-lg max-w-3xl mx-auto mt-4 text-gray-600">두 시스템은 서로 다른 철학과 강점을 가집니다. 레이더 차트로 특징을 한눈에 비교하고, 아래 버튼을 눌러 상세 내용을 확인하세요.</p>
                </div>
                <div class="bg-white rounded-lg shadow-md p-6 md:p-8 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                    <div class="chart-container">
                        <canvas id="comparison-radar-chart"></canvas>
                    </div>
                    <div class="space-y-4" id="comparison-text-section">
                        <div id="comparison-buttons" class="flex flex-wrap gap-2 justify-center">
                        </div>
                        <div id="comparison-details" class="p-6 bg-amber-50 rounded-lg min-h-[150px] transition-all duration-300">
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="conclusion" class="py-16 md:py-20">
             <div class="container mx-auto px-6">
                 <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold">결론: 통합적 지원 생태계를 향하여</h2>
                    <p class="text-md md:text-lg max-w-3xl mx-auto mt-4 text-gray-600">*Frühwarnsystem*의 예측력과 숙려제의 인간 중심적 개입을 결합한 *Hybridmodell*은 가장 이상적인 학생 지원 생태계를 구축할 수 있습니다.</p>
                </div>
                 <div id="accordion" class="max-w-3xl mx-auto space-y-3">
                 </div>
             </div>
        </section>
    </main>

    <footer class="bg-gray-800 text-white py-8">
        <div class="container mx-auto px-6 text-center">
            <p class="text-sm">본 인포그래픽은 제공된 연구 보고서를 기반으로 제작되었습니다.</p>
            <p class="text-xs text-gray-400 mt-2">© 2025 Interactive Report. All Rights Reserved.</p>
        </div>
    </footer>

    <script>
    document.addEventListener('DOMContentLoaded', function () {
        const createTooltipCallback = () => ({
            plugins: {
                tooltip: {
                    callbacks: {
                        title: function(tooltipItems) {
                            const item = tooltipItems[0];
                            let label = item.chart.data.labels[item.dataIndex];
                            return Array.isArray(label) ? label.join(' ') : label;
                        }
                    }
                }
            }
        });

        const wrapLabel = (label) => {
            const maxLength = 16;
            if (typeof label !== 'string' || label.length <= maxLength) return label;
            const words = label.split(' ');
            const lines = [];
            let currentLine = '';
            words.forEach(word => {
                if ((currentLine + ' ' + word).trim().length > maxLength) {
                    lines.push(currentLine.trim());
                    currentLine = word;
                } else {
                    currentLine = (currentLine + ' ' + word).trim();
                }
            });
            if (currentLine) lines.push(currentLine);
            return lines;
        };

        new Chart(document.getElementById('dropout-chart'), {
            type: 'doughnut',
            data: {
                labels: ['학업 지속', '학업 중단'],
                datasets: [{
                    data: [93.1, 6.9],
                    backgroundColor: ['#8D6E63', '#E0E0E0'],
                    borderColor: '#F5F5F5',
                    borderWidth: 4,
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '70%',
                plugins: {
                    legend: { display: false },
                    tooltip: createTooltipCallback().plugins.tooltip
                }
            }
        });

        const radarLabels = ['선제성 (Proaktivität)', '인간중심성 (Menschlichkeit)', '확장성 (Skalierbarkeit)', '기술의존도 (Technikabhängigkeit)', '법적강제성 (Rechtszwang)', '개입의 깊이 (Interventionstiefe)'].map(wrapLabel);
        
        new Chart(document.getElementById('comparison-radar-chart'), {
            type: 'radar',
            data: {
                labels: radarLabels,
                datasets: [
                    {
                        label: '독일 Frühwarnsystem',
                        data: [9, 4, 8, 9, 8, 5],
                        borderColor: '#8D6E63',
                        backgroundColor: 'rgba(141, 110, 99, 0.2)',
                    },
                    {
                        label: '한국 숙려제',
                        data: [3, 9, 4, 2, 6, 8],
                        borderColor: '#A1887F',
                        backgroundColor: 'rgba(161, 136, 127, 0.2)',
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: { r: { beginAtZero: true, max: 10, pointLabels: { font: { size: 12 } }, ticks: { display: false } } },
                plugins: {
                    legend: { position: 'top' },
                    tooltip: createTooltipCallback().plugins.tooltip
                }
            }
        });

        const comparisonData = {
            '접근 방식': {
                title: 'Ansatz (접근 방식)',
                content: '<strong>독일 Frühwarnsystem:</strong> 예측 분석을 통한 선제적/통계적 위험 식별<br><strong>한국 숙려제:</strong> 명확한 위기 징후 및 의사 표현 기반의 반응적 식별'
            },
            '개입 시점': {
                title: 'Interventionszeitpunkt (개입 시점)',
                content: '<strong>독일 Frühwarnsystem:</strong> 문제가 발현되기 전, 가능한 이른 시점<br><strong>한국 숙려제:</strong> 위기 상황 발생 또는 의사 표명 후'
            },
            '데이터 초점': {
                title: 'Datenfokus (데이터 초점)',
                content: '<strong>독일 Frühwarnsystem:</strong> 정량적/예측적 데이터 (ABCs, 사회경제적 요인 등)<br><strong>한국 숙려제:</strong> 정성적/관찰 데이터 (교사 의견, 상담 내용 등)'
            },
            '법적 근거': {
                title: 'Rechtliche Grundlage (법적 근거)',
                content: '<strong>독일 Frühwarnsystem:</strong> *Schulpflicht* (의무 교육)에 기반한 강제성<br><strong>한국 숙려제:</strong> 법률에 따른 ‘숙려 기회’ 제공 및 출석 인정'
            }
        };

        const comparisonButtonsContainer = document.getElementById('comparison-buttons');
        const comparisonDetailsContainer = document.getElementById('comparison-details');
        Object.keys(comparisonData).forEach((key, index) => {
            const button = document.createElement('button');
            button.className = `px-4 py-2 rounded-full text-sm font-semibold transition ${index === 0 ? 'bg-[#8D6E63] text-white' : 'bg-white text-[#8D6E63] hover:bg-gray-100'}`;
            button.textContent = key;
            button.onclick = () => {
                document.querySelectorAll('#comparison-buttons button').forEach(btn => {
                    btn.className = 'px-4 py-2 rounded-full text-sm font-semibold transition bg-white text-[#8D6E63] hover:bg-gray-100';
                });
                button.className = 'px-4 py-2 rounded-full text-sm font-semibold transition bg-[#8D6E63] text-white';
                comparisonDetailsContainer.innerHTML = `<h4 class="font-bold text-lg mb-2 text-gray-800">${comparisonData[key].title}</h4><p class="text-gray-600">${comparisonData[key].content}</p>`;
            };
            comparisonButtonsContainer.appendChild(button);
            if (index === 0) button.click();
        });

        const accordionData = [
            { title: '제언 1: 예측 분석 통합', content: '숙려제 대상 학생을 더 조기에 식별하기 위해 EWS의 *prädiktive Analysen* 원칙을 도입하여 예방적 조치를 강화합니다.' },
            { title: '제언 2: 인간 중심 개입 강화', content: 'EWS 프레임워크에 숙려제의 맞춤형 상담, *Schulsozialarbeit*와 같은 인간 중심 요소를 도입하여 지원의 깊이를 더합니다.' },
            { title: '제언 3: 데이터 품질 및 윤리 확보', content: 'EWS 예측 모델의 데이터 품질을 높이고 알고리즘 편향(*Bias*)을 막으며, 숙려 과정이 진정성 있게 운영되도록 교직원 전문성을 개발합니다.' },
            { title: '제언 4: 다층적 지원 생태계 조성', content: 'EWS로 위험군을 선별하고, 숙려제로 집중 지원하는 다층적 지원 시스템(*mehrstufiges Unterstützungssystem*)을 구축합니다.' },
            { title: '제언 5: 지속적인 평가 및 개선', content: '두 시스템의 효과를 지속적으로 평가하고, 그 결과를 바탕으로 정책과 실천 방안을 끊임없이 개선해 나갑니다.' }
        ];

        const accordionContainer = document.getElementById('accordion');
        accordionData.forEach((item, index) => {
            const itemEl = document.createElement('div');
            itemEl.className = 'bg-white rounded-lg shadow-sm';
            itemEl.innerHTML = `
                <button class="w-full text-left p-4 flex justify-between items-center font-bold text-gray-700">
                    <span>${item.title}</span>
                    <span class="plus-icon text-[#A1887F] text-xl font-light transform transition-transform duration-300">+</span>
                </button>
                <div class="accordion-content px-4">
                    <p class="py-4 text-gray-600 border-t border-gray-200">${item.content}</p>
                </div>
            `;
            const button = itemEl.querySelector('button');
            const content = itemEl.querySelector('.accordion-content');
            const icon = button.querySelector('.plus-icon');
            button.addEventListener('click', () => {
                const isOpen = content.style.maxHeight !== '0px';
                if(isOpen){
                    content.style.maxHeight = '0px';
                    icon.classList.remove('rotate-45');
                } else {
                    content.style.maxHeight = content.scrollHeight + 'px';
                    icon.classList.add('rotate-45');
                }
            });
            accordionContainer.appendChild(itemEl);
        });
        
        const navLinks = document.querySelectorAll('.nav-link');
        const sections = document.querySelectorAll('main section');
        const onScroll = () => {
            let current = '';
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (pageYOffset >= sectionTop - 80) {
                    current = section.getAttribute('id');
                }
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href').substring(1) === current) {
                    link.classList.add('active');
                }
            });
        };
        window.addEventListener('scroll', onScroll);
        onScroll();
    });
    </script>
</body>
</html>
