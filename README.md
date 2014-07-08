# grunt-ftp-push-fullpath

> Deploy your files to a FTP server <br>
> Notice: Currently SFTP is not supported

## Getting Started
This plugin requires Grunt `~0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-ftp-push-fullpath --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-ftp-push-fullpath');
```

## The "ftp_push" task

### Overview
In your project's Gruntfile, add a section named `ftp_push` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  ftp_push: {
    your_target: {
      options: {
        // Task-specific options go here.
      },
      files: {
        // Target-specific file lists.
      }
    }
  }
})
```

### Options

#### authKey
Type: `String` 
Default: `None`

Name of authKey that will be used for your credentials to access the FTP server.  This name should match the name of the credentials you want to use in the `.ftpauth` file.

#### host
Type: `String` 
Default: `None`

URL host of your FTP Server.

#### dest
Type: `String` 
Default: `None`

Destination of where you want your files pushed to, relative to the host.

#### port
Type: `Number` 
Default: `21`

Port for accessing the FTP server.

### Usage Examples

#### Sample .ftpauth file

This file should be named `.ftpauth` and be in the same directory as your `Gruntfile.js`.  It is a JSON object with an "authKey" that has a username and password for it's value. Use the following as a guide for setting up your file.

```js
{
	"serverA":{
		"username":"myUserName@gmail.com",
		"password":"password123456"
	},
	"serverB":{
  		"username":"myOtherUsername@gmail.com",
  		"password":"12345Pass"
  	}
}
```

#### Default Options
In this example, the default options are used to set up the necessary components of pushing files to an FTP server. This is meant to be very basic, the files you specify in `files` will be pushed one by one to `host + dest`.

```js
grunt.initConfig({
  ftp_push: {
    your_target: {
      options: {
        authKey: "serverA",
        host: "sample.server.com",
        dest: "/html/test/",
        port: 21
      },
      files: [ // Enable Dynamic Expansion, Src matches are relative to this path, Actual Pattern(s) to match
        {expand: true,cwd: 'test',src: ['**/*']}
      ]
    }
  }
})
```

#### Optional Options
For your options object which normally looks like this:
```js
options: {
	authKey: "serverA",
    host: "sample.server.com",
    dest: "/html/test/",
    port: 21
},
```
You can also not create an .ftpauth file if you choose and pass the username and password in this way: 
```js
options: {
	username: "myUsername",
	password: "myPassword",
    host: "sample.server.com",
    dest: "/html/test/",
    port: 21
}
```
## Dependencies

This plugin uses Sergi Mansilla's <a href="https://github.com/sergi/jsftp">jsftp</a> node.js module.

## Coming Soon
Adding in list of files to exclude from the upload.<br>
Updating jsftp to version 1.3.0<br>
Ability to push to multiple destinations with different sets of files in one target<br>
Possibly adding in support for SFTP

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
<ul>
<li>2014/07/08 - v 0.2.3 &nbsp; Use full path whe uploading files</li>
<li>2014/07/03 - v 0.2.0 &nbsp;<a href='https://github.com/Robert-W/grunt-ftp-push/issues/6' target='_blank'>#6</a>&nbsp; Fixed issue with pushing files from root directory when cwd is set to '.' or './'</li>
</ul>
