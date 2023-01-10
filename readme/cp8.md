# Chapter8

## 学び
* HTTPはステートレスなプロコトル（HTTPのリクエスト1つ1つは、それより前のリクエストの情報をまったく利用できない、独立したトランザクションとして扱われる）  

* Userリソースではモデルを介してデータベースに値を登録するのに対して、Sessionではデータベースの変わりにcookiesを保存場所として扱う  

```
rails test test/integration/users_login_test.rb
```
上の例のように、rails testの引数にテストファイルを与えると、そのテストファイルだけを実行することができる  

* flashメソッドは再度レンダリングを行ってもメッセージは消えないのに対してflash.nowメソッドはレンダリングが終わっているページで特別にフラッシュメッセージを表示することができるメソッドのためその後リクエストが発生したときに消滅する  

* cookiesにはブラウザを閉じると自動的に有効期限が切れるものと、ブラウザを閉じても保持されるものがある  

* `redirect_to user`は`user_url(user)`と同義  

```
def current_user
  if session[:user_id]
    User.find_by(id: session[:user_id])
  end
end
```
このような関数を定義すると、実行するたびにDBに問い合わせる必要があるので時間がかかる。そこでインスタンス変数に保存する工夫を行う（メモ化）
```
if @current_user.nil?
  @current_user = User.find_by(id: session[:user_id])
else
  @current_user
end
```
これは
```
if session[:user_id]
    @current_user ||= User.find_by(id: session[:user_id])
end
```
これと同義（Rubyでは、||演算子をいくつも連続して式の中で使う場合、項を左から順に評価し、最初にtrueになった時点で処理を終えるように設計されている）  

* `@current_user = @current_user || User.find_by(id: session[:user_id])` と`@current_user ||= User.find_by(id: session[:user_id])`も同義  

