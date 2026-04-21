# CHANGELOG

本文件记录 duoyuan-skill 的所有版本变更。

格式遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [SemVer](https://semver.org/lang/zh-CN/)。

---

## [Unreleased]

计划中的 Phase 2 变更：
- 接入 MCP Server（腾讯云 CloudBase）
- 启用 `get_news` 工具
- 增加英文版本支持
- API Key 认证机制

---

## [0.1.0] - 2026-04-21

### Added
- 首次发布 Phase 1 MVP
- `SKILL.md` 主指令文件，内嵌公司静态数据
- `skill.json` 定义 8 个可用工具：
  - `get_company_info`（公司基本信息）
  - `get_business_overview`（三大业务板块）
  - `get_products`（产品目录）
  - `get_solutions`（解决方案）
  - `get_project_cases`（项目案例）
  - `get_certifications`（资质荣誉）
  - `get_history`（发展历程）
  - `get_contact`（联系方式）
- `references/` 目录：结构化权威数据源
  - `company-profile.md`
  - `product-catalog.md`
  - `project-cases.md`
  - `certifications.md`
- `UPGRADE.md` 更新机制说明
- `README.md` 与 MIT License

### Deferred（暂缓）
- `get_news` 工具（需 Phase 2 MCP Server 提供实时数据）
- `submit_inquiry` 工具（Phase 3 询盘提交）
- 英文版支持（Phase 2）
