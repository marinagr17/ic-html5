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
        	sh '''
            	      pip install --upgrade pip setuptools wheel
            	      pip install --no-cache-dir --retries 5 --default-timeout=1000 html5validator
            	      html5validator --root _build/
	           '''
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
                sh 'surge ./_build/ proyectoCI_CD.surge.sh --token $TOKEN'
            }
        }
        
    }
}
