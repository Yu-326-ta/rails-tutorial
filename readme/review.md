# レビューで学んだこと

* ファイルの末尾には改行を入れる必要がある  
　vscodeのinsertFinalNewlineの設定をオンにすると保存時に改行が入る

* 式展開や特殊文字の使用時以外はしんシングルコーテーションでを使うのが習慣  
　rubocop(linter)を用いてチェックし、自動変換する

* モデルでバリデーションを作成するとき、できるだけ見やすく！！  
```
validates :name,  presence: true, length: { maximum: 50 }
VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-]+(\.[a-z\d\-]+)*\.[a-z]+\z/i
validates :email, presence: true, length: { maximum: 255 },
                  format: { with: VALID_EMAIL_REGEX },
                  uniqueness: true
has_secure_password
validates :password, presence: true, length: { minimum: 6 }
```
↓↓  
```
VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-]+(\.[a-z\d\-]+)*\.[a-z]+\z/i
validates :name,  presence: true, length: { maximum: 50 }
validates :email, presence: true, length: { maximum: 255 },
                  format: { with: VALID_EMAIL_REGEX },
                  uniqueness: true
validates :password, presence: true, length: { minimum: 6 }
has_secure_password
```

* rails console --sandboxもrails c -sのエイリアスが使用可能（どんなエイリアスがあるか一回調べて目を通す）  

* 本来バリデーションはmigrationファイルでかけてしまう（`t.string :email`ではなく`t.string :email, null: false`など）  
てことはモデルでバリデーションをかける必要がない？？  
