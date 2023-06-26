# Local testing of npm packages / NPM link

## Symbolic Linking

At the root directory of your npm package under test, run the below command.

`npm link`

It would create a symbolic link to the entire folder to the global namespace. So, a folder will be created in the directory where global packages are stored with the name that is the same as that of the value of `name` property in `package.json`.

To test/consume this package, at the root of the target project, run below command.

`npm link [package name]`

`[package name]` is the value of the package created in the previous step.

**Cons**: Every file in the directory gets linked, which can create problems and can interfere with the build process if the linked package is consumed in another project.

## Install Tar File

You can first run below command at the root directory of the project under test. It will generate a tar file with the name `[package-name]-[version].tgz`.

`npm pack`

Now, go to the root directory of target project where you want to consume it, and run below command.

`npm install [path to the tar file created above]`

**Cons**: The process is a bit cumbersome as you need to install the tar file every time.

## Manual Process

You can first run below command at the root directory of the project under test. It will generate a tar file with the name `[package-name]-[version].tgz`.

`npm pack`

Then, unzip the tar file content to a new directory, separate from your project. Go, to this new directory where the tar contents have been extracted, and run below command from the directory root.

`npm link`

A folder will be created in the directory where global packages are stored with the name that is the same as that of the value of `name` property in `package.json`.

To test/consume this package, at the root of the target project, run below command.

`npm link [package name]`

`[package name]` is the value of the package created in the previous step.

**Cons**: The process is a bit cumbersome and involves a lot of steps.
