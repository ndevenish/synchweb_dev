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
