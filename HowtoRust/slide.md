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

- Rustでデバッグできるようになる

- Rustがより好きになる

  





# アジェンダ

1. Rustの特徴
2. Rustで作られたプロジェクト
3. おすすめ Rust製CLI
4. Rustで推したい機能
5. 開発Tips





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



- 強力な型推論
- 代数的にデータを表現する型
- パターンマッチ
- トレイトを使ったポリモーフィズム



# 強力な型推論1



```rust
fn main() {
    let num_1 = 1;
    let num_2 = 1;
    
    let i32_num: i32 = 1;
    let i64_num: i64 = 1;
    
    println!("is  same type? {}", num_1 == i32_num);	//⇒ true
    println!("is  same type? {}", num_2 == i64_num);	//⇒ true
    println!("is  same type? {}", num_1 == num_2);		//⇒ mismatched type error!!
}
```



# 強力な型推論2



```rust
fn main() {
    // アノテーションのおかげで、コンパイラは`elem`がu8型であることがわかる。
    let elem = 5u8;
    // この時点でコンパイラは`vec`の型を知らず、
    // 単に何らかの値のベクトル(`Vec<_>`)であるということだけを把握している
    let mut vec = Vec::new();
    // `elem`をベクトルに挿入
    vec.push(elem);
    
    // 以後コンパイラは`vec`が`u8`のベクトル(`Vec<u8>`)であることを把握する。
    println!("{:?}", vec);
}
```



# 強力な型推論3

引用

> https://doc.rust-jp.rs/rust-by-example-ja/types/inference.html

# 



# 代数的データ型

from Wikipedia

> **代数的データ型**（[英](https://ja.wikipedia.org/wiki/英語): **Algebraic data type**）とは[プログラミング](https://ja.wikipedia.org/wiki/プログラミング_(コンピュータ))、特に[関数型プログラミング](https://ja.wikipedia.org/wiki/関数型言語)や[型システム](https://ja.wikipedia.org/wiki/型システム)において使われる[データ型](https://ja.wikipedia.org/wiki/データ型)である。それぞれの代数的データ型の[値](https://ja.wikipedia.org/wiki/値_(情報工学))には、1個以上の[コンストラクタ](https://ja.wikipedia.org/wiki/コンストラクタ)があり、各コンストラクタには0個以上の[引数](https://ja.wikipedia.org/wiki/引数)がある。

代数的データ型の値（データ）の感覚的な説明としては、引数で与えられた他のデータ型の値を、コンストラクタで包んだようなもの、である。コンストラクタに引数がある代数データ型は複合型（他のデータ型を組み合わせて形成する型）である。



# 代数的データ型

- C++, Javaに実装されているデータ構造とは違って柔軟性が高いデータ構造になっている
- 関数型言語(Haskell)などで実装されている
- Rustの列挙型(enum)は名前とは裏腹に代数的データ型で以下すべてを構成できる。
  - 列挙型
  - 直積型
  - 直和型





# 代数的データ型

`Result<i32, String>`で考えてみる

```Rust
# 入れ物としての理解
Result --- Ok --- 1
              --- 2
              --- 3
       --- Err -- "Error 1"
           -- "Error 2"

# 直和集合としての理解（orの表現）
Result --- 1 (Ok)
       --- 2 (Ok)
       --- 3 (Ok)
       --- "Error 1" (Err)
       --- "Error 2" (Err)
```





# 代数的データ型

引用

> https://ja.wikipedia.org/wiki/%E4%BB%A3%E6%95%B0%E7%9A%84%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B

オススメYoutube

> **https://www.youtube.com/watch?v=r7XNiB6Easw**



# 



# パターンマッチ





# トレイトを使ったポリモーフィズム







# 開発Tips







# 開発Tips



```Rust
main() {
    struct SomeTypes {
        id: i32,
    	strings: String,
    }
}
```





# 開発Tips



```Rust
main() {
    struct SomeTypes {
        id: i32,
    	strings: String,
    }
    
    impl fmt::Display for SomeTypes{
         fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
             write!(f, "id:{}, strings: {}", self.id, self.strings);
        }
    }
    
}
```









