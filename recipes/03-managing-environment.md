## Bring everything up

> You need to perform the following actions in the *root* of the project.

If you have everything configured, but just need to wake up the containers -

1. Set the `COMPOSER_AUTH` in your terminal, as it will be used for Authentication during the Magento 2 installation / upgrade check.
You can find/obtain credentials using [Magento2 Marketplace](https://account.magento.com/applications/customer/login/)

```console
export COMPOSER_AUTH='{"http-basic":{"repo.magento.com": {"username": "REPLACE_THIS", "password": "REPLACE_THIS"}}}'
```

2. Once `COMPOSER_AUTH` is set, you can bring everything up
```console
docker-compose -f docker-compose.yml -f docker-compose.local.yml -f docker-compose.ssl.yml up -d
```

3. Wait until all the scripts will be executed and fpm will be prepared. You can track the progress by running
```console
docker-compose logs -f app
```

## Bring everything down

> You need to perform the following actions in the *root* of the project.

You can simply put the environment down by running the following command -

```console
docker-compose -f docker-compose.yml -f docker-compose.local.yml -f docker-compose.ssl.yml down
```

## Go in the app container

> You need to perform the following actions in the *root* of the project.

```console
docker-compose exec app bash
```

## Execute Magento command

> You need to perform the following actions in the *root* of the project.

```console
docker-compose exec app /var/www/public/bin/magento {Magento command}
```
<br>

To get the list of all available commands run
```console
docker-compose exec app /var/www/public/bin/magento list
```


