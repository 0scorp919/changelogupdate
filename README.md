# 🧊 Autonomous Capsule System

> **Портативна, самодостатня робоча система для Windows.**
> Все в одній папці. Підключив флешку/диск — працюєш.

```
Автор: Oleksii Rovnianskyi
Email:  oleksii.rovnianskyi@gmail.com
GitHub: oleksii-rovnianskyi (main) | 0scorp919 (devops / personal)
Версія: 2.3.65
```

---

## ️ Структура капсули

```
C:\!Oleksii_Rovnianskyi\
│
├── 📁 apps/          ← Портативні застосунки (git, python, node, pwsh, vscode, chrome, obsidian, ...)
├── 📁 second-brain/  ← Obsidian vault + Git repo (PARA: Inbox, Projects, Areas, Resources, Archives)
├── 📁 devops/        ← Менеджери автооновлення (по одному на кожен застосунок) та проекти
├── 📁 backups/       ← Резервні копії (AES-256, 7 щоденних + 4 тижневих)
├── 📁 logs/          ← Логи менеджерів (7 днів + 50 MB ротація)
├── 📁 downloads/     ← Тимчасові завантаження
├── 📁 tags/          ← .lnk ярлики для запуску (Win+R → <name>)
│
├── 📄 .clinerules              ← Правила AI-асистента (Cline Architect)
├── 📄 Active_Tasks.md          ← Активні завдання
├── 📄 CHANGELOG.md             ← Журнал змін
├── 📄 README.md                ← Цей документ (детальний опис проекту)
└── 📄 Main_System.code-workspace  ← VS Code workspace (capsule + second-brain + devops)
```

---

## 🚀 Компоненти системи

Патерн запуску: `Win+R → <name>` → `tags/<name>.lnk` → `devops/<name>update/<name>_manager.py` → `apps/<name>/`

Кожен менеджер при запуску: UAC elevation → PATH check → ротація логів → резервна копія (якщо є дані) → перевірка оновлень → оновлення → запуск застосунку → автозакриття (30 сек).

### Застосунки

- `Win+R → code` · `vsupdate/vscode_manager.py` · v1.3 · `apps/vscode/`
  VS Code Portable. Бекап `data/` (AES-256). Vaultwarden. При старті запускає всі менеджери паралельно у фоні.

- `Win+R → chrome` · `chromeupdate/chrome_manager.py` · v9.4.15 · `apps/chrome/`
  Chrome Portable (portableapps.com, NSIS). Бекап профілю (AES-256). Vaultwarden. ⚠️ Тільки Ctrl+V (UIPI/UAC).

- `Win+R → git` · `gitupdate/git_manager.py` · v1.6 · `apps/git/`
  Git for Windows Portable. Бекап `apps/git/` + `.ssh/` (AES-256, `-mhe=on`). SSH перевірка обох акаунтів. Vaultwarden.

- `Win+R → node` · `nodeupdate/node_manager.py` · v1.5 · `apps/node/`
  Node.js LTS Portable (парна мажорна версія). Збереження глобальних пакетів, `npm rebuild`. Запускає PowerShell з Node у PATH.

- `Win+R → python` · `pythonupdate/python_manager.py` · v1.1 · `apps/python/current/`
  WinPython Portable (dot edition). `pip freeze` → відновлення → upgrade. Бекап `current/` (AES-256). Запускає WinPython Command Prompt.

- `Win+R → pwsh` · `pwshupdate/pwsh_manager.py` · v5.3 · `apps/pwsh/`
  PowerShell Portable (GitHub Releases). Бекап профілю (AES-256). Vaultwarden.

- `Win+R → obsidian` · `obsidianupdate/obsidian_manager.py` · v1.3 · `apps/obsidian/`
  Obsidian Portable. Бекап `second-brain/` vault (AES-256). Запуск через URI `obsidian://open?path=...`. Vaultwarden.

- `Win+R → telegram` · `telegramupdate/telegram_manager.py` · v1.1 · `apps/telegram/`
  Telegram Portable. Очищення медіа-кешу. Бекап `tdata/` (AES-256). `tdata/` не замінюється при оновленні.

- `Win+R → doublecmd` · `doublecmdupdate/doublecmd_manager.py` · v1.5 · `apps/doublecmd/`
  Double Commander Portable (GitHub Releases). Бекап `settings/` (AES-256). Vaultwarden.

- `Win+R → rdp` · `rdpupdate/rdp_manager.py` · v3.1.0
  Менеджер RDP: Група→Сервер→Акаунт з `.env`. `.rdp` генерується в пам'яті (`tempfile`). `cmdkey` видаляє паролі після сесії.

### DevOps утиліти

- `Win+R → 7zip` · `7zipupdate/7zip_manager.py` · v1.4 · `apps/7zip/`
  7-Zip Extra (7-zip.org HTML парсинг). Без бекапу — CLI без даних користувача.

- `Win+R → bin` · `binupdate/bin_manager.py` · v2.5 · `apps/bin/`
  DevOps CLI: helm, kubectl, terraform, rclone, gh, bw, sqlite3. `GITHUB_TOKEN` у `.env` (60→5000 req/год).

- `Win+R → path` · `pathupdate/path_manager.py` · v1.6.0
  Перевірка capsule-шляхів (PATH ✅/❌ + Диск ✅/⚠️). UAC → `fix_path.ps1 -AutoClose`.

- `Win+R → changelog` · `changelogupdate/changelog_manager.py` · v1.3.2
  Парсинг CHANGELOG.md → архів `second-brain/4_Archives/Capsule_Changelog/YYYY/MM_MonthName.md`. Merge-логіка.

### Спільні можливості всіх менеджерів

- `__version__` + `get_manager_hash()` — версія та SHA256 self-check цілісності
- Self-healing pip install — автовстановлення залежностей (тільки локально, вимкнено в CI/Docker)
- Шифровані резервні копії 7-Zip AES-256 (пароль у `.env` або Vaultwarden)
- Ротація логів: 7 днів + 50 MB (поточний день не видаляється; при >50 MB → part-файл)
- Ротація резервних копій: 7 щоденних + 4 тижневих (ISO-тижні)
- Пароль резервної копії обов'язковий — без пароля ERROR + HALT (або пропозиція Vaultwarden)
- Шляхи auto-detect від `SCRIPT_DIR` → `CAPSULE_ROOT` (хардкод заборонено)

**Шаблон нового менеджера:** `devops/_template/capsule_manager/` (base_manager.py + .env.example + .gitignore + README.md)

---

## 🔐 Git & SSH

### Конфігурація

- **user.name / user.email** → `apps/git/etc/gitconfig`
- **SSH ключ (main)** — `apps/git/.ssh/id_ed25519_main` → GitHub: `oleksii-rovnianskyi`
- **SSH ключ (security)** — `apps/git/.ssh/id_ed25519_security` → GitHub: `0scorp919`
- **SSH binary** — `apps/git/usr/bin/ssh.exe` (портативний, не системний)

### Налаштування акаунту для репозиторію

Акаунт визначається вручну через `core.sshCommand` для кожного репозиторію (CAPSULE_ROOT auto-detect):

**Акаунт `oleksii-rovnianskyi`:**
```bash
git config --local core.sshCommand "<CAPSULE_ROOT>/apps/git/usr/bin/ssh.exe -i <CAPSULE_ROOT>/apps/git/.ssh/id_ed25519_main -F <CAPSULE_ROOT>/apps/git/.ssh/config"
git config --local user.email "oleksii.rovnianskyi@gmail.com"
```

**Акаунт `0scorp919`:**
```bash
git config --local core.sshCommand "<CAPSULE_ROOT>/apps/git/usr/bin/ssh.exe -i <CAPSULE_ROOT>/apps/git/.ssh/id_ed25519_security -F <CAPSULE_ROOT>/apps/git/.ssh/config"
git config --local user.email "0scorp919@gmail.com"
```

> ⚠️ `second-brain` — виняток: `core.sshCommand` вже прописано в `second-brain/.git/config` вручну.

### Репозиторії

**`oleksii-rovnianskyi`:**
- `second-brain`  **private** — Obsidian vault + AI-правила · `git@github.com:oleksii-rovnianskyi/second-brain.git` → `second-brain/`
- `oleksii-rovnianskyi` 🌐 **public** — GitHub Profile README
- `proton-pass-windows-portable` 🌐 **public** — Офлайн-розшифрування Proton Pass (PGP) на Windows
- `ResourceWatch` 🌐 **public** — Моніторинг Windows: CPU/RAM/диски, IP, e-mail алерти
- `watt-stream-yuz` 🌐 **public** — Corporate SPA для енергетичного трейдера

**`0scorp919`:**
- `0scorp919` 🌐 **public** — GitHub Profile README
- `ICE_OleksiiRovnianskyi` 🌐 **public** — ICE файл: медична та контактна інформація (UA/EN/PL)
- `7zipupdate` 🌐 **public** · `git@github.com:0scorp919/7zipupdate.git` → `devops/7zipupdate/`
- `binupdate` 🌐 **public** · `git@github.com:0scorp919/binupdate.git` → `devops/binupdate/`
- `changelogupdate` 🌐 **public** · `git@github.com:0scorp919/changelogupdate.git` → `devops/changelogupdate/`
- `chromeupdate`  **public** · `git@github.com:0scorp919/chromeupdate.git` → `devops/chromeupdate/`
- `doublecmdupdate` 🌐 **public** · `git@github.com:0scorp919/doublecmdupdate.git` → `devops/doublecmdupdate/`
- `gitupdate` 🌐 **public** · `git@github.com:0scorp919/gitupdate.git` → `devops/gitupdate/`
- `nodeupdate` 🌐 **public** · `git@github.com:0scorp919/nodeupdate.git` → `devops/nodeupdate/`
- `obsidianupdate` 🌐 **public** · `git@github.com:0scorp919/obsidianupdate.git` → `devops/obsidianupdate/`
- `pathupdate` 🌐 **public** · `git@github.com:0scorp919/pathupdate.git` → `devops/pathupdate/`
- `pwshupdate` 🌐 **public** · `git@github.com:0scorp919/pwshupdate.git` → `devops/pwshupdate/`
- `pythonupdate`  **public** · `git@github.com:0scorp919/pythonupdate.git` → `devops/pythonupdate/`
- `rdpupdate` 🌐 **public** · `git@github.com:0scorp919/rdpupdate.git` → `devops/rdpupdate/`
- `telegramupdate`  **public** · `git@github.com:0scorp919/telegramupdate.git` → `devops/telegramupdate/`
- `vsupdate` 🌐 **public** · `git@github.com:0scorp919/vsupdate.git` → `devops/vsupdate/`

---

## 🔑 Vaultwarden

Самохостований Bitwarden-сумісний сервер для паролів резервних копій.

- **Хост:** `https://pass.sysadmin.express`
- **CLI:** `apps/bin/bw.exe` (керується `bin_manager.py`)
- **Стан CLI:** `apps/bin/.bw_data/` (портативний)
- **Використовується у:** `chrome`, `git`, `doublecmd`, `obsidian`, `vscode`, `pwsh` менеджерах
- **Не використовується у:** `python`, `telegram`, `rdp`, `node` — прямий пароль з `.env`

**Логіка автентифікації:**
- `unauthenticated` → `bw login` (email + майстер-пароль + TOTP/Email 2FA)
- `locked` → `bw unlock` (тільки майстер-пароль)
- `unlocked` → `bw unlock --raw` (свіжий session token)
- `bw sync --session` після login/unlock → `bw lock` після отримання пароля

**Режими у `.env`:**
- Режим 1 (прямий): `<APP>_BACKUP_PASSWORD=...`
- Режим 2 (Vaultwarden): `BW_HOST + BW_EMAIL + BW_METHOD + BW_ITEM_NAME`

---

## 🤖 AI-асистент (Cline)

**Architect (Шеф)** — основний AI-екземпляр капсули. Cline VS Code extension через OpenRouter.

### Конфігурація

- **Тип:** VSCode extension (saoudrizwan.claude-dev)
- **Конфігурація (portable):** `C:\!Oleksii_Rovnianskyi\apps\vscode\data\user-data\User\globalStorage\saoudrizwan.claude-dev\`
- **Модель:** `minimax/minimax-m2.5`
- **Налаштування моделі:** `planModeOpenRouterModelId`, `actModeOpenRouterModelId`

### Налаштування Cline (VSCode extension)

- Parallel Tool Calling — ❌ (Race Condition → Ghost Edits)
- Native Tool Call — ✅
- Enable Thinking — ❌ (~2000 зайвих токенів)
- Auto Compact — ✅
- Subagents — 
- Terminal Output Limit — 1000–2000 рядків
- Shell — Git Bash (портативний)

### Правила

- `.clinerules` — компактна версія для AI-асистента (Cline)
- `second-brain/rules/Clinerules_Full.md` — повна версія для людини (українською)

> ⚠️ **Зміна архітектури (v2.3.34):** CLI Worker видалено. Капсула тепер працює виключно через VSCode Cline (Architect / Шеф).

---

## ️ Цикл виконання (Execution Cycle)

Після отримання будь-якої задачі — **ОБОВ'ЯЗКОВО** дотримуватись цього циклу:

### 1. PLAN & CONFIRM
- Детально описати план дій (покроково)
- Зупинитись і чекати підтвердження
- Формат: "Планую зробити: 1)..., 2)..., 3)..."
- Ключові слова: "Go", "Ok", "Confirm", "Proceed", "Дій", "Підтверджую"

### 2. REVISE (якщо потрібно)
- Якщо є коментарі/побажання — переробити план
- Знову чекати підтвердження
- Цикл до отримання явного підтвердження

### 3. REGISTER
- **ТІЛЬКИ** після підтвердження: додати задачі до Active_Tasks.md
- Формат: - [ ] для нових, - [x] для виконаних

### 4. EXECUTE
- Виконати заплановані дії
- Поступово оновлювати статуси в Active_Tasks.md

### 5. VERIFY
- Запустити лінтери/компіляцію/тести
- Перевірити результат

### 6. SELF-EVOLUTION
- Запустити протокол самоеволюції
- Запропонувати зміни до правил/бази знань
- Чекати підтвердження перед оновленням

### 7. SESSION CLOSING
- Запустити протокол закриття сесії
- Запропонувати план оновлення документації
- Чекати підтвердження, потім оновити CHANGELOG.md, README.md, Active_Tasks.md

**ПРИНЦИП:** Будь-яка зміна = план → підтвердження → виконання → верифікація → синхронізація

---

## ️ Протоколи безпеки

### Протокол реагування на інциденти

- **P1** — Active breach, data exfiltration → **STOP ALL OPERATIONS** — негайно зупинити все
- **P2** — Compromised credentials → Rotate immediately — негайно ротація облікових даних
- **P3** — Potential vulnerability → Schedule remediation — запланувати виправлення
- **P4** — Minor misconfiguration → Log for review — залогувати для перегляду

### Стандарт обробки помилок

- **ValidationError** — Invalid input, missing required params → FAIL FAST
- **ConfigurationError** — Missing .env, wrong config → FAIL WITH MESSAGE
- **NetworkError** — Timeout, connection refused → RETRY with backoff (1s, 2s, 4s)
- **PermissionError** — Access denied → FAIL WITH CLEAR MESSAGE
- **IntegrityError** — Checksum mismatch, corrupted file → QUARANTINE + ALERT

### Протокол конфліктів правил

Якщо запит користувача суперечить правилам з `.clinerules`:
1. **Ідентифікувати** конкретне правило, що конфліктує
2. **Інформувати:** "Це суперечить правилу [rule_name]. Зробити виняток чи оновити правила?"
3. **Запропонувати:** 2-3 варіанти з pros/cons/risks
4. **Чекати підтвердження** перед виконанням

---

##  Глосарій термінів

### Основні терміни

- **Autonomous Capsule (Капсула)** — portable, self-contained working system в `C:\!Oleksii_Rovnianskyi\`
- **Architect (Шеф)** — primary Cline instance через OpenRouter (minimax/minimax-m2.5), decision-maker капсули
- **Manager Script (Менеджер)** — `<app>_manager.py` скрипт для автооновлення застосунків
- **Portable Tool (Портативний інструмент)** — застосунок в `apps/` що не потребує інсталяції

### Типи запускачів

- **Windows Shortcut (.lnk)** — ярлик в `tags/` для запуску через `Win+R`. Вказує на портативний запускач в `devops/<app>update/`. Не публікується на GitHub.
- **Portable Launcher (.bat)** — `.bat` файл в `devops/<app>update/` з auto-detect CAPSULE_ROOT. GitHub-ready.

### Edge Cases

- **Rule conflict** — коли запит користувача суперечить поточним інструкціям
- **Missing context** — коли README.md відсутній або недостатній
- **Incomplete specification** — коли задача потребує додаткових припущень
- **Technical limitations** — коли інструменти не підтримують потрібну функціональність

### Технічні визначення

- **Large logs** — лог-файли >1MB
- **Brief summary** — 1-2 параграфи з головним результатом виконання
- **Destructive operation** — операція що може призвести до втрати даних (rm -rf, DROP TABLE тощо)

---

##  Обслуговування

### Резервна копія всієї капсули
```bash
robocopy "C:\!Oleksii_Rovnianskyi" "D:\Backup\Capsule" /MIR /XD node_modules .git
```

### Перенос на інший комп'ютер
1. Скопіювати `C:\!Oleksii_Rovnianskyi\` на нову машину
2. Додати `C:\!Oleksii_Rovnianskyi\tags\` в системний `PATH`
3. Запустити `Win+R → path` для реєстрації шляхів
4. `Win+R → code` — і все працює ✅

### Що НЕ зберігається в капсулі
- **Windows Credential Manager** — перезайти в GitHub при потребі
- **Obsidian vault path** — вказати `second-brain/` при першому запуску
- **Vaultwarden сесія** — `bw lock` після кожного запуску (Security by Design)
- **RDP credentials** — `cmdkey` видаляє паролі після закриття сесії (навмисно)

---

## 📜 Історія змін

Див. `CHANGELOG.md` · Архів: `second-brain/4_Archives/Capsule_Changelog/`

---

> *"Одна папка. Нуль залежностей від системи. Підключив — працюєш."*
