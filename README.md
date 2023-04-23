# WordPress with Email

This is a docker stack for testing WordPress (e.g. as base to [clone a LIVE instance](https://www.consulting.heikol.de/en/blog/wordpress-clone-manually/)) including the ability to check mails. You can check the mails from WordPress with [MailDev](https://github.com/maildev/maildev), a SMTP server with web interface. [msmtp](https://marlam.de/msmtp/) is used as a simple SMPT client.

A small WordPress plugin sets the sender email address (from field) fixed to 'webmaster@docker.local' and fixes the problem of undeliverable address 'wordpress@localhost' inside Docker container. Installing it as [must-use WordPress plugin](https://wordpress.org/support/article/must-use-plugins) to have it already actived.

![mails](mails.png)

Running the docker compose command creates four containers:
  * wp_wordpress – WordPress CMS
    * http://localhost:3080 – WordPress instance, ready for installation
    * WordPress files are available mapped to docker host in directory 'wp'
  * wp_mariadb – MariaDB database
    * database available as mysql:3306
    * user 'root', password 'root' and database 'wordpress'
  * wp_phpmyadmin – phpmyadmin database administration app
    * http://localhost:3081 – phpMyAdmin to work with the database
  * wp_maildev - MailDev for collecting and displaying emails
    * listening on emails as maildev:1025
    * http://localhost:3082 – MailDev web interface

```bash
git clone https://github.com/muhme/wordpress-maildev
cd wordpress-maildev
docker compose up -d
```

All four containers are used in the latest version.

![docker](docker.png)

## Testing
You can test mails from WordPress after the initial installation using the "Forgot your password?" feature at http://localhost:3080/wp-login.php.

For the following two tests, you need to go into the Docker container:
```bash
docker exec -it wp_wordpress /bin/bash
```

You can test [msmtp](https://marlam.de/msmtp/) inside container with:
```bash
echo -e "Subject: Test Mail\r\nTo: you@test.com\r\n\r\nEverything working?" | msmtp --debug -f me@test.com -- you@test.com
```

You can test PHP email configuration inside container with:
```bash
php -r "mail('you@test.com','Test Mail from PHP', 'Working too?', 'From: me@test.com');"
```

## License
This project is licensed under the MIT License.

## Contact
Don't hesitate to ask if you have any questions or comments.
