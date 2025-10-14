<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Цифровой Двойник - Презентация</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #0a0a0a;
            color: #ffffff;
            overflow-x: hidden;
        }

        .slide-container {
            width: 100vw;
            height: 100vh;
            overflow-y: scroll;
            scroll-snap-type: y mandatory;
            scrollbar-width: none;
        }

        .slide-container::-webkit-scrollbar {
            display: none;
        }

        .slide {
            width: 100%;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 60px 40px;
            scroll-snap-align: start;
            position: relative;
        }

        .slide::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: radial-gradient(circle at 50% 50%, rgba(102, 126, 234, 0.1) 0%, transparent 70%);
            pointer-events: none;
        }

        .slide-content {
            max-width: 1200px;
            width: 100%;
            z-index: 1;
        }

        /* Title Slide */
        .title-slide {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .main-title {
            font-size: clamp(3rem, 8vw, 6rem);
            font-weight: 900;
            margin-bottom: 30px;
            line-height: 1.1;
            text-align: center;
        }

        .main-subtitle {
            font-size: clamp(1.2rem, 3vw, 2rem);
            opacity: 0.95;
            text-align: center;
            margin-bottom: 50px;
        }

        /* Standard Slide */
        .slide h2 {
            font-size: clamp(2rem, 5vw, 3.5rem);
            margin-bottom: 40px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .slide h3 {
            font-size: clamp(1.5rem, 3vw, 2rem);
            margin-bottom: 25px;
            color: #ffd700;
        }

        .slide p, .slide li {
            font-size: clamp(1rem, 2vw, 1.3rem);
            line-height: 1.8;
            margin-bottom: 20px;
            color: rgba(255,255,255,0.9);
        }

        /* Problem Slide */
        .problem-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin-top: 40px;
        }

        .problem-card {
            background: rgba(255,255,255,0.05);
            padding: 35px;
            border-radius: 20px;
            border-left: 5px solid #ff6b6b;
            backdrop-filter: blur(10px);
        }

        .problem-card h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
        }

        /* Comparison Slide */
        .comparison-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            margin-top: 40px;
        }

        .comparison-side {
            background: rgba(255,255,255,0.05);
            padding: 40px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
        }

        .comparison-side.bad {
            border: 3px solid #ff6b6b;
        }

        .comparison-side.good {
            border: 3px solid #51cf66;
        }

        .comparison-side h3 {
            color: inherit;
            margin-bottom: 25px;
            text-align: center;
        }

        .comparison-side.bad h3 {
            color: #ff6b6b;
        }

        .comparison-side.good h3 {
            color: #51cf66;
        }

        .comparison-item {
            padding: 15px 0;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .comparison-item:last-child {
            border-bottom: none;
        }

        /* Process Steps */
        .process-steps {
            margin-top: 40px;
        }

        .step {
            background: rgba(255,255,255,0.05);
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 25px;
            border-left: 5px solid #667eea;
            backdrop-filter: blur(10px);
        }

        .step-number {
            display: inline-block;
            width: 50px;
            height: 50px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 50%;
            text-align: center;
            line-height: 50px;
            font-size: 1.5rem;
            font-weight: bold;
            margin-right: 15px;
        }

        .step h4 {
            display: inline;
            font-size: 1.5rem;
            color: #ffd700;
        }

        .step-content {
            margin-top: 20px;
            padding-left: 65px;
        }

        /* Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin-top: 40px;
        }

        .stat-card {
            text-align: center;
            padding: 40px;
            background: rgba(255,255,255,0.05);
            border-radius: 20px;
            backdrop-filter: blur(10px);
        }

        .stat-number {
            font-size: 4rem;
            font-weight: 900;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 15px;
        }

        .stat-label {
            font-size: 1.2rem;
            color: rgba(255,255,255,0.8);
        }

        /* Checklist */
        .checklist {
            margin-top: 30px;
        }

        .checklist-item {
            background: rgba(255,255,255,0.05);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            display: flex;
            align-items: flex-start;
            gap: 15px;
        }

        .checklist-icon {
            font-size: 1.5rem;
            flex-shrink: 0;
        }

        /* Quote */
        .quote {
            background: rgba(255,255,255,0.05);
            padding: 40px;
            border-radius: 20px;
            border-left: 5px solid #ffd700;
            margin: 40px 0;
            font-style: italic;
            font-size: 1.3rem;
            backdrop-filter: blur(10px);
        }

        .quote-source {
            text-align: right;
            margin-top: 20px;
            font-style: normal;
            color: #ffd700;
        }

        /* Research */
        .research-card {
            background: rgba(255,255,255,0.05);
            padding: 35px;
            border-radius: 20px;
            margin-bottom: 30px;
            border-left: 5px solid #667eea;
            backdrop-filter: blur(10px);
        }

        .research-card h4 {
            color: #667eea;
            font-size: 1.4rem;
            margin-bottom: 15px;
        }

        /* Navigation */
        .slide-nav {
            position: fixed;
            right: 30px;
            top: 50%;
            transform: translateY(-50%);
            z-index: 100;
        }

        .nav-dot {
            width: 12px;
            height: 12px;
            background: rgba(255,255,255,0.3);
            border-radius: 50%;
            margin: 15px 0;
            cursor: pointer;
            transition: all 0.3s;
        }

        .nav-dot:hover {
            background: rgba(255,255,255,0.6);
            transform: scale(1.2);
        }

        /* Highlight */
        .highlight {
            color: #ffd700;
            font-weight: 600;
        }

        .bad-text {
            color: #ff6b6b;
        }

        .good-text {
            color: #51cf66;
        }

        /* CTA Slide Title */
        .cta-title {
            color: white !important;
            font-size: clamp(2.5rem, 6vw, 4.5rem);
            margin-bottom: 40px;
            text-shadow: 2px 2px 8px rgba(0,0,0,0.5);
            font-weight: 900;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .comparison-container {
                grid-template-columns: 1fr;
            }

            .slide {
                padding: 40px 20px;
            }

            .step-content {
                padding-left: 0;
            }
        }
    </style>
</head>
<body>
    <div class="slide-container">
        
        <!-- Slide 1: Title -->
        <div class="slide title-slide">
            <div class="slide-content">
                <h1 class="main-title">ЦИФРОВОЙ ДВОЙНИК</h1>
                <p class="main-subtitle">Персонализированный AI, который пишет КАК ВЫ.<br>Не как ChatGPT для всех.</p>
            </div>
        </div>

        <!-- Slide 2: Problem Context -->
        <div class="slide">
            <div class="slide-content">
                <h2>Проблема, которую признала даже OpenAI</h2>
                
                <div class="research-card">
                    <h4>📊 Август 2025: OpenAI откатила GPT-5</h4>
                    <p><span class="bad-text">Причина:</span> Массовые жалобы пользователей на <span class="highlight">"роботизированность и неискренность"</span> текстов.</p>
                    <p>Компания с миллиардными инвестициями <span class="bad-text">не смогла</span> решить проблему "человечности" в AI-текстах.</p>
                </div>

                <div class="research-card">
                    <h4>📊 Апрель 2025: ChatGPT обвиняют в "подхалимстве"</h4>
                    <p>После обновления система стала <span class="bad-text">"излишне вежливой"</span>, пользователи жалуются на льстивость и согласие со всем.</p>
                    <p>OpenAI снова откатила обновление из-за критики.</p>
                </div>

                <div class="research-card">
                    <h4>📊 Июль 2025: "Язык ChatGPT заразителен"</h4>
                    <p>Исследование университетов: ChatGPT <span class="bad-text">меняет язык людей</span>, они начинают писать шаблонно и структурированно.</p>
                    <p>Эксперты обеспокоены <span class="highlight">потерей индивидуальности</span> в письменной речи.</p>
                </div>
            </div>
        </div>

        <!-- Slide 3: Market Pain -->
        <div class="slide">
            <div class="slide-content">
                <h2>Три боли экспертов в 2025 году</h2>
                
                <div class="problem-grid">
                    <div class="problem-card">
                        <h3>❌ ChatGPT убивает стиль</h3>
                        <p>Вы пробовали писать через ChatGPT. Получили шаблон. Безликий. Не ваш.</p>
                        <p>Аудитория <span class="bad-text">чувствует</span>: "Это не он пишет".</p>
                        <p><span class="highlight">Доверие падает.</span></p>
                    </div>

                    <div class="problem-card">
                        <h3>⏰ Нет времени писать самому</h3>
                        <p>2 часа на один пост × 20-30 постов в месяц = <span class="bad-text">40-60 часов</span>.</p>
                        <p>Это больше недели работы только на контент.</p>
                        <p>А ещё есть бизнес, клиенты, продукты...</p>
                    </div>

                    <div class="problem-card">
                        <h3>💔 Копирайтеры не попадают</h3>
                        <p>Нанял копирайтера. Объяснил, объяснял... Всё равно <span class="bad-text">не ваш голос</span>.</p>
                        <p>Правок больше, чем пользы.</p>
                        <p>Проще написать самому. Но нет времени.</p>
                    </div>
                </div>

                <div class="quote">
                    "Вопрос не в том, использовать ли AI. Вопрос в том, КАК использовать AI, не теряя себя."
                </div>
            </div>
        </div>

        <!-- Slide 4: ChatGPT vs Personalized AI -->
        <div class="slide">
            <div class="slide-content">
                <h2>ChatGPT vs Цифровой Двойник</h2>
                
                <div class="comparison-container">
                    <div class="comparison-side bad">
                        <h3>❌ Обычный ChatGPT</h3>
                        
                        <div class="comparison-item">
                            <p><strong>Для кого:</strong> Для всех одинаково</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Стиль:</strong> Шаблонный, предсказуемый</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Настройка:</strong> Никакой (максимум — короткий промт)</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Фирменные выражения:</strong> Не знает</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Структура:</strong> Всегда одинаковая (введение-тело-заключение)</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Метафоры:</strong> Случайные, общие</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Тон:</strong> Излишне формальный или льстивый</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Попадание в стиль:</strong> <span class="bad-text">30-40%</span></p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Узнаваемость:</strong> <span class="bad-text">Аудитория чувствует AI</span></p>
                        </div>
                    </div>

                    <div class="comparison-side good">
                        <h3>✅ Цифровой Двойник</h3>
                        
                        <div class="comparison-item">
                            <p><strong>Для кого:</strong> Только для вас</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Стиль:</strong> Ваш уникальный</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Настройка:</strong> 15-20 часов работы над профилем</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Фирменные выражения:</strong> Все сохранены и используются</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Структура:</strong> Ваша личная (как вы строите мысли)</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Метафоры:</strong> Ваши характерные</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Тон:</strong> Ваш точный (формальный/дружеский/провокационный)</p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Попадание в стиль:</strong> <span class="good-text">90-95%</span></p>
                        </div>
                        <div class="comparison-item">
                            <p><strong>Узнаваемость:</strong> <span class="good-text">Не заметят разницы</span></p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 5: How It Works - Overview -->
        <div class="slide">
            <div class="slide-content">
                <h2>Как создаётся ваш Цифровой Двойник</h2>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-number">5-7</div>
                        <div class="stat-label">часов ваших видео/лекций анализируется</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">50+</div>
                        <div class="stat-label">постов изучается до деталей</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">15-20</div>
                        <div class="stat-label">часов работы над вашим профилем</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">8-12</div>
                        <div class="stat-label">страниц детального описания вашего стиля</div>
                    </div>
                </div>

                <div class="quote">
                    "Это не 'быстрый промт' для ChatGPT. Это глубокое исследование вашей манеры думать, говорить и писать."
                </div>
            </div>
        </div>

        <!-- Slide 6: Analysis Process -->
        <div class="slide">
            <div class="slide-content">
                <h2>Что анализируется в вашем стиле</h2>
                
                <div class="process-steps">
                    <div class="step">
                        <span class="step-number">1</span>
                        <h4>Лексика и словарный запас</h4>
                        <div class="step-content">
                            <p>• Какие слова вы используете чаще всего</p>
                            <p>• Ваши фирменные выражения ("по сути", "давай честно", "суть в том")</p>
                            <p>• Профессиональный жаргон вашей ниши</p>
                            <p>• Эмоциональная окраска: "круто" или "эффективно"?</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">2</span>
                        <h4>Синтаксис и структура предложений</h4>
                        <div class="step-content">
                            <p>• Длина предложений (короткие 5-7 слов или длинные 20+)</p>
                            <p>• Простые конструкции или сложные с придаточными</p>
                            <p>• Как часто используете вопросы</p>
                            <p>• Ритм и паузы (много коротких подряд или длинные абзацы)</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">3</span>
                        <h4>Композиция и архитектура текста</h4>
                        <div class="step-content">
                            <p>• Как начинаете: с вопроса, истории, тезиса или провокации?</p>
                            <p>• Как развиваете мысль: линейно, спирально, через примеры?</p>
                            <p>• Как завершаете: выводом, призывом, вопросом?</p>
                            <p>• Используете ли списки (и какие: маркированные, нумерованные)</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 7: Analysis Process Part 2 -->
        <div class="slide">
            <div class="slide-content">
                <h2>Что ещё анализируется</h2>
                
                <div class="process-steps">
                    <div class="step">
                        <span class="step-number">4</span>
                        <h4>Тон и эмоциональность</h4>
                        <div class="step-content">
                            <p>• Уровень формальности: деловой или дружеский?</p>
                            <p>• Эмоциональная насыщенность: много восклицаний или сдержанность?</p>
                            <p>• Категоричность: "всегда/никогда" или "часто/иногда"?</p>
                            <p>• Использование юмора: есть ли? Какой (сарказм, ирония)?</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">5</span>
                        <h4>Аргументация и логика</h4>
                        <div class="step-content">
                            <p>• Тип доказательств: истории, статистика, логика, примеры?</p>
                            <p>• Соотношение: 70% историй + 25% примеры + 15% статистика</p>
                            <p>• Как работаете с возражениями: предвосхищаете, игнорируете, разбираете?</p>
                            <p>• Призывы к действию: прямые или мягкие?</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">6</span>
                        <h4>Метафоры и образность</h4>
                        <div class="step-content">
                            <p>• Откуда берёте метафоры: спорт, природа, бизнес, кино?</p>
                            <p>• Частота образов: в каждом посте или редко?</p>
                            <p>• Тип историй: личные, клиентские, притчи?</p>
                            <p>• Повторяющиеся образы: "жизнь как марафон", "бизнес как шахматы"</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 8: Quality Control -->
        <div class="slide">
            <div class="slide-content">
                <h2>Система контроля качества</h2>
                <h3>Каждый текст проходит проверку по 20 пунктам</h3>
                
                <div class="checklist">
                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Детектор AI:</strong> Текст должен показывать "написано человеком" минимум в 85% случаев
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Устранение структурированности:</strong> AI любит делить на введение-основную часть-заключение. Мы ломаем эту структуру под ваш естественный стиль
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Проверка клише:</strong> Удаляем типичные AI-фразы ("в современном мире", "подводя итог", "важно отметить")
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Ритм речи:</strong> Проверяем, что предложения неравномерной длины (как у человека), а не идеально сбалансированы
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Фирменные выражения:</strong> Ваши маркерные слова должны появляться с правильной частотой
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Эмоциональность:</strong> ChatGPT либо слишком сдержан, либо излишне восторжен. Мы настраиваем под ваш реальный тон
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Естественные "неровности":</strong> Добавляем живые элементы: недосказанность, отступления, риторические вопросы
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div>
                            <strong>Сравнение с оригиналом:</strong> Каждый текст сравнивается с вашими реальными постами — попадание должно быть 90%+
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 9: "Humanization" Process -->
        <div class="slide">
            <div class="slide-content">
                <h2>Процесс "очеловечивания"</h2>
                <h3>Как мы убираем "AI-запах"</h3>
                
                <div class="comparison-container">
                    <div class="comparison-side bad">
                        <h3>❌ Типичные AI-маркеры</h3>
                        
                        <p><strong>1. Излишняя структурированность</strong></p>
                        <p class="bad-text">"Во-первых... Во-вторых... В-третьих... В заключение..."</p>
                        <br>
                        
                        <p><strong>2. Клише и шаблоны</strong></p>
                        <p class="bad-text">"В современном мире...", "Важно отметить...", "Подводя итог..."</p>
                        <br>
                        
                        <p><strong>3. Идеальная грамматика</strong></p>
                        <p class="bad-text">Нет живых "неровностей", всё слишком правильно</p>
                        <br>
                        
                        <p><strong>4. Равномерный ритм</strong></p>
                        <p class="bad-text">Все предложения одной длины, все абзацы одинаковые</p>
                        <br>
                        
                        <p><strong>5. Отсутствие личного</strong></p>
                        <p class="bad-text">Нет историй, нет "я", только общие рассуждения</p>
                    </div>

                    <div class="comparison-side good">
                        <h3>✅ Как мы исправляем</h3>
                        
                        <p><strong>1. Разрушаем структуру</strong></p>
                        <p class="good-text">Используем вашу естественную логику: можете начать с середины, вернуться к началу, закончить вопросом</p>
                        <br>
                        
                        <p><strong>2. Заменяем на ваши фразы</strong></p>
                        <p class="good-text">Вместо "в современном мире" → ваше фирменное выражение</p>
                        <br>
                        
                        <p><strong>3. Добавляем живость</strong></p>
                        <p class="good-text">Незавершённые мысли, отступления, "кстати", "вообще", междометия</p>
                        <br>
                        
                        <p><strong>4. Варьируем ритм</strong></p>
                        <p class="good-text">Короткое. Потом длинное предложение с деталями и пояснениями. Снова короткое.</p>
                        <br>
                        
                        <p><strong>5. Вплетаем личное</strong></p>
                        <p class="good-text">Ваши истории, наблюдения, примеры из практики — как вы делаете в реальных постах</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 10: Profile Creation -->
        <div class="slide">
            <div class="slide-content">
                <h2>Что входит в ваш стилистический профиль</h2>
                <h3>Документ на 8-12 страниц — ваша "цифровая ДНК"</h3>
                
                <div class="process-steps">
                    <div class="step">
                        <span class="step-number">1</span>
                        <h4>Частотный словарь</h4>
                        <div class="step-content">
                            <p>Топ-50 ваших любимых слов и выражений с частотой использования</p>
                            <p><em>Пример: "конкретно" — используется в 35% постов, "по сути" — в 28%</em></p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">2</span>
                        <h4>Синтаксические правила</h4>
                        <div class="step-content">
                            <p>Средняя длина предложений: 12 слов</p>
                            <p>Типичные конструкции: начинаете с вопроса в 40% случаев</p>
                            <p>Соотношение простых/сложных предложений: 70/30</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">3</span>
                        <h4>Структурные шаблоны</h4>
                        <div class="step-content">
                            <p>Как строите тексты: вопрос → история → анализ → вывод</p>
                            <p>Длина абзацев: 2-3 предложения</p>
                            <p>Использование списков: редко, только для перечисления</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">4</span>
                        <h4>Тональный профиль</h4>
                        <div class="step-content">
                            <p>Уровень формальности: 6/10 (дружеский, но профессиональный)</p>
                            <p>Эмоциональность: умеренная, без восклицаний</p>
                            <p>Категоричность: 4/10 (больше "часто" чем "всегда")</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 11: Profile Creation Part 2 -->
        <div class="slide">
            <div class="slide-content">
                <h2>Что ещё в профиле</h2>
                
                <div class="process-steps">
                    <div class="step">
                        <span class="step-number">5</span>
                        <h4>Аргументационная модель</h4>
                        <div class="step-content">
                            <p>Типы доказательств: 60% истории + 25% примеры + 15% статистика</p>
                            <p>Как работаете с возражениями: предвосхищаете и разбираете</p>
                            <p>Призывы к действию: мягкие, через вопросы ("А вы как думаете?")</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">6</span>
                        <h4>Метафорический словарь</h4>
                        <div class="step-content">
                            <p>Источники образов: 70% спорт, 20% бизнес, 10% кино</p>
                            <p>Характерные метафоры: "бизнес как марафон", "команда как оркестр"</p>
                            <p>Частота использования: 2-3 метафоры на пост</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">7</span>
                        <h4>Табу (что НИКОГДА не делаете)</h4>
                        <div class="step-content">
                            <p>❌ Не используете нумерованные списки</p>
                            <p>❌ Никогда не пишете "в заключение"</p>
                            <p>❌ Не используете смодзи в середине текста</p>
                            <p>❌ Не начинаете с цитат</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">8</span>
                        <h4>Эталонные примеры</h4>
                        <div class="step-content">
                            <p>10-15 характерных отрывков из ваших реальных текстов</p>
                            <p>С пометками: "Типичное начало", "Характерный переход", "Ваша концовка"</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 12: Testing Process -->
        <div class="slide">
            <div class="slide-content">
                <h2>Процесс тестирования и калибровки</h2>
                
                <div class="process-steps">
                    <div class="step">
                        <span class="step-number">1</span>
                        <h4>Генерация тестовых постов</h4>
                        <div class="step-content">
                            <p>Создаём 15-20 постов на разные темы</p>
                            <p>Разной длины (короткие, средние, длинные)</p>
                            <p>В разных форматах (истории, аналитика, мнение)</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">2</span>
                        <h4>Ваша оценка</h4>
                        <div class="step-content">
                            <p>Вы читаете каждый пост</p>
                            <p>Оцениваете: "Звучит как я? Что не так?"</p>
                            <p>Даёте детальную обратную связь</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">3</span>
                        <h4>Корректировка профиля</h4>
                        <div class="step-content">
                            <p>Мы анализируем ваши комментарии</p>
                            <p>Дорабатываем профиль (добавляем/убираем правила)</p>
                            <p>Генерируем новую партию для проверки</p>
                        </div>
                    </div>

                    <div class="step">
                        <span class="step-number">4</span>
                        <h4>Финальная проверка</h4>
                        <div class="step-content">
                            <p>Цель: вы не можете отличить сгенерированный текст от своего</p>
                            <p>Попадание в стиль: минимум 90-95%</p>
                            <p>Детектор AI: показывает "человек" в 85%+ случаев</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 13: Results -->
        <div class="slide">
            <div class="slide-content">
                <h2>Что вы получаете на выходе</h2>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-number">40</div>
                        <div class="stat-label">часов экономии каждый месяц</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">90%+</div>
                        <div class="stat-label">попадание в ваш стиль</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">3×</div>
                        <div class="stat-label">больше контента без усилий</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">10</div>
                        <div class="stat-label">минут на правку вместо 2 часов на написание</div>
                    </div>
                </div>

                <div class="quote">
                    "Аудитория не заметит разницы. Вы останетесь собой. Просто будете везде."
                </div>

                <div class="checklist">
                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div><strong>Стилистический профиль</strong> (8-12 страниц) — ваша интеллектуальная собственность</div>
                    </div>
                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div><strong>Работающая система</strong> генерации контента в вашем стиле</div>
                    </div>
                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div><strong>Чек-лист проверки</strong> из 20 пунктов — сможете контролировать качество сами</div>
                    </div>
                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div><strong>Инструкции</strong> по работе с системой и обновлению профиля</div>
                    </div>
                    <div class="checklist-item">
                        <span class="checklist-icon">✓</span>
                        <div><strong>Ежемесячная калибровка</strong> — ваш стиль эволюционирует, профиль тоже</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 14: Case Examples -->
        <div class="slide">
            <div class="slide-content">
                <h2>Примеры: Когда система работает</h2>
                
                <div class="research-card">
                    <h4>📌 Кейс: Бизнес-коуч</h4>
                    <p><strong>Проблема:</strong> Использовал слово-маркер "конкретно" в каждом втором посте. ChatGPT этого не воспроизводил — аудитория чувствовала фальшь.</p>
                    <p><strong>Решение:</strong> Система зафиксировала частоту и контекст использования. Теперь маркер появляется естественно.</p>
                    <p><strong>Результат:</strong> <span class="good-text">Аудитория не заметила разницы. Экономия 35 часов/мес.</span></p>
                </div>

                <div class="research-card">
                    <h4>📌 Кейс: Психолог</h4>
                    <p><strong>Проблема:</strong> Всегда начинал посты с клиентской истории, потом анализ. ChatGPT начинал с тезиса.</p>
                    <p><strong>Решение:</strong> Профиль зафиксировал структуру: история → эмоции → анализ → вывод.</p>
                    <p><strong>Результат:</strong> <span class="good-text">95% попадание в стиль. Подписчики пишут: "Как всегда глубоко".</span></p>
                </div>

                <div class="research-card">
                    <h4>📌 Кейс: Эксперт по продажам</h4>
                    <p><strong>Проблема:</strong> Использовал уникальные метафоры из спорта. ChatGPT брал общие клише.</p>
                    <p><strong>Решение:</strong> Создали метафорический словарь с его образами: "продажи как марафон", "клиент как спарринг-партнёр".</p>
                    <p><strong>Результат:</strong> <span class="good-text">Тексты звучат узнаваемо. Вовлечённость выросла на 40%.</span></p>
                </div>
            </div>
        </div>

        <!-- Slide 15: Why Now -->
        <div class="slide">
            <div class="slide-content">
                <h2>Почему это актуально СЕЙЧАС</h2>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-number">70%</div>
                        <div class="stat-label">экспертов уже пробуют ChatGPT для контента</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">85%</div>
                        <div class="stat-label">из них недовольны результатом</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">2×</div>
                        <div class="stat-label">чаще аудитория замечает "AI-запах"</div>
                    </div>
                </div>

                <div class="research-card">
                    <h4>🔥 Август 2025: Блогеры протестуют против AI</h4>
                    <p>YouTube начал тайно улучшать контент через AI. Блогеры ополчились: <span class="bad-text">"Это убивает нашу аутентичность!"</span></p>
                    <p><strong>Вывод:</strong> Рынок боится потерять уникальность, но понимает — без AI не выжить.</p>
                </div>

                <div class="research-card">
                    <h4>🔥 2025: "Кто выживет в эпоху AI"</h4>
                    <p>Маркетологи признают: <span class="highlight">блогеры с уникальным стилем выживут</span>, те, кто использует AI "в лоб" — потеряют аудиторию.</p>
                    <p><strong>Решение:</strong> Нужен баланс — использовать AI, но сохранить себя.</p>
                </div>

                <div class="quote">
                    "Вопрос не в том, использовать ли AI. А в том, КАК использовать его правильно. СЕЙЧАС."
                </div>
            </div>
        </div>

        <!-- Slide 16: Problem Solved -->
        <div class="slide">
            <div class="slide-content">
                <h2>Проблема, которую не решил никто</h2>
                <h3>Даже OpenAI с миллиардами</h3>
                
                <div class="comparison-container">
                    <div class="comparison-side bad">
                        <h3>❌ Что НЕ работает</h3>
                        
                        <p><strong>ChatGPT "в лоб"</strong></p>
                        <p class="bad-text">Пишете промт → получаете шаблон → аудитория чувствует</p>
                        <br>
                        
                        <p><strong>"Хорошие промты"</strong></p>
                        <p class="bad-text">Даже с детальным промтом ChatGPT не знает ВАШ стиль</p>
                        <br>
                        
                        <p><strong>Копирайтеры</strong></p>
                        <p class="bad-text">Не могут передать ваш голос, как ни объясняй</p>
                        <br>
                        
                        <p><strong>Писать самому</strong></p>
                        <p class="bad-text">40+ часов в месяц → выгорание → нерегулярность</p>
                    </div>

                    <div class="comparison-side good">
                        <h3>✅ Что работает</h3>
                        
                        <p><strong>Персонализированная система</strong></p>
                        <p class="good-text">15-20 часов работы → профиль → система, которая пишет КАК ВЫ</p>
                        <br>
                        
                        <p><strong>Глубокий анализ</strong></p>
                        <p class="good-text">Изучаем часы вашего контента, находим уникальные паттерны</p>
                        <br>
                        
                        <p><strong>Многоуровневый контроль</strong></p>
                        <p class="good-text">Детектор AI + чек-лист 20 пунктов + ваша правка</p>
                        <br>
                        
                        <p><strong>Результат</strong></p>
                        <p class="good-text">Публикуете в 3 раза больше, оставаясь собой</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 17: Guarantees -->
        <div class="slide">
            <div class="slide-content">
                <h2>Гарантии, которые защищают вас</h2>
                
                <div class="checklist">
                    <div class="checklist-item">
                        <span class="checklist-icon">🎯</span>
                        <div>
                            <strong>Гарантия попадания в стиль</strong><br>
                            Если после тестов скажете "Это не мой стиль" — мы продолжим работу бесплатно до достижения результата. Или вернём 100% денег.
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">🔒</span>
                        <div>
                            <strong>Гарантия конфиденциальности</strong><br>
                            Ваш профиль — только для вас. Не передаётся третьим лицам. Не используется для обучения публичных моделей. По запросу — удаляется.
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">✨</span>
                        <div>
                            <strong>Гарантия качества</strong><br>
                            Каждый текст проверяется детектором AI. Должен показывать "человек". Если нет — переделываем бесплатно.
                        </div>
                    </div>

                    <div class="checklist-item">
                        <span class="checklist-icon">🔄</span>
                        <div>
                            <strong>Гарантия поддержки</strong><br>
                            Первый месяц — безлимитные правки и корректировки. Вы должны быть довольны на 100%.
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Slide 18: Call to Action -->
        <div class="slide title-slide">
            <div class="slide-content">
                <h2 class="cta-title">Готовы увидеть вашего Цифрового Двойника?</h2>
                
                <div class="quote">
                    <h3 style="color: #ffd700; margin-bottom: 20px;">Бесплатное демо</h3>
                    <p>✓ Мы возьмём 2-3 часа ваших материалов</p>
                    <p>✓ Создадим экспресс-профиль</p>
                    <p>✓ Сгенерируем 3 поста в вашем стиле</p>
                    <p>✓ Вы оцените: "Похоже или нет?"</p>
                    <br>
                    <p style="font-size: 1.5rem; color: #ffd700;">Никаких обязательств. Никаких предоплат.</p>
                </div>

                <div style="text-align: center; margin-top: 50px;">
                    <p style="font-size: 1.8rem; margin-bottom: 20px;">Напишите "Хочу демо"</p>
                    <p style="font-size: 1.3rem; opacity: 0.9;">Telegram / WhatsApp / Email</p>
                </div>
            </div>
        </div>

        <!-- Slide 19: Final Message -->
        <div class="slide">
            <div class="slide-content">
                <h2>Последнее, что важно понять</h2>
                
                <div class="quote">
                    "Проблема 'AI-запаха' настолько серьёзна, что OpenAI откатывает релизы.<br><br>
                    
                    Компания с миллиардными инвестициями не может создать AI, который пишет как человек.<br><br>
                    
                    Потому что они пытаются создать систему для ВСЕХ.<br><br>
                    
                    А мы создаём систему для ВАС.<br><br>
                    
                    В этом вся разница."
                </div>

                <div class="stats-grid" style="margin-top: 60px;">
                    <div class="stat-card">
                        <div class="stat-number">∞</div>
                        <div class="stat-label">OpenAI потратила на попытку решить проблему</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">0</div>
                        <div class="stat-label">результат (откатили релиз)</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">15-20</div>
                        <div class="stat-label">часов работы над ВАШИМ профилем</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">90%+</div>
                        <div class="stat-label">попадание в ваш стиль</div>
                    </div>
                </div>

                <div class="quote" style="margin-top: 60px; background: linear-gradient(135deg, rgba(102, 126, 234, 0.2) 0%, rgba(118, 75, 162, 0.2) 100%);">
                    <p style="font-size: 1.8rem; text-align: center;">Демо покажет больше, чем любые слова.</p>
                    <p style="font-size: 1.3rem; text-align: center; margin-top: 20px; opacity: 0.9;">Увидеть — значит поверить.</p>
                </div>
            </div>
        </div>

    </div>

    <div class="slide-nav">
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
        <div class="nav-dot"></div>
    </div>

    <script>
        // Smooth scroll navigation
        const dots = document.querySelectorAll('.nav-dot');
        const slides = document.querySelectorAll('.slide');
        
        dots.forEach((dot, index) => {
            dot.addEventListener('click', () => {
                slides[index].scrollIntoView({ behavior: 'smooth' });
            });
        });

        // Update active dot on scroll
        const container = document.querySelector('.slide-container');
        container.addEventListener('scroll', () => {
            const scrollPos = container.scrollTop;
            const slideHeight = window.innerHeight;
            const currentSlide = Math.round(scrollPos / slideHeight);
            
            dots.forEach((dot, index) => {
                if (index === currentSlide) {
                    dot.style.background = 'rgba(255, 255, 255, 1)';
                    dot.style.transform = 'scale(1.3)';
                } else {
                    dot.style.background = 'rgba(255, 255, 255, 0.3)';
                    dot.style.transform = 'scale(1)';
                }
            });
        });
    </script>
</body>
</html>
