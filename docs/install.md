---
title: Installing
---

Basic instructions for installing and updating from GitHub can be found in the [ReadMe](https://github.com/omeka/omeka-s/blob/develop/README.md) of the Omeka S github repository.

## Installing from released zip file

1. Download the latest release from the release page
1. Open config/database.ini and add your MySQL username, password, database name, and host name. The user and database must be created before this step.
1. Make sure the files/ directory is writable by Apache.
1. In your web browser, navigate to the omeka-s directory, where you can complete installation.

## Initial setup
Once you have successfully installed and configured the database.ini file, you can navigate to the location of your Omeka S install.

The first time you to the install site, you will need to enter information for the first user, along with basic information for your install. There are two sections on this page: *Create the first user* and *Settings*. 

In the First User section, enter:

- an *email* address, and type again to confirm.
- confirm the *password* and type again in the next input to confirm.
- a *display name* for the user

Note that you can change all of these later in the [User](/admin/users.md) management section of your install.

![First user section with fields as described](/files/installOmekaS1.png)

In the Settings section, enter:

- An *installation title* which will display on the admin site,
- The installation's *time zone* (select from dropdown), and
- select a *locale* for the language of the admin side of the installation.

![Settings section with fields as described](/files/installOmekaS2.png)

You can changes these at any time in the in the [Settings](/admin/settings.md) section of your [Admin Dashboard](/admin-dashboard.md)

## Configuration options
The following can be configured in the file local.config.php (located in the config directory)

- `thumbnailer` Default is `Omeka\File\Thumbnailer\ImageMagick`. Also available are `Omeka\File\Thumbnailer\Imagick` and `Omeka\File\Thumbnailer\Gd`
- `phpcli_path` Default is to attempt to detect correct path to PHP. Use this option to specify a path if needed in your server configuration. For example: 
```
    'cli' => array(
        'phpcli_path' => '/usr/bin/php55',
    ),
```

- `mail` Default is to use Sendmail. If using SMTP use this example configuration (see the [zend-mail docs](https://docs.zendframework.com/zend-mail/transport/smtp-options/) for clarification):
```
    'mail' => [
        'transport' => [
            'type' => 'smtp',
            'options' => [
                'name' => 'localhost',
                'host' => '127.0.0.1',
                'port' => 25, // 465 for 'ssl', and 587 for 'tls'
                'connection_class' => 'smtp', // 'plain', 'login', or 'crammd5'
                'connection_config' => [
                    'username' => null,
                    'password' => null,
                    'ssl' => null, // 'ssl' or 'tls'
                    'use_complete_quit' => true,
                ],
            ],
        ],
    ],
```

## Updating
1. Download the latest release from the release page
1. Make a copy of your /config directory. You will need to restore your local.config.php and database.ini files from that copy.
1. Make a copy of your /modules and /themes directories.
1. Make a copy of your /files directory.
1. Remove all Omeka S files, and replace them with the files from the updated zip file.
1. Replace your original /config/local.config.php file, and the /modules, /themes, and /files directories that you copied.
1. In your web browser, go to your site and run any migrations that are needed.
