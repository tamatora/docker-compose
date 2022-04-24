1. SELinuxの無効化
事前に無効化しておくこと

2. 古いバージョンのDockerモジュール削除
```
sudo yum remove docker
```

3. 必要なパッケージのインストール
```
sudo yum install yum-utils
```

4. Dockerリポジトリの追加
```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

5. Dockerのインストール
```
sudo yum install docker-ce docker-ce-cli containerd.io
```

6. Doker起動
```
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
docker run hello-world
```

7. Docker Compseのインストール
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

8. docker-compose操作
```
sudo docker-compose up -d
sudo docker-compose down
```

