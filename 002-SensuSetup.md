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

### Setup backend (with autorestart)

```
# Replace `<username>` and `<password>` with the username and password
# you want to use for your admin user credentials.
sudo docker run -v /var/lib/sensu:/var/lib/sensu \
-d --name sensu-backend \
-p 3000:3000 -p 8080:8080 -p 8081:8081 \
-e SENSU_BACKEND_CLUSTER_ADMIN_USERNAME=admin \
-e SENSU_BACKEND_CLUSTER_ADMIN_PASSWORD=1qa2ws3eD! \
sensu/sensu:latest \
sensu-backend start --state-dir /var/lib/sensu/sensu-backend --log-level debug
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

## Setup the Sensu CLI on LIN

```
sensuctl configure -n \
--username 'admin' \
--password '1qa2ws3eD!' \
--namespace default \
--url 'http://10.0.99.10:8080'
``` 


## Setup the Sensu CLI on WIN

```
Invoke-WebRequest -Uri https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/6.13.0/sensu-go_6.13.0_windows_amd64.zip  `
  -OutFile sensu-go_6.13.0_windows_amd64.zip
```

```
Expand-Archive -LiteralPath sensu-go_6.13.0_windows_amd64.zip -DestinationPath .
```

```
./sensuctl.exe configure -n --url http://sensu.cld.education/api `
  --username admin `
  --password "P@ssw0rd!" `
  --namespace default
```
