# Entity-Relationship

非エンジニアでも、要件・関係性・入出力・保存先 / 参照先を箱と線で整理し、段階的に確認しながら顧客説明用と AI / エンジニア解釈用の情報へ落とし込める、ローカル動作の単一 HTML ツールです。

アプリ本体は [index.html](Entity-Relationship/index.html) 1 ファイルで完結しています。外部ライブラリ、フレームワーク、CDN、バックエンドは使っていません。

## 現在できること
- 箱の追加 / 編集 / 削除 / 移動
- 図エリアをドラッグして箱を作成
- 箱のリサイズ
- 親箱の追加 / 編集 / 削除
- 箱内要件の追加 / 編集 / 削除
- 箱同士の接続
- 箱同士をドラッグで接続
- 箱内要件同士の接続
- Undo / Redo
- Ctrl + ホイール / Ctrl + ↑↓ によるズーム
- STEP1 / STEP2 / STEP3 判定
- STEP説明の常時表示
- 日本語での不足 / 不整合表示
- JSON 保存 / JSON 読込
- 旧 JSON の安全読込
- AI向け出力
- human向け出力
- AI相談JSON出力
- 初期サンプルデータ表示

## 起動方法
1. [index.html](Entity-Relationship/index.html) をブラウザで直接開きます。
2. 左カラムで箱や親箱を追加します。
3. 中央の図エリアで箱を動かし、線接続を作ります。
4. 右カラムで箱 / 線 / 箱内要件の詳細を編集します。
5. STEP1、STEP2、STEP3 を順に実行して不足や不整合を確認します。
6. 必要に応じて JSON 保存、JSON 読込、AI向け / human向け出力を使います。
7. AI に相談したいときは `AI相談JSON出力` を使います。

## 画面サイトマップ

### 左カラム
- 基本設定
  プロジェクト名、現在 STEP
- 操作
  箱追加、親箱追加、線接続開始 / 箱接続に戻る、削除、サンプルへ戻す、Undo / Redo
- 保存と読込
  JSON 保存、JSON 読込、AI向け出力、human向け出力、AI相談JSON出力
- 使い方
  操作の短い手順、STEP説明

### 中央カラム
- 図エリア
  箱、親箱、箱内要件、線の表示、ドラッグ箱作成、箱リサイズ、ドラッグ線接続
- 接続ガイド
  線接続中の案内
- 状態バッジ
  現在 STEP、プロジェクト名、箱数 / 線数、表示倍率

### 右カラム
- 詳細編集
  箱編集、線編集、箱内要件編集
- 現在状態の要約
  件数、カテゴリ内訳、接続モード、表示倍率、STEP 状況
- STEP結果表示
  STEP1 / STEP2 / STEP3 の結果を個別表示

## データの考え方

### 箱
- 通常の箱
  要件、画面、入力、保存、参照、出力、注釈を表します。
- 親箱
  複数の箱をまとめるための大きな枠です。
- 箱内要件
  箱の中に持てる箇条書き要件です。

### 線
- 箱同士の線
  全体の関係を表します。
- 箱内要件同士の線
  要件レベルのつながりを表します。
- 関係種別
  表示、入力、保存、参照、出力、関連

## STEP の役割

### STEP1
- 主要カテゴリ不足
- カテゴリ未設定
- タイトル未入力
- 独立箱
- 線がない状態

### STEP2
- 保存データと保存線の対応
- 参照データと参照線の対応
- 保存元不明
- 参照先不明
- 画面表示の参照不足
- ユーザー入力の行き先不足

### STEP3
- 顧客向け注釈不足
- 線説明不足
- 意味合い説明不足
- 顧客要望の説明不足
- 後で見返したときに分かりにくい要素

## JSON 保存 / 読込
- 保存対象
  `version`、`projectName`、`currentStep`、`nodes`、`edges`
- 読込時の考え方
  現行 JSON を優先しつつ、旧形式の `boxes` / `lines` / `connections` も読める範囲で吸収します。
- 読込時の安全処理
  不正な参照先を持つ線や、存在しない親箱参照は安全側に補正します。

保存用JSONは途中保存 / 再開用です。`AI相談JSON出力` は AI に相談するための別出力であり、`JSON読込` の対象ではありません。

詳細は [docs/JSON_SCHEMA.md](Entity-Relationship/docs/JSON_SCHEMA.md) を参照してください。

## 出力

### AI向け出力
- ID を含む構造化テキスト
- 箱、親箱、箱内要件、線、方向、STEP 状況を出力
- 顧客要望と関連実装要素の対応も出力

### human向け出力
- 顧客説明向けの自然文
- 図全体の目的
- 各箱の意味
- 各線の意味
- 入力 → 表示 → 保存 → 参照 → 出力 の流れ
- 顧客向け注釈

### AI相談JSON出力
- ファイル名は `<projectFileBase()>_AI相談.json`
- `format` `version` `projectName` `currentStep` `consultationPurpose` `stepGuide` を含みます
- `graphSummary` `validation` `activeConcerns` `graph` `aiRequest` を含みます
- STEPの気になる点や、保存 / 参照 / 表示 / 入力の曖昧さを AI に相談しやすい構造です
- 保存用JSONとは分離しており、途中保存 / 再開には使いません

## ファイル構成

### ルート
- [index.html](Entity-Relationship/index.html)
  アプリ本体です。HTML / CSS / JavaScript を 1 ファイルにまとめています。
- [README.md](Entity-Relationship/README.md)
  このプロジェクトの概要、使い方、ファイル説明です。
- [AGENTS.md](Entity-Relationship/AGENTS.md)
  このリポジトリで作業するときの厳守ルールです。

### docs
- [docs/SPEC.md](Entity-Relationship/docs/SPEC.md)
  全体仕様の整理です。
- [docs/VALIDATION_RULES.md](Entity-Relationship/docs/VALIDATION_RULES.md)
  STEP1 / STEP2 / STEP3 の判定観点をまとめた資料です。
- [docs/JSON_SCHEMA.md](Entity-Relationship/docs/JSON_SCHEMA.md)
  保存 / 読込する JSON の考え方と構造です。
- [docs/PHASE_SCOPE.md](Entity-Relationship/docs/PHASE_SCOPE.md)
  段階実装の範囲整理です。
- [docs/MANUAL_TEST.md](Entity-Relationship/docs/MANUAL_TEST.md)
  既存仕様を壊していないか確認するための手動確認手順です。

## 手動確認
手動確認の観点は [docs/MANUAL_TEST.md](Entity-Relationship/docs/MANUAL_TEST.md) にまとめています。変更後は、少なくとも以下を確認してください。

- 初期サンプルが表示される
- 左 / 中央 / 右の3カラムが崩れない
- 箱 / 親箱 / 箱内要件 / 線の基本操作ができる
- ドラッグで箱作成、箱リサイズ、ドラッグ線接続ができる
- Undo / Redo と Ctrl + Z / Ctrl + Y が効く
- Ctrl + ホイール / Ctrl + ↑↓ でズームできる
- STEP説明が見やすく表示される
- AI相談JSON出力ができる
- JSON 保存 / 読込ができる
- STEP1 / STEP2 / STEP3 の結果が読める
- AI向け / human向け出力が実行できる

## 注意点
- PowerShell 上では日本語が文字化けして見えることがありますが、表示上の問題だけでコード本体の文字列と一致しない場合があります。
- このプロジェクトでは、機能を広げるより既存仕様を壊さないことを優先します。
- 追加機能の候補があっても、明示指示がない限り実装対象にはしません。
