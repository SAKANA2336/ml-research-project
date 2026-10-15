# 项目协作说明

## 提交一次修改

先同步 `main`，再创建描述明确的分支，例如：

```powershell
git switch main
git pull --ff-only
git switch -c data/add-batch-002
```

把新文件放入对应目录，检查修改后提交并推送：

```powershell
git status
git add data/raw/2026-10-16_batch002
git commit -m "data: add batch 002"
git push -u origin data/add-batch-002
gh pr create --fill
```

PR 通过自动检查并由 `@SAKANA2336` 批准后，才能合并到 `main`。

## 原始数据规则

- 每批原始数据使用全新的目录，例如 `data/raw/2026-10-16_batch002/`。
- 不覆盖、删除、移动或重命名已经进入 `main` 的原始数据。
- 每批数据应附带 `metadata.json` 或 `README.md`，说明来源、采集日期、提交人、记录数量和字段含义。
- 发现旧数据错误时，新增更正批次，并在说明中写明被替代的批次；不要直接改写旧文件。
- 不得提交密码、令牌、个人敏感信息或未经授权公开的数据。

## 数据较大时

普通 Git 不适合大型数据集。单文件较大时使用 Git LFS；数据集非常大时，将数据存入有版本管理的对象存储，并在本仓库保存清单、版本号和校验值。
