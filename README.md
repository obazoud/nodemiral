# hitler [![Build Status](https://travis-ci.org/arunoda/hitler.png?branch=master)](https://travis-ci.org/arunoda/hitler)
### Server Automation for NodeJS over SSH

## Install
~~~js
npm install hitler
~~~

## Features

* Support connecting to any unix remote server
* Authenticate with password(using [`sshpass`](http://sourceforge.net/projects/sshpass/)) or with a `pem` file
* Can work with multiple servers at once
* Supports, `copy`, `execute` and `executeScript` at core methods
* Familiar NodeJS API

## Example
~~~js
var hitler = require('hitler');
var session = hitler.session('hostname', {username: 'root', password: 'password'});

session.execute('uname -a', function(err, code, logs) {
  console.log(logs.stdout);
});
~~~

## API

### Session

Create a session to a remote server. You can invoke following methods after created a session

    @param hostname - hostname or ip addess
    @param auth - object containing following fields: `username` and (`password` or `pem`)
    @param options - currently you can pass ejs options with `ejs` fields
    hitler.session(hostname, auth, options);

### Session Methods

#### execute
execute given shell command on the remote server

    @param shellCommand - shellCommand
    @param callback - callback containing following parameters
      err - err if exists
      code - status code of the ssh process
      logs - {stdout: 'stdout logs', stderr: 'stderr logs'}
    session.execute(shellCommand, callback);

#### executeScript
execute a local shell script in the remote server. You can template shell script with [EJS](https://github.com/visionmedia/ejs).

    @param localScriptFile - localScriptFile
    @param templateVars - optional variables to the template if uses ejs in the script
    @param callback - callback containing following parameters
      err - err if exists
      code - status code of the ssh process
      logs - {stdout: 'stdout logs', stderr: 'stderr logs'}
    session.executeScript(localScriptFile, templateVars, callback);

#### copy
copy a file from local machine to the remote machine. Supports binary files too.

    @param localFile - localFile
    @param remoteFileLocation - remoteFileLocation
    @param callback - callback containing following parameters
      err - err if exists
      code - status code of the ssh process
      logs - {stdout: 'stdout logs', stderr: 'stderr logs'}
    session.copy(localFile, remoteFileLocation, callback)