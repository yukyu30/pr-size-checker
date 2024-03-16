# pr-size-checker

このGitHub Actionsは、プルリクエストの変更ファイル数と変更された行数がそれぞれ指定された制限内であるかチェックして、制限を超えた場合はActionは失敗します。
削除されたファイルと削除された行数も、それぞれ変更ファイル数と変更行数に含まれます。

## 使用例

```yaml
name: PR Size and Lines Checker

jobs:
  blog_review:
    runs-on: ubuntu-latest
    steps:
      - name: PR Size and Lines Checker
        uses: yukyu30/pr-size-checker
          max-files: '100'
          max-lines: '300'
          exclude-filepath: |
            package.json
            yarn.lock

      - name: Continue if PR size and lines are within limits
        if: ${{ success() }}
        run: echo "PR size and lines are within limits"

```

## オプション

| 名前               | 説明                           | デフォルト値 | 必須 |
| ------------------ | ------------------------------ | ------------ | ---- |
| `max-files`        | PRで許可される最大ファイル数   | 20           | ✅   |
| `max-lines`        | PRで許可される最大変更行数     | 400          | ✅   |
| `exclude-filepath` | 除外するファイルパスのパターン | なし         | ❌   |
