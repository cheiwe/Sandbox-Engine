# «Гость» — фанатское продолжение Hello Neighbor (Unreal Engine 5)

План подготовки проекта и промпты для генерации концептов.
Источник: `Concept_Claude.docx` (описание Акта 1).

---

## 1. Что важно взять из Hello Neighbor

Hello Neighbor (Dynamic Pixels / tinyBuild, 2017) — стелс-хоррор от первого лица. Игрок пробирается в
дом соседа, мистера Питерсона, и выясняет, что тот прячет в подвале. В Hello Neighbor 2 (2022) появляется
**Гость** — высокий персонаж в тёмном плаще, с птичьей маской.

Что делает игру узнаваемой и что стоит перенести:

| Элемент | Как это сделано в оригинале | Что берём в «Гостя» |
|---|---|---|
| Визуальный стиль | Мультяшный, яркий, утрированные пропорции, «кривая» архитектура, пригород 1960-х | Тот же: сочные цвета днём, толстые силуэты, чуть искажённые стены и окна |
| ИИ противника | Видит, слышит, гонится; ставит ловушки и камеры там, где игрок часто ходит | Зрение + слух + уровни тревоги + патрульные зоны (см. концепт); адаптивность — в последующих актах |
| Головоломки | Физические предметы, ключи, ломы, ящики, неочевидная логика | Ключи 4 цветов, сейф, радиостанция, картина-ребус, лампочки |
| Физика | Предметы можно брать, бросать, ставить друг на друга | Нужна система захвата и броска предметов: ими можно отвлекать Гостя шумом |
| Смерть | Поимка → скример → возврат домой с сохранением инвентаря | То же самое плюс анимация резкого пробуждения |
| Атмосфера | Днём солнечный пригород, внутри дома тревожно | Нарастание: обычный дом → мигающий свет после жёлтого ключа → зловещий подвал |

**Юридическое замечание.** Hello Neighbor, мистер Питерсон и Гость — интеллектуальная собственность
tinyBuild. Для бесплатного фанатского релиза (itch.io, GameJolt) обычно хватает оригинальных моделей,
своего названия и пометки «fan game». Для продажи в Steam, PlayStation Store и т. п. нужна лицензия.
Поэтому промпты ниже описывают **оригинальные** дизайны в духе серии, а не копии.

---

## 2. Расхождения в концепте, которые нужно решить до старта

1. **Электричество и комната с лампочками.** Свет включается только после предохранителя из сейфа. Код
   сейфа при этом нужно прочитать при свете лампочек. Варианты: (а) у светильников в этой комнате
   отдельная линия от аккумулятора или генератора; (б) кровавые цифры светятся в ультрафиолете, а лампочки
   ультрафиолетовые и на батарейках. **Предлагаю (а).**
2. **Где лежат 4 лампочки?** Нужно разбросать их по этажам. Предлагаю: две на 2-м этаже, одна в подвале,
   одна в комнате с ломом.
3. **Красный ключ используется дважды** (цепь и сейф). Предлагаю, чтобы ключи не расходовались.
4. **Как попасть на шпиль крыши с антенной?** Предлагаю через слуховое окно на чердаке с выходом на
   конёк крыши. Оттуда же можно упасть и разбиться, это даже хорошо.
5. **Где лежит зелёный ключ и когда он доступен?** Шкаф на чердаке — после предохранителя и досок.
   Порядок получается такой: синий (сейф) → красный (картина) → жёлтый (радио) → зелёный (шкаф).
   Красный — первый по сюжету.
6. **Высота падения.** «3 роста» ≈ 5,4 м — смерть, «2 роста» ≈ 3,6 м — оглушение. Значит, с пожарной
   лестницы под окном 2-го этажа (≈ 4–5 м) упасть можно с оглушением. Высоты надо выверить при блокауте.
7. **Название игры и имена персонажей** — для меню, титров и стор-страниц.
8. **Целевые платформы**: только ПК (Windows/Linux)? Консоли (нужен devkit и аккаунт разработчика)?
   Android? От этого зависят бюджеты графики.
9. **Языки**: RU + EN?

---

## 3. Предложения для разделов «придумай»

### Ловушки для Гостя (игрок ставит сам, лимит — 2 одновременно)

| Ловушка | Где взять | Эффект |
|---|---|---|
| **Медвежий капкан** (старый, ржавый, мультяшный) | Сарай во дворе / подвал | Гость застревает на 5 с, громко кричит (выдаёт позицию) |
| **Ведро клея** (опрокинуть на пол) | Подвал | Лужа: Гость двигается на 60 % медленнее, 8 с |
| **Разбросанные стеклянные шарики** | Детская коробка, 2-й этаж | Гость поскальзывается и падает, 3 с |
| **Заводная игрушка-обезьянка с тарелками** | Комната с картинами | Бросаешь — шумит 10 с, Гость идёт проверять (приманка) |
| **Ведро над дверью** | Любое ведро | Надевается на голову Гостя, он слепнет на 4 с |

### Ловушки для игрока (срабатывают на манипуляциях)

| Ловушка | Где | Что происходит |
|---|---|---|
| **Падающая балка** | Отрываешь ломом доски от лестницы на чердак | Балка падает: успел отскочить — повезло, не успел — оглушение. Подсказка: скрип и сыпется пыль |
| **Проваливающийся пол** | Чердак, по пути к радиостанции | Провал на 2-й этаж (падение на 2 роста → оглушение + шум, который привлекает Гостя) |
| **Растяжка с банками** | Коридор 2-го этажа после ленты | Громкий шум → Гость идёт проверять |
| **Ложная ступенька** | Длинная лестница в закрытый подвал | Ступенька проваливается, игрок съезжает вниз (без урона, скример-звук) |
| **Ящик-сюрприз в столе** | Если неправильно расставить предметы перед столом | Выскакивает пружинная голова-клоун + звонок → Гость слышит |
| **Падающий шкаф** | Подвал у щитка | Если трогать щиток с открытым ящиком рядом — шкаф падает, перекрывая путь на 10 с |

---

## 4. План работ до и во время подготовки проекта

### Этап 0. Решения и ограничения (до начала)

- Ответить на вопросы из раздела 2.
- **Версия движка:** UE 5.x, последняя стабильная (5.6+). Язык — C++ для систем, Blueprints для уровней и
  событий.
- **Репозиторий.** Текущий репозиторий `Sandbox-Engine` — форк Godot; Unreal-проект лучше вести в
  **отдельном репозитории с Git LFS** (`.uasset`, `.umap`, текстуры, аудио).
- **Что реально могу сделать я, а что нет:**
  - Могу: весь C++ код (персонаж, ИИ, инвентарь, головоломки, сохранения, настройки графики), конфиги
    (`DefaultEngine.ini`, `DefaultInput.ini`, `DefaultScalability.ini`), Python-скрипты для редактора,
    которые сами импортируют ассеты, создают Blueprint-классы, Data Table и собирают уровень из блоков.
    Также: тексты, промпты, таблицы баланса, документацию.
  - Не могу: запустить Unreal Editor в этом облачном контейнере (нет движка и GPU) и создать бинарные
    `.uasset` / `.umap` напрямую. Модели, анимации, звук и музыку тоже не нарисую сам — их нужно
    сгенерировать нейросетями или взять из библиотек по промптам и спискам из этого плана.
  - Поэтому финальную сборку делаешь ты: открываешь проект, запускаешь один Python-скрипт импорта и
    сборки, и он раскладывает всё по местам. Я готовлю всё, что для этого нужно, и пишу инструкцию.

### Этап 1. Дизайн-документ и планировка

1. GDD Акта 1: полный список предметов, головоломок, триггеров, состояний Гостя, порядок прохождения
   (граф зависимостей «предмет → действие → награда»).
2. **Поэтажная схема** (двор, 1-й этаж, 2-й этаж, чердак, подвал, закрытый подвал) с размерами в метрах.
3. Зоны ИИ: «запретные» комнаты у входа (NavArea с повышенной ценой / тег), патрульные маршруты, точки
   осмотра, места для укрытий и тёмные зоны.
4. Сценарии кат-сцен: интро (вид из окна на нападение), смерть + пробуждение, финальная видеозапись,
   титры «Продолжение следует».

### Этап 2. Арт-дирекшн и концепты

1. Мудборд стиля (палитра, пропорции, материалы).
2. Генерация концептов по промптам из раздела 5 (Midjourney / DALL·E / Flux / SDXL).
3. Отбор, правки, утверждение — **до** генерации 3D.
4. Тёрнараунды персонажей (вид спереди, сбоку, сзади в A-позе) — основа для 3D-генерации.

### Этап 3. Техническая база проекта

- Шаблон First Person, C++. Структура папок: `Content/Game/{Characters,Environment,Props,Audio,VFX,UI,Maps,Data}`.
- **Enhanced Input:** контексты `IMC_Keyboard` и `IMC_Gamepad`, автоматическое переключение подсказок
  (иконки клавиш или кнопок) по последнему устройству ввода, переназначение клавиш в меню.
  - Клавиатура: WASD, мышь, E — взять, ЛКМ — использовать или бросить, ПКМ — бросок с замахом,
    Ctrl/C — присесть, Shift — бег, Space — прыжок, 1–6 / колесо — слоты, Q — выбросить, Esc — меню.
  - Геймпад: стики, A/✕ — прыжок, B/○ — присесть, X/□ — взять, RT — использовать или бросить,
    LT — замах, LB/RB — слоты, Y/△ — выбросить, Start — меню. Вибрация при скримере и падении.
- Сохранения (`USaveGame`): инвентарь, состояния головоломок, открытые двери; при смерти — респаун у
  дома с сохранением инвентаря.
- Локализация (Localization Dashboard): RU/EN.

### Этап 4. Основные системы (C++)

| Система | Содержание |
|---|---|
| Персонаж игрока | Движение, приседание (тихий шаг), бег, прыжок, урон от падения (2 роста — оглушение, 3 роста — смерть), руки от первого лица |
| Взаимодействие | Интерфейс `IInteractable`, подсветка, подсказки, захват, физический бросок предметов |
| Инвентарь | 6 слотов, предметы как Data Assets (ключи, лом, ножницы, предохранитель, лампочки, антенна, ружьё) |
| Двери и замки | Двери с цепями и 4 цветными замками, доски (ломаются ломом), паутина (ножницы), лента |
| Шум | `UAISense_Hearing`: громкость от действия (бег, падение предмета, разбитое окно, ловушка) |
| Укрытия и тьма | Освещённость игрока (сэмпл света) влияет на дальность обзора Гостя; укрытия за мебелью |
| Головоломки | Картина-ребус и стол; сейф с барабанами (случайные цифры 3 и 4); лампочки; щиток; радиостанция на Simon Says (4/5/6 сигналов из 8 мониторов, без повторов прошлых последовательностей) |
| Ловушки | Базовый класс `ATrapBase` для ловушек игрока и Гостя |
| Космическое ружьё | Опционально: попадание → Гость «растворяется» на 1,5 с |
| События | Мигание света после жёлтого ключа, музыкальные слои по уровню тревоги |
| Кат-сцены | Level Sequencer: интро, смерть / пробуждение, кассета, НЛО, финал |

### Этап 5. ИИ Гостя

- **StateTree** или Behavior Tree + `UAIPerceptionComponent` (зрение, слух).
- Состояния: *Бродит* → *Подозревает* (идёт на шум) → *Ищет* → *Преследует* → *Ловит* (скример) →
  *Остывает* → возврат к патрулю.
- Уровень тревоги 0–100 с затуханием; при высокой тревоге снимается запрет на две комнаты у входа.
- Фазы активности по прогрессу: старт (1-й этаж) → после цепей (1-й и 2-й этаж, иногда заглядывает
  к входу) → после красного ключа (активнее на 2-м) → после жёлтого (агрессивнее, быстрее).
- Гость не замечает игрока за укрытием, кроме как вплотную; присевшего игрока не слышит.
- Реакции на ловушки и на космическое ружьё.
- Отладка: визуализация конусов зрения и радиусов слуха.

### Этап 6. Производство ассетов

| Категория | Источник / инструмент | Объём (Акт 1) |
|---|---|---|
| Персонажи | Концепт → 3D-генерация (Meshy / Tripo / Rodin / Hunyuan3D) → чистка, ретопология, UV в Blender → риг (AccuRIG / Mixamo / UE IK Retargeter) | Гость, сосед, игрок (руки + полное тело для кат-сцен), паук, пришелец-силуэт в НЛО |
| Анимации | Mixamo, UE5 Animation Sample / Game Animation Sample, генерация (Cascadeur, нейросети motion-to-anim), ручные дочистки | Ходьба, бег, поиск, осмотр, захват, крик, «растворение», связанный сосед, пробуждение игрока, лазание |
| Окружение | Модульный кит (стены, полы, двери, окна, лестницы) + 3D-генерация пропсов | ~150–200 уникальных пропсов |
| Материалы | Substance / Quixel Megascans / процедурные материалы UE; стилизация через мастер-материал | 1 мастер-материал + инстансы |
| Звуки | ElevenLabs SFX, Freesound (CC0), Sonniss GDC bundles | ~150 звуков: шаги по поверхностям, двери, замки, Гость, скримеры, радио, щиток |
| Музыка | Suno / Udio (с коммерческой лицензией) или композитор; слои: спокойно / тревога / погоня / финал | 6–8 треков + стингеры |
| VFX | Niagara: пыль, искры щитка, паутина, «растворение», зелёный луч НЛО, помехи на мониторах | ~15 эффектов |
| UI | Главное меню, пауза, настройки (графика, звук, управление), иконки инвентаря, подсказки | — |

### Этап 7. Оптимизация и масштабирование графики

| Пресет | Освещение | Геометрия | Прочее |
|---|---|---|---|
| **Низкий** (GTX 960 / iGPU) | Без Lumen: SkyLight + дешёвые динамические тени, без глобального освещения | LOD, без Nanite | 50–70 % разрешения + FSR/TSR, без SSR, минимум частиц |
| **Средний** | Lumen Software, низкое качество | Nanite для окружения | TSR, тени Virtual Shadow Maps (низкие) |
| **Высокий / Эпический** | Lumen (Hardware RT, если есть), отражения Lumen | Nanite | DLSS / FSR / XeSS, объёмный туман, высокая плотность частиц |

- Автоопределение пресета при первом запуске (`RunHardwareBenchmark`), ручная настройка в меню.
- Освещение динамическое (из-за мигающего света), но лампы с ограниченным радиусом и без теней там,
  где это допустимо.
- Цель: 60 FPS на среднем ПК в 1080p, 30+ FPS на слабом. Профилирование через Unreal Insights /
  `stat unit` / `stat gpu`.
- Окклюзия: дом поделён на небольшие помещения, уровни — через World Partition или Level Streaming
  (двор / дом / подвал).

### Этап 8. Тестирование и экспорт

- Чек-листы прохождения, тест ИИ (застревания, NavMesh), тест падений, тест обоих способов ввода.
- Pak-файлы, профили упаковки: Windows (DX12 + DX11/SM5 для старых GPU), Linux (Vulkan), при
  необходимости Android (ES3.1 / Vulkan — отдельный пресет графики). Консоли — только с devkit.
- Инструкция по экспорту в `README` проекта.

### Порядок выдачи результатов

1. GDD + схемы уровней + концепты (утверждение).
2. C++ ядро проекта + блокаут дома из серых коробок → **играбельный прототип всего Акта 1**.
3. Импорт ассетов и замена серых коробок (по мере готовности моделей).
4. Звук, музыка, VFX, кат-сцены.
5. Оптимизация, полировка, сборки.

---

## 5. Промпты для генерации концептов

Промпты на английском — генераторы понимают его лучше. Стилевой блок общий для всех; его стоит
добавлять в каждый промпт, чтобы картинки были в одном стиле.

**Стилевой блок (STYLE):**
```
stylized cartoon horror game concept art, in the style of a quirky 3D animated movie, exaggerated
chunky proportions, slightly crooked and bent architecture, saturated warm colors, 1960s American
suburbia, clean readable shapes, hand-painted textures, soft global illumination, high detail,
game-ready design
```

**Для 3D-генерации (добавлять к персонажам и предметам):**
```
full body, A-pose, front view, orthographic, neutral light grey background, even studio lighting,
no shadows, no motion blur, no props overlapping the body, single character, centered
```
Тёрнараунд: `character turnaround sheet, front view, side view, back view, same character, consistent
design, A-pose`.

Негативный промпт (для SD / Flux): `photorealistic, blurry, cropped, extra limbs, multiple
characters, text, watermark, logo, busy background, dramatic shadows on character`.

### 5.1 Двор и экстерьер

**Улица: дом игрока и дом соседа (общий план)**
```
[STYLE], wide establishing shot of a quiet suburban street on a sunny afternoon, two houses facing
each other across the road: on the left a small cozy cream-colored house with a white picket fence
(player's house), on the right a tall, narrow, unsettling two-story house with a steep roof, an attic
dormer window and a pointed metal spire on top, dark teal walls with peeling paint, boarded windows on
the ground floor, an overgrown lawn, an old rusty van parked in the driveway, warm sunlight contrasting
with the gloomy neighbor house
```

**Двор дома соседа с сетчатым забором и пожарной лестницей**
```
[STYLE], side yard of a creepy two-story suburban house, a small area enclosed by a tall chain-link
fence attached to the house wall, a ground-floor window with broken glass inside the fenced area, a
straight vertical rusty metal fire ladder hanging on the wall leading up to a second-floor window,
weeds and old garden tools, a wooden outhouse boarded up with planks standing in the shadow of a big
tree in the back of the yard, late afternoon light
```

**Деревянный туалет (пропс)**
```
[STYLE], isolated prop, old wooden outdoor toilet outhouse with a crescent moon cut-out on the door,
door nailed shut with crooked wooden planks, weathered grey wood, moss at the bottom, neutral grey
background, three-quarter view
```

**Крыша со шпилем и НЛО (кат-сцена)**
```
[STYLE], night scene, roof of a creepy suburban house with a pointed metal spire, a small dented
satellite dish attached to the spire, a classic retro flying saucer hovering above, shining a bright
green tractor beam down onto the roof, a futuristic toy-like ray gun slowly descending in the beam,
stars and purple sky, magical and slightly comedic mood
```

### 5.2 Дом соседа — интерьеры

**Прихожая и коридор с дверью на цепях (центральная локация)**
```
[STYLE], interior, entrance hallway of a creepy old suburban house, view from the front door down a
long corridor, at the far end a heavy wooden door wrapped with three thick chains, each chain locked
with a big colored padlock (red, yellow, blue), a large green padlock on the door itself covered by
thick spider web, doorways to two rooms on the left and right near the entrance, worn floral
wallpaper, creaky wooden floor, dim light through dusty windows, unsettling atmosphere
```

**Левая комната (стол с ломом)**
```
[STYLE], interior, small cluttered storage room of a 1960s house, a wooden worktable with a red
crowbar lying on it, shelves with paint cans and boxes, a dusty lamp, cardboard boxes, a dark corner
behind a cabinet suitable for hiding, warm muted colors, mysterious mood
```

**Правая комната — кабинет (ребус с картиной)**
```
[STYLE], interior, old study room, a large heavy wooden writing desk with an empty surface and a
closed drawer, next to the desk an empty marble pedestal for a sculpture, an inkwell, a thick book,
a small globe and a plaster bust of a mustached man scattered on the floor in different places,
bookshelves, green desk lamp, dusty curtains, puzzle room for a game
```

**Лестница на 2-й этаж**
```
[STYLE], interior, narrow wooden staircase going up to a locked door at the top, the doorway at the
bottom of the stairs boarded up with crooked nailed planks, a window at the bottom landing of the
stairs, cobwebs, dramatic diagonal light rays, claustrophobic feeling
```

**Коридор 2-го этажа (лента, кровавый след, картина)**
```
[STYLE], interior, upstairs hallway of a creepy house, yellow police tape stretched across the
corridor entrance, a smeared dark red trail on the wooden floor leading deep into the hallway, on the
wall a framed painting of a mustached man standing behind a writing desk with an inkwell, a book and
a small globe on it from left to right, flickering ceiling light, ominous mood
```

**Комната с картинами золотого яблока**
```
[STYLE], interior, bedroom-like room with several framed paintings of a golden apple on the walls in
different styles and sizes, one painting slightly tilted, an old wardrobe, a boarded door to the right
of the paintings, faded wallpaper, soft daylight through curtains
```

**Комната с сейфом**
```
[STYLE], interior, small dark closet room, a heavy old steel safe with four vertical rotating number
drums on the front and a keyhole, rust and scratches, a single hanging bulb, dust particles in the air
```

**Комната с лампочками и кровавыми цифрами**
```
[STYLE], interior, dark storage room full of stacked cardboard boxes, four empty wall lamp sockets on
two opposite walls, numbers crudely written in red paint on the wall barely visible in the dark, a
torn note on the floor behind boxes, eerie atmosphere, flashlight-like light
```

**Подвал с электрощитком**
```
[STYLE], interior, damp basement of an old house, a large vintage electrical fuse box on a brick wall
with an empty fuse slot and sparking wires, pipes along the ceiling, old furniture covered with sheets,
a water heater, cold blue and green light, puddles on concrete floor
```

**Чердак с радиостанцией**
```
[STYLE], interior, cramped wooden attic under a steep roof, a huge homemade retro radio station
occupying one wall: eight small CRT monitors in a row, many glowing lamps, dials, antennas, a panel
with eight big toggle switches below the monitors and three red indicator lamps on top, on the left a
small red metal box behind a wire grill, near the entrance an old wardrobe built into the wall and
nailed shut with planks, a dormer window, dust, cables everywhere, mysterious mad-scientist mood
```

**Закрытый подвал — комната видеонаблюдения (финал)**
```
[STYLE], interior, secret basement room at the bottom of a long dark staircase, a surveillance console
with several old CRT monitors showing static, stacks of VHS cassettes, a VCR, a rolling office chair,
concrete walls, a single red lamp, very dark and sinister atmosphere
```

**Дом игрока (стартовая комната и пробуждение)**
```
[STYLE], interior, cozy teenager bedroom in a small suburban house, a bed by the window, the window
looking directly at a creepy neighbor house across the street, posters, toys, a desk with a lamp,
warm evening light, safe and comfortable mood contrasting with the house outside
```

### 5.3 Персонажи

**Игрок (подросток; полное тело для кат-сцен и руки от первого лица)**
```
[STYLE], original character design, curious teenage boy around 14 years old, slim build, slightly
oversized head and big expressive eyes, messy brown hair, wearing a red and white striped t-shirt
under an open denim vest, blue shorts with rolled hems, worn sneakers, band-aid on the knee, a small
backpack, adventurous and brave expression, [3D-блок]
```
Руки: `first-person view game arms, two hands of a teenage boy with denim vest sleeves cut at the
shoulder... stylized cartoon, separate isolated arms, neutral background`.

**Сосед (жертва; появляется в интро, на картине, в бюсте и на видеозаписи)**
```
[STYLE], original character design, stocky middle-aged man around 50 years old, big round belly,
large bushy black mustache, thick unibrow, short dark hair with a bald spot, wearing a light blue
collared shirt with rolled-up sleeves under a brown knitted sweater vest, dark brown trousers with
suspenders, brown leather shoes, grumpy but not evil expression, [3D-блок]
```
Вариант «связанный»: `same character, hands tied with thick rope, mouth covered with duct tape,
scared expression`.

**Гость (главный антагонист)**
```
[STYLE], original villain character design, extremely tall and thin mysterious figure around 2.3
meters tall, unnaturally long arms and fingers in black leather gloves, wearing a long tattered black
trench coat with a high raised collar, a wide-brimmed black hat, face hidden behind a pale cracked
porcelain mask with a long curved bird-like beak and two dark empty eye holes, crow feathers sticking
out from under the collar, slightly hunched posture, unsettling and menacing but stylized, not gory,
[3D-блок]
```
Скример (для 2D-референса кат-сцены): `extreme close-up of the masked figure lunging at the camera,
beak mask filling the frame, gloved hands reaching forward, harsh rim light, dark background`.

**Паук (скример у паутины)**
```
[STYLE], isolated creature, small cartoon spider with big googly eyes and fuzzy legs, more funny than
scary, black body with orange spots, [3D-блок, view from above and front]
```

### 5.4 Ключевые предметы (для 3D-генерации)

Каждый промпт = `[STYLE], isolated game prop, <описание>, neutral grey background, three-quarter view,
even lighting`:

- `big old-fashioned skeleton key with a colored painted bow` — ×4 цвета (red, yellow, blue, green)
- `heavy padlock painted bright <color> with a thick chain`
- `red metal crowbar with worn paint`
- `old steel scissors with black handles`
- `vintage ceramic electrical fuse with brass caps`
- `vintage incandescent light bulb`
- `small dented rusty satellite dish antenna`
- `retro sci-fi toy ray gun with glowing green tube and chrome fins`
- `inkwell with a feather quill`, `thick old leather book`, `small desk globe on a brass stand`,
  `plaster bust of a mustached man`
- `wind-up cymbal monkey toy`, `rusty bear trap`, `bucket of sticky glue`, `bag of glass marbles`
- `VHS cassette with handwritten label`, `CRT surveillance monitor`

---

## 6. Что нужно от тебя для старта

1. Ответы на вопросы из раздела 2 (или «бери предложенные варианты»).
2. Утверждение концептов (после генерации по промптам).
3. Список платформ и минимальное «железо».
4. Подтверждение, что Unreal-проект ведём в **отдельном** репозитории (Git LFS), а не в форке Godot.
