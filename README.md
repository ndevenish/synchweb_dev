This installation uses synchweb from the local folder to allow local
development. This needs to be cloned and initialised with dependencies.

First NPM:
```
git clone https://github.com/DiamondLightSource/SynchWeb.git synchweb
cd synchweb/client
npm install
npm run-script build:dev
```

If running composer in PHP7, add to api/composer.json:
```
  "config": {
    "platform": {
      "php": "5.6.17"
    }
  },
```
Then
```
cd api
composer install
```

Configure `synchweb/api/config.php`
```
cp synchweb_build/config.php synchweb/api
```

## Running
Just do `docker-compose up`.

## Alternative
WIP: Alternatively you cna use the synchweb_build docker image. It requires
`--build-arg GITHUB_TOKEN=<key>` where key is gotten from:
    https://github.com/settings/tokens/new?scopes=repo&description=Docker_secret