ご質問のに内容について、以下2点と解釈いたしました。  

1．rails g model(controller ,etc...) モデル名(コントローラ名 ,etc...)実行時の単数形、複数形の使い分けについて  
2．ルーティングの単数形、複数形の使い分けについて  


まず1.についてですが、ご認識の通りモデル名は単数形の名称を、コントローラ名は複数形の名称を指定しており、それに従ってファイル名やクラス名も単数形、複数形で自動生成されています。  
これらはrailsの仕様と考えられます。例えばrailsのルーティング仕様では、HTTPリクエストがクライアントから飛んできた際、URIパターンに含まれるコントローラ名が単数形(/blog)、複数形(/blogs)に関わらず複数形のコントローラ名(blogs_controller.rbのBlogsControllerクラス)のアクションに処理を渡すようになっています。従ってコントローラ名は複数形にしなくてはなりません。  
ではなぜ、モデル名は単数形なのかですが、これはORマッピング(ORM)する際の命名規則が関係しています。ORマッピングとはリレーショナルデータベース(RDBMS)をRubyなどのオブジェクト指向プログラミング(OOP)言語で操作できるようにする技術です。ORMでは、テーブル名とクラス名が1：1で対応付けされますがこのとき、テーブル名は複数形(blogs)、クラス名は単数形(blog)にするという制約があります。従ってrailsでモデル名を指定する際は単数形にしなくてはいけません。  
※テーブル名は自動で複数形にしてくれます  

続いて、2．についてざっくりな説明ですが、これは対象とするデータが1件のみしか必要ない場合単数形、複数件取得する可能性がある場合複数形のプレフィックスで表しています。特にｉｄ指定する操作の場合は1件に絞られるため単数形のプレフィックスになっています。上記は感覚的な説明なので、例外が存在する可能性があります(confirm_blogsは1件のみ取得だが複数形)。厳密には単数形リソースが適用されるか、複数形リソースが適用されるかなどの違いが関わってきます。以下に参考URLを記載していますので、ご自身で調べてみてください！

＜参考URL＞  
・「Active Recordの基礎/Railsガイド」  
https://railsguides.jp/active_record_basics.html  

・「Railsルーティング/Railsガイド」  
https://railsguides.jp/routing.html  


