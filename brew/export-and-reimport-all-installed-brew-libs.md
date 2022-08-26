To keep not only installed brews but also casks and taps i recommend to

	$ brew bundle dump --describe --global
	$ brew bundle install --global

the first command will write ~/.Brewfile which will be read again in the second call.