# エラーで学んだこと

* fixtureで作成したデータを使用してテストを書いたが、user.ymlが読み込まれずエラーが出た  
```
def setup
  @user = users(:michael)
end
```
このusersが関数として認識されてしまいテストが通らなかった  
(NoMethodError: undefined method `users' for #<InvalidPasswordTest:0x000000010f4830e0>
test/integration/users_login_test.rb:5:in `setup')  
* 考えたこと  
ymlファイルのインデントが間違っている？？→→フォーマッターを使用したがエラー治らず
* 解決した方法  
関数一行目に`fixtures :users`を追加するとテストが通った→→そもそもymlが読み込まれてなさそう
test_helper.rbに`fixtures :all`を記述すると解決した（すべてのfixtureを読み込めるようにした）  

* `redirect_to(root_url, status: :see_other) unless current_user.admin?`で`NoMethodError: undefined method 'admin?' for nil:NilClass`のエラー吐かれた（DBのculumにadmin追加済み）  
→current_userがnilであることが問題だった  
