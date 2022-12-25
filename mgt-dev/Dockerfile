FROM mgtcommerce/mgt-dev:v3

# Install and enable Source Gaurdian loader for php 8.1
# Install msmtp and config Mailhog for php 8.1
RUN PHP_VERSION=8.1 \
    && mkdir -p /tmp/sourceguardian \
    && cd /tmp/sourceguardian \
    && curl -Os https://www.sourceguardian.com/loaders/download/loaders.linux-x86_64.tar.gz \
    && tar xzf loaders.linux-x86_64.tar.gz \
    && cp ixed.${PHP_VERSION}.lin "$(php -i | grep '^extension_dir =' | cut -d' ' -f3)/sourceguardian.so" \
    && echo  "\nextension=sourceguardian.so" >> /etc/php/${PHP_VERSION}/fpm/php.ini \
    && echo  "\nextension=sourceguardian.so" >> /etc/php/${PHP_VERSION}/cli/php.ini \
    && rm -rf /tmp/sourceguardian \
    && sudo apt-get install msmtp msmtp-mta -y \
    && echo  "\nsendmail_path = \"/usr/bin/msmtp --host=mailhog --port=1025 -f test@test.localhost -t \"" >> /etc/php/${PHP_VERSION}/fpm/php.ini \
    && echo  "\nsendmail_path = \"/usr/bin/msmtp --host=mailhog --port=1025 -f test@test.localhost -t \"" >> /etc/php/${PHP_VERSION}/cli/php.ini

COPY ./php/8.1/fpm/php.ini /etc/php/8.1/fpm/php.ini


