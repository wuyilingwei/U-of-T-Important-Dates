# Task Plan: 001_[Feature]_UTM日历爬虫与GH-Pages

## 目标
构建完整的 UTM 重要日期日历系统：爬虫脚本 + ICS 生成 + GitHub Pages + 每日自动更新。

## 原子操作步骤

### 阶段1：调研与分析
- [x] 获取 UTM 重要日期页面内容（通过 fetch_webpage 工具）
- [x] 分析 HTML 结构 → 发现 Elfsight JS Widget（app ID: f242be0e-1d36-4aef-8bbf-d260c4c8f05e）
- [x] 尝试 Elfsight API 端点 → 均返回 404/DNS 失败
- [x] 确定技术方案：Playwright headless browser
- [x] 研究日期文本格式：`MON DD [MON DD] SESSION_LABEL description`

### 阶段2：核心功能实现
- [x] 创建 `scripts/requirements.txt`
- [x] 创建 `scripts/scrape_utm.py`（Playwright 爬虫 + ICS 生成器）
- [x] 本地测试脚本，验证输出 utm.ics 正确性

### 阶段3：前端 & 文档
- [x] 创建 `docs/index.html`（GitHub Pages 主页）
- [x] 创建 `README.md`

### 阶段4：CI/CD
- [x] 创建 `.github/workflows/update-calendar.yml`

### 阶段5：验证
- [x] 安装依赖并本地运行一次，生成初始 ICS 文件（175个事件）
- [x] 检查生成的 ICS 格式正确性（全天事件、跨年日期范围）
- [x] 修复 Bug：月份标题（如"April 2026"）渗漏进事件描述
- [x] 修复 Bug：re.search() 可能返回 None 的类型安全问题
- [x] 清理临时调试文件（通过 .gitignore 排除）
