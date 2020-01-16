# For github throttling issues, goto
#   https://github.com/settings/tokens/new?scopes=repo&description=Docker_secret
# and pass in with --build-arg GITHUB_TOKEN=XXXXXXXX
# WARNING: THIS MIGHT NOT BE SECURE ENOUGH FOR DEPLOYMENT
#          - in principle build args are kept in the image history, but multi-
#          stage builds look like they eliminate that, so it might be ok???

FROM php:5-fpm


RUN apt-get update && apt-get install -y git wget unzip

# Get node
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get install -y nodejs


# Get composer
RUN cd /tmp && \
    wget https://raw.githubusercontent.com/composer/getcomposer.org/b9cc694e39b669376d7a033fb348324b945bce05/web/installer -O - -q | php -- --quiet && \
    mv composer.phar /usr/local/bin/composer


# Now install synchweb
RUN git clone https://github.com/DiamondLightSource/SynchWeb.git /synchweb
RUN cd /synchweb/client && npm install
RUN cd /synchweb/client && npm run build:dev
# Composer; Set github access token, if supplied
ARG GITHUB_TOKEN
RUN if [ -n "$GITHUB_TOKEN" ]; then composer config -g github-oauth.github.com $GITHUB_TOKEN; fi
RUN cd /synchweb/api && composer install

# Copy the default, local configuration
COPY config.php /synchweb/api/config.php

# Now create the php-fpm-mysql container for Synchweb
FROM php:5-fpm
RUN docker-php-ext-install mysqli
COPY --from=0 /synchweb /synchweb

