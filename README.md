# chronos

[Singularity Dojo](https://singularity-dojo.vercel.app) の Bonus「自分の Chronos を作る」で使うテンプレートです。

毎日の終わりに、AI エージェント（Codex）と一緒にその日を振り返り、記録を GitHub に push します。Chronos は使うほど段階が上がり、できることが増えます。

## 使い方

1. GitHub でこのページの **Use this template** → **Create a new repository** を押し、名前を `chronos`、**Private** にして作る
2. 自分の `chronos` を `~/chronos` に clone する
3. `~/.bashrc` に、振り返りを1語で始めるシェル関数 `reflect` を足す（1回だけ）
4. 毎日の終わりに、どこからでも `reflect` と打つ。`~/chronos` で Codex が起動し、`$chronos-reflect` が送られて振り返りが始まる。終えると元の場所に戻る

```bash
cat >> ~/.bashrc <<'EOF'

# ~/chronos で Codex を起動して、振り返りを始める（終えると元の場所に戻る）
reflect() {
  (cd ~/chronos && codex '$chronos-reflect')
}
EOF
source ~/.bashrc
```

くわしい手順は、道場の Bonus のガイドを見てください。

## ディレクトリ構造

```
~/chronos/
├── README.md                 ← このファイル
├── AGENTS.md                 ← Chronos の話し方と決まり（Codex が起動したときに読む）
├── .agents/
│   └── skills/
│       └── chronos-reflect/  ← $chronos-reflect のスキル（~/chronos で起動したときだけ使える）
│           ├── SKILL.md      ← 振り返りの手順書
│           └── stages.md     ← 段階の中身と、上がるきっかけ
├── logs/                     ← 毎日の振り返り（Chronos が書く）
│   └── 2026-11-02.md
└── context/                  ← Chronos が覚えておくこと（Chronos が書く）
    ├── progress.md           ← 今の段階・上がった記録・数えているもの
    ├── thoughts.md           ← 段階1から
    ├── self-profile.md       ← 段階2から
    └── retrospectives/       ← 月の振り返り
```

`README.md`・`AGENTS.md`・`.agents/` は道場が用意したしくみ、`logs/`・`context/` は Chronos があなたの記録を書く場所です。

## 毎日・毎月

- push のあとに、今月の草（記録した日が ■）が出ます
- 月の最終日には、1か月の振り返りとカレンダーを `context/retrospectives/` に書きます

## 段階

記録がたまると、段階が自動で上がり、Chronos のできることが増えます。

| 段階 | できること | 上がるきっかけ |
|---|---|---|
| 0 | 4つの問いで振り返り、記録して push する。playground のその日の記録を読んで下書きを出す | 始めたとき |
| 1 記憶 | 前の記録を読み、くり返しに気づく | 記録が合計10日分たまった |
| 2 自分を知る | 自分の癖を書き、「数年後のあなた」として話す | 気づきが3回当たった |
| 3 行動へ | 何度も出る「次にやってみたいこと」を Issue にする | 同じ「次にやってみたいこと」が3回出た |

段階4から先は準備中です。
