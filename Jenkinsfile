pipeline {
    agent any
    stages {
        stage ('Get Code'){
            steps {
                //Optenemos el codigo de nuestro Git
                git 'http://github.com/santife/helloworld.git'
            }
        }
        
        stage ('Build') {
            steps {
                echo WORKSPACE
                sh 'hostname'
                sh 'ls -lrt'
            }
        }
        
        stage('unit') {
            steps {
                sh '''
                    export PYTHONPATH=$(pwd)
                    pytest --junitxml=result_unit.xml test/unit
                '''
            }
        }
        
        stage('Rest') {
            steps {
                sh '''
                    java -jar /var/lib/jenkins/workspace/wiremock/wiremock-standalone-3.3.1.jar --port 9090 --root-dir test/wiremock/ &
                    sleep 3 
                    export FLASK_APP=app/api.py
                    export FLASK_ENV=development
                    flask run & 
                    export PYTHONPATH=$(pwd)
                    pytest --junitxml=result_unit.xml test/unit
                '''
            }
        }
        
        stage ('Result') {
            steps {
                junit 'result*.xml'
            }
        }

    }
}
