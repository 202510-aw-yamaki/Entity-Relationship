# JSON 保存形式固定書

## 目的
本書は、ブラウザだけで保存と読込が完結するための JSON 形式を固定する。

## 保存対象
最低限、以下を保存対象に含める。

- `version`
- `projectName`
- `currentStep`
- `nodes`
- `edges`

## 基本形

```json
{
  "version": 1,
  "projectName": "sample",
  "currentStep": "STEP1",
  "nodes": [],
  "edges": []
}
```

## ルート構造

| 項目 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `version` | number | 必須 | 将来拡張に備えたバージョン |
| `projectName` | string | 必須 | プロジェクト名 |
| `currentStep` | string | 必須 | `STEP1` / `STEP2` / `STEP3` |
| `nodes` | array | 必須 | 箱一覧 |
| `edges` | array | 必須 | 線一覧 |

## 箱データ構造

```json
{
  "id": "node-1",
  "category": "画面表示",
  "title": "顧客一覧画面",
  "meaning": "顧客情報を一覧で確認する画面",
  "customerNote": "顧客向けには一覧表示の画面として説明する",
  "x": 120,
  "y": 80,
  "width": 220,
  "height": 120
}
```

| 項目 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | string | 必須 | 箱の一意 ID |
| `category` | string | 必須 | 固定カテゴリから選ぶ |
| `title` | string | 必須 | 箱タイトル |
| `meaning` | string | 必須 | 箱の意味合い説明 |
| `customerNote` | string | 必須 | 顧客向け注釈 |
| `x` | number | 必須 | X 座標 |
| `y` | number | 必須 | Y 座標 |
| `width` | number | 必須 | 幅 |
| `height` | number | 必須 | 高さ |

## 線データ構造

```json
{
  "id": "edge-1",
  "fromType": "node",
  "fromId": "node-1",
  "toType": "node",
  "toId": "node-2",
  "relationType": "参照",
  "label": "一覧表示のために顧客データを参照する",
  "arrowStart": "none",
  "arrowEnd": "arrow"
}
```

| 項目 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | string | 必須 | 線の一意 ID |
| `fromType` | string | 必須 | 接続元種別 |
| `fromId` | string | 必須 | 接続元 ID |
| `toType` | string | 必須 | 接続先種別 |
| `toId` | string | 必須 | 接続先 ID |
| `relationType` | string | 必須 | 固定関係種別から選ぶ |
| `label` | string | 必須 | 線の説明 |
| `arrowStart` | string | 必須 | 始点側の向き |
| `arrowEnd` | string | 必須 | 終点側の向き |

## 固定値の扱い

### `currentStep`
- `STEP1`
- `STEP2`
- `STEP3`

### `category`
- `顧客要望`
- `画面表示`
- `ユーザー入力`
- `保存データ`
- `参照データ`
- `出力結果`
- `注釈`

### `relationType`
- `表示`
- `入力`
- `保存`
- `参照`
- `出力`
- `関連`

## 互換性方針
- 後続フェーズで項目を増やす場合も、既存 JSON の互換性をできるだけ壊さない
- 将来の追加候補は `parentId` と `items` に限定する
- `fromType` / `toType` は将来の箱内要件接続も扱えるように保持する
- 既存データの再読込、再判定が壊れないことを前提にする

## AI 向け出力との関係
JSON は途中保存・再開用の内部保存形式とする。AI 向け出力は別ファイルとし、JSON をそのまま出力ファイル扱いしない。

## human 向け出力との関係
human 向け出力は自然文で再構成する。JSON の生データをそのまま見せる前提にはしない。

## 今回まだ実装しないもの
- 実際のダウンロード処理
- 実際の読込処理
- スキーマ自動検証処理
- 後続フェーズ項目の保存
