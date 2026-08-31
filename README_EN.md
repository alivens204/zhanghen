# Zhang Hen（账痕） — Personal Accounting App (No Ads, Ever)

> Every transaction leaves its trace!

---

## 📱 About

**Zhang Hen（账痕）** is a personal accounting app with fast entry, detailed recording, reimbursement management, budget tracking, and statistical analysis. All data is stored locally for security, with multi-language support and flexible import/export formats.

| Item | Details |
|------|---------|
| **Version** | v0.5.0 |
| **App Name** | Zhang Hen |
| **Platforms** | Android, Web |
| **Package** | com.accounting.app |
| **Min Android** | API 24 (Android 7.0) |

---

## ✨ Key Features

### 1. 🌐 Multi-Language Support

Three languages with one-tap switching — instant, no restart required:

| Language | App Name | Notes |
|----------|----------|-------|
| Simplified Chinese | 账痕 | Source language, full coverage |
| Traditional Chinese | 賬痕 | Taiwan conventions (匯入/匯出/設定/賬戶) |
| English | Zhang Hen | Full English interface |

**How to switch**: Profile → 🌐 Language → Select language

**Translation coverage**:
- All page titles and navigation
- Category names (餐饮→Food, 交通→Transport, etc.)
- Account names (现金→Cash, 银行卡→Bank Card, etc.)
- Buttons, dialogs, prompts
- Statistical chart labels
- Reimbursement status labels
- Reimbursement note prefixes (auto-translates stored Chinese)
- Date formats (Chinese "3月25日" → English "Mar 25")

### 2. 🔍 Record Search

Search bar at the top of the Records page:
- **Scope**: Notes, category names (current language), amounts
- **Method**: Fuzzy match, case-insensitive
- **Combined filtering**: Works with "All / Pending / Reimbursed" status filter
- **Real-time**: Type-to-search with one-tap clear button

### 3. 💰 Dual-Mode Recording

#### Quick Mode
- Tap the "+" button on Home to open a quick-entry panel
- Multi-line input, one record per line
- Format: `item amount` (e.g., `noodles 12`, `coffee 25`, `taxi 15`)
- Auto-detects categories via smart mapping (80+ category names supported)
- Supports reimbursement status selection

#### Detailed Mode
- Full recording form
- Select: type, amount, category, account, note, date/time
- 4 reimbursement statuses: None, Pending, Full, Partial

### 4. 🧾 Reimbursement Management

| Status | Description | Auto-Generated Record |
|--------|-------------|----------------------|
| None | Regular expense | ❌ |
| Pending | Awaiting reimbursement | ❌ |
| Full | Fully reimbursed | ✅ Income record |
| Partial | Partially reimbursed | ✅ Income record (with amount) |

**Workflow**:
1. Add an expense with status "Pending"
2. After reimbursement, edit the record to "Full" or "Partial"
3. System auto-generates the corresponding reimbursement income record
4. Original record shows "Full" or "Partial" badge
5. Reimbursement note uses current language prefix (`报销：` / `報銷：` / `Reimbursement:`)

### 5. 📊 Budget Management

- Set monthly budgets by category
- Home page shows budget execution progress
- Overspending warnings

### 6. 📈 Statistical Analysis

- Monthly/yearly income & expense summaries
- Category expense breakdown (bar chart)
- Monthly trend chart (line chart, income + expense)
- Account balance statistics
- Visual chart display

### 7. 💾 Data Import/Export

#### Export Formats
| Format | Description |
|--------|-------------|
| XLSX | Excel spreadsheet (default) |
| XLS | Legacy Excel |
| TXT | Plain text (tab-delimited) |
| CSV | Comma-separated |

#### Import Capabilities
- **Native format**: Full compatibility with Zhang Hen exports
- **Third-party**: Supports importing from other apps (e.g., XiaoHei Accounting)
- **Smart detection**: Auto-matches date/time formats and category names
- **80+ category mappings**: Automatic conversion of various Chinese category names

#### Export Filename Format
```
ZhangHen_2026-08-25_1530.xlsx
```

---

## 📂 Project Structure

```
accounting-app/
├── app/                      # Pages
│   ├── (tabs)/              # Bottom tab pages
│   │   ├── _layout.tsx      # Tab layout
│   │   ├── home.tsx         # Home (monthly overview + daily records)
│   │   ├── records.tsx      # Records (search + filter)
│   │   ├── stats.tsx        # Statistics
│   │   └── profile.tsx      # Profile (language switch)
│   ├── add-record.tsx       # Add record page
│   ├── budget.tsx           # Budget management
│   ├── accounts.tsx         # Account management
│   ├── reimbursement.tsx    # Reimbursement management
│   ├── db-config.tsx        # Database configuration
│   ├── sync.tsx             # Data sync
│   └── _layout.tsx          # Root layout
├── i18n/                    # Multi-language translations
│   ├── zhHans.ts            # Simplified Chinese
│   ├── zhHant.ts            # Traditional Chinese
│   ├── en.ts                # English
│   └── index.ts             # Translation engine + t() function
├── components/              # Components
│   ├── TransactionItem.tsx  # Transaction list item
│   ├── CategoryPicker.tsx   # Category picker
│   └── AccountPicker.tsx    # Account picker
├── constants/               # Constants
│   ├── categories.ts        # Category config (11 expense + 7 income)
│   ├── accounts.ts          # Account config (5 account types)
│   └── theme.ts             # Theme styling
├── database/                # Database
│   ├── migration.ts         # Database initialization
│   └── queries.ts           # Database queries
├── store/                   # State management
│   ├── useRecordStore.ts    # Transaction data store
│   ├── useLanguageStore.ts  # Language state store
│   └── useBudgetStore.ts    # Budget store
├── utils/                   # Utility functions
│   ├── exportImport.ts      # Import/export core
│   ├── nativeFilePicker.ts  # Android native file picker
│   ├── quickParse.ts        # Quick entry parser (80+ category mappings)
│   └── format.ts            # Formatting utilities
├── android/                 # Android native code
├── dist/                    # Web build output
└── ZhangHen-v0.5.0.apk     # Android installer
```

---

## 🎨 UI Layout

### Bottom Navigation

| Tab | Function |
|-----|----------|
| 🏠 Home | Monthly overview + daily income/expense records |
| 📋 Records | All records (search + reimbursement status filter) |
| 📊 Stats | Income/expense statistical charts |
| 👤 Profile | Settings, import/export, language switch, version info |

### Home Page

```
┌─────────────────────────────────────┐
│  Zhang Hen                          │
├─────────────────────────────────────┤
│  < Aug / 8月 >                      │
│  Income · Expense · Balance         │
├─────────────────────────────────────┤
│  28 Fri       Income ¥12  Expense ¥12│
│  ─────────────────────────────────  │
│  🚗 No note              -¥12      │
│     15:49 · Transport    Full      │
│  💰 Reimbursement: ...   +¥12      │
│     15:49 · Reimbursement Full     │
├─────────────────────────────────────┤
│                            [+] New  │
└─────────────────────────────────────┘
```

### Records Page

```
┌─────────────────────────────────────┐
│  All Records                        │
├─────────────────────────────────────┤
│  🔍 Search records...               │
├─────────────────────────────────────┤
│  [All]  [Pending]  [Reimbursed]     │
├─────────────────────────────────────┤
│  28 Fri       Income ¥12  Expense ¥12│
│  🚗 No note              -¥12      │
│  💰 Reimbursement: ...   +¥12      │
└─────────────────────────────────────┘
```

### Profile Page

```
┌─────────────────────────────────────┐
│  Profile                            │
├─────────────────────────────────────┤
│  Asset Overview                     │
│  Total Balance            ¥0.00     │
│  💵 Cash  🏦 Bank Card  💳 Credit  │
├─────────────────────────────────────┤
│  📋 Account Management              │
│  📊 Budget Management               │
│  🧾 Reimbursement Management        │
│  📝 Recording Mode                  │
│  📥 Import Data                     │
│  📤 Export Data                     │
│  🌐 Language                        │
├─────────────────────────────────────┤
│  Zhang Hen v0.5.0                   │
│  Every transaction has its trace!   │
│  Custom Edition                     │
└─────────────────────────────────────┘
```

---

## 📊 Supported Categories

### Expense Categories (11)

| Icon | English | ID |
|------|---------|-----|
| 🍜 | Food | expense_food |
| 🚗 | Transport | expense_transport |
| 🛒 | Daily | expense_daily |
| 👔 | Clothing | expense_clothing |
| 🎮 | Entertainment | expense_entertainment |
| 🏠 | Housing | expense_housing |
| 💊 | Medical | expense_medical |
| 📚 | Education | expense_education |
| 📱 | Communication | expense_communication |
| 💳 | Finance | expense_finance |
| 📦 | Other Expense | expense_other |

### Income Categories (7)

| Icon | English | ID |
|------|---------|-----|
| 💼 | Salary | income_salary |
| 🎁 | Bonus | income_bonus |
| 📈 | Investment | income_investment |
| 💻 | Part-time | income_parttime |
| 🧧 | Red Packet | income_redpacket |
| 💰 | Reimbursement | income_reimbursement |
| 💰 | Other Income | income_other |

---

## 💳 Supported Accounts

| Icon | English | ID |
|------|---------|-----|
| 💵 | Cash | cash |
| 🏦 | Bank Card | bank |
| 💳 | Credit Card | credit |
| 📱 | Alipay | alipay |
| 💬 | WeChat | wechat |

---

## 🌐 Translation System Architecture

### Core Files

| File | Description |
|------|-------------|
| `i18n/zhHans.ts` | Simplified Chinese translations (source, ~150 keys) |
| `i18n/zhHant.ts` | Traditional Chinese translations (Taiwan conventions) |
| `i18n/en.ts` | English translations |
| `i18n/index.ts` | Translation engine + utility functions |
| `store/useLanguageStore.ts` | Language state (Zustand + AsyncStorage persistence) |

### Utility Functions

| Function | Description | Example |
|----------|-------------|---------|
| `t(key)` | Translate text | `t('nav.home')` → "首页" / "Home" |
| `getCategoryName(id)` | Category name | `getCategoryName('expense_food')` → "Food" |
| `getAccountName(id)` | Account name | `getAccountName('cash')` → "Cash" |
| `getReimbursementLabel(status)` | Reimbursement status | `getReimbursementLabel('pending')` → "Pending" |
| `getWeekday(index)` | Weekday name | `getWeekday(1)` → "Mon" |
| `getMonthName(num)` | Month name | `getMonthName(3)` → "Mar" |
| `getMonthWithUnit(num)` | Month with unit | `getMonthWithUnit(3)` → "Mar" |
| `formatDateLocalized(date)` | Localized date | `formatDateLocalized('2026-03-25')` → "Mar 25" |
| `translateNote(note)` | Translate stored note | `translateNote('报销：...')` → "Reimbursement: ..." |

### Technical Highlights

- **Zero dependencies**: Custom lightweight i18n solution, no third-party libraries
- **Instant switching**: Zustand state + AsyncStorage persistence
- **Flat translation keys**: `t('profile.title')` — clean and intuitive
- **Runtime translation**: Translations executed at render time, supports dynamic language switching
- **Backward compatible**: `translateNote()` auto-translates previously stored Chinese notes

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|-----------|
| Framework | React Native + Expo |
| Language | TypeScript |
| Routing | Expo Router |
| State Management | Zustand |
| UI Components | React Native Paper |
| Local Storage | AsyncStorage |
| Database | expo-sqlite |
| Charts | react-native-gifted-charts |
| Date Handling | Day.js |
| Excel Processing | xlsx |
| Gestures | react-native-gesture-handler |
| Multi-language | Custom i18n (zero dependencies) |

### Build Information

| Item | Details |
|------|---------|
| Android SDK | 36 |
| Build Tools | 36.0.0 |
| NDK | 27.1.12297006 |
| CMake | 3.22.1 |
| Java | JDK 21 |
| Gradle | 9.3.1 |
| APK Size | ~109 MB |

---

## 📱 Installation & Usage

### Android Installation

1. Download `ZhangHen-v0.5.0.apk` (~110MB)
2. Allow installation from unknown sources
3. Complete installation

### Building APK

```bash
# 1. Generate Android native project
npx expo prebuild --platform android --clean

# 2. Build Release APK
cd android
set ANDROID_HOME=D:\android-sdk
set JAVA_HOME=D:\java\jdk-21
gradlew.bat assembleRelease

# 3. APK output path
# android/app/build/outputs/apk/release/app-release.apk
```

---

## Development Info

| Item | Details |
|------|---------|
| Framework | React Native + Expo |
| Language | TypeScript |
| Database | expo-sqlite |
| UI Library | React Native Paper |
| State Management | Zustand |
| Build Tools | Expo CLI + Gradle |
| Last Updated | 2026-08-31 |

---

## License

Copyright © 2026 alive-ns. Personal developer.

---

> 📱 **Zhang Hen（账痕）** — Every transaction leaves its trace!
