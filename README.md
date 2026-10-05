# license

离线生成开源许可证文件的小工具：许可证名进，标准文本出。纯标准库，零依赖，不联网。

## 快速开始

```bash
# 打印 MIT 文本（年份默认今年，权利人默认 ljiang9）
python -m license mit

# 指定权利人和年份
python -m license mit --holder "Zhang San" --year 2026

# 写入 LICENSE 文件（已存在时拒绝覆盖，除非加 --force）
python -m license apache-2.0 --write

# 只看 SPDX 标识符（给 CI 用）
python -m license mit --spdx
# 输出：MIT

# 列出支持的许可证
python -m license --list
```

## 支持的许可证

| 名称 | SPDX | 一句话 |
|---|---|---|
| `mit` | MIT | 简短宽松，商用友好，最常用 |
| `apache-2.0` | Apache-2.0 | 宽松，带专利授权条款 |
| `gpl-3.0` | GPL-3.0-only | 强 copyleft：衍生作品必须同样开源 |
| `bsd-2` | BSD-2-Clause | 极简宽松，只要求保留版权声明 |
| `bsd-3` | BSD-3-Clause | BSD-2 加禁止背书条款 |
| `isc` | ISC | 功能等价于简化版 MIT |
| `unlicense` | Unlicense | 放弃版权，释放到公有领域 |

别名：`apache`、`apache2`、`gpl`、`gpl3`、`bsd2`、`bsd3`。

## 设计取舍

- 文本是各许可证的**官方标准文本**，工具只做"填空"（年份/权利人），不改写、不删减。
- Apache-2.0 附录里的 `Copyright [yyyy] [name of copyright owner]` 会自动填上；GPL-3.0 末尾"如何应用"里的 `<year>` / `<name of author>` 同理。
- Unlicense 是公有领域声明，没有权利人占位符，`--holder` 对它无效（不报错）。
- `--write` 默认拒绝覆盖已存在的 LICENSE，防止手滑丢了自己改过的文本。

## 退出码

| 退出码 | 含义 |
|---|---|
| 0 | 成功 |
| 1 | `--write` 时文件已存在且未加 `--force` |
| 2 | 用法错误（未知许可证、缺名称等） |

## 诚实说明

- **本工具不是法律建议。** 选许可证涉及专利、兼容性、商业策略，请咨询律师；工具只解决"把标准文本填好"的体力活。
- 文本以各许可证发布时的官方版本为准；SPDX 标识符遵循 SPDX License List。
- GPL-3.0 标记为 `GPL-3.0-only`（仅 v3），如需"v3 或更高"请手动把标识改为 `GPL-3.0-or-later`。

## 已知局限

- 只收录 7 种最常用的许可证；LGPL、MPL、AGPL 等暂不支持（欢迎提需求）。
- 不做许可证兼容性检查（比如"GPL 代码能不能进 MIT 项目"这种问题）。
