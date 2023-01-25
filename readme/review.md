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
てことはモデルでバリデーションをかける必要がない？？→結論、両方でかける  

* privateメソッドでメソッドを定義するときは、インデントをprivate行に揃える   
```
private

def user_params
  params.require(:user).permit(:name, :email, :password, :password_confirmation)
end
```

* インデントは４文字じゃなくて２文字にする！  

* class定義の後の空行はいらない  

* クラスメソッドの定義方法は、クラス名ではなくselfを使用  
```
-  def User.new_token
+  def self.new_token
```
ただし定義するときに限る（したのUserをselfにするとテストでエラーが起きる）  
```
def remember
    self.remember_token = User.new_token
    update_attribute(:remember_digest, User.digest(remember_token))
    remember_digest
end
```

* シンボルや文字の配列は%記法を用いる  
```
-  before_action :logged_in_user, only: [:index, :edit, :update, :destroy]
+  before_action :logged_in_user, only: %i[index edit update destroy]
```

* 現在の時刻を取得するときは`Time.zone.new`ではなく`Time.current`メソッドの方がよく使われる  
```
-  update_columns(activated: true, activated_at: Time.zone.now)
+  update_columns(activated: true, activated_at: Time.current)
```

* モデルでアソシエーションを定義しているときは、関連づけているモデルに対するバリデーションはいらない  
```
belongs_to :user
has_one_attached :image do |attachable|
  attachable.variant :display, resize_to_limit: [500, 500]
end
default_scope -> { order(created_at: :desc) }
validates :user_id, presence: true
validates :content, presence: true, length: { maximum: 140 }
```
`validates :user_id, presence: true`はいらない  
