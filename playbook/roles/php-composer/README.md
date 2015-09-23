# ansible-role-composer

[![Build Status](https://travis-ci.org/kosssi/ansible-role-composer.svg?branch=master)](https://travis-ci.org/kosssi/ansible-role-composer)

Installs Composer, the PHP Dependency Manager.

## Requirements

- php (version 5.3+) should be installed.

## Role Defaults Variables

    composer_path: /usr/local/bin/composer
    composer_update: true
    composer_update_day: 20
    env_proxy: {}

The path where composer will be installed and available to your system. Should be in your user's `$PATH` so you can run
commands simply with `composer` instead of the full path.

You can specify where is php with `env_proxy` variable. For example :

    env_proxy:
      PATH: "/usr/local/zend/bin"

You can also setup a global composer directory and make the bin directory available in the `$PATH` automatically by:
 
    composer_path_env: true
    composer_home_path: /opt/composer
    composer_home_owner: root
    composer_home_group: root
    composer_global_packages:
      phpunit/phpunit: "@stable"

If your project use a lot of libraries from github, you may see next message during `composer install`:

    Could not fetch `...`, enter your GitHub credentials to go over the API rate limit
    A token will be created and stored in "~/.composer/auth.json", your password will never be stored
    To revoke access to this token you can visit https://github.com/settings/applications

So your `composer install` can get stuck.

To prevent that, you must configure github oauth token to go over the API rate limit. Visit https://github.com/settings/applications and generate personal access token and assign it to `composer_github_oauth` variable.

    composer_github_oauth: f03401aae1e276abb073f987c08a32410f462e73

## Example Playbook

      roles:
        - { role: kosssi.composer }

## Vagrant

If you have vagrant, you can test this role:

    cd tests
    vagrant up

## Special thanks to contributors

* [jnakatsui](https://github.com/jnakatsui)
* [yoshz](https://github.com/yoshz)
* [jrobeson](https://github.com/jrobeson)

## License

Licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
