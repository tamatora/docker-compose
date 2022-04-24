version: "3" # おまじない（Composeファイル形式の宣言）
services: # サービス
  db: # (任意の文字列) サービスの名称：データベース
    image: mysql:5.7 # 用いるdockerイメージの指定
    #container_name: "mysql57" # (任意の文字列) コンテナの名称
    volumes: # 作業フォルダの同期（コンテナ側ディレクトリをホスト側へマウント）
      - ./db/mysql:/var/lib/mysql # ホストの作業フォルダ内「./db/mysql」とコンテナ内「/var/lib/mysql」を同期
    restart: always # おまじない（いつもコンテナの再起動を実施）
    environment: # 環境変数の指定
      MYSQL_ROOT_PASSWORD: root_pass_fB3uWvTS # (任意の文字列) mysqlのルートパスワード
      MYSQL_DATABASE: wordpress_db # (任意の文字列) mysql内のデータベース名 ※1
      MYSQL_USER: user # (任意の文字列) mysqlへログインする際のユーザー名 ※2
      MYSQL_PASSWORD: user_pass_Ck6uTvrQ # (任意の文字列) mysqlへログインする際のパスワード ※3

  wordpress: # (任意の文字列) サービスの名称：ワードプレス
    image: wordpress:latest # 用いるdockerイメージの指定
    #container_name: "wordpress" # (任意の文字列) コンテナの名称
    volumes: # 作業フォルダの同期（コンテナ側ディレクトリをホスト側へマウント）
      - ./wordpress/html:/var/www/html # ホストの作業フォルダ内「./wordpress/html」とコンテナ内「/var/www/html」を同期
      - ./php/php.ini:/usr/local/etc/php/conf.d/php.ini # ホストの作業フォルダ内「./php/php.ini」とコンテナ内「/usr/local/etc/php/conf.d/php.ini」を同期 ※注意！
    restart: always # おまじない（いつもコンテナの再起動を実施）
    depends_on: # サービス間の依存関係を指定
      - db # サービス「db」と関係がありますよ（先に「db」を起動してね。「wordpress」の起動には「db」の起動が必要よ）
    ports: # 公開用のポートの指定
      - "8080:80" # ホスト側のブラウザで「localhost:8080」にアクセスしたら、コンテナ側の「80ポート」につながり、WordPressが表示される
    environment: # 環境変数の指定
      WORDPRESS_DB_HOST: db:3306 # サービス「db」の3306ポートに接続してね
      WORDPRESS_DB_NAME: wordpress_db #  (任意の文字列) 使うデータベースは「wordpress_db」だよ ※1と合わせる
      WORDPRESS_DB_USER: user # (任意の文字列) mysqlへログインする際のユーザー名 ※2と合わせる
      WORDPRESS_DB_PASSWORD: user_pass_Ck6uTvrQ # (任意の文字列) mysqlへログインする際のパスワード ※3と合わせる

  phpmyadmin: # (任意の文字列) サービスの名称：phpmyadmin
    image: phpmyadmin/phpmyadmin:latest # 用いるdockerイメージの指定
    #container_name: "phpmyadmin" # (任意の文字列) コンテナの名称
    restart: always # おまじない（いつもコンテナの再起動を実施）
    depends_on: # サービス間の依存関係を指定
      - db # サービス「db」と関係がありますよ（先に「db」を起動してね。「phpmyadmin」の起動には「db」の起動が必要よ）
    ports: # 公開用のポートの指定
      - "8888:80" # ホスト側のブラウザで「localhost:8888」にアクセスしたら、コンテナ側の「80ポート」につながり、phpmyadminが表示される

