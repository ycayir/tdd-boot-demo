### Local MySQL setup

After installing mysql with
```
brew install mysql
```

To have launchd start mysql now and restart at login:
```
brew services start mysql
```

Or, if you don't want/need a background service you can just run:
```
mysql.server start
```

To connect to mysql:
```
mysql -u root -p
```

Create DB:
```
CREATE DATABASE urls
```

Create Table:
```
CREATE TABLE link(short_url VARCHAR(255) NOT NULL PRIMARY KEY,full_url VARCHAR(255));
```

Add click count column: 
```
ALTER TABLE link ADD click_count INT
```

Create new user:
```
create user 'linkservice'@'localhost' identified by 'linkservice';
```

Give all privileges to the new user on the newly created database:
```
grant all privileges on urls to 'linkservice'@'localhost';
```

Don't forget to flush ;)
```
flush privileges;
```


### Local RabbitMQ setup

Install rabbitmq:
```
brew install rabbitmq
```

To have launchd start rabbitmq now and restart at login:
```
brew services start rabbitmq
```

Or, if you don't want/need a background service you can just run:
```
rabbitmq-server
```


### Launch Application

On the command line:
```
mvn spring-boot:run
```

### Test Application

Launch Postman or your most favorite URL test program and test the following URLs:
```
GET http://localhost:8080/shorten?fullUrl=https://projects.spring.io/spring-boot/
GET http://localhost:8080/expand?shortUrl=85b917b2
```
