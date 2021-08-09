This installation uses synchweb from the local folder to allow local
development. This needs to be cloned and initialised with dependencies.

Check node version `node --version`. If node is v16, then it won't work and
falls over on - at least - node-sass ([`sass/node-sass#3077`](https://github.com/sass/node-sass/issues/3077)).


```
git clone https://github.com/DiamondLightSource/SynchWeb.git synchweb -b vue_master
cd synchweb/client
npm install
npm run-script build:dev
```

If running composer in PHP!=5 (which you almost certainly are), add to
`synchweb/api/composer.json`:
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