# language-tutorial

すべてのプログラミング言語のチュートリアルを目指すリポジトリ。
本文は **AsciiDoc** で書き、**Antora** でドキュメントサイトを生成します。
同じ AsciiDoc ソースから **EPUB** の本も作れます。

## 構成

```
.
├── antora-playbook.yml        # Antora のサイト設定
├── package.json               # Antora (Node.js)
├── Gemfile                    # EPUB 用: asciidoctor-epub3 (Ruby)
├── docs/
│   ├── antora.yml             # Antora コンポーネント定義
│   ├── book.adoc              # EPUB 用の本マスター文書（全ページを include）
│   └── modules/ROOT/
│       ├── nav.adoc           # サイト左ナビ
│       ├── pages/             # 言語ごとに1ページ (index / template / python / ...)
│       └── examples/          # 実行できるコード例 (python, javascript)
└── .github/workflows/docs.yml # サイトを GitHub Pages へ、EPUB を artifact へ
```

深さは3段階で育てています。全言語を1ページ紹介（Tier C）、
31言語を Hello World まで（Tier B）、完成チュートリアルは Python と JavaScript（Tier A）から。
章立ては全言語共通で、仕上げ課題（FizzBuzz など）もそろえています。

## サイトをビルドする

Node.js 20 以上が必要です。

```sh
npm install
npm run docs        # build/site/ に HTML が生成される
```

マージされると GitHub Actions が自動で GitHub Pages に公開します
（初回のみ、リポジトリの Settings → Pages で公開元を "GitHub Actions" にしてください）。

## EPUB をビルドする

Antora は HTML サイト専用なので、EPUB は同じソースから別経路で作ります。
`docs/book.adoc` が全言語ページを include する本マスター文書になっていて、
それを Asciidoctor EPUB3 で変換します（Ruby が必要です）。

```sh
bundle install
bundle exec asciidoctor-epub3 -D build/epub docs/book.adoc
# build/epub/book.epub が生成される
```

GitHub Actions では EPUB も自動生成され、artifact としてダウンロードできます。

## ライセンス

MIT
