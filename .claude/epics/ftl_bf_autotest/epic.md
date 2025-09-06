---
name: ftl_bf_autotest
status: backlog
created: 2025-09-06T15:16:44Z
progress: 0%
prd: .claude/prds/ftl_bf_autotest.md
github: https://github.com/yuanann/ftl-bf-autotest-framework/issues/1
---

# Epic: ftl_bf_autotest

## Overview

建立 FinTech Life 後台管理系統的自動化測試框架，採用 Stagehand + Playwright + Python 技術棧。框架採用模組化設計，每個功能使用單一 function 實作，具備截圖記錄、測試報告和錯誤處理能力。目標是建立穩定、可擴展的測試自動化解決方案。

## Architecture Decisions

### 核心技術選擇
- **Python 3.8+**: 主要開發語言，生態豐富且易於維護
- **Playwright**: 現代化瀏覽器自動化工具，支援多瀏覽器且穩定性佳
- **Stagehand**: AI 驅動的自動化測試工具，提升測試腳本智能化程度
- **pytest**: 測試框架，提供豐富的測試功能和報告
- **python-dotenv**: 環境變數管理，確保配置與程式碼分離

### 設計模式
- **Page Object Model (POM)**: 每個頁面功能封裝成獨立 function
- **單一職責原則**: 一個 function 只負責一個特定功能或測試場景
- **配置外部化**: 使用 .env 檔案管理所有環境相關配置
- **截圖驅動除錯**: 每個關鍵步驟自動截圖，便於問題追蹤

## Technical Approach

### 測試框架架構
```
ftl_autotest/
├── config/
│   ├── settings.py      # 載入 .env 配置
│   └── test_data.py     # 測試數據管理
├── pages/
│   ├── login_page.py    # 登入頁面功能
│   ├── system_role_page.py  # 系統角色功能
│   └── base_page.py     # 共用頁面功能
├── tests/
│   ├── test_login.py    # 登入測試案例
│   ├── test_system_settings.py  # 系統設定測試
│   └── conftest.py      # pytest 配置
├── utils/
│   ├── screenshot.py    # 截圖工具
│   ├── logger.py        # 日誌系統
│   └── report.py        # 測試報告生成
├── reports/            # 測試報告輸出目錄
├── screenshots/        # 截圖存檔目錄
└── main.py            # 主執行入口
```

### 核心組件設計

#### 1. 基礎工具類別
- **ScreenshotManager**: 統一截圖功能，支援時間戳記命名
- **ConfigLoader**: 載入 .env 配置，提供配置驗證
- **Logger**: 結構化日誌記錄，支援不同等級輸出
- **ReportGenerator**: HTML/JSON 格式測試報告生成

#### 2. 頁面功能模組
- **LoginPage**: 處理登入、登出、帳密驗證
- **SystemRolePage**: 系統角色相關功能測試
- **NavigationHelper**: 選單導航和頁面切換
- **FormHelper**: 表單填寫和驗證通用功能

#### 3. 測試執行引擎
- **TestRunner**: 測試案例執行控制器
- **RetryHandler**: 失敗重試機制
- **ParallelExecutor**: 並行測試執行 (預留)

## Implementation Strategy

### Phase 1: 基礎框架搭建 (2 週)
1. 建立專案結構和依賴管理
2. 實作核心工具類別 (截圖、日誌、配置)
3. 建立 Playwright + Stagehand 整合基礎
4. 實作登入功能測試作為 POC

### Phase 2: 核心功能實作 (3 週)
1. 實作系統設定模組測試功能
2. 建立頁面物件模型和通用函數
3. 實作測試報告生成系統
4. 加入錯誤處理和重試機制

### Phase 3: 擴展和優化 (2 週)
1. 擴展更多業務功能測試
2. 實作並行測試執行
3. 整合 CI/CD 支援
4. 效能優化和穩定性提升

### 風險緩解策略
- **環境依賴**: 建立詳細的環境設定文件和檢查腳本
- **元素定位**: 使用多種定位策略 (role, text, selector) 提高穩定性
- **網路不穩定**: 實作智能等待和重試機制
- **測試數據**: 建立測試數據隔離機制

## Task Breakdown Preview

高層級任務分類 (≤10 個任務):

- [ ] **專案初始化**: 建立專案結構、依賴管理、基本配置
- [ ] **核心工具開發**: 實作截圖、日誌、配置載入等基礎工具
- [ ] **Playwright 整合**: 建立瀏覽器控制和頁面操作基礎
- [ ] **登入功能實作**: 實作登入/登出功能及相關測試
- [ ] **系統設定測試**: 實作系統角色、權限管理等功能測試
- [ ] **測試報告系統**: 建立 HTML/JSON 報告生成和截圖整合
- [ ] **錯誤處理機制**: 實作重試、異常捕捉、優雅降級
- [ ] **業務功能擴展**: 實作其他主要業務功能測試模組
- [ ] **執行框架完善**: 建立測試套件執行、並行處理等功能
- [ ] **文件和部署**: 完成使用文件、部署腳本和 CI/CD 整合

## Dependencies

### 外部技術依賴
- **Python 3.8+**: 程式執行環境
- **Node.js**: Playwright 瀏覽器驅動依賴
- **Chrome/Chromium**: 測試執行瀏覽器
- **SIT 測試環境**: https://sit-admin.fintech-life.com/ 可用性

### 內部團隊依賴
- **QA 團隊**: 提供測試案例需求和驗證標準
- **開發團隊**: 提供系統功能說明和變更通知
- **DevOps 團隊**: 協助 CI/CD 整合和環境配置

### 基礎設施依賴
- **Git 版本控制**: 程式碼管理
- **測試專用帳號**: 具備適當權限的測試帳號
- **網路環境**: 穩定的網路連線至測試環境

## Success Criteria (Technical)

### 效能基準
- **測試執行速度**: 單一測試 < 30 秒，完整套件 < 10 分鐘
- **測試穩定性**: 連續執行成功率 > 95%
- **資源使用**: 記憶體使用 < 1GB，CPU 使用合理

### 品質標準
- **程式碼覆蓋率**: 測試程式碼覆蓋所有主要功能
- **文件完整性**: 所有 function 具備清晰註解和使用範例
- **錯誤處理**: 所有異常情況都有適當的處理機制

### 驗收標準
- **功能測試**: 能成功執行登入和系統設定相關測試
- **報告生成**: 能產生包含截圖的詳細測試報告
- **擴展性**: 新增功能測試模組容易且不影響現有功能

## Estimated Effort

### 總體時程評估
- **總開發時間**: 7 週 (35 個工作天)
- **開發資源**: 1-2 名 Python 開發者
- **測試時間**: 每週 2-3 天進行功能驗證

### 關鍵路徑項目
1. **基礎框架搭建** (關鍵): 影響後續所有開發工作
2. **Playwright 整合** (關鍵): 核心自動化引擎
3. **登入功能實作** (關鍵): 所有測試的前置條件
4. **測試報告系統** (重要): 影響測試結果可視性

### 風險緩衝
- **預留 20% 時間緩衝**用於處理技術難題和整合問題
- **分階段驗收**確保每個 Phase 都能達到預期目標
- **持續溝通**與團隊保持密切協作，及時調整實作策略

## Tasks Created
- [ ] #10 - 業務功能模組擴展 (parallel: true)
- [ ] #11 - 測試執行框架與文件完善 (parallel: false)
- [ ] #2 - 專案初始化與環境建置 (parallel: true)
- [ ] #3 - 核心工具類別開發 (parallel: true)
- [ ] #4 - Playwright 與 Stagehand 整合基礎 (parallel: false)
- [ ] #5 - 登入功能模組實作 (parallel: true)
- [ ] #6 - 登入功能測試案例開發 (parallel: true)
- [ ] #7 - 系統設定模組測試實作 (parallel: true)
- [ ] #8 - 測試報告與截圖系統實作 (parallel: true)
- [ ] #9 - 錯誤處理與重試機制實作 (parallel: true)

Total tasks:       10
Parallel tasks:        8
Sequential tasks: 2
Estimated total effort: 90-128 hours
