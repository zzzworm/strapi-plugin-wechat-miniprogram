# 发布流程

此插件通过 GitHub Release 提供已构建的 npm tarball，供下游 Strapi 项目直接安装。

## 发布前检查

```bash
npm ci
npm pack --dry-run
```

确认产物只包含 `package.json` 和 `dist/` 下的运行时文件。

## 发布

1. 更新 `package.json` 的版本号。
2. 提交版本修改并创建同名 tag，例如 `v1.0.13`。
3. 推送 tag。GitHub Actions 会执行构建、生成 `strapi-plugin-wechat-miniprogram-<version>.tgz`，并将其附加到对应的 GitHub Release。

```bash
git add package.json .github/workflows/release.yml RELEASING.md
git commit -m "release: v1.0.13"
git tag v1.0.13
git push origin main --tags
```

下游项目使用 Release asset，而不是 Git URL：

```json
"strapi-plugin-wechat-miniprogram": "https://github.com/zzzworm/strapi-plugin-wechat-miniprogram/releases/download/v1.0.13/strapi-plugin-wechat-miniprogram-1.0.13.tgz"
```

安装 tarball 不需要为该插件配置 pnpm 的 `allowBuilds` 或 `onlyBuiltDependencies`。
