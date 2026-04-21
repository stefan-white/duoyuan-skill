# duoyuan-skill

> 郑州多元智能装备股份有限公司 AI Skill 开发仓库

本仓库是多元智能 AI Skill 的开发工作区，包含 Skill 发布包、Phase 2 MCP Server 代码预留，以及开发文档。

如果你是**用户**想安装使用，直接看 [`duoyuan-skill/README.md`](./duoyuan-skill/README.md)。

---

## 项目定位

为 AI 助手（Claude Code / Cursor / Windsurf / Trae 等）提供郑州多元智能装备股份有限公司的专业知识能力：

- 回答公司信息、业务板块、产品线、项目案例查询
- 提供联系方式、工作时间、资质荣誉等基本信息
- 根据受众（国内/海外/求职者/合作伙伴）调整回答风格
- Phase 2 后通过 MCP Server 实时同步公司动态

---

## 仓库结构

```
dy-skills/
├── duoyuan-skill/         # Skill 发布包（用户安装的部分）
│   ├── SKILL.md           # Agent 主指令
│   ├── skill.json         # MCP 工具定义
│   ├── references/        # 权威结构化数据
│   ├── CHANGELOG.md       # 版本记录
│   └── UPGRADE.md         # 更新机制说明
│
├── mcp-server/            # Phase 2：MCP Server（预留目录）
│
└── docs/                  # 开发文档
    └── duoyuan-skill-dev-doc.md
```

---

## 快速开始

### 用户安装（Claude Code 示例）

```bash
git clone https://github.com/stefan-white/duoyuan-skill.git ~/.claude/skills/duoyuan-skill-src
ln -s ~/.claude/skills/duoyuan-skill-src/duoyuan-skill ~/.claude/skills/duoyuan-skill
```

其他平台路径见 [`duoyuan-skill/README.md`](./duoyuan-skill/README.md#安装)。

### 本地试用

新开会话询问：

```
介绍一下郑州多元智能
多元的焊装线有哪些产品？
多元做过哪些海外项目？
```

---

## 开发进度

| Phase | 目标 | 状态 |
|-------|------|------|
| **Phase 1** | MVP：纯静态数据 + 8 个工具 + 中文 | ✅ v0.1.0 已发布 |
| **Phase 2** | MCP Server（腾讯云 CloudBase）+ 实时数据 + 英文版 | 🔜 规划中 |
| Phase 3 | 询盘提交 + 微信生态集成 + Gitee/ClawHub 镜像 | ⏳ 待启动 |
| Phase 4 | 技术参数库 + 智能选型 + 3D/视频内容 | ⏳ 长期 |

详细路线图见 [`docs/duoyuan-skill-dev-doc.md`](./docs/duoyuan-skill-dev-doc.md) 第五章。

---

## 开发指引

### 修改数据

**权威源是 `duoyuan-skill/references/` 下的 Markdown 文件**。修改流程：

1. 编辑对应 reference 文件（如 `product-catalog.md`）
2. 同步到 `duoyuan-skill/SKILL.md` 的对应章节
3. 根据变更规模升级版本号（`skill.json` + `SKILL.md` frontmatter）
4. 更新 `duoyuan-skill/CHANGELOG.md`
5. Git commit + tag + push

详细规则见 [`duoyuan-skill/UPGRADE.md`](./duoyuan-skill/UPGRADE.md)。

### 修改工具定义

编辑 `duoyuan-skill/skill.json`：

- 新增 / 删除工具需升级 MINOR 版本
- 修改工具签名需升级 MAJOR 版本（且先在 MINOR 版本标记 `deprecated`）

### Phase 2 MCP Server 开发

见 [`mcp-server/README.md`](./mcp-server/README.md) 与开发文档 §4。

---

## 文档索引

| 文档 | 说明 |
|------|------|
| [`duoyuan-skill/README.md`](./duoyuan-skill/README.md) | Skill 用户手册（安装、能力、触发词） |
| [`duoyuan-skill/SKILL.md`](./duoyuan-skill/SKILL.md) | Agent 运行时指令 |
| [`duoyuan-skill/CHANGELOG.md`](./duoyuan-skill/CHANGELOG.md) | 版本变更记录 |
| [`duoyuan-skill/UPGRADE.md`](./duoyuan-skill/UPGRADE.md) | 更新机制与发布流程 |
| [`docs/duoyuan-skill-dev-doc.md`](./docs/duoyuan-skill-dev-doc.md) | 完整开发方案（含研究、架构、路线图） |

---

## 贡献

内部开发，暂不开放外部 PR。公司内部成员如需补充数据或修正内容：

1. 在原仓库新建分支
2. 按"修改数据"流程更新
3. 发 PR 给维护者审核

---

## 联系

| 渠道 | 信息 |
|------|------|
| 公司服务热线 | 400-666-1196 |
| 公司邮箱 | info@duoyuan.cn |
| 国内官网 | [www.zzdy.cn](https://www.zzdy.cn) |
| 国际官网 | [duoyuan.cn](https://duoyuan.cn) |
| 仓库维护 | Stefan White |

---

## License

MIT © 2026 Stefan White
