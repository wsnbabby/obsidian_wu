
https://docs.sonarsource.com/sonarqube/latest/setup-and-upgrade/install-the-server/



```bash
参考：https://www.toutiao.com/article/7064862999240229383/

# 安装postgresql
docker run -d --name postgresql --restart=always -p 5432:5432 -e ALLOW_EMPTY_PASSWORD=yes -e POSTGRESQL_USERNAME=postgres -e POSTGRESQL_DATABASE=sonar bitnami/postgresql:13

# 安装sonar
docker run -d --name sonarqube -p 9000:9000 -e ALLOW_EMPTY_PASSWORD=yes -e SONARQUBE_DATABASE_HOST=10.10.77.223 -e SONARQUBE_DATABASE_PORT_NUMBER=5432 -e SONARQUBE_DATABASE_USER=postgres -e SONARQUBE_DATABASE_NAME=sonar bitnami/sonarqube:9

```