# Chapter6

## 学び
* コマンドで作成する、コントローラ名には複数形を使い、モデル名には単数形を用いるという慣習がある。  
`$ rails generate controller Users new` コントローラ  
`$ rails generate model User name:string email:string` モデル（モデル名は単数形（User）だが、テーブル名は複数形（users）になる）  

* Railsコンソールをサンドボックスモードで起動（データベースへの変更が反映されない）  
```
rails console --sandbox
Loading development environment in sandbox (Rails 7.0.4)
Any modifications you make will be rolled back on exit
```

* オブジェクトの作成  [チュートリアルオブジェクト作成](https://railstutorial.jp/chapters/modeling_users?version=7.0#sec-creating_user_objects)
`User.new`でオブジェクト作成  
`.save`でデータを格納  
`.create`で作成と格納を同時に行う  
`.destroy`でオブジェクトの削除を行う（メモリには残る）  

* `%w[foo bar baz]`で配列を簡単に作ることができる。（["foo", "bar", "baz"]の配列ができる）  

* `uniqueness: { case_sensitive: false }`とするとRailsは:uniquenessをtrueと判断する  

* `rails generate model モデル名（単数）`新しいモデルを作成→マイグレーションファイルも自動で生成される（マイグレーションは、データベースの構造を段階的に変更する手段を提供）  
  既に存在するモデルに構造を追加する場合は、`rails generate migration add_index_to_users_email`のようにmigrationジェネレーターを使ってマイグレーションを直接作成する必要がある  

* 大文字小文字を区別しないためにデータベースに保存する前に大文字を小文字に変換したい→Active Recordオブジェクトが存在する間の特定の時点で呼び出されるコールバックメソッドを使う
```
class User < ApplicationRecord
    before_save { self.email = email.downcase }
    ...
end
```
before_saveメソッドはデータベースに保存する前に呼び出される  
