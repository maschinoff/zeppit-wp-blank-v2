# The starter clean theme for WordPress based on [_S](https://underscores.me/)

This was tested on the macOS Mojave 10.14.2 with PHPStorm 2018.1.6 and latest versions of [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/). Some things might work a little different in other Operating Systems.

### Instalation

1. Clone the repository to a local folder
```$xslt
git@github.com:maschinoff/zeppit-wp-blank-v2.git
```

2. Change your WordPress setting in environment file .env

3. Run docker compose
```$xslt
docker-compose up
```

4. Your new WordPress site will be viewable at this URL:
```$xslt
http://127.0.0.1:8888
``` 

### PHPStorm - XDebug configurations
1. __The first thing you should do is to check your Debug settings.__

PhpStorm -> Preferences -> Languages and Frameworks -> PHP -> Debug

Make sure you have the same port that you have configured previously in "XDEBUG_CONFIG" environment variable: 9001 by default.

Uncheck the next checkbox (we need to debug only our theme not WordPress):
 - Force break at first line when no path mapping specified

Click "Apply" to save your configurations.

2. __The second we need to enable DBGp proxy in PhpStorm__

PhpStorm -> Preferences -> Languages and Frameworks -> PHP -> Debug -> DBGp Proxy

And configure it:

It should match the value you have defined in your "XDEBUG_CONFIG" environment variable.

- IDE key: PHPSTORM
- HOST: docker.for.mac.localhost
- PORT: 9001

Click "Apply" to save your configurations.

3. __Then we need to configure a server. This is how PhpStorm will map the file paths in your local system to the ones in your container.__

PhpStorm -> Preferences -> Languages and Frameworks -> PHP -> Servers

Give a name to your server. It should match the value you have defined in your "PHP_IDE_CONFIG" environment variable. It calls "zeppit-wordpress" by default.

The "host" and "port" is how will access your application. By default is 127.0.0.1:8888. (You could change it in the docker-compose file)

In the "Use path mapping" section you have to map the root path of your WordPress theme to the path inside the container. In our case its "/var/www/html/wp-content".

Click "Apply" to save your configurations.

4. __Now it is time to configure the remote debugger for your project.__

Run -> Edit Configurations...

Click on the "plus" sign at the top left and select "PHP Remote Debug" from the list.

Now configure it:
- Name: XDebug
- Server: zeppit-wordpress
- IDE key(session id): PHPSTORM

Your IDE should be now correctly configured.

#### XDebug testing

1. Open "wp-content/themes/zeppit/header.php" and place a breakpoint on the "the_custom_logo()" function.
2. Click on the "Start Listening for PHP Debug connections" icon on the top right corner of PhpStorm.
3. Open in your browser http://127.0.0.1:8888

If you did everything well you should see the execution stop at your breakpoint.

