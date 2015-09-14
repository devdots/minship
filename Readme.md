# minship

Minimalistic SSH deployment.


## Installation

    $ binpath=/usr/bin/minship; \
        curl -o $binpath https://raw.githubusercontent.com/devdots/minship/master/bin/minship; \
        chmod +x $binpath; \
        unset binpath

You can use this command to update minship too.

*Use `sudo` or replace `/usr/bin/minship` to path somewhere inside your home directory.*

## Usage

    minship [command|option]

### Options

| Option          | Description |
| --------------- | --- |
| -V, --version   | Print program version |
| -h, --help      | Print help (this screen) |

### Commands

| Command         | Description |
| --------------- | --- |
| `<target>`      | Executes `target` target on remote host (run `minship` to execute 'deploy' target) |
| list            | Print list of available targets |
| console         | Open an SSH session on remote host |
| exec `<cmd>`    | Execute `cmd` on remote host |
| copy `<file>`   | Copies `files` to remote host |

### Command aliases

| Command         | Aliases |
| --------------- | --- |
| list            | ls |
| console         | shell, ssh |
| exec            | run |
| copy            | cp |

### Examples

    $ minship

Will execute `deploy` target.

    $ minship status

Will execute `status` target.

    $ minship list

Will show a list of available targets.

    $ minship exec uptime

Will execute `uptime` command on remote host.


## Configuration

You need to create `Shipfile` file in your project’s directory.

Here is a typical config:

    host='myhost'
    path='sites/example.com'

    [deploy]
    git checkout master
    git pull
    npm install
    node -e "require('grunt').cli()" _ deploy

    [status]
    uptime

The only required things is `host` and `path` parameters and `[deploy]` target.

### Parameters

### host

It’s the same host you use in `ssh` command. It could be string of format `<username>@<ip>:<port>` or just a name of `~/.ssh/config` record.

### path

Project path on remote host. minship will `cd` to this directory before executing any command.

### Targets

Target is just a bunch of shell command that will be executed on remote host via SSH. You can define as many targets as you want.

Note that you can’t use blank lines inside targets but you can use comments (#) and other things—it’s just a shell script.


## Changelog

The changelog can be found in the [Changelog.md](Changelog.md) file.


---

## License

The MIT License, see the included [License.md](License.md) file.
