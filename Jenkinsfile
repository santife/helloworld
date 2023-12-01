pipeline {
    agent any
    stages {
        stage('Build') {
            agent any
            steps {
                sh 'echo "Hello World"'
                sh '''
                echo "Multiline shell steps works too"
                ls -lah
                '''
            }
        }
        stage('Unity'){
            agent any
            steps {
                git 'https://github.com/santife/helloworld.git'
                sh 'ls -lrt'
            }
        }
    }
}
