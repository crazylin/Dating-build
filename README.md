# Dating-build

公开打包仓：clone 私有 [`crazylin/Dating`](https://github.com/crazylin/Dating) 指定 tag，产出五平台安装包并上传到 Cloudflare R2 `Dating/{version}/`，再回写许可服 `product_id=dating`。

## 工作流

| 文件 | 用途 |
|---|---|
| `build-dating.yml` | 发版：测试 + 四平台打包 + R2 + 许可 release 行 |
| `test-dating.yml` | 仅跑源码仓 `scripts/ci-test.sh`，不打包 |
| `publish-r2-only.yml` | 补传 R2（需已有 build run 的 artifact） |
| `set-min-update-id.yml` | PATCH `dating.min_update_id` |
| `prune-r2-versions.yml` | 按前缀清理 R2 旧版本 |

## Secrets（与 TalkyTimes-build 同名）

- `PD_CLONE_SSH_KEY` 或 `PD_CLONE_PAT`：clone 私有 Dating 仓
- `R2_*`、`TALKY_LICENSE_SERVER_URL`、`TALKY_LICENSE_DEPLOY_TOKEN`、`TALKY_LICENSE_ADMIN_TOKEN`

私有 Dating 仓 tag 推送会通过 `dispatch-build.yml` 发 `repository_dispatch` 到本仓。
