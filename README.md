# fast-api_react_mysql_ngingx_phpmyadmin_template
fast-apiとreact viteとmysqlとphpmyadminとnginxをwindows上のdockerで動かすテンプレートです  

## 使い方
docker desktopをインストールして起動後、このディレクトリをクローン。  

### DB設定
デフォルトではrootのパスワードは12345678になっている。  
userアカウントもuserになっていて、パスワードも12345678になっている。  
mysql/Dockerfileの
>ENV MYSQL_ROOT_PASSWORD=12345678  
>ENV MYSQL_USER=user  
>ENV MYSQL_PASSWORD=12345678  
を任意の値に書き換える  

docker-compose.ymlの  
>    db：  
>    image: mysql:8.0  
>    container_name: mysql_db  
>    environment:  
>      MYSQL_ROOT_PASSWORD: "12345678"  
>      MYSQL_USER: "user"  
>      MYSQL_PASSWORD: "12345678"  
>      MYSQL_DATABASE: "user_db"  # 必要ならデフォルトDBも作成  　　
>    ports:  
>      - "3306:3306"  
>    volumes:  
>      - db-data:/var/lib/mysql  

それと  
> phpmyadmin:  
>  image: phpmyadmin:latest  
>  container_name: pma
>  depends_on:
>      - db
>     environment:
>       # phpMyAdmin が接続する DB サーバー情報
>       PMA_HOST: db
>       # root でログインしたい場合は以下も活用
>       MYSQL_ROOT_PASSWORD: "12345678"  
>       ports:  
>       - "8080:80"

のユーザー名とパスワードも適宜変更する事

### ビルドと起動
クローンしたルートディレクトリをpower shellで開いて  
> docker-compose build  
コマンドを実行後  
> docker-compose up -d  
を実行し、最後に  
>  .\nginx.exe  
を実行する。  

## アクセスURL
PHPmyAdmin http://localhost:8080/  
React vite http://localhost:5174/  
fast -api  http://localhost:8000/api/hello  
でそれぞれアクセスできる  



