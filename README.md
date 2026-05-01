# cds-twenty-demo

CDS 部署 [Twenty CRM](https://github.com/twentyhq/twenty) 的最小化 deploy repo。

CDS 通过 GitHub link 接入此 repo,读取 `cds-compose.yml`,
自动拉 `twentycrm/twenty:latest` 预构建镜像 + `postgres:16` + `redis:7` 三件套,
跑 server + worker。无需 twenty 源码(image 自含)。

## 这是 Phase 6 实战的产物

- Phase 1-5 机制已就位,见 `inernoro/prd_agent` 的 plan.cds-mysql-readiness.md
- Twenty 暴露的 cdscli 真盲区(B1/B2/B3/B8) 已立 Phase 7 backlog
- 本 repo 用手补 yaml 绕过 cdscli bug,作为"可跑"基线

## 部署方式

```bash
# CDS Dashboard 设置 → 项目 → 添加 → GitHub link → inernoro/cds-twenty-demo
# CDS 自动 webhook → 拉 yaml → docker compose up

# 或本地 CDS:
curl -X POST "http://127.0.0.1:9900/api/projects" \
  -H "X-AI-Access-Key: $AI_ACCESS_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name":"twenty","slug":"twenty","kind":"git","repoUrl":"https://github.com/inernoro/cds-twenty-demo.git"}'
```

## 必填环境变量

部署后在 CDS Dashboard 项目环境变量页面填:
- `SERVER_URL`: 预览域名,如 `http://127.0.0.1:5500/` 或 `https://<branch>-<prefix>-twenty.miduo.org`
