-	add test task

	-	New Item: choose "Freestyle project"
	-	Project name: [self pick]
	-	Source Code Management:
		-	choose Git
		-	Repository URL: [self pick]
		-	Credentials: select the key add in above 'set credentials' part
		-	Branches to build: */develop
			-	develop is a branch for developing, can be replaced with own branch
	-	Build Environment:
		-	check "Provide Node & npm bin/ folder to PATH"
	-	Build:
		-	Execute shell
			-	#!/bin/sh npm install mocha test
	-	Post-build Actions: (add until deploy task is created, run deploy task when test task is stable)
		-	Build other projects:
			-	Projects to build: [deploy task name]
			-	Trigger only if build is stable

![enter image description here](https://lh3.googleusercontent.com/-DXyB3r3qs74/VUCZ7o9PYfI/AAAAAAAAP-A/qXBPlFxB3Mk/s0/Screen+Shot+2015-04-22+at+5.38.15+PM.png)

![enter image description here](https://lh3.googleusercontent.com/-r-Lruzqt_MU/VUCaAQugQHI/AAAAAAAAP-M/exgqLJ3Fo2g/s0/Screen+Shot+2015-04-22+at+5.40.10+PM.png)

![enter image description here](https://lh3.googleusercontent.com/-orYAoGThZh4/VUCaFAvihZI/AAAAAAAAP-Y/M7OvwClXh70/s0/Screen+Shot+2015-04-22+at+5.41.26+PM.png)
