If you have landed here from an outer space and *do not have any environment configured* - [then come here](/recipes/01-bring-everything-up-first.md) and later return.
<br>
<div style="text-align:center">
    <img alt="Outer Space" src="../images/recipes/outer-space.png">
</div>

## Install ScandiPWA Demo theme

If your environment is running - then skip till the step #1.
Otherwise you will need to bring it up, as it is not possible to conquer the world, when conqueror is sleaping!

* * *

First, you will need to have the `COMPOSER_AUTH` set in your terminal as it will be used for Authentication during the Magento 2 installation / upgrade check 
You should set `COMPOSER_AUTH` on your machine (you can obtain credentials using [Magento2 Marketplace](https://account.magento.com/applications/customer/login/))

> This variable is required every time you are bringing an environment up, not only during the installation step

```console
export COMPOSER_AUTH='{"http-basic":{"repo.magento.com": {"username": "REPLACE_THIS", "password": "REPLACE_THIS"}}}'
```

Once variable is set - you can bring the infrastructure up

```console
docker-compose -f docker-compose.yml -f docker-compose.local.yml -f docker-compose.ssl.yml up -d
```

* * *

1.  Stop the application container
```console
docker-compose stop app
```

2.  Recreate existing database 
```console
docker-compose exec mysql mysql -u root -pscandipwa -e "DROP DATABASE magento; CREATE DATABASE magento;"
```

3.  Import DEMO ScandiPWA database: 
```console
docker-compose exec -T mysql mysql -u root -pscandipwa magento < deploy/latest.sql
```

4.  Recreate Docker infrastructure
```console
docker-compose -f docker-compose.yml -f docker-compose.local.yml -f docker-compose.ssl.yml up -d --force-recreate
```

5. Wait until all the scripts will be executed and fpm will be prepared. You can track the progress by running
```console
docker-compose logs -f app
```


## Add ScandiPWA Demo media
1) Download [media](https://s3-eu-west-1.amazonaws.com/scandipwa-public-assets/scandipwa_media.tgz)

2) Put archive into the `pub/media` folder (if mounted)

3) Extract archive `tar -zxvf scandipwa_media.tgz`

