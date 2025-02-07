pipeline {
	agent any

	environment {
        IMAGE_NAME = "my-podman-image"
    }

	triggers {
		pollSCM 'H/10 * * * *'
	}

	options {
		disableConcurrentBuilds()
		buildDiscarder(logRotator(numToKeepStr: '14'))
	}

	stages {
		stage("build container") {
			options { timeout(time: 30, unit: 'MINUTES') }
			steps {
				 sh "podman build -t ${IMAGE_NAME} ."
			}
		}

	}
}
