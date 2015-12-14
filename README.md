# docker-spawn
Node.js ChildProcess.spawn for running docker containers

# usage

```js

var spawn = require('.').spawn;

var ps = spawn('mitmdump', [], {
  stdio: ['ignore', process.stdout, process.stderr],
  config: {
    Image: 'mitmproxy/releases:0.14',
    Tty: false,
    OpenStdin: false,
    Binds: [
      '/Users/user/share:/data'
    ],
    PortBindings: {
      '8080/tcp': [ { HostIp: '', HostPort: '8080' } ]
    }
  }
});

ps.stdout.pipe(process.stdout);
ps.stderr.pipe(process.stderr);

ps.on('close', function (code, signal) {
  console.log('exited with code', code, signal);
});

console.log('container name:', ps.container);

setTimeout(function () {
  ps.kill('SIGKILL');
}, 10000);

```
