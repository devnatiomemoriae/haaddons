# yodocker

yodocker is a simple Home Assistant add-on which allows any number of docker-compose commands to be run upon add-on startup. In addition, files can be nominated to be monitored for writes and can trigger execution of the configured docker-compose commands.

## WARNING

The add-on allows access to the docker api and can also execute arbitrary shell commands, albeit in a limited environment. In the wrong or inexperienced hands, it could damage your system.

## Installation

- Add the devnatiomemoriae home assistant repository to your home assistant via the Supervisor
- Add the youdocker add-on via the Supervisor

To be able to use this add-on, you'll need to disable protection mode on this
add-on. Without it, the add-on is unable to access Docker.

1. Search for the "yodocker" add-on in the Supervisor add-on store and
   install it.
1. Set the "Protection mode" switch to off.
1. Start the "yodocker" add-on.
1. Check the logs of the "Portainer" add-on to see if everything went well.

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
commands:
  - command: docker-compose -p 'yodocker' up -d --remove-orphans
    monitor: /config/docker-compose.yaml
  - command: docker-compose -f /share/dc.yaml up -d
  - command: some_script
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Required: `commands`

List of commands to run on startup and possibly when monitored change detected

### Required: `command`

Specify (docker-compose) command. This command will be run upon startup of the add-on.

The working directory is `/config`.

The full command is required. For flexibility, the command could in fact be any command, not just a docker-compose.

The command is expected to return so don't forget to run as detached.

### Option: `monitor`

File to watch for close write events (only). When event detected the associated `command` will be run.

The working directory is `/config`.

## Known issues and limitations

Only close write events (inotify CLOSE_WRITE) are currently monitored for simplicity of implementation.

## License

MIT License

Copyright (c) 2018-2020 devnatiomemoriae

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
