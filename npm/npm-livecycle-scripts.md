# Livecycle script in package.json

You can add scripts in the ``package.json`` which will be run on a point in the livecycle of a package. (see https://docs.npmjs.com/cli/v8/using-npm/scripts)

For example

	"scripts": {
    	"build": "some build code",
    	"format": "some format code",
    	"lint": "some linting code",
    	"test": "some test code",
    	"prerelease": "executed in the prerelease livecycle",
    	"postinstall": "executed in the postinstall livecycle"
  	},

## Life Cycle Operation Order

	npm cache add

- prepare

	npm ci

- preinstall
- install
- postinstall
- prepublish
- preprepare
- prepare
- postprepare

These all run after the actual installation of modules into node_modules, in order, with no internal actions happening in between

	npm diff

- prepare

	npm install

These also run when you run npm install -g <pkg-name>

- preinstall
- install
- postinstall
- prepublish
- preprepare
- prepare
- postprepare

If there is a binding.gyp file in the root of your package and you haven't defined your own install or preinstall scripts, npm will default the install command to compile using node-gyp via node-gyp rebuild

These are run from the scripts of <pkg-name>

	npm pack

- prepack
- prepare
- postpack

	npm publish

- prepublishOnly
- prepack
- prepare
- postpack
- publish
- postpublish

prepare will not run during --dry-run

	npm rebuild

- preinstall
- install
- postinstall
- prepare

prepare is only run if the current directory is a symlink (e.g. with linked packages)

	npm restart

If there is a restart script defined, these events are run, otherwise stop and start are both run if present, including their pre and post iterations)

- prerestart
- restart
- postrestart

	npm run <user defined>

- pre<user-defined>
- <user-defined>
- post<user-defined>

	npm start

- prestart
- start
- poststart

If there is a ``server.js`` file in the root of your package, then npm will default the start command to node ``server.js``. ``prestart`` and ``poststart`` will still run in this case.

	npm stop

- prestop
- stop
- poststop

	npm test

- pretest
- test
- posttest

	npm version

- preversion
- version
- postversion

## Pre & Post Scripts

To create "pre" or "post" scripts for any scripts defined in the "scripts" section of the package.json, simply create another script with a matching name and add "pre" or "post" to the beginning of them.

	{
  		"scripts": {
    		"precompress": "{{ executes BEFORE the `compress` script }}",
    		"compress": "{{ run command to compress files }}",
    		"postcompress": "{{ executes AFTER `compress` script }}"
  		}
	}

In this example npm run compress would execute these scripts as described.
