# 更新机制

> 版本号、CHANGELOG、各平台更新路径与数据同步流程说明

---

## 1. 版本号规则（SemVer）

采用语义化版本 `MAJOR.MINOR.PATCH`：

| 类型 | 触发场景 | 示例 |
|------|----------|------|
| **PATCH** | 数据微调、文案修正、bug 修复 | `0.1.0` → `0.1.1` |
| **MINOR** | 新增工具、新增字段、向后兼容的能力增强 | `0.1.1` → `0.2.0` |
| **MAJOR** | 工具签名变更、触发词结构重构、不兼容改动 | `0.x.x` → `1.0.0` |

版本号需同时更新以下三处：
- `skill.json` 的 `version` 字段
- `SKILL.md` frontmatter 的 `version` 字段
- `CHANGELOG.md` 新增条目

---

## 2. CHANGELOG 维护

每次发布必须在 `CHANGELOG.md` 顶部新增条目，格式：

```markdown
## [0.1.1] - 2026-04-25

### Added
- get_products 新增"物流仓储"子类

### Changed
- MALS 系统描述补充结构形式说明

### Fixed
- 联系方式邮箱拼写
```

分类关键词：`Added` / `Changed` / `Deprecated` / `Removed` / `Fixed` / `Security`

---

## 3. 数据更新流程

**权威数据源**：`references/` 目录下的 Markdown 文件。

更新步骤（按顺序执行）：

```
1. 编辑 references/ 下的对应文件（例如 product-catalog.md）
2. 同步摘要到 SKILL.md（保持两者内容一致）
3. 根据变更规模决定版本号升级
4. 更新 CHANGELOG.md
5. git commit + tag（例：git tag v0.1.1）
6. 推送到 GitHub，用户通过 git pull 获取更新
```

> **禁止**只改 SKILL.md 不改 references/，会导致数据源漂移。

---

## 4. 用户更新路径（各平台）

### 方式一：Git Pull（推荐）

适合所有 `.md/.json` 文件安装方式的平台。

```bash
cd .claude/skills/duoyuan-skill  # 或对应平台路径
git pull origin main
```

若通过 `git clone` 安装，此方式最省事。

### 方式二：重新安装

适合不是 git clone 安装的情况：

```bash
# 1. 删除旧版本
rm -rf .claude/skills/duoyuan-skill

# 2. 克隆最新版本
git clone https://github.com/stefan-white/duoyuan-skill.git .claude/skills/duoyuan-skill
```

### 方式三：脚本化更新（Phase 2 提供）

Phase 2 将提供 `scripts/update.sh`，自动完成：
- 检测当前版本
- 对比远程最新版本
- 备份本地修改
- 拉取更新

---

## 5. 平台差异说明

| 平台 | 安装目录 | 更新生效方式 |
|------|----------|-------------|
| Claude Code | `.claude/skills/duoyuan-skill/` | 重启会话 |
| Cursor | `.cursor/skills/duoyuan-skill/` | 重启 IDE |
| Windsurf | `.windsurf/skills/duoyuan-skill/` | 重启 IDE |
| Trae | `.trae/skills/duoyuan-skill/` | 重启 IDE |
| 通用 | `.agents/skills/duoyuan-skill/` | 按宿主平台规则 |

> 多数平台在启动时扫描 skills 目录并加载 `SKILL.md`，重启是最可靠的生效方式。

---

## 6. MCP Server 更新（Phase 2 生效）

接入 MCP Server 后，**数据更新不再依赖用户拉取**：

```
管理员更新 references/ → CI 同步到 CloudBase 数据库 → 用户下次调用自动拿到新数据
```

用户仅在以下情况需要更新本地 Skill：
- `skill.json` 工具签名变更（新增/删除工具、改参数）
- `SKILL.md` 指令与品牌调性调整
- MCP 端点变更

静态数据变更不再要求用户更新本地文件。

---

## 7. 废弃与破坏性变更

破坏性变更（MAJOR 升级）必须提前一个 MINOR 版本标记废弃：

```yaml
# skill.json
tools:
  - name: get_old_tool
    deprecated: true
    deprecated_since: "0.5.0"
    replaced_by: "get_new_tool"
    removal_version: "1.0.0"
```

废弃工具在 MINOR 版本期间保持可用，并在返回值末尾附上迁移提示。

---

## 8. 发布检查清单

发布前确认：

- [ ] `references/` 和 `SKILL.md` 内容一致
- [ ] `version` 字段三处同步
- [ ] `CHANGELOG.md` 已更新
- [ ] Git tag 已创建（`git tag v0.x.y`）
- [ ] GitHub Release 已发布（附迁移说明）
- [ ] 至少一个平台本地测试通过

---

## 9. 历史版本兼容性

| 版本范围 | 支持状态 |
|----------|----------|
| `0.1.x` | 当前稳定（Phase 1，静态模式） |
| `0.2.x` | 规划中（Phase 2，MCP 接入） |
| `< 0.1.0` | 无（首次发布起） |

用户停留在旧 MINOR 版本仍可用，但不保证与新 MCP 端点兼容。
