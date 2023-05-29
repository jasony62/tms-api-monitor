# tms-monitor

监控工具栈，包括：nginx，promethues，grafana 等。

# nginx

用 nginx 作为 api 的代理网关。添加`nginx-module-vts`模块提供监控指标。

进入`nginx`目录，执行命令，构造镜像。

```shell
docker build -f Dockerfile -t jasony62/nginx-vts .
```

运行

```
docker run -it --rm -p 8888:80 -v $PWD/nginx.conf:/etc/nginx/nginx.conf jasony62/nginx-vts
```

生成密码文件

```shell
htpasswd -nb admin 12345678 > /etc/nginx/admin.pwd
```

# prometheus

使用 prometheus 抓去 vts 数据

# grafana

使用 grafana 展示数据

# keycloak

用 keycloak 给 grafana 提供用户认证服务

```
curl -L https://github.com/keycloak/keycloak/releases/download/21.1.1/keycloak-21.1.1.tar.gz -o ~/keycloak-21.1.1.tar.gz
```

```
docker build -f Dockerfile.alpine -t jasony62/keycloak-alpine .
```

```
docker run -it --rm -p 6666:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin123! -e KC_HOSTNAME_URL=http://host.docker.internal:6666 jasony62/keycloak-alpine start-dev
```

# 参考

tms-efk
