# puppet-sudo [![Build Status](https://secure.travis-ci.org/saz/puppet-sudo.png)](http://travis-ci.org/saz/puppet-sudo)

Manage sudo configuration via Puppet

### Gittip
[![Support via Gittip](https://rawgithub.com/twolfson/gittip-badge/0.2.0/dist/gittip.png)](https://www.gittip.com/saz/)

## Usage

### WARNING
**This module will purge your current sudo config**

If this is not what you're expecting, set `purge` and/or `config_file_replace` to **false**

### Install sudo with default sudoers

#### Purge current sudo config
```puppet
    class { 'sudo': }
```

#### Purge sudoers.d directory, but leave sudoers file as it is
```puppet
    class { 'sudo':
      config_file_replace => true,
    }
```

#### Leave current sudo config as it is
```puppet
    class { 'sudo':
      purge               => false,
      config_file_replace => false,
    }
```

### Adding sudoers configuration snippet

```puppet
    class { 'sudo': }
    sudo::conf { 'web':
      source => 'puppet:///files/etc/sudoers.d/web',
    }
    sudo::conf { 'admins':
      priority => 10,
      content  => "%admins ALL=(ALL) NOPASSWD: ALL",
    }
    sudo::conf { 'joe':
      priority => 60,
      source   => 'puppet:///files/etc/sudoers.d/users/joed',
    }
```

### sudo::conf notes
* You can pass template() through content parameter.
* One of content or source must be set.

## Additional class parameters
* enable: true or false. Set this to remove or purge all sudoers configs
* package: string, default: OS specific. Set package name, if platform is not supported.
* package_ensure: string, latest, absent, or a specific version of the package you need.
* package_source: string, default: OS specific. Set package source, if platform is not supported.
* purge: true or false, default: true. Purge unmanaged files from config_dir.
* config_file: string, default: OS specific. Set config_file, if platform is not supported.
* config_file_replace: true or false, default: true. Replace config file with module config file.
* config_dir: string, default: OS specific. Set config_dir, if platform is not supported.
* source: string, default: OS specific. Set source, if platform is not supported.

## sudo::conf parameters
* ensure: present or absent, default: present
* priority: number, default: 10
* content: string, default: undef
* source: string, default: undef
* sudo_config_dir: string, default: OS specific. Set sudo_config_dir, if platform is not supported.
