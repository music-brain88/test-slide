---
marp: true
page_number: true
theme: gaia
paginate: true
class: lead
header: セキュリティのお話
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

以下の問に回答できる

- OAuth2.0のスコープとは？

- Authorization Code は何の証か

- OAuth2.0使用したWebApplicationの場合どのフロー採用するのが最適か？

  

# アジェンダ

1. OAuthとは？

2. OAuthの登場人物について

3. OAuthのトークンの種類

4. エンドポイントの種類

5. 認証認可のフロー

   

# OAuthとは？

- 以下はRFC 5849に記載されているOAuth2.0に基づいた記載です。
  - HTTPサービスへの限定的なアクセスを可能にする認可フレームワーク
  - リソースオーナーとHTTPサービスの間で同意のためのインタラクション

# OAuthのロール



# OAuthのロール

OAuthのロール（役割）は以下に分けられます

1. リソースオーナ
2. クライアント
3. リソースサーバ
4. 認可サーバ



# リソースオーナ (resource owner)

- 保護されたリソースへのアクセスを許可するエンティティ. 

- リソースオーナーが人間の場合, エンドユーザーと呼ばれる



e.g.

- Google photoとか

- Twitterのアカウントの連携とか





# リソースサーバ (resource server)

- アクセストークンを用いた保護されたリソースへのリクエストを受理してレスポンスを返すことのできるサーバ

e.g.

- Google photoとか

- Twitterのアカウントの連携とか

# クライアント (client)

- RO(リソースオーナ)の認可を得て,**ROの代理として**保護されたリソースに対するリクエストを行うアプリケーション
- OAuthクライアントは該当アプリケーションの実装上の特徴には関係がないです

e.g.

- サーバアプリケーション
- デスクトップアプリケーション
- その他のデバイスアプリケーション

# 認可サーバ (authorization server)

- ROの認証とROからの認可取得が成功した後, アクセストークンをクライアントに発行するサーバ

e.g.

- Google Account Login



# 各ロールの関係性

<div class="mermaid">
sequenceDiagram
participant Client_App
participant 認可サーバ
participant User
participant リソースサーバ
Client_App->認可サーバ:アクセストークンください
認可サーバ->User:ClientAppが許可しろと言っているけどいいの？
User->認可サーバ:ええで
認可サーバ->Client_App:アクセストークン発行してこの時だけ許可しとくわ
Client_App->リソースサーバ:アクセストークン貰ってきたからアクセスさせてや
リソースサーバ->Client_App:しょうがないなぁ、のび太君は
</div>

<!-- mermaid.js -->

<script src="https://unpkg.com/mermaid@8.1.0/dist/mermaid.min.js"></script>
<script>mermaid.initialize({startOnLoad:true});</script>

# 各ロールの関係性

```mermaid
sequenceDiagram
participant Client_App
participant 認可サーバ
participant User
participant リソースサーバ
Client_App->>認可サーバ:アクセストークンください
認可サーバ->>User:ClientAppが許可しろと言っているけどいいの？
User->>認可サーバ:ええで
認可サーバ->>Client_App:アクセストークン発行してこの時だけ許可しとくわ
Client_App->>リソースサーバ:アクセストークン貰ってきたからアクセスさせてや
リソースサーバ->>Client_App:しょうがないなぁ、のび太君は
```







# OAuthのトークンの種類

- アクセストークン
  - スコープ
  -  有効期限
-  リフレッシュトークン
-  認可コード



# アクセストークン

アクセストークンには次の情報が紐付いています。

- 誰のどのリソースにどのような操作を行うことが許可されているか(scope)
- 有効期限はいつまでか(expires_in)



# リフレッシュトークン

- クライアントから認可サーバーに対してアクセストークンの
  再発行を要求する際に利用

- ご利用の API によってはリフレッシュトークンが発行

  

# 認可コード

- リソースオーナーがクライアントへの権限委譲に同意した証
- クライアントから認可サーバーに対してアクセストークンを要求する時に使用



# エンドポイント種類

- 認可エンドポイント
- トークンエンドポイント
- リダイレクトエンドポイント(URI)



# 認可エンドポイント

- 認可エンドポイントは、認可サーバーによって提供されるエンドポイントで、認可コー ドの発行が主な役割になります。
- 認可エンドポイントにアクセスします。認可エンドポイントではユー ザー名とパスワードの入力などによってリソースオーナーの認証が行われます。
- 同意の証として 認可コードがリダイレクトエンドポイントに送られます。



　# トークンエンドポイント

- トークンエンドポイントは、認可サーバーによって提供されるエンドポイント。
- トークンエンドポイントにリクエストを投げることで、アクセストークンを取得できます。　
- トークンエンドポイントでは Basic 認証によって、クライアントのアイデンティティが 確認されます。
- Basic 認証として Auhotization ヘッダーに設定されるのは、クライアン ト ID とクライアントシークレットです。
- ここでクライアント ID はクライアントの識別子、クライアントシークレットはパスワードに相当するものです。このクライアント ID とクライアントシークレットは認可サーバーにクライアントを事前登録する際に発行さ れます。



#  リダイレクトエンドポイント (リダイレクト URI)

- リダイレクト URI は認可サーバーから認可コードを受け取るために使われます。
- 認可サーバーは、リソースオーナーの権限委譲の同意がおこなわれると、ステータス コード 302 のレスポンスを返してリダイレクト URI にブラウザーをリダイレクトします。 その際、クエリパラメーターとして認可コードの値が渡されます。リダイレクト URI を 「https://client.example.com/callback」とすると、認可サーバーからのレスポンスは次 のような形になります。

```shell
HTTP/1.1 302 Found
Location: https://client.example.com/callback?code=SplxlOBeZQQYbYS6WxSbIA
```







# 認証認可フロー1

- 認可コード
- インプリシット
- リソースオーナパスワードクレデンシャル
- クライアントクレデンシャル



# 認証認可フロー補足

- OAuth を認証に拡張した、OpenID Connect では同じものを「フロー (flow)」とよびます。
- 二年前はPKCEは推奨であったが今は前述の通りほぼ必須(Must)となった。



# 認可コードタイプ

```mermaid
sequenceDiagram
participant Client_App
participant 認可サーバ
participant User
participant リソースサーバ
User->>Client_App:1 Authスタート
Client_App-->>+User:2 リダイレクト
User->>-認可サーバ:3 認可リクエスト
Note over 認可サーバ:認可エンドポイント
認可サーバ-->>User:4 認証画面
User->>認可サーバ:5 認証情報の入力
認可サーバ-->>User:6権限移譲の確認画面
User->>+認可サーバ:7 委譲への同意
認可サーバ-->>-User:8 認可コード
User->>+Client_App:9 リダイレクトURIへリダイレクト
Note over Client_App:リダイレクトURI
Client_App->>-認可サーバ:10 トークンリクエスト
Note over 認可サーバ:トークンエンドポイント
認可サーバ-->>Client_App:11 トークンレスポンス(アクセスポイント)
Client_App->>リソースサーバ:12 リソースへのアクセス
リソースサーバ->>Client_App:13 リソースの提供提供
```

