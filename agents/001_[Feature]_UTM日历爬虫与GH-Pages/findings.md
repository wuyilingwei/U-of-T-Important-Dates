# Findings: 001_[Feature]_UTM日历爬虫与GH-Pages

## 技术调研

### 页面结构分析
- UTM 重要日期页面使用 **Drupal 11** CMS
- 日期内容由第三方服务 **Elfsight** 提供（`https://static.elfsight.com/platform/platform.js`）
- Widget App ID：`f242be0e-1d36-4aef-8bbf-d260c4c8f05e`
- HTML 中的 widget 占位符：`<div class="elfsight-app-f242be0e-..." data-elfsight-app-lazy>&nbsp;</div>`

### 尝试的 Elfsight API 端点（均失败）
- `https://core.service.elfsight.com/widget-data/?guid=...` → HTTP 404
- `https://api2.elfsight.com/widget-data/widget/?uuid=...` → DNS 解析失败
- `https://apps.elfsight.com/api/widget/data/?uuid=...` → HTTP 404
- `https://static.elfsight.com/apps/{id}/data.json` → 超时/失败

**结论**：Elfsight 的 API 端点不对外公开或需要认证，无法直接获取数据。

### 解决方案
- 使用 **Playwright** headless Chromium 渲染页面，等待 Elfsight widget 加载完成后提取文本内容
- 等待条件：`.elfsight-app-{id}` 容器的 `textContent` 超过 50 字符

### 日期文本格式（从 fetch_webpage 工具观察到）
```
March 2026  MAR 2   APR 30 SUMMER 2026 Program selection...
April 2026  APR 3 FALL 2025-WINTER 2026 Good Friday...
            APR 7   APR 8 FALL 2025-WINTER 2026 Study break.
```
- 月份标题：`Month Year`（如 `March 2026`）
- 单日事件：`MON DD SESSION description`
- 跨日事件：`MON DD   MON DD SESSION description`
- 描述末尾可能有 `[LEARN MORE](#)` 链接标记

### 年份推断逻辑
| Session | 月份范围 | 年份 |
|---------|---------|------|
| FALL YYYY-WINTER YYYY+1 | Aug-Dec | YYYY |
| FALL YYYY-WINTER YYYY+1 | Jan-Jul | YYYY+1 |
| SUMMER YYYY | May-Aug | YYYY |
| FALL YYYY | Aug-Dec | YYYY |
| WINTER YYYY | Jan-Apr | YYYY |

特殊情况：`DEC 24   JAN 2 FALL 2025-WINTER 2026` → Dec 24, 2025 到 Jan 2, 2026（跨年）

## 失败记录
- `[直接HTTP请求无法获取日期] -> [尝试 requests/urllib] -> [HTML中无日期数据，仅有 Elfsight 占位符]`
- `[Elfsight API端点] -> [尝试4个端点] -> [均失败，不提供公开API]`
