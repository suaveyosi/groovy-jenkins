// comment
pipeline {
 agent any
 stages {
        stage('Checkout-git'){
		steps{
			git poll: true, url: 'https://github.com/suaveyosi/david-python.git'
		}
	}
	stage('CreateVirtualEnv'){
		steps{
			sh '''
				bash -c "virtualenv entorno_virtual && source entorno_virtual/bin/activate"
			'''
		}
	}
	stage('InstallRequirements'){
		steps{
			sh '''
				bash -c "source entorno_virtual/bin/activate && pip install -r requirements.txt"
			'''
		}
	}
	stage('TestApp'){
		steps{
			sh '''
				bash -c "source $(WORKSPACE)/entorno_virtual/bin/activate && cd src && $(WORKSPACE)/entorno_virtual/bin/python $(WORKSPACE)/entorno_virtual/bin/pytest && cd .."
			'''
		}

	}
	stage('BuildDocker'){
		steps{
			sh '''
				docker build . -t suaveyosi/python:1.0
			'''
		}

	}
	stage('PushDockerImage'){
		steps{
			sh '''
				docker push suaveyosi/python:1.0
	
			'''
		}
	}
 }
}
