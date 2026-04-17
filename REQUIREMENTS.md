# ユーザー要望メモ

## この文書の役割
- この文書には、ユーザー要望の原文と要望メモを追記します。
- ここに書かれた要望は、まず実装可否と `docs/SPEC.md` との整合性をユーザーに確認してから扱います。
- ユーザー承認後、固定仕様として扱う内容は `docs/SPEC.md` に反映し、まだ未実装なら `docs/UNMET_REQUIREMENTS.md` に記述します。
- `docs/UNMET_REQUIREMENTS.md` に記述した際は、この文書の該当要望の下に日付と該当項目を追記します。
- この文書から要望本文を除去するのは、ユーザー確認後にユーザーが行います。

---

## 要望一覧

**userLevelフィールドの追加（できれば最初の画面で選べる）**

【ユーザー設定】
・理解度レベル：非エンジニア寄り
・AIツール経験：あり
・エンジニア経験：なし

この情報をもとに、
『専門用語は使わず、平易な言葉で回答してください。』
みたいな一文がAIで土台やAI相談JSONの冒頭に自動で入り、受け側のAIがユーザーのIT理解度を把握できるイメージですね。

レベル設定のUIも、難しく考えずシンプルに：
あなたのITの経験を教えてください
　○ はじめて（聞いたことはある程度）
　○ 少し知っている（AIと対話したことがある）
　○ ある程度わかる（コードを少し触ったことがある）
　○ エンジニア寄り
くらいの4択

2026-04-17 追記:
この要望のうち `userLevel` フィールド追加は、開始画面での4段階選択、保存JSONへの保持、AI向け出力 / AI相談JSONへの反映を固定仕様として扱う前提で承認済みです。
未達管理先は `docs/UNMET_REQUIREMENTS.md` の「userLevel を追加し、開始画面選択・保存JSON保持・AI向け出力反映を行う」項目です。

2026-04-17 追記:
今回の整理では、開始画面で `userLevel` を必ず選ぶ前提とし、通常操作では未選択を作らない方針で承認済みです。
旧JSONや想定外データで `userLevel` が無い場合のみ、フォールバック値は `はじめて` を採用します。
開始後は `canvas-toolbar` の `toolbar-side` 内で `connect-guide` の下に現在の `userLevel` を置き、見かけ上のバランスを取りつつ必要なら変更できる構成を想定します。
未達管理先は次の項目です。
- `docs/UNMET_REQUIREMENTS.md` の「開始画面に `userLevel` の4段階必須選択UIを追加する」
- `docs/UNMET_REQUIREMENTS.md` の「`userLevel` を保存JSONに保持し、再読込時に復元し、未設定データ読込時は `はじめて` を採用する」
- `docs/UNMET_REQUIREMENTS.md` の「`canvas-toolbar` の `toolbar-side` 内で `connect-guide` の下に現在の `userLevel` を表示し、開始後も変更できるようにする」
- `docs/UNMET_REQUIREMENTS.md` の「AI向け出力に `userLevel` と説明粒度の案内文を反映する」
- `docs/UNMET_REQUIREMENTS.md` の「AI相談JSONに `userLevel` と説明粒度の案内文を反映する」

2026-04-17 追記:
上記 `userLevel` 要望のうち、開始画面選択 / 保存JSON保持 / `canvas-toolbar` 表示 / AI向け出力 / AI相談JSON 反映は実装済みです。
達成管理先は次の項目です。
- `docs/COMPLETED_REQUIREMENTS.md` の「開始画面に `userLevel` の4段階選択UIを表示できる」
- `docs/COMPLETED_REQUIREMENTS.md` の「開始画面で `userLevel` を選んでから `空の状態から始める` `サンプルから始める` `AIとの対話を箱と線で見える化しながら土台を作る` を使える」
- `docs/COMPLETED_REQUIREMENTS.md` の「`canvas-toolbar` の `toolbar-side` 内で `connect-guide` の下に現在の `userLevel` を表示し、開始後も変更できる」
- `docs/COMPLETED_REQUIREMENTS.md` の「`userLevel` を保存用 JSON に保持し、再読込時に復元できる」
- `docs/COMPLETED_REQUIREMENTS.md` の「AI向け Markdown と AI相談JSON に `userLevel` と説明粒度の案内を含められる」

**細かい要望**
- 現在はhtmlを開くと左のサイドパネルが閉じているが開いていて欲しい。
- AIに出力するものに対して、ユーザーがどのAIに張ればいいか迷わないように「あなたの使用しているAI」というのを把握できる構造にしてほしい
- 箱から出る矢印が箱をしっかりととらえてほしい
- サンプルで生成される箱のサイズを中身がすべて表示される高さを維持してほしい
- 親箱と子箱の違いをもう少し分かりやすくしてほしい
- 理想は初期のユーザー設定でのレベルに応じて、カテゴリの意味を理解できる粒度になるとなおよし

