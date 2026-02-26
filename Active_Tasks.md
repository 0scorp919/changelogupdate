# 🎯 Active Tasks — Autonomous Capsule System

Цей файл містить список активних завдань, що потребують виконання або контролю.

---

## [📅] Заплановано (Фаза 2.5 — Remote Desktop)

- [ ] **RustDesk — крос-платформний RDP/VDI клієнт** (https://rustdesk.com/?lang=en)
  - [ ] Дослідження: RustDesk vs TeamViewer vs AnyDesk (переваги/ризики)
  - [ ] Створення `devops/rustdeskupdate/` (за шаблоном rdpupdate)
  - [ ] Завантаження портативної версії (Windows x64)
  - [ ] Створення `rustdesk_manager.py`:
    - [ ] Автозавантаження останньої версії з rustdesk.com
    - [ ] Конфігурація ID/Key (з Vaultwarden)
    - [ ] Підтримка власного сервера (relay server)
    - [ ] Бекап конфігурації (AES-256)
  - [ ] Створення `rustdesk_launcher.bat`
  - [ ] Створення `.env` + `.env.example`
  - [ ] Публікація на GitHub (0scorp919/rustdeskupdate)

---

## [📅] Заплановано (Фаза 3 — Автоматизація)

- [ ] **Скрипт бекапу всієї капсули**: Створення універсального скрипта для AES-256 шифрування всієї структури `C:\!Oleksii_Rovnianskyi` (окремо від `robocopy`-копіювання).
  - [ ] Розробка `capsule_backup_manager.py` з AES-256 шифруванням
  - [ ] Інтеграція з Vaultwarden для пароля
  - [ ] Ротація 7+4 (ISO-week стандарт)
  - [ ] Верифікація архіву після створення
  - [ ] Виключення тимчасових файлів (downloads/, logs/ старші 7 днів)
- [ ] **Health-check скрипт**: Перевірка цілісності бінарних файлів (SHA256), наявності необхідних шляхів у PATH, стану Vaultwarden-з'єднання.
  - [ ] Перевірка SHA256 бінарних файлів у `apps/`
  - [ ] Перевірка наявності всіх 12 шляхів капсули в системному PATH
  - [ ] Тест Vaultwarden з'єднання (bw status)
  - [ ] Перевірка цілісності `.env` файлів (відсутність реальних даних у `.env.example`)
  - [ ] Аудит відповідності менеджерів шаблону `base_manager.py`

---

## [📅] Заплановано (Фаза 4 — Security Lab)

- [ ] **Окремий workspace для Security Lab** (`0scorp919`)
  - [ ] Створення `Security_Lab.code-workspace` з окремими коренями
  - [ ] Налаштування окремого SSH ключа для security репозиторіїв
  - [ ] Ізоляція PATH (security tools окремо від основної капсули)

- [ ] **Інструменти pentesting** (портативні, в `apps/`)
  - [ ] Дослідження та вибір портативних інструментів (nmap, wireshark, burp suite portable)
  - [ ] Створення менеджерів для кожного інструменту (за шаблоном `base_manager.py`)
  - [ ] Інтеграція з Vaultwarden для конфіденційних конфігурацій

- [ ] **VPN/proxy конфігурація**
  - [ ] Налаштування портативного VPN клієнта
  - [ ] Автоматичне перемикання профілів VPN залежно від активності
  - [ ] Ізоляція трафіку security tools через окремі мережеві інтерфейси

---

## [📅] Заплановано (Фаза 5 — Синхронізація)

- [ ] **Sync між пристроями** (Syncthing / rclone)
  - [ ] Дослідження Syncthing Portable vs rclone
  - [ ] Створення менеджера синхронізації
  - [ ] Конфлікт-детекшн для файлів капсули

- [ ] **Автоматичний git push `second-brain` за розкладом**
  - [ ] Розробка `git_sync_manager.py` з розкладом (щоденно/щотижня)
  - [ ] Перевірка змін перед push (чи не порожній commit)
  - [ ] Обробка помилок мережі/автентифікації

- [ ] **Конфлікт-резолюція для Obsidian vault**
  - [ ] Аналіз форматів конфліктів Git для `.md` файлів
  - [ ] Розробка скрипта автоматичного merge (з підтримкою frontmatter)
  - [ ] Інтеграція з Obsidian через URI схеми

---

## [📅] Заплановано (Фаза 6 — Системні покращення)

- [x] **Оновлення README.md з актуальними версіями** (2026-02-26)
  - [x] Ручне оновлення версій: 7zip v1.3→v1.4, bin v1.7→v2.2, changelog v1.1.0→v1.3.2
  - [x] Версія капсули: 2.3.35 → 2.3.49
  - [x] Консистентність з CHANGELOG.md ✅

- [ ] **Скрипт автоматичного парсингу версій з `*_manager.py` файлів**
  - [ ] Оновлення таблиці версій при кожному запуску менеджера
  - [ ] Перевірка консистентності версій між README та реальними файлами

- [ ] **Розширення .cline_worker_rules з конкретними шаблонами**
  - [ ] Додавання шаблонів для типових задач (форматування, пошук, документація)
  - [ ] Правила для уникнення розгортання Windows змінних середовища
  - [ ] Чеклист перевірки перед записом у CHANGELOG/Active_Tasks

- [ ] **Автоматична перевірка консистентності .clinerules ↔ Clinerules_Full.md**
  - [ ] Скрипт порівняння структур
  - [ ] Виявлення розбіжностей під час сесії
  - [ ] Автоматичне створення PR для виправлення

- [ ] **Шаблони документації для нових менеджерів**
  - [ ] Розширення `devops/_template/capsule_manager/` шаблону
  - [ ] Автоматичне створення README.md з плейсхолдерами
  - [ ] Чеклист публікації на GitHub

- [ ] **Оптимізація процесу CHANGELOG**
  - [ ] Скрипт автоматичного додавання записів з git commit history
  - [ ] Валідація формату "Keep a Changelog"
  - [ ] Автоматичне архівування старих записів

## [📅] Заплановано (Фаза 7 — Покращення менеджерів)

- [ ] **Аналіз та резолюція конфлікту між manager_standard та реальними менеджерами**
  - [ ] Етап 1: Аудит поточного стану (класифікація менеджерів)
  - [ ] Етап 2: Оновлення шаблону base_manager.py (збільшення до 12 обов'язкових функцій)
  - [ ] Етап 3: Створення двох нових шаблонів: full_manager.py (з даними користувача) та cli_manager.py (без даних)
  - [ ] Етап 4: Документація різниці між типами менеджерів в .clinerules та README.md
  - [ ] Етап 5: Послідовне оновлення існуючих менеджерів до нових шаблонів
  - [ ] Етап 6: Оновлення .clinerules з уточненими вимогами manager_standard

- [ ] **Класифікація менеджерів (3 типи):**
  - [ ] Повні менеджери (з даними користувача): chrome, git, obsidian, python, vscode, telegram, rdp, doublecmd
  - [ ] CLI менеджерів (без даних користувача): 7zip, bin, pwsh, node, clinecli, path
  - [ ] Спеціальні менеджери (унікальна логіка): changelog

- [ ] **Критичні покращення:**
  - [ ] Додавання відсутніх функцій: get_manager_hash(), ensure_dependencies(), Colors class + cprint(), draw_progress()
  - [ ] Уніфікація логіки здоров'я: health_check() для перевірки стану Vaultwarden, дисків, мережі
  - [ ] Інтеграція OpenTelemetry hooks для спостережності
  - [ ] Auto‑close after 30 секунд неактивності (запобігання orphaned console)
  - [ ] Документація кожного менеджера у README проекту з поясненням типу

- [ ] **Аудит менеджерів на відповідність новим правилам .clinerules**
  - [ ] Перевірка всіх менеджерів на відповідність 10MB ліміту для логів (>1MB streaming, >50MB rotation)
  - [ ] Оновлення логіки cleanup_old_logs() для дотримання нового стандарту
  - [ ] Перевірка відповідності новій AI термінології (Architect via OpenRouter, CLI Worker via OpenRouter)
  - [ ] Оновлення документації менеджерів згідно з новими правилами делегування
  - [ ] Перевірка та оновлення шаблонів у devops/_template/capsule_manager/

---

## [✅] Нещодавно завершено

- [x] **binupdate — стандартизація динамічного таймера автозакриття** (2026-02-26): `bin_manager.py` v2.3 → v2.4:
  - Замінено статичне "Вікно закриється через 30 секунд..." на динамічний зворотний відлік
  - Тепер показує: `Автозакриття через 30 с...` → `...29 с...` → `...0 с`
  - Патерн: `for i in range(30, 0, -1)` + `sys.stdout.write(f"\r...")` + `time.sleep(1)`
  - Відповідає референсу 7zip_manager.py та стандарту manager_standard
  - Оновлено CHANGELOG.md [2.3.54], README.md проекту v2.4 ✅.

- [x] **capsule_manager template — оновлено за референсом 7zipupdate v1.4** (2026-02-26): `base_manager.py` v3.0 → v3.1:
  - Додано `show_path_info()` — інформація про реєстрацію в PATH
  - Додано `ENABLE_BACKUPS` — флаг для вимкнення бекапів (для CLI-інструментів без даних)
  - Покращено `ensure_in_system_path()` — логіка з show_path_info()
  - Покращено `_rotate_log_if_needed()` — >50 MB → part-файл
  - Покращено `cleanup_old_logs()` — стискання part-файлів в .gz
  - Покращено `main()` — порядок кроків: PATH → logs → update
  - Додано `AutoCloseTimer reset()` в cprint/draw_progress
  - Оновлено `network_request_with_retry()` — retry з backoff
  - Оновлено README.md template — версія 3.1
  - Синхронізовано CHANGELOG.md [2.3.52]. ✅.

- [x] **changelogupdate — рахувальний таймер автозакриття + виправлення логіки архівування** (2026-02-26): `changelog_manager.py` v1.3.1 → v1.3.2. (1) Рахувальний countdown loop: `for i in range(30, 0, -1)` замість `time.sleep(30)`. Показує "Автозакриття через 30 с..." → "...0 с". (2) Видалено секцію `[Заплановано]` з парсингу — тепер не вважається частиною записів. (3) Логіка KEEP_DAYS працює правильно: cutoff = сьогодні - 5 днів. Синхронізовано CHANGELOG.md [2.3.48]. ✅.

- [x] **changelogupdate — виправлено AutoCloseTimer** (2026-02-26): `changelog_manager.py` v1.2.0 → v1.2.1. Проблема: вікно закривалось одразу після завершення роботи. Фікс: `time.sleep(30)` після успішного виконання + повідомлення "Вікно закриється через 30 секунд...". Синхронізовано CHANGELOG.md [2.3.44]. ✅.
- [x] **7zipupdate — приведено до стандарту manager_standard v3.0** (2026-02-26): `7zip_manager.py` v1.3 → v1.4:
  - `health_check()` — перевірка критичних компонентів
  - `error_reporting()` — структурована обробка помилок
  - `DEFAULT_TIMEOUT` + `network_request_with_retry()` — retry з backoff
  - `AutoCloseTimer` — автозакриття через 30 сек бездіяльності
  - `_load_env()` — завантаження .env (сумісність)
  - `cleanup_old_logs()`: стискання part-файлів в .gz
  - Оновлено `.gitignore`: додано `*.log.gz`, `.pytest_cache/`, `.mypy_cache/`
  - Оновлено `README.md`: CHANGELOG v1.4
  - Синхронізовано `CHANGELOG.md` [2.3.36]. ✅.
- [x] **Додано Security Incident Response Protocol** (2026-02-25): Додано новий розділ `<security_incident_response>` до `.clinerules`:
  - **Triggers**: compromised credentials detected, secret leakage in logs/repo, unauthorized access attempt, malware/vulnerability detected
  - **Actions**: isolate affected component → log incident with timestamp, severity (P1-P4), affected systems → notify user within 5 minutes → do NOT auto-remediate without confirmation → document root cause in `logs/.incidents/`
  - **Severity levels**: P1 (Active breach, data exfiltration → STOP ALL OPERATIONS), P2 (Compromised credentials → rotate immediately), P3 (Potential vulnerability → schedule remediation), P4 (Minor misconfiguration → log for review)
  - Синхронізовано `.clinerules` та `second-brain/rules/Clinerules_Full.md`. Оновлено CHANGELOG.md [2.3.30]. ✅.
- [x] **Аналіз та усунення системних проблем .clinerules** (2026-02-25): Додано Risk Levels в .clinerules для розуміння делегування без читання .cline_worker_rules. Додано SSH архітектуру в .clinerules (раніше був тільки в Clinerules_Full.md). Уточнено що сесія = виклик attempt_completion, закривається тільки після "Кінець сесії". Синхронізовано Clinerules_Full.md з резюме Risk Levels. Оновлено CHANGELOG.md [2.3.26]. ✅.
- [x] **Оновлення глосарію запускачів у .clinerules з уточненням трьох типів** (2026-02-25): Уточнено визначення трьох типів запускачів: Windows Shortcut (.lnk) — Windows shortcut file in `tags/` for launch via `Win+R`. Points to the corresponding portable launcher in `devops/<app>update/`. Uses WScript.Shell COM object for creation. Not published to GitHub. Portable Launcher (Портативний запускач) — `.bat` file in `devops/<app>update/` with auto‑detect `CAPSULE_ROOT`. Contains full launch logic, including path detection, error handling, and UI. GitHub‑ready, published with the project. System Launcher (Legacy) — `.bat` file in `tags/_old/` (archived). Formerly used as symbolic link to portable launchers. Replaced by Windows shortcuts (.lnk) for cleaner architecture. Контекст: Ярлики `.lnk` створюються скриптом `tags/_create_shortcuts.ps1` та спрямовують на портативні лаунчери. Оновлено CHANGELOG.md [2.3.25]. ✅.
- [x] **Усунення суперечливості щодо обробки великих логів між `<devops_standards>` та делегуванням Worker** (2026-02-24): Виявлено логічну проблему: у `<devops_standards>`: "NEVER read full log files if >1MB", у делегуванні: "Searching large logs (>1MB) — using bash tools (tail, grep, head)". Замінено абсолютний заборон у `<devops_standards>` на практичний: "NEVER load entire log file into memory or use read_file on log files >1MB. Instead, use streaming tools (tail, grep, head, awk) with appropriate limits to extract relevant context without reading entire file." Це узгоджує правило з делегуванням пошуку великих логів CLI Worker. Оновлено `.clinerules`, `second-brain/rules/Clinerules_Full.md` та CHANGELOG.md [2.3.24]. ✅.
- [x] **Усунення дублювання інформації про делегування між .clinerules, .cline_worker_rules та Clinerules_Full.md** (2026-02-24): Виявлено та вирішено проблему DRY-порушення. Конкретні критерії делегування (рівні ризиків, приклади) тепер зосереджені **тільки** в `.cline_worker_rules`. З `.clinerules` видалено секцію `<delegation_criteria>`, залишено лише концептуальні правила `<delegation_protocol>`. Оновлено `.cline_worker_rules` з повними критеріями делегування. Синхронізовано `Clinerules_Full.md` з поясненням системи DRY. Створено резервні копії всіх файлів перед змінами. ✅.
- [x] **Переклад глосарію термінів у .clinerules на англійську мову з українськими відповідниками** (2026-02-24): Глосарій тепер містить англійські терміни для міжнародного розуміння з українськими відповідниками: Autonomous Capsule (Капсула), Architect (Шеф), CLI Worker (Раб), Manager Script (Менеджер), Launcher (Запускач), Portable Tool (Портативний інструмент). Додано розділи: Delegation Criteria, Edge Cases, Technical Definitions. Синхронізовано з second-brain/rules/Clinerules_Full.md (розділ 11). Оновлено CHANGELOG.md [2.3.21]. ✅.
- [x] **node_manager.py v1.4 → v1.5 — фікс Windows-специфічного npm багу ENOTEMPTY** (2026-02-24): Виправлено попередження `npm warn cleanup Failed to remove some directories` з помилкою `ENOTEMPTY: directory not empty, rmdir '...\node_modules\hline\date-fns\locale\de-AT'`. Замінено `npm update -g` на окремі `npm install -g <pkg>@latest` для кожного застарілого пакету. Обробка warning-ів: якщо `npm install -g` повертає помилку з "ENOTEMPTY", вважаємо це лише warning cleanup та логуємо як успішне оновлення. Оновлено CHANGELOG.md [2.3.20], README.md v1.5 та node_manager.py __version__ = "1.5". ✅.
- [x] **Session Analysis & Documentation Sync** (2026-02-23): Аналіз структури капсули, перегляд Active_Tasks.md, CHANGELOG.md, README.md, визначення пріоритетів за планом Фаз 3-6. Виконання session_closing_protocol: синхронізація документації. Оновлено CHANGELOG.md [2.3.18] та Active_Tasks.md. README.md перевірено на актуальність (версії, репозиторії). ✅.
- [x] **Аудит 7zipupdate / binupdate / changelogupdate — ISO-week compliance** (2026-02-23): Повний аудит `_rotate_backups()`, `cleanup_old_logs()`, CAPSULE_ROOT auto-detect. Всі три менеджери відповідають стандарту — зміни не потрібні. `7zip_manager.py` v1.3, `bin_manager.py` v1.7, `changelog_manager.py` v1.1.0 ✅. CHANGELOG [2.3.17].
- [x] **Аудит менеджерів — ISO-week ротація бекапів** (2026-02-23): Повний аудит та виправлення `_rotate_backups()` у всіх менеджерах капсули. Замінено Monday-only алгоритм на ISO-week (7 щоденних + 4 тижневих). Виправлено: `chrome_manager.py`, `git_manager.py` v1.6, `obsidian_manager.py` v1.3, `python_manager.py` v1.1, `vscode_manager.py` v1.3, `telegram_manager.py` v1.1, `rdp_manager.py` v3.1, `doublecmd_manager.py` v1.5, `base_manager.py`. Також виправлено `cleanup_old_logs()` today-protection та CAPSULE_ROOT auto-detect. CHANGELOG [2.3.16].
- [x] **pathupdate — публікація на GitHub як публічний репозиторій** (2026-02-23): Створено `0scorp919/pathupdate` (public). Git init + commit `54addf3` + push → `git@github-security:0scorp919/pathupdate.git`. Виправлено коментарі `PATH_12→NN` у `fix_path.ps1`. Оновлено `CHANGELOG.md` [2.3.12].
- [x] **pathupdate — рефакторинг path_manager.py v1.6.0: єдине джерело правди** (2026-02-23): Видано хардкод `_default_paths` (12 шляхів). `load_capsule_paths()` читає `PATH_01..PATH_NN` ТІЛЬКИ з `.env` (як `fix_path.ps1`). Без `.env` або без `PATH_*` → ERROR + exit. Підтримка динамічних `PATH_13+`. `.env.example` оновлено: `PATH_*` розкоментовані як обов'язкові. `README.md` оновлено. Оновлено `CHANGELOG.md` [2.3.11].
- [x] **pathupdate — фікс path_launcher.bat v2.1** (2026-02-23): `path_launcher.bat` v1.2→v2.1 — поганий вигляд при запуску з `devops\pathupdate\`. Причини: кирилиця в `echo` → `...`, PowerShell `Split-Path` для CAPSULE_ROOT, відсутній `setlocal`. Фікс: ASCII-only echo, `for %%A in ("%SCRIPT_DIR%..\..") do set "CAPSULE_ROOT=%%~fA"` (два рівні вгору), `setlocal` до UAC. Оновлено `CHANGELOG.md` [2.3.10].
- [x] **pathupdate — фікс подвійного виводу в консоль** (2026-02-23): `path_manager.py` v1.5.0→v1.5.1 — прибрано `StreamHandler(sys.stdout)` з `logging.basicConfig`. Лог → тільки файл, консоль → виключно через `cprint()` у `log()`. Оновлено `CHANGELOG.md` [2.3.8].
- [x] **pathupdate — повний аудит та приведення до стандарту** (2026-02-23): `path_manager.py` v1.4→v1.5 (українська мова, емодзі, log→stdout+file, таймер). `tags/path.bat` v1.0→v2.0 (прибрано хардкод, auto-detect від `%~dp0`). `README.md` оновлено: версії v1.5.0, PATH_01..12, секція лаунчерів, алгоритми, CHANGELOG. Оновлено `CHANGELOG.md` [2.3.7].
- [x] **pathupdate — verify_paths() фікс: завжди [--]** (2026-02-23): Виявлено два баги: (1) `os.environ["PATH"]` — стале значення від батьківського процесу; (2) `.env` зберігає шляхи з `/`, системний PATH має `\` → порівняння завжди `False`. Фікс: нова функція `_get_system_path_from_registry()` читає PATH з HKLM реєстру через `winreg`. Нормалізація: `p.replace("/", "\\").rstrip("\\").lower()`. Підтверджено тестом: 12/12 `[OK]`. Також: `ensure_in_system_path()` → no-op, `run_fix_path()` → портативний `PWSH_EXE`. Оновлено `CHANGELOG.md` [2.3.6].
- [x] **pathupdate — path_launcher.bat v1.2: фікс CMD + `!` у шляху** (2026-02-23): PowerShell `Split-Path` для auto-detect `CAPSULE_ROOT`. Оновлено `CHANGELOG.md` [2.3.6].
- [x] **pathupdate — fix_path.ps1 v1.6: шляхи з .env** (2026-02-23): Усунено дублювання — шляхи більше не хардкодовані у скрипті. `Read-EnvPaths` парсить `.env`, `SortedDictionary`. Оновлено `CHANGELOG.md` [2.3.5].
- [x] **pathupdate — підготовка до публікації в git** (2026-02-23): Рефакторинг `path_manager.py` v1.0→v1.4, `.env` з 12 шляхами, `.env.example` до PATH_12. Оновлено `CHANGELOG.md` [2.3.3–2.3.5].
- [x] **obsidianupdate — публікація на GitHub** (2026-02-23): Створено репо `0scorp919/obsidianupdate`. Git init + commit `f206eef` + push → `git@github-security:0scorp919/obsidianupdate.git`. Оновлено `CHANGELOG.md` [2.3.2].
- [x] **obsidianupdate — підготовка до публікації в git** (2026-02-23): Виправлено `obsidian_launcher.bat`. Видано ~16700 символів мертвого коду. Оновлено `README.md`. Оновлено `CHANGELOG.md` [2.3.1].
- [x] **GitHub repo visibility fix — clinecliupdate та nodeupdate → public** (2026-02-23): Всі 10 репозиторіїв `0scorp919` тепер public ✅. Оновлено `CHANGELOG.md` [2.2.6].
- [x] **clinecli_manager.py v1.2 — фікс npm install при timeout registry** (2026-02-23): Флаг `npm_view_ok`. Linter OK. Оновлено `CHANGELOG.md` [2.2.5].
- [x] **Launcher.bat (FULL style) + .gitignore для всіх devops проектів** (2026-02-23): 8 лаунчерів + 7 `.gitignore`. Оновлено `CHANGELOG.md` [2.2.4].
- [x] **nodeupdate — публікація на GitHub** (2026-02-23): Commit `1ed6d99` → `git@github-security:0scorp919/nodeupdate.git`. Оновлено `CHANGELOG.md` [2.2.3].
- [x] **clinecliupdate — публікація на GitHub** (2026-02-23): Git init + push → SSH `id_ed25519_security`. Оновлено `CHANGELOG.md` [2.2.2].
- [x] **binupdate — git push v1.7** (2026-02-23): Commit `94533de`. Оновлено `CHANGELOG.md` [2.2.1].
- [x] **SSH архітектура капсули — документування та фікс** (2026-02-22): `core.sshCommand` у `second-brain/.git/config`. `<capsule_git_ssh>` у `.clinerules`. Оновлено `CHANGELOG.md` [2.1.7].
- [x] **README.md (root) — повний перегляд та оновлення** (2026-02-22): Актуальні версії менеджерів, sqlite3 в bin/, таблиці → bullet-списки. Оновлено CHANGELOG.md [2.1.5].
- [x] **clinecliupdate — аудит перед публікацією на GitHub** (2026-02-22): README v1.0→v1.1, шляхи, CHANGELOG секція. Оновлено CHANGELOG.md [2.1.4].
- [x] **Cline terminalOutputLineLimit: 1000 → 500** (2026-02-22): Фікс `prompt is too long`. Оновлено `CHANGELOG.md` [2.1.3].
- [x] **clinecli_manager.py v1.1 — фікс PowerShell EncodedCommand** (2026-02-22): `-EncodedCommand <base64 UTF-16LE>`. Linter OK. Оновлено `CHANGELOG.md` [2.1.1].
- [x] **FinOps AI-архітектура: Cline CLI + CLI Worker** (2026-02-22): `.cline_worker_rules`, `clinecli_manager.py` v1.0, `<delegation_protocol>` у `.clinerules`. Оновлено `CHANGELOG.md` [2.1.0].
- [x] **binupdate v1.6: sqlite3.exe** (2026-02-22): `get_latest_version_sqlite_org()`, int-порівняння версій. Лінтер OK.
- [x] **nodeupdate — підготовка до публікації на GitHub** (2026-02-22): `node_manager.py` v1.3→v1.4, `node_launcher.bat`, `.gitignore`, `.env.example`. Оновлено `CHANGELOG.md`.
- [x] **gitupdate — підготовка та публікація на GitHub** (2026-02-22): `git_manager.py` v1.5→v1.6, `git_launcher.bat`. Опубліковано: https://github.com/0scorp919/gitupdate. Оновлено `CHANGELOG.md` [2.0.6–2.0.8].
- [x] **README.md — секція "Репозиторії": локальні шляхи та позначки** (2026-02-22): SSH URL + локальний шлях для 5 репозиторіїв. Оновлено `CHANGELOG.md` [2.0.5].
- [x] **session_closing_protocol — додано в .clinerules та Clinerules_Full.md** (2026-02-22): `<session_closing_protocol>` блок. Оновлено `Clinerules_Full.md`.
- [x] **doublecmdupdate — підготовка до публікації на GitHub** (2026-02-22): `doublecmd_manager.py` v1.3→v1.4, `doublecmd_launcher.bat`, `.gitignore`. Оновлено `CHANGELOG.md` [2.0.2].
- [x] **chromeupdate — підготовка до публікації на GitHub** (2026-02-21): `chrome_manager.py` v9.4.14→v9.4.15, `chrome_launcher.bat`, `.gitignore`. Оновлено `CHANGELOG.md` [2.0.1].
- [x] **changelogupdate — підготовка до публікації на GitHub** (2026-02-21): `changelog_manager.py` v1.0.0→v1.1.0, `changelog_launcher.bat`, `.gitignore`, `.env.example`. Оновлено `CHANGELOG.md` [2.0.0].
- [x] **binupdate — підготовка до публікації в GitHub** (2026-02-21): `bin_manager.py` v1.4→v1.5, `bin_launcher.bat`, `.gitignore`. Оновлено `CHANGELOG.md` [1.9.9].
- [x] **7zipupdate — портативний лаунчер для GitHub** (2026-02-21): `7zip_launcher.bat`. Оновлено `CHANGELOG.md`.
- [x] **7zipupdate — підготовка до публікації в GitHub** (2026-02-21): `7zip_manager.py` v1.2→v1.3, `.gitignore`. Оновлено `CHANGELOG.md`.
- [x] **README.md аудит та оновлення** (2026-02-21): Версії менеджерів, Vaultwarden секція, downloads/ опис.
- [x] **Chrome Manager v9.4.14** (2026-02-20): Фікс NSIS online-інсталятора.
- [x] **Git Manager v1.5** (2026-02-20): Резервна копія `apps/git/` + `.ssh/` з Vaultwarden.
- [x] **Obsidian Manager v1.3** (2026-02-20): Фікс розміру бекапу (162 MB → ~1 MB).
- [x] **Changelog Manager v1.0** (2026-02-20): Архівування CHANGELOG.md → second-brain/4_Archives/.
- [x] **Path Manager v1.0** (2026-02-20): Python-обгортка для fix_path.ps1 з таблицею стану PATH.
- [x] **Подвійне зависання таймера** (2026-02-20): Фікс у всіх 11 менеджерах + 11 лаунчерах.
- [x] **ANSI кольори в CMD** (2026-02-20): Фікс `os.system("")` у path_manager та changelog_manager.
- [x] **Chrome Manager v9.4.x** (2026-02-20): Повний Vaultwarden-стек, bw status логіка, clipboard UIPI фікс.
- [x] **RDP Manager v3.0** (2026-02-19): Рефакторинг на конфігурацію Група→Сервер→Акаунт у `.env`.
- [x] **Node.js Manager** (2026-02-19): Автооновлення LTS + глобальні npm-пакети.
- [x] **Python Manager** (2026-02-19): Автооновлення WinPython + pip freeze/restore/upgrade.
- [x] **Git Manager v1.4** (2026-02-19): Виправлення парсингу версій, інтеграція GitHub CLI.
- [x] **Bin Manager v1.4** (2026-02-19): Додано bw.exe, GITHUB_TOKEN, get_manager_hash().

---

## 📊 Пріоритети та оцінка часу

**Високий пріоритет (1-2 тижні):**
1. Health-check скрипт (частина Фази 3) — критично для стабільності
2. Скрипт автоматичного парсингу версій — для підтримки актуальності README
3. Розширення .cline_worker_rules — зменшує помилки Worker

**Середній пріоритет (2-4 тижні):**
4. Скрипт бекапу всієї капсули — важливий для безпеки
5. Автоматична перевірка консистентності .clinerules — запобігає розбіжностям
6. Шаблони документації — прискорює створення нових менеджерів

**Низький пріоритет (1-2 місяці):**
7. Security Lab workspace — новий функціонал
8. Sync між пристроями — складність інтеграції
9. Оптимізація процесу CHANGELOG — покращення workflow

---

## ✅ Критерії успіху для кожного завдання

- [ ] Відповідність стандартам капсули (auto-detect шляхів, AES-256, ротація)
- [ ] Повна документація у 4 місцях (скрипт, CHANGELOG, README проекту, README капсули)
- [ ] Self-healing та ідемпотентність
- [ ] Інтеграція з Vaultwarden де потрібно
- [ ] Портативність (без хардкоду, працює з будь-якого шляху)

---

> *Оновлено: 2026-02-26 (README.md — приведення у відповідність до версій менеджерів)*
