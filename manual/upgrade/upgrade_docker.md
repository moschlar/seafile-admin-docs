# Upgrade Seafile Docker

For maintenance upgrade, like from version 10.0.1 to version 10.0.4, just download the new image, stop the old docker container, modify the Seafile image version in docker-compose.yml to the new version, then start with docker-compose up.

For major version upgrade, like from 10.0 to 11.0, see instructions below.

Please check the **upgrade notes** for any special configuration or changes before/while upgrading.


## Upgrade from 10.0 to 11.0

Download the new image, stop the old docker container, modify the Seafile image version in docker-compose.yml to the new version.

Migrate your configuration for LDAP and OAuth according to <https://manual.seafile.com/upgrade/upgrade_notes_for_11.0.x>

Start with docker-compose up.

## Upgrade from 9.0 to 10.0

Download the new image, stop the old docker container, modify the Seafile image version in docker-compose.yml to the new version, then start with docker-compose up.

If you are using pro edition with ElasticSearch, SAML SSO and storage backend features, follow the upgrading manual on how to update the configuration for these features: <https://manual.seafile.com/upgrade/upgrade_notes_for_10.0.x>

If you want to use the new notification server and rate control (pro edition only), please refer to the upgrading manual: <https://manual.seafile.com/upgrade/upgrade_notes_for_10.0.x>

## Upgrade from 8.0 to 9.0

Just download the new image, stop the old docker container, modify the Seafile image version in docker-compose.yml to the new version, then start with docker-compose up.

### Let's encrypt SSL certificate

Since version 9.0.6, we use Acme V3 (not acme-tiny) to get certificate.

If there is a certificate generated by an old version, you need to back up and move the old certificate directory and the seafile.nginx.conf before starting.

```shell
mv /opt/seafile/shared/ssl /opt/seafile/shared/ssl-bak

mv /opt/seafile/shared/nginx/conf/seafile.nginx.conf /opt/seafile/shared/nginx/conf/seafile.nginx.conf.bak
```

Starting the new container will automatically apply a certificate.

```shell
docker-compose down
docker-compose up -d
```

Please wait a moment for the certificate to be applied, then you can modify the new seafile.nginx.conf as you want. Execute the following command to make the nginx configuration take effect.

```sh
docker exec seafile nginx -s reload
```

A cron job inside the container will automatically renew the certificate.

## Upgrade from 7.1 to 8.0

Just download the new image, stop the old docker container, modify the Seafile image version in docker-compose.yml to the new version, then start with docker-compose up.


## Upgrade from 7.0 to 7.1

Just download the new image, stop the old docker container, modify the Seafile image version in docker-compose.yml to the new version, then start with docker-compose up.
