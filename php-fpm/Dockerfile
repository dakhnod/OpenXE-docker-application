FROM php:8.2-fpm-alpine

WORKDIR /

RUN apk add imap-dev libzip-dev

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN docker-php-ext-install imap && docker-php-ext-enable imap
RUN docker-php-ext-install zip && docker-php-ext-enable zip

COPY php-fpm/www.conf /usr/local/etc/php-fpm.d/

RUN wget https://github.com/OpenXE-org/OpenXE/archive/refs/heads/master.zip -O openxe.zip
RUN unzip openxe.zip -x /OpenXE-master/userdata/wiki
RUN rm openxe.zip

RUN sed -i 's/\$setup\[2\]\[\x27fields\x27\]\[\x27WFdbhost\x27\]\[\x27default\x27\] = ".*";/$setup[2]['\''fields'\'']['\''WFdbhost'\'']['\''default'\''] = "mariadb";/' /OpenXE-master/www/setup/setup.conf.php # very sorry for this, need to somehow replace the default values...
RUN sed -i 's/\$setup\[2\]\[\x27fields\x27\]\[\x27WFdbname\x27\]\[\x27default\x27\] = ".*";/$setup[2]['\''fields'\'']['\''WFdbname'\'']['\''default'\''] = "openxe";/' /OpenXE-master/www/setup/setup.conf.php
RUN sed -i 's/\$setup\[2\]\[\x27fields\x27\]\[\x27WFdbuser\x27\]\[\x27default\x27\] = ".*";/$setup[2]['\''fields'\'']['\''WFdbuser'\'']['\''default'\''] = "openxe";/' /OpenXE-master/www/setup/setup.conf.php

CMD php-fpm --allow-to-run-as-root