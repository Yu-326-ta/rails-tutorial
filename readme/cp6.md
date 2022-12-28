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
