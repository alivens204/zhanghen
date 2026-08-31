# 账痕（Zhang Hen） — 个人记账应用（永远没有广告）

> 让每一笔账单都有痕迹！

---

## 📱 应用简介

**Zhang Hen（账痕）** 是一款个人记账应用，支持快速记账、详细记账、报销管理、预算管理、统计分析等功能。应用采用本地存储，数据安全可靠，支持多语言切换，支持多种数据导入导出格式。

| 项目 | 信息 |
|------|------|
| **当前版本** | v0.5.0 |
| **应用名称** | 账痕 / 賬痕 / Zhang Hen |
| **支持平台** | Android、Web |
| **包名** | com.accounting.app |
| **最低 Android** | API 24 (Android 7.0) |

---

## ✨ 核心功能

### 1. 🌐 多语言支持

支持三种语言一键切换，即时生效，无需重启：

| 语言 | 应用名称 | 说明 |
|------|---------|------|
| 简体中文 | 账痕 | 源语言，完整支持 |
| 繁體中文 | 賬痕 | 含台灣用語習慣（匯入/匯出/設定/賬戶等） |
| English | Zhang Hen | 完整英文界面 |

**切换方式**：我的 → 🌐 语言设置 → 选择语言

**翻译覆盖范围**：
- 所有页面标题和导航
- 分类名称（餐饮→Food、交通→Transport 等）
- 账户名称（现金→Cash、银行卡→Bank Card 等）
- 按钮、对话框、提示信息
- 统计图表标签
- 报销状态标签
- 报销记录备注（自动翻译已存储的中文前缀）
- 日期格式（中文"3月25日"→英文"Mar 25"）

### 2. 🔍 记录搜索

在「记录」页顶部新增搜索栏：
- **搜索范围**：备注、分类名称（当前语言）、金额
- **匹配方式**：模糊匹配，大小写不敏感
- **组合筛选**：与"全部/待报销/已报销"筛选组合使用
- **实时过滤**：输入即搜索，带一键清除按钮

### 3. 💰 双模式记账

#### 快捷模式
- 点击首页「+」按钮，弹出半全屏快速记账面板
- 支持多行输入，每行一条记录
- 输入格式：`物品名称 金额`（如：`面 12`、`咖啡 25`、`打车 15`）
- 自动识别分类（通过智能映射表，支持 80+ 种分类名称）
- 支持选择报销状态（无需报销/待报销/已报销）

#### 详细模式
- 完整的记账表单
- 支持选择：类型、金额、分类、账户、备注、日期时间
- 支持4种报销状态：无需报销、待报销、全额报销、部分报销

### 4. 🧾 报销管理

| 状态 | 说明 | 自动生成记录 |
|------|------|-------------|
| 无需报销 | 普通消费 | ❌ |
| 待报销 | 等待报销 | ❌ |
| 全额报销 | 报销全额 | ✅ 收入记录 |
| 部分报销 | 报销部分金额 | ✅ 收入记录（标注金额） |

**报销流程**：
1. 添加消费记录时选择"待报销"
2. 报销后，编辑该记录选择"全额报销"或"部分报销"
3. 系统自动生成对应的报销收入记录
4. 原记录显示"全额报销"或"部分报销"标签
5. 报销记录备注自动使用当前语言前缀（`报销：` / `報銷：` / `Reimbursement:`）

### 5. 📊 预算管理

- 支持按分类设置月度预算
- 首页显示预算执行情况
- 超支预警提示

### 6. 📈 统计分析

- 月度/年度收支统计
- 分类支出占比分析（柱状图）
- 月度趋势图（折线图，收入+支出）
- 账户余额统计
- 图表可视化展示

### 7. 💾 数据导入导出

#### 导出格式
| 格式 | 说明 |
|------|------|
| XLSX | Excel表格（默认） |
| XLS | 旧版Excel |
| TXT | 纯文本 |
| CSV | 逗号分隔 |

#### 导入能力
- **自有格式**：完美兼容账痕导出的文件
- **第三方软件**：支持导入小黑记账等其他软件的账单
- **智能识别**：自动匹配日期时间格式、分类名称
- **80+分类映射**：支持各种中文分类名称自动转换

#### 导出文件名格式
```
账痕_日期_时间（时分）.xlsx
账痕_2026-08-25_1530.xlsx
```

## 📂 项目结构

```
accounting-app/
├── app/                      # 页面目录
│   ├── (tabs)/              # 底部标签页
│   │   ├── _layout.tsx      # 标签页布局
│   │   ├── home.tsx         # 首页（月总览+记录列表）
│   │   ├── records.tsx      # 记录页（搜索+筛选）
│   │   ├── stats.tsx        # 统计页
│   │   └── profile.tsx      # 我的页面（语言切换）
│   ├── add-record.tsx       # 记一笔页面
│   ├── budget.tsx           # 预算管理
│   ├── accounts.tsx         # 账户管理
│   ├── reimbursement.tsx    # 报销管理
│   ├── db-config.tsx        # 数据库配置
│   ├── sync.tsx             # 数据同步
│   └── _layout.tsx          # 全局布局
├── i18n/                    # 多语言翻译
│   ├── zhHans.ts            # 简体中文
│   ├── zhHant.ts            # 繁體中文
│   ├── en.ts                # English
│   └── index.ts             # 翻译引擎 + t() 函数
├── components/              # 组件目录
│   ├── TransactionItem.tsx  # 交易记录项
│   ├── CategoryPicker.tsx   # 分类选择器
│   └── AccountPicker.tsx    # 账户选择器
├── constants/               # 常量定义
│   ├── categories.ts        # 分类配置（11支出+7收入）
│   ├── accounts.ts          # 账户配置（5种账户）
│   └── theme.ts             # 主题样式
├── database/                # 数据库
│   ├── migration.ts         # 数据库初始化
│   └── queries.ts           # 数据库查询
├── store/                   # 状态管理
│   ├── useRecordStore.ts    # 记账数据Store
│   ├── useLanguageStore.ts  # 语言状态Store
│   └── useBudgetStore.ts    # 预算Store
├── utils/                   # 工具函数
│   ├── exportImport.ts      # 导入导出核心
│   ├── nativeFilePicker.ts  # Android原生文件选择
│   ├── quickParse.ts        # 快捷输入解析（80+分类映射）
│   └── format.ts            # 格式化工具
├── android/                 # Android原生代码
├── dist/                    # Web构建输出
└── 账痕-v0.5.0.apk          # Android安装包
```

---

## 🎨 界面说明

### 底部导航栏

| 标签 | 功能 |
|------|------|
| 🏠 首页 | 月总览 + 每日收支记录 |
| 📋 记录 | 全部记录（搜索 + 按报销状态筛选） |
| 📊 统计 | 收支统计图表 |
| 👤 我的 | 设置、导入导出、语言切换、版本信息 |

### 首页布局

```
┌─────────────────────────────────────┐
│  账痕 / Zhang Hen                   │
├─────────────────────────────────────┤
│  < 8月 / Aug >                      │
│  月收入 · 月支出 · 月结余            │
├─────────────────────────────────────┤
│  28日 周五     收入 ¥12 支出 ¥12     │
│  ─────────────────────────────────  │
│  🚗 No note              -¥12      │
│     15:49 · Transport    Full      │
│  💰 Reimbursement: ...   +¥12      │
│     15:49 · Reimbursement Full     │
├─────────────────────────────────────┤
│                            [+] 按钮  │
└─────────────────────────────────────┘
```

### 记录页布局

```
┌─────────────────────────────────────┐
│  All Records / 全部记录              │
├─────────────────────────────────────┤
│  🔍 Search records... / 搜索记录...  │
├─────────────────────────────────────┤
│  [All]  [Pending]  [Reimbursed]     │
├─────────────────────────────────────┤
│  28 Fri       Income ¥12  Expense ¥12│
│  🚗 No note              -¥12      │
│  💰 Reimbursement: ...   +¥12      │
└─────────────────────────────────────┘
```

### 我的页面布局

```
┌─────────────────────────────────────┐
│  Profile / 我的                      │
├─────────────────────────────────────┤
│  Asset Overview / 资产概览           │
│  Total Balance / 总余额    ¥0.00    │
│  💵 Cash  🏦 Bank Card  💳 Credit   │
├─────────────────────────────────────┤
│  📋 Accounts / 账户管理              │
│  📊 Budget / 预算管理                │
│  🧾 Reimbursement / 报销管理         │
│  📝 Recording Mode / 记账方式        │
│  📥 Import Data / 导入数据           │
│  📤 Export Data / 导出数据           │
│  🌐 Language / 语言设置              │
├─────────────────────────────────────┤
│  Zhang Hen v0.5.0                   │
│  Every transaction has its trace!   │
│  Custom Edition                     │
└─────────────────────────────────────┘
```

---

## 📊 支持的分类

### 支出分类（11种）

| 图标 | 简体中文 | 繁體中文 | English | ID |
|------|---------|---------|---------|-----|
| 🍜 | 餐饮 | 餐飲 | Food | expense_food |
| 🚗 | 交通 | 交通 | Transport | expense_transport |
| 🛒 | 日用 | 日用 | Daily | expense_daily |
| 👔 | 服饰 | 服飾 | Clothing | expense_clothing |
| 🎮 | 娱乐 | 娛樂 | Entertainment | expense_entertainment |
| 🏠 | 住房 | 住房 | Housing | expense_housing |
| 💊 | 医疗 | 醫療 | Medical | expense_medical |
| 📚 | 教育 | 教育 | Education | expense_education |
| 📱 | 通讯 | 通訊 | Communication | expense_communication |
| 💳 | 金融 | 金融 | Finance | expense_finance |
| 📦 | 其他支出 | 其他支出 | Other Expense | expense_other |

### 收入分类（7种）

| 图标 | 简体中文 | 繁體中文 | English | ID |
|------|---------|---------|---------|-----|
| 💼 | 工資 | 工資 | Salary | income_salary |
| 🎁 | 奖金 | 獎金 | Bonus | income_bonus |
| 📈 | 投资 | 投資 | Investment | income_investment |
| 💻 | 兼职 | 兼職 | Part-time | income_parttime |
| 🧧 | 红包 | 紅包 | Red Packet | income_redpacket |
| 💰 | 报销 | 報銷 | Reimbursement | income_reimbursement |
| 💰 | 其他收入 | 其他收入 | Other Income | income_other |

---

## 💳 支持的账户

| 图标 | 简体中文 | 繁體中文 | English | ID |
|------|---------|---------|---------|-----|
| 💵 | 现金 | 現金 | Cash | cash |
| 🏦 | 银行卡 | 銀行卡 | Bank Card | bank |
| 💳 | 信用卡 | 信用卡 | Credit Card | credit |
| 📱 | 支付宝 | 支付寶 | Alipay | alipay |
| 💬 | 微信 | 微信 | WeChat | wechat |

---

## 🌐 翻译系统架构

### 核心文件

| 文件 | 说明 |
|------|------|
| `i18n/zhHans.ts` | 简体中文翻译（源语言，~150个key） |
| `i18n/zhHant.ts` | 繁體中文翻译（含台灣用語） |
| `i18n/en.ts` | English 翻译 |
| `i18n/index.ts` | 翻译引擎 + 工具函数 |
| `store/useLanguageStore.ts` | 语言状态管理（Zustand + AsyncStorage 持久化） |

### 工具函数

| 函数 | 说明 | 示例 |
|------|------|------|
| `t(key)` | 翻译文本 | `t('nav.home')` → "首页" / "Home" |
| `getCategoryName(id)` | 分类名称 | `getCategoryName('expense_food')` → "餐饮" / "Food" |
| `getAccountName(id)` | 账户名称 | `getAccountName('cash')` → "现金" / "Cash" |
| `getReimbursementLabel(status)` | 报销状态 | `getReimbursementLabel('pending')` → "待报销" / "Pending" |
| `getWeekday(index)` | 星期名称 | `getWeekday(1)` → "周一" / "Mon" |
| `getMonthName(num)` | 月份名称 | `getMonthName(3)` → "三月" / "Mar" |
| `getMonthWithUnit(num)` | 带单位月份 | `getMonthWithUnit(3)` → "3月" / "Mar" |
| `formatDateLocalized(date)` | 本地化日期 | `formatDateLocalized('2026-03-25')` → "3月25日" / "Mar 25" |
| `translateNote(note)` | 翻译存储的备注 | `translateNote('报销：...')` → "Reimbursement: ..." |

### 技术特点

- **零依赖**：自研轻量 i18n 方案，无第三方库
- **即时切换**：Zustand 状态 + AsyncStorage 持久化，切换即时生效
- **翻译键扁平化**：`t('profile.title')` 简洁直观
- **运行时翻译**：翻译在渲染时执行，支持动态语言切换
- **向后兼容**：`translateNote()` 自动翻译已存储的中文备注

---

## 🛠️ 技术架构

### 技术栈

| 类别 | 技术 |
|------|------|
| 框架 | React Native + Expo |
| 语言 | TypeScript |
| 路由 | Expo Router |
| 状态管理 | Zustand |
| UI组件 | React Native Paper |
| 本地存储 | AsyncStorage |
| 数据库 | expo-sqlite |
| 图表 | react-native-gifted-charts |
| 日期处理 | Day.js |
| Excel处理 | xlsx |
| 手势 | react-native-gesture-handler |
| 多语言 | 自研 i18n（零依赖） |

### Android原生模块

| 模块 | 说明 |
|------|------|
| NativeFilePicker | 自定义文件选择器，绕过expo-document-picker兼容性问题 |

### 构建信息

| 项目 | 信息 |
|------|------|
| Android SDK | 36 |
| Build Tools | 36.0.0 |
| NDK | 27.1.12297006 |
| CMake | 3.22.1 |
| Java | JDK 21 |
| Gradle | 9.3.1 |
| APK大小 | ~110 MB |

---

## 📱 安装与使用

### Android安装

1. 下载 `张痕-v0.5.0.apk`（约110MB）
2. 允许安装未知来源应用
3. 完成安装

### 构建APK

```bash
# 1. 生成Android原生项目
npx expo prebuild --platform android --clean

# 2. 构建Release APK
cd android
set ANDROID_HOME=D:\android-sdk
set JAVA_HOME=D:\java\jdk-21
gradlew.bat assembleRelease

# 3. APK输出路径
# android/app/build/outputs/apk/release/app-release.apk
```

---

## 开发信息

| 项目 | 信息 |
|------|------|
| 开发框架 | React Native + Expo |
| 编程语言 | TypeScript |
| 数据库 | expo-sqlite |
| UI 组件库 | react-native-paper |
| 状态管理 | Zustand |
| 构建工具 | Expo CLI + Gradle |
| 最后更新 | 2026-08-28 |

---

## 许可证

Copyright © 2026 alive-ns 个人开发者

---

> 📱 **账痕（Zhang Hen）** — 让每一笔账单都有痕迹！
