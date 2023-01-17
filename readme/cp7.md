# Chapter7

## 学び
* `<%= debug(params) if Rails.env.development? %>`で開発環境のみデバック情報を表示  

* テスト環境のデバッグなど、他の環境でconsoleを実行する必要が生じた場合は、環境をオプションとしてconsoleスクリプトに渡すことができる  
```
$ rails console --environment test
  Loading test environment
  >> Rails.env
  => "test"
  >> Rails.env.test?
  => true
```
* debuggerメソッドを使うことでより詳しい情報を得られる  
```
def show
    @user = User.find(params[:id])
    debugger
end
```
ブラウザから/users/idにアクセスするとターミナルで情報を見れる  

`<%= form_with(model: @user) do |f| %>`のブロック変数fはHTMLフォーム要素（テキストフィールド、ラジオボタン、パスワードフィールドなど）に対応するメソッドが呼び出されると、@userの属性を設定するために特別に設計されたHTMLを返す  
```
<%= f.label :name %>
<%= f.text_field :name %>
```
↑これはUserモデルのname属性を設定する、ラベル付きテキストフィールド要素を作成するのに必要なHTMLを作成している。  

* .empty?メソッド（空だとtrueを返す）、.any?（空でなければtrueを返す）は配列に対対してもそのまま使える  

* assert_no_differenceメソッドはブロックを実行する前後で引数が変化しないことを検証する  
```
assert_no_difference 'User.count' do
  post users_path, params: { user: { name:  "",
                                     email: "user@invalid",
                                     password:              "foo",
                                     password_confirmation: "bar" } }
end
```
無効なユーザーデータを登録してもユーザー数が変化しないことを検証している  

* assert_differenceもassert_no_differenceメソッドと同様にブロックを実行する前後で引数が変化しないことを検証する（第一引数に比較したい値を代入）  



