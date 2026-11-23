# AGENTS.md

Hexo 静态博客（基于阿里云开发平台的 Hexo 模板 fork）。无自定义源码，主要工作内容是写文章、调配置、升级依赖。

## 目录结构

- `source/_posts/` — 博客文章（Markdown，front-matter 用 `title/date/tags`）
- `scaffolds/` — `hexo new` 的模板
- `themes/` — 空（仅 `.gitkeep`）；主题 landscape 通过 npm 包 `hexo-theme-landscape` 提供，不要往这里放主题文件
- `public/` — 构建产物，已 gitignore，不要手工编辑
- `_config.yml` — 站点配置；`_config.landscape.yml` — 主题配置覆盖（当前为空文件）

## 常用命令

```bash
npm install                # 安装依赖（首次必需）
npm run server             # 本地预览 http://localhost:4000
npm run build              # hexo generate，输出到 public/
npm run clean              # 清除 public/ 与 db.json 缓存
npx hexo new "文章标题"     # 新建文章到 source/_posts/
```

改完 `_config.yml` 后需要 `npm run clean` 再重启 server，否则配置不生效。

## 注意事项

- **`build.sh` 是阿里云开发平台的部署脚本**，push 后由云端自动执行。它会先清空并重建 `public/`（不可恢复），再复制出 `build/` 目录。本地不要运行它；如确需本地清理构建产物，先向用户列出要删除的具体目录并确认后再操作。
- Hexo 锁定在 **5.4.0**（`package.json` 的 `hexo.version`），依赖均为旧主版本。远程存在 dependabot 的 Hexo 6 升级分支——升级属变更工作，不要顺手 bump。
- 固定链接格式 `:year/:month/:day/:title/`（`_config.yml`），修改会破坏已发布文章的 URL。
- 无 lint / test / typecheck 设施，验证方式就是 `npm run build` 成功且 `npm run server` 预览正常。
- 当前开发分支 `feature/1.0.0`，PR 目标分支为 `main`。
- README.md 是阿里云模板的中文使用说明（面向云端部署流程），与本仓库实际维护关系不大。
