# 2026雙北程式設計節

> 這是一個基於 **Nuxt 3.16.0** 的前端專案，使用 Vue 3、Pinia、Tailwind CSS，並支援 i18n。

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](./LICENSE) file for details.

## 系統需求

請確保你的環境符合以下要求：

| **需求**   | **最低版本**  | **建議版本**  |
|------------|-------------|-------------|
| **Node.js** | `>=18.14.0` | `18 LTS` (`18.17.0` 以上) |
| **NPM**    | `>=8.0.0`   | `8.x` 或 `9.x` |
| **Nuxt**   | `3.16.0`    | `3.16.0` |

## 專案設定

請確保已經安裝 Node.js 和 npm，並執行執行以下指令：

```sh
npm install
```

### 開發模式

```bash
npm run dev
```

啟動後，請在瀏覽器開啟：`http://localhost:3000`

### 專案打包

```bash
npm run generate
```

### 專案部署

專案使用 CI/CD 自動部署，請發起 Pull Request，待審核通過並成功合併至 main 分支後，即會自動觸發部署流程。

## 開發規範與工具

### 格式與 Lint

- **ESLint**：程式碼檢查
- **Prettier**：程式碼格式化
- **Stylelint**：樣式檢查

### 檢查指令

```bash
npm run lint:js     # JavaScript / TypeScript / Vue 檢查
npm run lint:style  # SCSS / Style 檢查
```

## 專案結構

components 元件管理採用 [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/)。

- atom: 不可分割元件，通常為 base 類型元件，ex: `button`, `input`。
- molecule: 由 atom 元件組成，具有單一功能性，ex: search bar (`input` + `button`)。
- organism: 由 atom 與 molecule 元件組成，多功能性的元件，ex: header。

元件命名規則採 UpperCamelCase，引用元件時需帶上分類 prefix，ex: \<AtomButton />。

結構規則採用 Nuxt3 結構 [Diectory Structure](https://nuxt.com/docs/guide/directory-structure/nuxt)。

## 專案維護說明

### 多語系檔案維護 (zh.json)

網站文案主要存放於 `assets/locales/zh.json` 檔案中，採用巢狀 JSON 格式。以下說明如何進行文案更新：

#### 更新步驟

1. **修改文案**
   - 依照現有的 JSON 結構找到對應的區塊
   - 保持相同的縮排格式

2. **注意事項**
   - 修改時請確保 JSON 格式正確，可使用 JSON 驗證工具檢查
   - 文字中如有特殊字元（如引號），需使用跳脫字元 `\`
   - 更新後請在本地測試，確認顯示正常
   - 建議保留一份修改前的備份
3. **測試驗證**
   - 文案更新後，請至少檢查以下項目：
     - 頁面是否正常渲染
     - 文字是否正確換行
     - RWD 版面是否正常
     - 特殊字元是否正確顯示

#### 參數對照表

| 參數 | 子參數 | 說明 | 範例 |
|------|--------|------|------|
| hero_banner | section_title | 首頁大標題文字 | "2026雙北程式設計節" |
| | content | 競賽資訊列表 | [{"label": "競賽日", "value": "5/31 Sat - 6/1 Sun"}, {"label": "競賽地點", "value": "新北市政府大樓"}] |
| rules | available | 控制競賽規則區塊是否顯示 | true |
| | section_title | 競賽規則區塊標題 | "競賽規則" |
| | description | 競賽規則說明文字或標語 | "The power of ..." |
| | content_title | 內容標題 | "概念" |
| | content | 詳細內容 | "在智慧城市與數據驅動時代..." |
| | buttons | 相關連結按鈕 | 參考 [Button](#Button) |
| | judges | 評審資訊 | {"available": true, "list": [...]}  <br>可控制 available 參數來決定此區塊是否顯示<br>list 內容請參考 [JudgeList](#JudgeList) |
| | prospectus | 競賽規則概要 | 參考 [Prospectus](#Prospectus) |
| schedule | available | 控制重要時程區塊是否顯示 | true |
| | section_title | 時程區塊標題 | "重要時程" |
| | apppy_count_down | 報名截止倒數計時目標日期 | "2025-04-30 23:59:59" |
| | count_down | 競賽倒數計時目標日期 | "2025-05-31 10:00:00" |
| | list | 時程列表 | 參考 [ScheduleList](#ScheduleList) |
| news | available | 控制最新消息區塊是否顯示 | true |
| | section_title | 最新消息區塊標題 | "最新消息" |
| | list | 消息列表 | 參考 [News](#News) |
| past | available | 控制參賽回顧區塊是否顯示 | true |
| | section_title | 參賽回顧區塊標題 | "參賽回顧" |
| | description | 參賽回顧區塊說明 | "收錄獲獎團隊及影音回顧" |
| | winning_teams | 獲獎團隊回顧 | 參考 [PastWinningTeams](#PastWinningTeams) |
| | videos | 影片回顧 | 參考 [PastVideos](#PastVideos) |
| sponsor | available | 控制感謝單位區塊是否顯示 | true |
| | section_title | 感謝單位區塊標題 | "感謝單位" |
| | list | 感謝單位列表 | 參考 [Sponsor](#Sponsor) |
| faq | section_title | FAQ區塊標題 | "FAQ" |
| | list | FAQ列表 | {"type": "流程疑問", "list": [...]}<br>type為常見問題 Tab 標頭，傳入 "流程疑問" \| "技術疑問"<br>list 內容請參考 [Faq](#Faq) |
| contact | address_ntpc | 新北市政府地址 | "220242 新北市板橋區中山路一段161號" |
| | address_tpe | 台北市政府地址 | "110204 臺北市信義區市府路1號" |
| | line_id | Line ID | "@552qhvcr" |
| | office_hours | 辦公時間 | "週一至週五 09:00-17:00" |
| | email | 電子郵件 | "codefesttaipei@gov.taipei" |
| | phone | 聯絡電話 | "02-77097801 #7584" |
| | buttons | 聯絡按鈕列表 | 參考 [Button](#Button) |
| policy | available | 控制政策區塊是否顯示 | false |
| | list | 政策列表 | 參考 [PolicyItem](#PolicyItem) |
| apply_url | | 報名表單連結 | "https://www.surveycake.com/s/mVlKa" |
| past_url | | 歷屆紀錄連結(Welcome Page) | "https://codefest.taipei/welcome" |

##### Button
| 參數 | 說明 | 範例 |
|------|------|------|
| name | 按鈕顯示文字 | "Line" |
| link | 按鈕連結網址 | "https://line.me/R/ti/p/@552qhvcr" |

##### JudgeList
| 參數 | 說明 | 範例 |
|------|------|------|
| name | 評審列表類別 | "初選/決選" |
| list | 評審列表 | 參考 [Judge](#Judge) |

##### Judge
| 參數 | 說明 | 範例 |
|------|------|------|
| id | 評審編號 | 0 |
| thumbnail | 評審照片路徑 | "images/judge-sample.png" |
| name | 評審姓名 | "評審1" |
| corporation | 服務單位 | "台北市資訊局" |
| position | 職稱 | "專門委員" |

##### Prospectus
| 參數 | 說明 | 範例 |
|------|------|------|
| title | 簡章標題 | "規則概要" |
| image_url | 簡章圖片路徑 | "images/prospectus-sample.png" |
| contents | 簡章內容列表 | 參考 [Content](#Content) |

##### Content
| 參數 | 說明 | 範例 |
|------|------|------|
| sub_title | 內容章節標題 | "< 壹、活動背景說明 >" |
| sub_content | 內容章節說明，支援 HTML 格式 | "臺北市政府資訊局及新北市政府資訊中心..." |

##### ScheduleList
| 參數 | 說明 | 範例 |
|------|------|------|
| id | 時程 id | "online" |
| schedule_name | 時程名稱 | "線上說明會 04.07" |
| schedule_sub_name | 時程次要名稱 | "2025年04月07日 星期一" |
| button | 時程連結按鈕 | 參考 [ScheduleButton](#ScheduleButton) |
| schedule_headers | 時程標頭 | 參考 [ScheduleHeaders](#ScheduleHeaders) |
| schedule | 時程內容 | 參考 [Content](#Content) |

##### ScheduleButton
| 參數 | 說明 | 範例 |
|------|------|------|
| text | 按鈕名稱 | "立即報名" |
| link | 按鈕連結 | "apply" |
| type | 按鈕類型 | "outside_link" \| "route" \| "dialog" |

按鈕類型說明：
- `outside_link`：外部連結，完整 URL
- `route`：內部路由
  
- `dialog`：彈出視窗，可傳入：
  - `apply`：報名表單
  - `news`：最新消息
  - `mobileMenu`：小網 navbar menu
  - `winningTeam`：獲獎團隊

##### ScheduleHeaders
| 參數 | 說明 | 範例 |
|------|------|------|
| name | 標頭名稱 | "時間" \| "議程" \| "主講人" |

##### Schedule
| 參數 | 說明 | 範例 |
|------|------|------|
| col1 | 時程內容欄位1 | "17:05-17:35" |
| col2 | 時程內容欄位2 | "競賽須知\n臺北城市儀表板使用技術說明" |
| col3 | 時程內容欄位3 | "活動執行團隊\n開發團隊" |

##### News
| 參數 | 說明 | 範例 |
|------|------|------|
| id | 貼文編號 | 1 |
| date | 發布日期 | "2025.03.31" |
| title | 貼文標題 | "📢 最新消息｜2025 雙北程式設計節-城市儀表板大黑客松正式開跑！" |
| image_url | 貼文圖片路徑 | |
| content | 貼文內容，支援 HTML 格式與換行符號 \n | "讓數據發聲，開源創新！「2025 雙北程式設計節-城市儀表板大黑客松」 即將登場，首獎 30 萬，總獎金 70 萬，等你來挑戰！\n\n本競賽由臺北市政府資訊局與新北市政府資訊中心共同主辦..." |
| available | 控制貼文是否顯示 | true |
| tag | 貼文類型 | "news" (最新消息) \| "media" (媒體報導) |

##### PastWinningTeams
| 參數 | 說明 | 範例 |
|------|------|------|
| title | 區塊標題 | "獲獎團隊" |
| more_winning_team_photos_url | 更多獲獎團隊照片連結 | |
| list | 獲獎團隊列表 | 參考 [WinningTeam](#WinningTeam) |

##### WinningTeam
| 參數 | 說明 | 範例 |
|------|------|------|
| id | 團隊編號 | 0 |
| ranking | 獲獎名次 | "[春季] 第一名 \|" |
| team_name | 團隊名稱 | "綠擘者聯盟" |
| thumbnail | 團隊照片路徑 | "images/news-sample.png" |
| team_members | 團隊成員 | "吳典叡(臺大電機系學會-資訊部長)、陳柏叡(臺大電機系學會-資訊部長)..." |
| descriptions | 團隊介紹 | [{"title": "團隊簡介", "content": "建築減碳健診隊團隊開發高互動性的災害應變儀表板..."}] |
| image_list | 團隊作品圖片列表 | ["images/news-sample.png", "images/news-sample2.png", ...] |

##### PastVideos
| 參數 | 說明 | 範例 |
|------|------|------|
| title | 區塊標題 | "影音回顧" |
| more_videos_url | 更多影音回顧連結 | |
| list | 影片列表 | 參考 [Video](#Video) |

##### Video
| 參數 | 說明 | 範例 |
|------|------|------|
| id | 影片編號 | 0 |
| date | 影片發佈日期 | "2024.09.20" |
| title | 影片標題 | "[秋季] 2024城市通微服務大黑客松" |
| thumbnail | 影片縮圖路徑 | "images/videos/video-sample.png" |
| video_url | 影片連結 | "https://www.youtube.com/watch?v=8_ZaFYZ9BQU" |

##### Sponsor
| 參數 | 說明 | 範例 |
|------|------|------|
| id | 感謝單位編號 | 0 |
| image_url | 感謝單位 logo | "images/sponsors/sponsor-sample.png" |

##### Faq
| 參數 | 說明 | 範例 |
|------|------|------|
| title | 問題標題 | "競賽什麼時候、在哪裡辦？" |
| content | 問題內容，支援 HTML 格式 | "2025年5月31日（星期六）到6月1日（星期日），兩天一夜，在新北市板橋區中山路一段161號（新北市政府大樓）。" |

##### PolicyItem
| 參數 | 說明 | 範例 |
|------|------|------|
| name | 政策名稱 | "政府網站資料開放宣告" |
| link | 政策連結 | |

[![Maintained by Koafaith](https://img.shields.io/badge/maintained%20by-Koafaith-blue)](https://github.com/Koafaith)