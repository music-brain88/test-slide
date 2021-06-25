---
marp: true
page_number: true
theme: gaia
paginate: true
class: lead
header: Rustのお話
footer: エンジニアMTG

---

<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif&display=swap');
section {
    font-family: 'Noto Serif', serif;

}

</style>

<!-- headingDivider: 1 -->

<!-- #　見出しの前にスライドページを自動的に分割 -->

# エンジニアMTGのゴール



- RustのCLIを知ることでterminalでの生産性を上げる

- Rustデバッグでできるようになる

- Rustがより好きになる

  





# アジェンダ

1. Rustの特徴
2. Rustで作られたプロジェクト
3. おすすめ Rust製CLI
4. Rustで推したい機能
5. 開発TIps
6. 問題





# Rustの特徴







# Rustの特徴



- 安全なシステムプログラミング言語
- マシンコードへコンパイル
- ゼロコスト抽象化
- GCを行わない軽量なランタイム





# Rustで作られたプロジェクト









# Rustで作られたプロジェクト





| OS/Software                                                  | Web                                                       | Tool                                               |
| ------------------------------------------------------------ | --------------------------------------------------------- | -------------------------------------------------- |
| [Windows](https://github.com/microsoft/windows-rs)           | [npm レジストリ](https://www.npmjs.com)                   | [Gremlin](https://www.gremlin.com)[^1]             |
| [Discord](https://discord.com)                               | [FireFox](https://research.mozilla.org/rust/)             | [Linkerd](https://linkerd.io)[^2]                  |
| [fuchsia(Android OS)](https://fuchsia.dev/fuchsia-src/development/languages/rust) | [Sentry](https://sentry.io/welcome/)                      | [Canonicalモニタリング](https://canonical.com)     |
| [Dropbox](https://www.dropbox.com)                           | [Cloudflare](https://github.com/cloudflare/cloudflare-rs) | [Atlassianの解析ツール](https://www.atlassian.com) |

1:カオスエンジニアリングツール

2:サービスメッシュ AWSのサービスメッシュより良さげ





# おすすめ Rust製CLI







# おすすめ Rust製CLI



| 検索系                                           | ハイライト                            | システム                                     | 開発補助                                                     |
| ------------------------------------------------ | ------------------------------------- | -------------------------------------------- | ------------------------------------------------------------ |
| [ripgrep](https://github.com/BurntSushi/ripgrep) | [bat](https://github.com/sharkdp/bat) | [procs](https://github.com/dalance/procs)    | [cargo-update](https://github.com/nabijaczleweli/cargo-update) |
| [fd-find](https://github.com/sharkdp/fd)         | [exa](https://github.com/ogham/exa)   | [dust](https://github.com/bootandy/dust)     | [cargo-edit](https://github.com/killercup/cargo-edit)        |
| [tealdeer](https://github.com/dbrgn/tealdeer)    |                                       | [tokei](https://github.com/XAMPPRocky/tokei) | [z](https://github.com/rupa/z)                               |
|                                                  |                                       |                                              | [delta](https://github.com/dandavison/delta)                 |









# Rustで推したい機能







# Rustで推したい機能









# 開発TIps









# 開発TIps







# 問題







# 問題









