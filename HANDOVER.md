# 引き継ぎ書

## このプロジェクトの一言要約
このプロジェクトは、**非エンジニアでも「顧客要望 → 画面 → 入力 → 保存 → 参照 → 出力」の関係を、箱と線で段階的に整理し、顧客・作成者・AI・エンジニアの全員が読み取れる形へ落とし込むための、ローカル動作の単一HTMLツール**です。現在のアプリ本体は `index.html` 1ファイルで完結し、外部ライブラリやバックエンドを使わない構成です。 :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

---

## まず最初に理解してほしいこと
このツールは、単なる「図を描く道具」ではありません。

本来の目的は、
- 顧客の思いつきや曖昧な要望を
- いきなり実装へ渡さず
- 非エンジニアでも見える形に整理し
- STEPごとに抜け漏れや不整合を確認し
- 最後に顧客向け・AI向け・エンジニア向けの橋渡し資料にすること

です。  
AGENTS.md でも、見た目だけの図ツールではなく、**判定と説明文出力を重視すること**が明示されています。 :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

---

## このプロジェクトで一番大事な思想
このチャットで詰めた考え方として、以下は単なる好みではなく、**プロジェクトの中心思想**です。

### 1. 主役は非エンジニア
利用者はエンジニアではなく、**非IT人材や顧客側担当者**を強く想定しています。  
そのため、UI文言・警告文・説明文は「技術者向けの正しさ」だけでなく、**非エンジニアでも意味が取れるやさしい日本語**であることが必須です。 :contentReference[oaicite:4]{index=4}

### 2. 図を描くこと自体が目的ではない
このツールの本質は、図を描くことではなく、**関係性の認識合わせと合意形成**です。  
特に以下が重要です。

- STEP1: 要件同士の関係を整理する
- STEP2: 保存先⇔参照先を中心に、実装へ落ちる関係にする
- STEP3: 顧客や将来の自分が読んでも意味が分かる粒度まで注釈を整える

この3段階の考え方は README、VALIDATION_RULES、AGENTS にも反映されています。 :contentReference[oaicite:5]{index=5} :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

### 3. 顧客とのすり合わせをしやすくする
このツールは、エンジニア内部だけで使う設計図ではなく、**顧客と「この理解で合っているか」を確認するための道具**です。  
そのため、箱や線には「正しさ」だけでなく、**人に説明しやすい注釈**が必要です。human向け出力もそのために存在します。 :contentReference[oaicite:8]{index=8}

### 4. AIとの往復を前提にしている
このHTMLと、保存したJSON、AI向け出力をAIへ渡し、  
「このつながりでおかしいところはどこか」「不足しているところは何か」を相談する運用を前提にしています。  
つまり、**このHTML自体が完成品というより、AIと人間の橋渡し用インターフェース**です。 :contentReference[oaicite:9]{index=9}

### 5. 段階的であることが重要
一気に正しい設計図を作るのではなく、
- まず大枠
- 次に保存/参照
- 最後に説明可能性

という順に固める考え方が非常に重要です。  
この思想は最初の仕様固定フェーズから一貫しており、PHASE_SCOPE にも「段階実装」「実装範囲を勝手に広げない」として残っています。 :contentReference[oaicite:10]{index=10}

---

## 現在の完成状態
現在の `index.html` は、以下の機能を持つ単一HTMLアプリです。

- 箱の追加 / 編集 / 削除 / 移動
- 親箱の追加 / 編集 / 削除
- 箱内要件の追加 / 編集 / 削除
- 箱同士の接続
- 箱内要件同士の接続
- STEP1 / STEP2 / STEP3 判定
- 日本語での不足 / 不整合表示
- JSON 保存 / JSON 読込
- 旧 JSON の安全読込
- AI向け出力
- human向け出力
- 初期サンプルデータ表示 :contentReference[oaicite:11]{index=11}

また、`index.html` の実装上も、
- 3カラム構成
- 箱、親箱、箱内要件
- item-item接続
- JSON保存/読込
- AI/human出力
- STEP1/2/3 判定
が入っています。 :contentReference[oaicite:12]{index=12}

---

## 現在のファイル構成と役割
現時点で重要なファイルは以下です。

### ルート
- `index.html`  
  アプリ本体。HTML / CSS / JavaScript を1ファイルにまとめた実装。現在の最重要ソース。 :contentReference[oaicite:13]{index=13}
- `README.md`  
  現在できること、起動方法、画面サイトマップ、出力、ファイル構成の要約。**新しく参画した人が最初に読むべき概要資料**。 :contentReference[oaicite:14]{index=14}
- `AGENTS.md`  
  このプロジェクトで作業するときの厳守ルール。**開発時の最上位運用ルール**。特に文字化け判断、一括置換、一時ファイルの扱いは必読。 :contentReference[oaicite:15]{index=15} :contentReference[oaicite:16]{index=16} :contentReference[oaicite:17]{index=17}

### docs
- `docs/SPEC.md`  
  仕様固定時点の全体像。思想の土台として重要。 :contentReference[oaicite:18]{index=18}
- `docs/VALIDATION_RULES.md`  
  STEP1 / STEP2 / STEP3 の判定思想。特に STEP2 の保存先⇔参照先の重視を理解するために重要。 :contentReference[oaicite:19]{index=19}
- `docs/JSON_SCHEMA.md`  
  JSON保存形式の考え方。互換性や保持項目の理解に必要。 :contentReference[oaicite:20]{index=20}
- `docs/PHASE_SCOPE.md`  
  仕様固定フェーズ時の範囲整理。**履歴として重要**。ただし、現在はその後続フェーズ機能まで実装が進んでいるので、現状把握の一次資料ではありません。 :contentReference[oaicite:21]{index=21}
- `docs/MANUAL_TEST.md`  
  手動確認手順。変更後の確認観点として実用的。 :contentReference[oaicite:22]{index=22}

---

## 現在の仕様理解で優先順位が高いもの
新しく触る人は、次の順で理解してください。

1. `AGENTS.md`
2. `README.md`
3. `index.html`
4. `docs/MANUAL_TEST.md`
5. `docs/VALIDATION_RULES.md`
6. `docs/JSON_SCHEMA.md`
7. `docs/SPEC.md`
8. `docs/PHASE_SCOPE.md`

理由は、`SPEC.md` と `PHASE_SCOPE.md` は**初期の固定資料**であり、そこでは `items` や `parentId` が「後続フェーズ候補」として書かれていますが、現在の実装ではすでに箱内要件・箱内要件接続・親箱が入っているためです。  
つまり、**履歴資料としては正しいが、現状の機能一覧としては README と index.html の方が新しい**、という扱いです。 :contentReference[oaicite:23]{index=23} :contentReference[oaicite:24]{index=24} :contentReference[oaicite:25]{index=25}

---

## STEPの本来の意味
このプロジェクトでは STEP は単なる画面段階ではありません。

### STEP1
要件の大枠が図として成立しているかを見る段階です。  
主な観点は、主要カテゴリ不足、カテゴリ未設定、タイトル未入力、独立箱、線なしです。 :contentReference[oaicite:26]{index=26}

### STEP2
最重要段階です。  
**保存先⇔参照先の関係が曖昧でないか**を中心に確認します。  
保存データ、参照データ、画面表示、入力の関係が最低限つながっているかを見ます。 :contentReference[oaicite:27]{index=27} :contentReference[oaicite:28]{index=28}

### STEP3
顧客にも将来の作成者にも意味が通る粒度まで説明できているかを見る段階です。  
顧客向け注釈、線ラベル、意味合い説明、顧客要望の説明不足を見ます。 :contentReference[oaicite:29]{index=29}

---

## このプロジェクトで「正しい修正」と「誤った修正」
### 正しい修正
- 今ある思想を壊さず、分かりやすさや安定性を上げる
- 既存の JSON 互換性を壊さない
- AGENTS.md のルールに従い、承諾前の大きな置換を避ける
- 既存機能を壊さないことを優先する
- docs は履歴を消さずに追記ベースで扱う :contentReference[oaicite:30]{index=30} :contentReference[oaicite:31]{index=31}

### 誤った修正
- 勝手に機能を増やす
- 非エンジニア向け文言を技術者向けへ寄せる
- 保存/読込の互換性を壊す
- PowerShell表示だけで「文字化けしている」と断定して全置換する
- `tmp-*` や `*-check.*` のような一時ファイルを勝手に残す :contentReference[oaicite:32]{index=32} :contentReference[oaicite:33]{index=33} :contentReference[oaicite:34]{index=34}

---

## 文字化けと置換に関する重要事項
このプロジェクトでは、過去に **PowerShell上の見え方** と **実ファイル本体** の差が問題になりました。  
そのため AGENTS.md では、以下が厳守事項です。

- PowerShell の出力だけを根拠に文字化けと断定しない
- 修正前に現物確認をする
- ユーザー承諾なしに全体置換をしない
- UTF-8、BOMなしを維持する
- 一時ファイルを勝手に残さない :contentReference[oaicite:35]{index=35} :contentReference[oaicite:36]{index=36}

このルールは、単なる注意ではなく、**運用上の事故防止策**です。

---

## このツールの使い方の本筋
README と MANUAL_TEST にある通り、基本運用は以下です。

1. `index.html` をブラウザで直接開く
2. 箱 / 親箱を追加する
3. 箱を編集し、必要なら箱内要件を追加する
4. 線接続で関係を作る
5. STEP1 → STEP2 → STEP3 の順で確認する
6. JSON保存で途中状態を残す
7. AI向け / human向け出力を使う :contentReference[oaicite:37]{index=37} :contentReference[oaicite:38]{index=38}

---

## このチャットで固まった「ユーザーの考え」
このプロジェクトを今後扱う人は、以下を前提にしてください。

- ユーザー自身は **非エンジニア側** の視点を非常に重視している
- クライアントも **非IT分野の人間** を想定している
- 価値の中心は「誰にでもわかりやすく図を描写できる機能」
- 特に重要なのは、**保存先⇔参照先の関係が見えること**
- 顧客との合意形成に使いやすいことが重要
- 最終的には AI やエンジニアに渡せる形へ落ちることが重要
- つまり、このツールは「設計支援ツール」であり、「合意形成ツール」であり、「AI入力支援ツール」でもある

この思想が崩れると、たとえ機能が増えても、このプロジェクトの本質から外れます。

---

## 今後の扱い方
今後は、大きく新機能を広げる段階ではなく、**既存の完成度を上げる段階**と考えるのが妥当です。  
README でも、「機能を広げるより既存仕様を壊さないことを優先」と整理されています。 :contentReference[oaicite:39]{index=39}

優先順位は次の通りです。

1. 既存機能を壊さない
2. 非エンジニアにとって分かりやすくする
3. JSON保存/読込の安定性を保つ
4. STEP判定の分かりやすさを上げる
5. AI向け / human向け出力の読みやすさを上げる
6. docs の追記整備

---

## 変更前の最低確認
何か変更する前に、最低でも以下は確認してください。

- README を読む
- AGENTS.md を読む
- `docs/MANUAL_TEST.md` の確認観点を読む
- `index.html` をブラウザで開いて現状を確認する :contentReference[oaicite:40]{index=40} :contentReference[oaicite:41]{index=41} :contentReference[oaicite:42]{index=42}

---

## 変更後の最低確認
変更後は、少なくとも以下を実施してください。

- 初期サンプルが表示される
- 左 / 中央 / 右の3カラムが崩れない
- 箱 / 親箱 / 箱内要件 / 線の基本操作ができる
- JSON 保存 / 読込ができる
- STEP1 / STEP2 / STEP3 の結果が読める
- AI向け / human向け出力が実行できる :contentReference[oaicite:43]{index=43} :contentReference[oaicite:44]{index=44}

---

## 最後に
このプロジェクトの価値は、複雑な実装技術そのものではなく、  
**曖昧な要望を、非エンジニアでも扱える形で整理し、顧客・作成者・AI・エンジニアの間で意味の通る資料へ変換できること**にあります。  
この軸を外さない限り、細かな改善は歓迎されます。逆に、この軸を外す変更は、機能追加であっても歓迎されません。

この引き継ぎ書を読む人は、まず「何を増やすか」ではなく、  
**このプロジェクトは何を守るために作られているか** を理解してください。