# pr-size-checker

分かりました。以下のようにREADMEを作成しました。

# PR Size and Lines Checker

このGitHub Actionsは、プルリクエストの変更ファイル数と変更された行数がそれぞれ指定された制限内であるかチェックして、制限を超えた場合はActionは失敗します。
削除されたファイルと削除された行数も、それぞれ変更ファイル数と変更行数に含まれます。

## 使用例

```yaml
name: 'PR Size Check'

on:
  pull_request:
    branches:
      - main

jobs:
  pr-size-checker:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - name: Check PR Size
        uses: ./.github/actions/pr-size-checker
        with:
          max-files: 30
          max-lines: 500
          exclude-filepath: 'package.json|yarn.lock'
```

## オプション

| 名前               | 説明                           | デフォルト値 | 必須 |
| ------------------ | ------------------------------ | ------------ | ---- |
| `max-files`        | PRで許可される最大ファイル数   | 20           | ✅   |
| `max-lines`        | PRで許可される最大変更行数     | 400          | ✅   |
| `exclude-filepath` | 除外するファイルパスのパターン | なし         | ❌   |

## 注意点

- この Actionsは、`git diff`を使って変更を検出しています。そのため、git が追跡しているファイルのみ考慮されることに注意してください。
- `exclude-filepath`には正規表現を使用できます。正規表現の書き方に注意してください。
