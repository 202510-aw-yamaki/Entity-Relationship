# JSON 保存形式固定書

## この文書の役割
- 本書は、現行の保存 / 読込 JSON 仕様を固定する文書です。
- 保存形式や読込互換の扱いを変更した場合は、この文書も更新してください。
- AI相談JSONは別形式のため、本書の保存 / 読込 JSON には含めません。

---

## 保存対象
保存用 JSON には、最低限以下を含めます。

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

---

## ルート構造

| 項目 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `version` | number | 必須 | 現行は `1` |
| `projectName` | string | 必須 | プロジェクト名 |
| `currentStep` | string | 必須 | `STEP1` / `STEP2` / `STEP3` |
| `nodes` | array | 必須 | 箱一覧 |
| `edges` | array | 必須 | 線一覧 |

---

## 箱データ構造

```json
{
  "id": "node-1",
  "category": "画面表示",
  "title": "顧客一覧画面",
  "meaning": "顧客情報を一覧で確認する画面",
  "customerNote": "顧客向けには一覧表示の画面として説明する",
  "isGroup": false,
  "parentId": "",
  "items": [
    {
      "id": "item-1",
      "title": "顧客名を一覧で見たい",
      "description": "顧客名と状態を並べて確認する"
    }
  ],
  "x": 120,
  "y": 80,
  "width": 220,
  "height": 140
}
```

| 項目 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | string | 必須 | 箱の一意 ID |
| `category` | string | 必須 | 固定カテゴリ、または未設定時は空文字 |
| `title` | string | 必須 | 箱タイトル |
| `meaning` | string | 必須 | 箱の意味合い説明 |
| `customerNote` | string | 必須 | 顧客向け注釈 |
| `isGroup` | boolean | 必須 | 親箱かどうか |
| `parentId` | string | 必須 | 所属する親箱 ID。親箱自身は空文字 |
| `items` | array | 必須 | 箱内要件一覧 |
| `x` | number | 必須 | X 座標 |
| `y` | number | 必須 | Y 座標 |
| `width` | number | 必須 | 幅 |
| `height` | number | 必須 | 高さ |

### 箱内要件データ構造

```json
{
  "id": "item-1",
  "title": "顧客名を一覧で見たい",
  "description": "顧客名と状態を並べて確認する"
}
```

| 項目 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `id` | string | 必須 | 箱内要件の一意 ID |
| `title` | string | 必須 | 箱内要件名 |
| `description` | string | 必須 | 箱内要件の説明 |

---

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
| `fromType` | string | 必須 | `node` または `item` |
| `fromId` | string | 必須 | 接続元 ID |
| `toType` | string | 必須 | `node` または `item` |
| `toId` | string | 必須 | 接続先 ID |
| `relationType` | string | 必須 | 固定関係種別 |
| `label` | string | 必須 | 線の説明 |
| `arrowStart` | string | 必須 | `none` または `arrow` |
| `arrowEnd` | string | 必須 | `none` または `arrow` |

- `fromType` と `toType` はそれぞれ `node` または `item` を取れます。
- 現行 UI から新規作成できる線は `node -> node` または `item -> item` の同種接続のみです。

---

## 固定値

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

---

## 保存時の仕様
- 保存ファイル名は `<project>.json`
- 保存内容は `version` `projectName` `currentStep` `nodes` `edges` のみ
- 保存用 JSON には STEP 判定結果、表示倍率、Undo 履歴、AI相談用情報を含めない

---

## 読込時の互換と補正
- ルートの箱一覧は `nodes` を優先し、`boxes` も読込対象とする
- ルートの線一覧は `edges` を優先し、`lines` / `connections` も読込対象とする
- 不正な親箱参照は空文字へ補正する
- `isGroup` が `true` の箱は、`parentId` を空文字へ補正する
- 存在しない箱や箱内要件を参照する線は読込時に除外する
- 不正な `relationType` は `表示` に補正する
- 不正な `arrowStart` / `arrowEnd` は `none` に補正する
- 箱や箱内要件の ID が不足している場合は、読込時に補完する

---

## AI相談JSONとの関係
- `AI相談JSON出力` の JSON は保存 / 再開用ではない
- `JSON読込` は AI相談JSON を拒否し、保存用 JSON を選ぶよう案内する
