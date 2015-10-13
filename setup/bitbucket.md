-	add pull request test task
	-	(this task is for testing pull request before merging to check the pull request is fine to merge by hand )
	-	install jenkins plugin - bitbucket-pullrequest-builder-plugin
		-	https://github.com/jenkinsci/bitbucket-pullrequest-builder-plugin
		-	download this plugin from http://doc.densan-labs.net/bitbucket-pullrequest-builder.hpi (temporary link)
		-	go to Jenkins > Manage Plugins > Advanced
		-	choose file and select .hpi file above and upload
		-	ensure you restart jenkins
	-	creating a job
		-	New Item: choose "Freestyle project"
		-	Project name: [self pick]
		-	Source Code Management:
			-	choose Git
			-	Repository URL: [self pick]
			-	Credentials: select the key add in above 'set credentials' part
			-	Branches to build: */develop
				-	develop is a branch for developing, can be replaced with own branch
		-	Build Triggers
			-	check "Bitbucket Pull Requests Builder"
				-	Cron: * * * * \*
					-	every minute
				-	Bitbucket BasicAuth Username: [self bitbucket email]
				-	Bitbucket BasicAuth Password: [self bitbucket password]
				-	RepositoryOwner: [the username who opened bitbucket repository]
				-	RepositoryName: [the repository name]
		-	Build Environment:
			-	check "Provide Node & npm bin/ folder to PATH"
		-	Build:
			-	Execute shell
				-	#!/bin/sh npm install mocha test

![enter image description here](https://lh3.googleusercontent.com/-DXyB3r3qs74/VUCZ7o9PYfI/AAAAAAAAP-A/qXBPlFxB3Mk/s0/Screen+Shot+2015-04-22+at+5.38.15+PM.png)

![enter image description here](https://lh3.googleusercontent.com/c_1nBXP85sh7xApq02dCPnIZbo7Blc17_M46n_edmng=s0)

![enter image description here](https://lh3.googleusercontent.com/-r-Lruzqt_MU/VUCaAQugQHI/AAAAAAAAP-M/exgqLJ3Fo2g/s0/Screen+Shot+2015-04-22+at+5.40.10+PM.png)
