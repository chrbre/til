# What is husky

Husky is a dotnet tool that allows you to run arbitrary actions on specific git hooks. These could be to enforce the same sort of things that you would do centrally, but here they would run before committing code into git. For example, you could ensure your code built and passed all unit tests. Or you could run Fantomas to ensure that your code was correctly formatted. Or perhaps you have a rule that every commit needs to have an issue number in it! Any of these are possible because Husky simply runs any command line tool or arguments as needed; it also has the ability to pass in certain arguments from git, such as the list of files that are in the commit list.

## Usage

Edit ``package.json > prepare`` script and run it once:

	npm set-script prepare "husky install"
	npm run prepare

## Add a hook:

	npx husky add .husky/pre-commit "npm test"
	git add .husky/pre-commit

## Make a commit:

	git commit -m "Keep calm and commit"
	# `npm test` will run every time you commit

## A working example

create a ``pre-commit`` hook to run Fantomas to check that code is correctly formatted:

	dotnet husky add pre-commit -c "dotnet fantomas --check -r"

This creates a file that stores that command (and is therefore source controlled and will be accessible to all users of the repository). Then, the next time you try to commit code, Fantomas will run to ensure that your code is correctly formatted.
