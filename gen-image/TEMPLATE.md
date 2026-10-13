# gen_image.py 模板（复制为 gen_image.py 并填入 API key）

本技能的调用脚本 `gen_image.py` 含 API key，被 .gitignore 排除、不进仓库。
在新机器上重建：把本模板复制为同目录 `gen_image.py`，替换 `<YOUR_API_KEY>`。

API key 与 base_url 由用户提供（如遗失请向用户重新索取）。

---

脚本全文见本地 gen_image.py；结构要点（新机器重建时按此写）：

- `BASE_URL = "https://dcsapi.dcs.cloud/api/aigress/unified"`，key 填入 `API_KEY`
- 两个端点按模型分叉：
  - seedream-image-v5.0-pro → `POST /v1/wand/si-image/generation`，响应 `data[0].url`（腾讯云 COS 临时链接，约 12h 失效，必须下载到本地）
  - gpt-image-2 → `POST /v1/images/generations`（OpenAI 兼容），响应 `data[0].b64_json`（base64 PNG，直接落盘）
- 请求体：`{"model": ..., "prompt": ..., "size": "1024x1024"}`
- HTTP 全走 curl 子进程并带 `--ssl-no-revoke`（公司网络 TLS 吊销拦截，requests 不可用）
- 成功后 stdout 最后一行 `FILE: <绝对路径>`
