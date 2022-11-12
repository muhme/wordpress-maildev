# WordPress with Email

This is a WordPress test stack including the ability to inspect emails.

Running the docker compose command creates four containers:
  * wp_wordpress – WordPress CMS
    * http://localhost:3080
    * WordPress files are available mapped in directory 'wp'
  * wp_mariadb – MariaDB database
    * database available as mysql:3306
    * user 'root', password 'root' and database 'wordpress'
  * wp_phpmyadmin – phpmyadmin database administration app
    * http://localhost:3081
  * wp_maildev - MailDev for collecting and displaying emails
    * listening on emails as maildev:1025
    * http://localhost:3082

```
$ git clone https://github.com/muhme/wordpress+maildev
$ cd wordpress+maildev
$ docker compose up -d
```

## License
This project is licensed under the MIT License.

## Contact
Don't hesitate to ask if you have any questions or comments.