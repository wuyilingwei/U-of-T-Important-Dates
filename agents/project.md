# U-of-T-Important-Dates 项目索引

> 最后更新：2026-04-03

## 项目目标

自动抓取多伦多大学密西沙加校区（UTM）注册主任办公室发布的重要学术日期，生成标准 ICS 日历文件并通过 GitHub Pages 提供静态下载与动态 webcal 订阅。每日自动更新一次。

> **声明**：本项目不是多伦多大学的官方产品，仅为学生便利工具。

## 技术栈

- **运行时**：Python 3.12
- **网页渲染**：Playwright（Chromium headless）— 因为日期由 Elfsight JS widget 动态加载
- **日历生成**：icalendar + pytz
- **CI/CD**：GitHub Actions（每日 08:00 UTC cron）
- **托管**：GitHub Pages（`docs/` 文件夹）

## 模块结构

```
/
├── .github/
│   └── workflows/
│       └── update-calendar.yml     # 每日自动更新工作流
├── agents/                          # 项目文档与任务追踪
│   ├── project.md                   # 本文件
│   ├── tasks.md                     # 任务列表
│   └── 001_[Feature]_UTM日历爬虫与GH-Pages/
│       ├── task_plan.md
│       ├── findings.md
│       └── progress.md
├── scripts/
│   ├── scrape_utm.py                # 主爬虫脚本（Playwright + ICS生成）
│   └── requirements.txt             # Python 依赖
├── docs/                            # GitHub Pages 根目录
│   ├── index.html                   # 项目主页
│   └── utm.ics                      # 生成的 ICS 文件（自动更新）
└── README.md
```

## 关键发现

- UTM 重要日期页面：https://www.utm.utoronto.ca/registrar/dates
- 日期内容由 **Elfsight widget**（app ID: `f242be0e-1d36-4aef-8bbf-d260c4c8f05e`）动态渲染
- 原始 HTML 不含日期数据，必须使用 Playwright 等无头浏览器渲染后才能提取
- 日期格式：`MON DD [MON DD] SESSION_LABEL description`
- Session 标签示例：`FALL 2025-WINTER 2026`、`SUMMER 2026`
- 通过 session 标签推断年份

## User-Agent

`U-of-T-Calendar-Bot/1.0 (Contact: sy.lei@mail.utoronto.ca; Student Project)`
