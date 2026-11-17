# articles

Zenn と Qiita に投稿する記事を管理するリポジトリ。

```
articles/   Zenn の記事（zenn-cli）
books/      Zenn の本
public/     Qiita の記事（qiita-cli）
.github/workflows/publish.yml  main への push で Qiita に同期
```

同じ内容を両方に出す場合も、frontmatter の形式が違うので `articles/` と `public/` に別ファイルで置く。

## セットアップ

```sh
pnpm install
pnpm exec qiita login   # Qiita のアクセストークン（read_qiita, write_qiita）を入力
```

## Zenn

```sh
pnpm zenn:new        # articles/<slug>.md を作成
pnpm zenn:preview    # http://localhost:8000
```

`published: true` にして main に push すると公開される
（初回のみ zenn.dev のダッシュボード「GitHub からのデプロイ」でこのリポジトリを連携）。

## Qiita

```sh
pnpm qiita:new <basename>   # public/<basename>.md を作成
pnpm qiita:preview          # http://localhost:8888
```

main に push すると GitHub Actions が Qiita に同期する
（初回のみリポジトリの Actions secrets に `QIITA_TOKEN` を登録）。
限定共有にしたい記事は `private: true`、投稿させたくない下書きは `ignorePublish: true`。
