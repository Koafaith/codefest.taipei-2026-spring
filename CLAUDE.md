# codefest.taipei-2026-spring

2026 春季程式設計節官網，部署至 `codefest.taipei/2026-spring/`。

## 技術棧

- Nuxt 3.16.0（`ssr: false`，SPA 模式）
- Vue 3 + TypeScript
- Tailwind CSS
- i18n（`assets/locales/zh.json`）
- Vite

## 開發

```bash
# 安裝依賴
npm install

# 啟動 dev server
npx nuxi dev --port <port>
```

## 部署

本專案不直接部署，需透過 [codefest-deployment](https://github.com/Koafaith/codefest-deployment) repo 統一部署。

完整部署流程請參考 `codefest-deployment/CLAUDE.md`。

簡要流程：
1. 在本 repo 建立分支 → commit & push → PR → merge to main
2. 停掉 dev server
3. `npx nuxi generate && cp -r .output/public/* /path/to/codefest-deployment/public/2026-spring/`
4. 到 deployment repo 執行 `node addNonceToInlineScripts.js`
5. 部署到 demo 驗證 → 部署到 production

## Git 規範

- Commit 訊息格式：`feat: description` / `fix: description`，單行，不加 body
- 不直接 commit 到 main，一律走分支 → PR → merge
- PR body 不加 "Generated with Claude Code" 等 AI 標註

## 重要檔案

- `assets/locales/zh.json` — 所有文案、活動資料、獲獎團隊、影音回顧、照片回顧
- `nuxt.config.ts` — baseURL: `/2026-spring/`，SEO title 設定
- `interfaces/past.interface.ts` — PastWinningTeam、PastVideo 等型別定義
- `components/organism/WinningTeamDialog.vue` — 獲獎團隊彈窗元件
