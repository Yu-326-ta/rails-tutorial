# Chapter9

## 学び
* パスワードとトークンとの一般的な違いは、パスワードはユーザーが作成・管理する情報であるのに対し、トークンはコンピューターが作成・管理する情報である点（トークンもパスワードのような秘密情報）  

* IDを直接保存するとよくないので`cookies.encrypted[:user_id] = user.id`で暗号化する（cookieの永続化もする必要があるので`cookies.permanent.encrypted[:user_id] = user.id`←こうなる）  


