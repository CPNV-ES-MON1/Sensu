# 002 - Sensus Setup

* [Sensu Official Doc](https://docs.sensu.io/sensu-go/latest/operations/deploy-sensu/install-sensu/)

## Setup the Sensu Backend

* Pull the last image

```
sudo docker pull sensu/sensu
```

* Create the nework

```
sudo docker network create sensu
```

* Create the volume

```
sudo docker volume create sensu-backend-data
```

```
sudo docker run -d --rm --name sensu-backend \
  -p 8080:8080 -p 3000:3000 \
  -v sensu-backend-data:/var/lib/sensu \
  --network sensu  \
  sensu/sensu sensu-backend start
```

```
sudo docker run -d --rm --network sensu -p :3030 \
sensu/sensu sensu-agent start \
--backend-url ws://sensu-backend:8081 --deregister \
--keepalive-interval=5 --keepalive-warning-timeout=10 --subscriptions linux
```

```ps
$uri = 'http://sensu.cld.education/version'
$body = @{
    etcd = @{
        etcdserver = '3.3.13'
        etcdcluster = '3.3.0'
    }
    sensu_backend = '6.13.0'
} | ConvertTo-Json

Invoke-RestMethod -Method Post -Uri $uri -Body $body -ContentType 'application/json'
```

## Setup the Sensu CLI

```
Invoke-WebRequest -Uri https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/6.13.0/sensu-go_6.13.0_windows_amd64.zip  `
  -OutFile sensu-go_6.13.0_windows_amd64.zip
```

```
Expand-Archive -LiteralPath sensu-go_6.13.0_windows_amd64.zip -DestinationPath .
```

```
./sensuctl.exe configure -n --url http://sensu.cld.education `
  --username admin `
  --password "1qa2ws3eD!" `
  --namespace default
```
