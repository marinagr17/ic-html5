pipeline {
    environment {
        TOKEN = credentials('SURGE_TOKEN')
      }
    agent {
        docker { image 'josedom24/debian-npm'
        args '-u root:root'
        }
    }
    stages {
        stage('Clone') {
            steps {
                git branch:'master',url:'https://github.com/marinagr17/ic-html5.git'
            }
        }
	stage('Test html5') {
	    steps {
            sh 'apt update && apt install -y python3-pip default-jre'
	        sh 'pip install html5validator'
		    sh 'html5validator --root _build/'
            }
	    }
        
        stage('Install surge')
        {
            steps {
                sh 'npm install -g surge'
            }
        }
        stage('Deploy')
        {
            steps{
                sh 'surge ./_build/ josedom24.surge.sh --token $TOKEN'
            }
        }
        
    }
}
