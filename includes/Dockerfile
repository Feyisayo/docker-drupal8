FROM drupaldocker/php:7.1-apache

RUN rm -f /etc/apache2/sites-available/000-default.conf
RUN rm -f /etc/apache2/sites-enabled/000-default.conf
ADD ./000-default.conf /etc/apache2/sites-available
RUN ln -s /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-enabled/000-default.conf

# Install the mysql client or drush will have issues with sql-related commands
# Also install git
RUN apt update && apt install mysql-client -y && apt install git -y

# There seems to be a problem with using sendmail in a debian container,
# so we shall install ssmtp instead
RUN apt install ssmtp -y

# Remove ssmtp's default config
RUN rm /etc/ssmtp/ssmtp.conf
ADD ./ssmtp.conf /etc/ssmtp/

COPY ./ssmtp.ini /usr/local/etc/php/conf.d/

# Give ownership of webroot to apache
RUN chown -R www-data:www-data /var/www/html
