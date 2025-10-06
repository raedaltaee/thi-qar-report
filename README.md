<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تقرير الأداء والتخطيط الاستراتيجي</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals (Cream, Slate, Muted Teal) -->
    <!-- Application Structure Plan: The application is designed as a single-page dashboard with five distinct, scrollable sections: 1. A main overview providing a snapshot of all divisions. 2. A detailed situational analysis to diagnose challenges and strengths. 3. A section for proposed solutions linked to the identified challenges. 4. A forward-looking strategic plan with clear goals. 5. A data analysis section explaining the methodology. This structure was chosen to guide the user logically from a high-level overview to diagnosis, solution, and future planning, which is a more intuitive and actionable flow than a static report. Navigation is facilitated by a sticky header, allowing easy movement between these interconnected analytical stages. -->
    <!-- Visualization & Content Choices: 
        - Overview: Goal: Inform. Method: HTML/CSS cards for a quick status summary of each division. Interaction: None, purely informational. Justification: Provides a quick, scannable entry point.
        - Situational Analysis: Goal: Compare & Diagnose. Method: A dynamic Bar Chart (Chart.js) to compare challenges across divisions, and dynamic HTML lists for specific challenges/strengths. Interaction: A dropdown filter to select a division, which updates both the chart highlighting and the text lists. Justification: Bar charts are excellent for quantitative comparison, and interactive filtering allows users to drill down into specific areas of concern.
        - Strategic Plan: Goal: Organize & Plan. Method: A visual timeline/roadmap built with HTML/Tailwind. Interaction: Hover effects on goals to display more information (if implemented). Justification: A timeline is a universally understood and effective way to present strategic goals over time.
        - Data Analysis: Goal: Inform on methodology. Method: A Doughnut Chart (Chart.js) to show the data maturity of each division's database. Interaction: Hover tooltips on chart segments. Justification: A doughnut chart is ideal for showing part-to-whole relationships, effectively communicating the data quality distribution.
        - Library/Method: All visualizations use Chart.js rendered on Canvas, with dynamic updates handled by vanilla JavaScript. Interactive tables and lists are manipulated directly via the DOM. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background-color: #FDFBF5;
            color: #334155;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #F1F5F9;
        }
        ::-webkit-scrollbar-thumb {
            background: #94A3B8;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #64748B;
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
        }
        .nav-link:hover, .nav-link.active {
            color: #14B8A6;
            border-bottom-color: #14B8A6;
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white/80 backdrop-blur-md shadow-sm sticky top-0 z-50">
        <nav class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex-shrink-0">
                    <h1 class="text-xl font-bold text-slate-700">النهوض بالعمل المؤسسي</h1>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4 space-x-reverse">
                        <a href="#overview" class="nav-link text-gray-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">نظرة عامة</a>
                        <a href="#analysis" class="nav-link text-gray-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">تحليل الوضع</a>
                        <a href="#solutions" class="nav-link text-gray-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">الحلول المقترحة</a>
                        <a href="#plan" class="nav-link text-gray-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">الخطة الاستراتيجية</a>
                        <a href="#database" class="nav-link text-gray-600 px-3 py-2 rounded-md text-sm font-medium border-b-2 border-transparent">تحليل البيانات</a>
                    </div>
                </div>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <section id="overview" class="py-12 scroll-mt-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-800">نظرة عامة على أداء الشعب</h2>
                <p class="mt-2 text-lg text-slate-600">ملخص سريع للحالة التشغيلية والتحديات الرئيسية لكل شعبة.</p>
            </div>
            <div id="divisions-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            </div>
        </section>

        <div class="border-t border-slate-200 my-12"></div>

        <section id="analysis" class="py-12 scroll-mt-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-800">تحليل الوضع الراهن</h2>
                <p class="mt-2 text-lg text-slate-600">تشخيص دقيق للمعوقات والتحديات، واستعراض لنقاط القوة والفرص المتاحة.</p>
            </div>
            
            <div class="bg-white p-6 rounded-xl shadow-md mb-8">
                <div class="flex flex-col md:flex-row justify-between items-center mb-4">
                    <h3 class="text-xl font-semibold text-slate-700 mb-4 md:mb-0">توزيع المعوقات حسب الشعبة</h3>
                    <div class="w-full md:w-auto">
                        <select id="division-filter" class="w-full form-select block px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding bg-no-repeat border border-solid border-gray-300 rounded-lg transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-teal-600 focus:outline-none">
                            <option value="all">عرض الكل</option>
                        </select>
                    </div>
                </div>
                <div class="chart-container">
                    <canvas id="challengesChart"></canvas>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-xl font-semibold text-slate-700 mb-4 flex items-center">
                        <span class="w-8 h-8 rounded-full bg-red-100 text-red-600 flex items-center justify-center ml-3">!</span>
                        المعوقات والتحديات
                    </h3>
                    <div id="challenges-list" class="space-y-3">
                    </div>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-xl font-semibold text-slate-700 mb-4 flex items-center">
                        <span class="w-8 h-8 rounded-full bg-green-100 text-green-600 flex items-center justify-center ml-3">✓</span>
                        نقاط القوة والفرص
                    </h3>
                    <div id="strengths-list" class="space-y-3">
                    </div>
                </div>
            </div>
        </section>
        
        <div class="border-t border-slate-200 my-12"></div>

        <section id="solutions" class="py-12 scroll-mt-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-800">الحلول المقترحة</h2>
                <p class="mt-2 text-lg text-slate-600">خارطة طريق لمعالجة التحديات المحددة بإجراءات عملية وقابلة للقياس.</p>
            </div>
            <div class="bg-white p-6 rounded-xl shadow-md overflow-x-auto">
                <table class="w-full text-sm text-left text-slate-500">
                    <thead class="text-xs text-slate-700 uppercase bg-slate-50">
                        <tr>
                            <th scope="col" class="px-6 py-3">التحدي</th>
                            <th scope="col" class="px-6 py-3">الحل المقترح</th>
                            <th scope="col" class="px-6 py-3">الشعبة المسؤولة</th>
                            <th scope="col" class="px-6 py-3">الحالة</th>
                        </tr>
                    </thead>
                    <tbody id="solutions-table">
                    </tbody>
                </table>
            </div>
        </section>

        <div class="border-t border-slate-200 my-12"></div>
        
        <section id="plan" class="py-12 scroll-mt-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-800">الخطة الاستراتيجية للنهوض المؤسسي</h2>
                <p class="mt-2 text-lg text-slate-600">أهداف استراتيجية واضحة ومراحل تنفيذ محددة زمنياً.</p>
            </div>
            <div class="relative">
                <div class="border-r-2 border-teal-500 absolute h-full top-0" style="left: 15px;"></div>
                <ul class="space-y-12">
                    <li class="pl-12">
                        <div class="flex items-center">
                            <div class="bg-teal-500 rounded-full h-8 w-8 flex items-center justify-center text-white font-bold absolute" style="left: 0;">1</div>
                            <div class="ml-4 bg-white p-6 rounded-xl shadow-md w-full">
                                <h4 class="text-xl font-bold text-teal-700">المرحلة الأولى: التحليل والتشخيص (الشهر 1-2)</h4>
                                <p class="mt-2 text-slate-600">جمع البيانات من كافة الشعب، تحليلها باستخدام SPSS، وعقد ورش عمل لتحديد المعوقات ونقاط القوة بدقة، وإعداد تقرير تشخيصي شامل.</p>
                            </div>
                        </div>
                    </li>
                    <li class="pl-12">
                        <div class="flex items-center">
                            <div class="bg-teal-500 rounded-full h-8 w-8 flex items-center justify-center text-white font-bold absolute" style="left: 0;">2</div>
                            <div class="ml-4 bg-white p-6 rounded-xl shadow-md w-full">
                                <h4 class="text-xl font-bold text-teal-700">المرحلة الثانية: بناء وتطوير الحلول (الشهر 3-6)</h4>
                                <p class="mt-2 text-slate-600">تصميم الحلول المقترحة، تطوير الأنظمة الرقمية اللازمة، وإعادة هيكلة بعض الإجراءات الإدارية والمالية لزيادة الكفاءة والشفافية.</p>
                            </div>
                        </div>
                    </li>
                    <li class="pl-12">
                        <div class="flex items-center">
                            <div class="bg-teal-500 rounded-full h-8 w-8 flex items-center justify-center text-white font-bold absolute" style="left: 0;">3</div>
                            <div class="ml-4 bg-white p-6 rounded-xl shadow-md w-full">
                                <h4 class="text-xl font-bold text-teal-700">المرحلة الثالثة: التنفيذ والمتابعة (الشهر 7-12)</h4>
                                <p class="mt-2 text-slate-600">تطبيق الحلول المطورة على أرض الواقع، تدريب الموظفين، وإنشاء نظام متابعة مستمر لقياس مؤشرات الأداء الرئيسية (KPIs) وتقديم تقارير دورية.</p>
                            </div>
                        </div>
                    </li>
                     <li class="pl-12">
                        <div class="flex items-center">
                            <div class="bg-teal-500 rounded-full h-8 w-8 flex items-center justify-center text-white font-bold absolute" style="left: 0;">4</div>
                            <div class="ml-4 bg-white p-6 rounded-xl shadow-md w-full">
                                <h4 class="text-xl font-bold text-teal-700">المرحلة الرابعة: التقييم والتحسين المستمر (سنوي)</h4>
                                <p class="mt-2 text-slate-600">تقييم شامل لنتائج الخطة الاستراتيجية، تحديد الدروس المستفادة، وتحديث الخطة بناءً على المتغيرات الجديدة لضمان التطور المستمر.</p>
                            </div>
                        </div>
                    </li>
                </ul>
            </div>
        </section>

        <div class="border-t border-slate-200 my-12"></div>

        <section id="database" class="py-12 scroll-mt-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-800">تحليل البيانات وقاعدة البيانات</h2>
                <p class="mt-2 text-lg text-slate-600">أساس اتخاذ القرار: تقييم جودة البيانات ودورها في التحليل الاستراتيجي.</p>
            </div>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-xl font-semibold text-slate-700 mb-4">منهجية العمل</h3>
                    <p class="text-slate-600 leading-relaxed">
                        يعتمد هذا التقرير على تحليل البيانات المستخرجة من قواعد بيانات Microsoft Access الخاصة بكل شعبة. تم استخدام برنامج التحليل الإحصائي (SPSS) لتحديد الأنماط والعلاقات بين المتغيرات المختلفة، مما ساعد في تشخيص المعوقات بدقة وموضوعية.
                        <br><br>
                        إنشاء قاعدة بيانات مركزية وفعالة هو حجر الزاوية في عملية التطوير. تهدف الخطة إلى توحيد مصادر البيانات، ضمان جودتها وتكاملها، وتسهيل الوصول إليها لتحليلها بشكل دوري لدعم اتخاذ القرارات الاستراتيجية. الرسم البياني المجاور يوضح مستوى نضج البيانات الحالي لكل شعبة.
                    </p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-md">
                     <h3 class="text-xl font-semibold text-slate-700 mb-4 text-center">مستوى نضج البيانات حسب الشعبة</h3>
                    <div class="chart-container">
                        <canvas id="dataMaturityChart"></canvas>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-white border-t border-slate-200 mt-12">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8 py-6 text-center text-slate-500">
            <p>&copy; 2025 - تقرير الأداء والتخطيط الاستراتيجي. جميع الحقوق محفوظة.</p>
        </div>
    </footer>

    <script>
        const divisionsData = {
            'الهندسية': {
                challenges: ['تأخر في تسليم المشاريع بسبب الإجراءات الروتينية.', 'صعوبة الحصول على الموافقات اللازمة في الوقت المحدد.', 'نقص في الكوادر الفنية المتخصصة في بعض المجالات.'],
                strengths: ['خبرة فنية عالية في تنفيذ المشاريع الكبرى.', 'وجود تصاميم هندسية مبتكرة جاهزة للتنفيذ.', 'علاقات جيدة مع الموردين والمقاولين.'],
                solutions: [
                    { challenge: 'تأخر في تسليم المشاريع', solution: 'تطبيق نظام إلكتروني لتتبع الموافقات وتسريعها.', status: 'قيد التنفيذ' },
                ],
                dataMaturity: 75,
                status: { label: 'تحديات متوسطة', color: 'orange' }
            },
            'احياء الشعائر': {
                challenges: ['الحاجة إلى زيادة التنظيم في الفعاليات الكبرى.', 'ضعف التغطية الإعلامية لبعض الشعائر والمناسبات.'],
                strengths: ['قدرة تنظيمية عالية في إدارة الحشود.', 'تفاعل مجتمعي واسع مع الفعاليات المنظمة.', 'تاريخ طويل في إحياء الشعائر الدينية.'],
                 solutions: [
                    { challenge: 'ضعف التغطية الإعلامية', solution: 'التعاون مع شعبة الإعلام لوضع خطة إعلامية متكاملة.', status: 'لم يبدأ' },
                ],
                dataMaturity: 60,
                status: { label: 'أداء جيد', color: 'blue' }
            },
            'الادارية والمالية': {
                challenges: ['دورة مستندية طويلة ومعقدة.', 'نقص في السيولة المالية لتغطية النفقات التشغيلية أحياناً.', 'الحاجة إلى تحديث الأنظمة المحاسبية.'],
                strengths: ['ضبط عالي للنفقات والمصروفات.', 'فريق عمل ملتزم ومنضبط.', 'شفافية في التقارير المالية.'],
                 solutions: [
                    { challenge: 'دورة مستندية طويلة', solution: 'أتمتة العمليات الإدارية والمالية لتقليل الوقت والجهد.', status: 'مكتمل' },
                    { challenge: 'الحاجة لتحديث الأنظمة', solution: 'تطبيق نظام ERP متكامل لإدارة الموارد.', status: 'قيد التنفيذ' },
                ],
                dataMaturity: 85,
                status: { label: 'تحديات حرجة', color: 'red' }
            },
            'الاستثمار': {
                challenges: ['قلة الفرص الاستثمارية الواعدة في السوق الحالي.', 'عوائق قانونية وتنظيمية تعرقل بعض المشاريع.'],
                strengths: ['وجود أصول عقارية ذات قيمة استثمارية عالية.', 'فريق متخصص في دراسات الجدوى الاقتصادية.'],
                 solutions: [
                    { challenge: 'قلة الفرص الاستثمارية', solution: 'استكشاف قطاعات استثمارية جديدة وغير تقليدية.', status: 'لم يبدأ' },
                ],
                dataMaturity: 70,
                status: { label: 'تحديات متوسطة', color: 'orange' }
            },
            'الاعلام والاتصال الحكومي': {
                challenges: ['الحاجة إلى مواكبة التطورات السريعة في الإعلام الرقمي.', 'ضعف التنسيق مع باقي الشعب في نشر الأخبار.'],
                strengths: ['فريق إعلامي شاب ومبدع.', 'منصات إعلامية متعددة وفعالة.', 'قدرة على إنتاج محتوى مرئي عالي الجودة.'],
                 solutions: [
                    { challenge: 'ضعف التنسيق', solution: 'عقد اجتماعات دورية مع منسقي الإعلام في كل شعبة.', status: 'قيد التنفيذ' },
                ],
                dataMaturity: 80,
                status: { label: 'أداء جيد', color: 'blue' }
            },
            'الاملاك الموقوفة': {
                challenges: ['صعوبة في حصر وتوثيق جميع الأملاك الموقوفة.', 'وجود تعديات على بعض العقارات الوقفية.'],
                strengths: ['أرشيف تاريخي غني بالوثائق.', 'فريق قانوني متخصص في قضايا الوقف.'],
                 solutions: [
                    { challenge: 'صعوبة الحصر والتوثيق', solution: 'إطلاق مشروع رقمنة شامل لجميع وثائق الوقف.', status: 'لم يبدأ' },
                ],
                dataMaturity: 55,
                status: { label: 'تحديات متوسطة', color: 'orange' }
            },
            'البحوث والدراسات': {
                challenges: ['قلة الموارد المخصصة للبحث العلمي.', 'صعوبة نشر الأبحاث في المجلات العلمية المرموقة.'],
                strengths: ['وجود باحثين أكفاء في مختلف التخصصات.', 'مكتبة غنية بالمصادر والمراجع القيمة.'],
                 solutions: [
                     { challenge: 'قلة الموارد', solution: 'البحث عن شراكات مع جامعات ومراكز بحثية لتمويل مشترك.', status: 'لم يبدأ' },
                ],
                dataMaturity: 65,
                status: { label: 'أداء جيد', color: 'blue' }
            },
            'التخطيط والمتابعة': {
                challenges: ['ضعف الالتزام بالخطط الموضوعة من قبل بعض الشعب.', 'الحاجة إلى أدوات أكثر فعالية لقياس الأداء.'],
                strengths: ['قدرة على وضع خطط استراتيجية وتشغيلية محكمة.', 'فريق يمتلك رؤية مستقبلية واضحة.'],
                 solutions: [
                     { challenge: 'ضعف الالتزام بالخطط', solution: 'ربط مؤشرات الأداء بنظام الحوافز والمكافآت.', status: 'قيد التنفيذ' },
                ],
                dataMaturity: 90,
                status: { label: 'أداء ممتاز', color: 'green' }
            },
            'التدقيق والرقابة الداخلية': {
                challenges: ['مقاومة التغيير من بعض الأقسام عند تطبيق إجراءات رقابية جديدة.'],
                strengths: ['استقلالية وحيادية في العمل.', 'القدرة على كشف الأخطاء وتقديم توصيات بناءة.'],
                 solutions: [
                     { challenge: 'مقاومة التغيير', solution: 'تنظيم ورش عمل توعوية بأهمية الرقابة الداخلية.', status: 'مكتمل' },
                ],
                dataMaturity: 88,
                status: { label: 'أداء ممتاز', color: 'green' }
            },
            'التعليم الديني': {
                challenges: ['الحاجة إلى تحديث المناهج لتناسب متطلبات العصر.', 'عزوف بعض الشباب عن المشاركة في البرامج الدينية.'],
                strengths: ['وجود كادر تعليمي مؤهل وذو خبرة.', 'برامج تعليمية متنوعة تستهدف فئات عمرية مختلفة.'],
                 solutions: [
                    { challenge: 'الحاجة لتحديث المناهج', solution: 'تشكيل لجنة من الخبراء لتطوير المناهج التعليمية.', status: 'قيد التنفيذ' },
                ],
                dataMaturity: 78,
                status: { label: 'أداء جيد', color: 'blue' }
            }
        };

        const divisionNames = Object.keys(divisionsData);
        let challengesChart, dataMaturityChart;
        
        const statusColors = {
            'مكتمل': 'bg-teal-100 text-teal-800',
            'قيد التنفيذ': 'bg-blue-100 text-blue-800',
            'لم يبدأ': 'bg-yellow-100 text-yellow-800'
        };

        const statusPillColors = {
            'أداء ممتاز': 'bg-green-100 text-green-800',
            'أداء جيد': 'bg-blue-100 text-blue-800',
            'تحديات متوسطة': 'bg-orange-100 text-orange-800',
            'تحديات حرجة': 'bg-red-100 text-red-800',
        };

        function populateOverview() {
            const grid = document.getElementById('divisions-grid');
            grid.innerHTML = '';
            divisionNames.forEach(name => {
                const data = divisionsData[name];
                const card = `
                    <div class="bg-white p-5 rounded-xl shadow-md transition-transform hover:scale-105">
                        <h4 class="font-bold text-lg text-slate-800">${name}</h4>
                        <p class="text-sm text-slate-500 mt-1 mb-3">الحالة التشغيلية</p>
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full ${statusPillColors[data.status.label]}">
                                ${data.status.label}
                            </span>
                            <span class="text-sm font-semibold text-slate-600">${data.challenges.length} تحديات رئيسية</span>
                        </div>
                    </div>
                `;
                grid.innerHTML += card;
            });
        }

        function populateFilter() {
            const filter = document.getElementById('division-filter');
            divisionNames.forEach(name => {
                const option = document.createElement('option');
                option.value = name;
                option.textContent = name;
                filter.appendChild(option);
            });
        }
        
        function updateLists(division) {
            const challengesList = document.getElementById('challenges-list');
            const strengthsList = document.getElementById('strengths-list');
            challengesList.innerHTML = '';
            strengthsList.innerHTML = '';

            const divisionsToDisplay = (division === 'all') ? divisionNames : [division];

            divisionsToDisplay.forEach(name => {
                const data = divisionsData[name];
                data.challenges.forEach(challenge => {
                    challengesList.innerHTML += `<div class="bg-slate-50 p-3 rounded-lg text-slate-700">${challenge} <span class="text-xs text-slate-400">(${name})</span></div>`;
                });
                data.strengths.forEach(strength => {
                    strengthsList.innerHTML += `<div class="bg-slate-50 p-3 rounded-lg text-slate-700">${strength} <span class="text-xs text-slate-400">(${name})</span></div>`;
                });
            });
             if (challengesList.innerHTML === '') challengesList.innerHTML = '<p class="text-slate-500">لا توجد تحديات لعرضها.</p>';
             if (strengthsList.innerHTML === '') strengthsList.innerHTML = '<p class="text-slate-500">لا توجد نقاط قوة لعرضها.</p>';
        }

        function populateSolutionsTable() {
            const tableBody = document.getElementById('solutions-table');
            tableBody.innerHTML = '';
            divisionNames.forEach(name => {
                const data = divisionsData[name];
                if (data.solutions) {
                    data.solutions.forEach(item => {
                        const row = `
                            <tr class="bg-white border-b hover:bg-slate-50">
                                <td class="px-6 py-4 font-medium text-slate-900">${item.challenge}</td>
                                <td class="px-6 py-4">${item.solution}</td>
                                <td class="px-6 py-4">${name}</td>
                                <td class="px-6 py-4">
                                    <span class="px-2 py-1 font-semibold leading-tight text-xs rounded-full ${statusColors[item.status]}">
                                        ${item.status}
                                    </span>
                                </td>
                            </tr>
                        `;
                        tableBody.innerHTML += row;
                    });
                }
            });
        }
        
        function renderChallengesChart() {
            const ctx = document.getElementById('challengesChart').getContext('2d');
            const data = {
                labels: divisionNames,
                datasets: [{
                    label: 'عدد المعوقات',
                    data: divisionNames.map(name => divisionsData[name].challenges.length),
                    backgroundColor: 'rgba(20, 184, 166, 0.2)',
                    borderColor: 'rgba(13, 148, 136, 1)',
                    borderWidth: 2,
                    borderRadius: 5,
                }]
            };
            challengesChart = new Chart(ctx, {
                type: 'bar',
                data: data,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                precision: 0
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        }
                    }
                }
            });
        }
        
        function renderDataMaturityChart() {
            const ctx = document.getElementById('dataMaturityChart').getContext('2d');
            const data = {
                labels: divisionNames,
                datasets: [{
                    label: 'نضج البيانات (%)',
                    data: divisionNames.map(name => divisionsData[name].dataMaturity),
                    backgroundColor: [
                        '#14B8A6', '#0891B2', '#0284C7', '#4338CA', '#7E22CE',
                        '#A21CAF', '#BE185D', '#BE123C', '#DC2626', '#EA580C'
                    ],
                    hoverOffset: 4
                }]
            };
            dataMaturityChart = new Chart(ctx, {
                type: 'doughnut',
                data: data,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                font: {
                                    size: 10
                                }
                            }
                        }
                    }
                }
            });
        }

        document.getElementById('division-filter').addEventListener('change', (e) => {
            const selectedDivision = e.target.value;
            updateLists(selectedDivision);

            challengesChart.data.datasets[0].backgroundColor = divisionNames.map(name => 
                (selectedDivision === 'all' || selectedDivision === name) ? 'rgba(20, 184, 166, 0.6)' : 'rgba(20, 184, 166, 0.2)'
            );
            challengesChart.data.datasets[0].borderColor = divisionNames.map(name => 
                (selectedDivision === 'all' || selectedDivision === name) ? 'rgba(13, 148, 136, 1)' : 'rgba(13, 148, 136, 0.5)'
            );
            challengesChart.update();
        });
        
        document.addEventListener('DOMContentLoaded', () => {
            populateOverview();
            populateFilter();
            updateLists('all');
            populateSolutionsTable();
            renderChallengesChart();
            renderDataMaturityChart();

            const sections = document.querySelectorAll('section');
            const navLinks = document.querySelectorAll('nav a');

            window.onscroll = () => {
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 80) {
                        current = section.getAttribute('id');
                    }
                });

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').includes(current)) {
                        link.classList.add('active');
                    }
                });
            };
            
            navLinks.forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                });
            });
        });
    </script>
</body>
</html>
# thi-qar-report
