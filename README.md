# 山西财经大学期末资料索引

![山西财经大学期末资料索引：可检索、有清单、可校验](docs/assets/hero.png)

> A searchable public index of final-exam and study materials for Shanxi University of Finance and Economics, organized with a manifest and integrity hashes.

本仓库将山西财经大学历年期末真题与复习资料按科目、资料类型整理，并提供可搜索的索引、机器可读清单与 SHA-256 校验值。当前收录 **121 份资料**，涵盖 **21 个科目**。

## 快速查找

- 按资料类型与科目浏览：[INDEX.md](INDEX.md)
- 搜索完整文件清单：[MANIFEST.csv](MANIFEST.csv)
- 直接查看专题目录：[政治经济学历年真题](政治经济学-历年真题/README.md)（4 份）
- 在 GitHub 页面按 <kbd>t</kbd> 搜索文件名，或下载 `MANIFEST.csv` 后筛选科目、学年、资料类型与扩展名

## 资料统计

| 维度 | 数量 |
| --- | ---: |
| 文件总数 | 121 |
| 科目数 | 21 |
| 期末试卷 | 90 |
| 复习资料 | 22 |
| 其他资料 | 6 |
| 图片资料 | 3 |
| 政治经济学历年真题 | 4 |

文件格式包括 111 份 PDF、5 份 DOCX、2 份 DOC 与 3 份 JPG；统计以 [MANIFEST.csv](MANIFEST.csv) 为准。

## 仓库结构

```text
.
├── README.md                 # 项目入口与使用说明
├── INDEX.md                  # 按资料类型、科目整理的阅读索引
├── MANIFEST.csv              # 121 份文件的路径、属性与 SHA-256
├── 全部资料/                 # 按资料类型与科目归档的文件
├── 政治经济学-历年真题/      # 政治经济学试卷专题子集
└── docs/assets/              # README 与社交预览图的可复现源文件
```

## 如何使用 INDEX 与 MANIFEST

想快速浏览时，打开 [INDEX.md](INDEX.md)，先按「资料类型 + 科目」定位，再进入对应目录。政治经济学试卷也可通过[专题子集](政治经济学-历年真题/README.md)直接查看。

需要精确搜索、统计或校验时，使用 [MANIFEST.csv](MANIFEST.csv)。每行对应一份整理后的文件，包含来源期次、原始相对路径、整理后路径、专题路径、科目、资料类型、扩展名、字节数与 SHA-256。可在表格软件中筛选，也可在 PowerShell 中查询：

```powershell
Import-Csv .\MANIFEST.csv |
  Where-Object { $_.Subject -eq '高等数学' -and $_.MaterialType -eq '期末试卷' }
```

## 提交资料与纠错

提交新资料时，请提供：

- 科目
- 学年
- 资料类型（期末试卷、复习资料、图片资料或其他资料）
- 资料来源与允许公开的说明
- 已移除姓名、学号及其他可识别个人身份的信息

发现分类、文件信息或链接错误，或希望补充资料，请提交 GitHub Issue，说明对应文件路径和建议修改内容。请勿在 Issue 中公开个人信息或未获授权的资料。

## 隐私、版权与下架

本仓库仅用于学习交流与备考参考。对文件的整理、建立索引和计算哈希值，不代表底层文件的权利发生转移，也不构成对底层文件的重新许可。本仓库不授权任何商业性再分发。

如你是相关权利人，或发现资料包含姓名、学号等个人信息，可通过 GitHub Issue 提交下架或更正请求，并提供对应文件路径与必要说明；请避免在公开 Issue 中披露更多敏感信息。

## 完整性说明

[MANIFEST.csv](MANIFEST.csv) 为每份整理后文件记录 `SizeBytes` 与 `SHA256`。SHA-256 可用于检查下载文件是否与清单记录一致，但不代表内容来源、正确性或权利状态已获得背书。

PowerShell 校验示例：

```powershell
$row = Import-Csv .\MANIFEST.csv | Select-Object -First 1
(Get-FileHash -Algorithm SHA256 -LiteralPath $row.OrganizedRelativePath).Hash -eq $row.SHA256
```
