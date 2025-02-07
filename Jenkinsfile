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
				 sh '''
				 mkdir -p /etc/containers
				 echo -e "[registries.search]\nregistries=['docker.io', 'quay.io','registry.gitlab.com']" > /etc/containers/registries.conf
				 podman build -t ${IMAGE_NAME} .
				 '''
			}
		}

	}
}
