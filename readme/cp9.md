# Chapter9

## 学び
* パスワードとトークンとの一般的な違いは、パスワードはユーザーが作成・管理する情報であるのに対し、トークンはコンピューターが作成・管理する情報である点（トークンもパスワードのような秘密情報）  

* IDを直接保存するとよくないので`cookies.encrypted[:user_id] = user.id`で暗号化する（cookieの永続化もする必要があるので`cookies.permanent.encrypted[:user_id] = user.id`←こうなる）  

* 三項演算子(論理値? ? 何かをする : 別のことをする)
```
if params[:session][:remember_me] == '1'
  remember(user)
else
  forget(user)
end
```
と
```
params[:session][:remember_me] == '1' ? remember(user) : forget(user)
```
は同義（左の条件がtrueだったらremember(user)、falseだったらforget(user)）  

* cookiesに保存しているランダムで生成した記憶トークンと、ハッシュ化した記憶トークンに対応する記憶ダイジェストを関連づけることで永続的セッションを実現している  
