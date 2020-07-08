# API Gateway

## Kong API

```bash
cd ~/kong
docker-compose up -d
```

### Create services and routes

```bash
curl -i -X GET 'http://localhost:8001'
```

#### Amadues

```bash
curl -i -X POST http://localhost:8001/services \
 --data name=amadeus \
 --data url='http://192.168.20.101:50070'
```

```bash
curl -i -X POST http://localhost:8001/services/amadeus/routes \
  --data 'paths[]=/amadeus' \
  --data 'name=amadeus'
```

#### Bach

```bash
curl -i -X POST http://localhost:8001/services \
 --data name=bach \
 --data url='http://192.168.30.101:50070'
```

```bash
curl -i -X POST http://localhost:8001/services/bach/routes \
  --data 'paths[]=/bach' \
  --data 'name=bach'
```

#### Test

File List:

```bash
curl -sSL 'http://zimmer:8000/amadeus/webhdfs/v1/user/vagrant/input?op=LISTSTATUS'
curl -sSL 'http://zimmer:8000/bach/webhdfs/v1/user/vagrant/input?op=LISTSTATUS'
```

Open File:

```bash
curl -sSL 'http://zimmer:8000/amadeus/webhdfs/v1/user/vagrant/input/core-site.xml?op=OPEN&user.name=vagrant'
curl -sSL 'http://zimmer:8000/bach/webhdfs/v1/user/vagrant/input/core-site.xml?op=OPEN&user.name=vagrant'
```
