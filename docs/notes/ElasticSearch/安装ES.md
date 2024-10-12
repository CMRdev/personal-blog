# 安装 ES

## 一、下载并运行 ES

- 1、unix 类操作系统：

  ```bash
  tar zxf elasticsearch-*.tar.gz
  cd elasticsearch-*
  bin/elasticsearch
  ```

- 2、windows 系统：

  ```bash
  下载zip压缩包并解压
  运行：bin/elasticsearch.bat
  ```

- 3、ES 同样提供 RPM、DEB 包

  ```bash
  systemctl start elasticsearch.service
  (如果操作系统没有systemd软件，可使用：/etc/init.d/elasticsearch start)
  ```

- 4、docker 安装 ES

  ```bash
  docker network create elastic
  docker pull docker.elastic.co/elasticsearch/elasticsearch:8.9.2
  docker run --name es01 --net elastic -p 9200:9200 -it -m 1GB -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:8.9.2
  # 再次生成密码、kibana-token
  docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
  docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
  # Copy the http_ca.crt SSL certificate from the container to your local machine.
  docker cp es01:/usr/share/elasticsearch/config/certs/http_ca.crt .
  ```

- 5、首次安装：

  ```bash
  # Password for the elastic user (reset with `bin/elasticsearch-reset-password -u elastic`):
  A8uEgxy3ZTGnmqYcNvFp

  # HTTP CA certificate SHA-256 fingerprint:
  85f0c568daf33bcfb55d8a2b2ea4453911475978b5c9324c5c2e313bdd64714a

  # Configure Kibana to use this cluster:
  # Run Kibana and click the configuration link in the terminal when Kibana starts.
  # Copy the following enrollment token and paste it into Kibana in your browser (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjkuMiIsImFkciI6WyIxNzIuMTguMC4yOjkyMDAiXSwiZmdyIjoiODVmMGM1NjhkYWYzM2JjZmI1NWQ4YTJiMmVhNDQ1MzkxMTQ3NTk3OGI1YzkzMjRjNWMyZTMxM2JkZDY0NzE0YSIsImtleSI6Im1RYzNwNG9CVHhNWDZNREJpYmo1OlhQNDRvZGFaUnE2T0lIMFUzNFV3bUEifQ==

  # Configure other nodes to join this cluster:
  # Copy the following enrollment token and start new Elasticsearch nodes with `bin/elasticsearch --enrollment-token <token>` (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjkuMiIsImFkciI6WyIxNzIuMTguMC4yOjkyMDAiXSwiZmdyIjoiODVmMGM1NjhkYWYzM2JjZmI1NWQ4YTJiMmVhNDQ1MzkxMTQ3NTk3OGI1YzkzMjRjNWMyZTMxM2JkZDY0NzE0YSIsImtleSI6Im1nYzNwNG9CVHhNWDZNREJpYmo1Om44b1hweFpiUnBHMWZtalpxUXk0eFEifQ==

  # If you're running in Docker, copy the enrollment token and run:
  `docker run -e "ENROLLMENT_TOKEN=<token>" docker.elastic.co/elasticsearch/elasticsearch:8.9.2`
  ```

- 6、run Kibana

  ```bash
  docker pull docker.elastic.co/kibana/kibana:8.9.2

  docker run --name kib01 --net elastic -p 5601:5601 docker.elastic.co/kibana/kibana:8.9.2
  ```

- 7、移除

  ```bash
  # Remove the Elastic network
  docker network rm elastic
  # Remove Elasticsearch containers
  docker rm es01
  docker rm es02
  # Remove the Kibana container
  docker rm kib01
  ```

- 8、进入 docker 容器：

  ```bash
  docker exec -it es01 /bin/bash
  ```

## 二、ES 设置

- 9、修改 elastic 密码：

  ```bash
  POST /_security/user/elastic/_password
  {
    "password" : "elastic"
  }
  ```

- 10、http 无法访问 ES，https 可以访问，这是因为设置了 ssl 认证，关闭就好：

  ```bash
  在 ES/config/elasticsearch.yml 文件中把 xpack.security.http.ssl:enabled 设置成 false 即可
  ```

- 11、设置 ES 免登录：

  ```bash
  找到 elasticsearch.yml 文件， 把 xpack.security.enabled 属性设置为 false 即可。
  ```

- 12、调整 ES 占用内存大小（设置太大 ES 会崩掉）

  > ES 的内存是自己调节的。在 `config/jvm.options` 文件中设置

  ```bash
  -Xms256m
  -Xmx256m
  ```
