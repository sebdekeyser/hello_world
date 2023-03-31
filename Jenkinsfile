pipeline {
    //agent any
    agent { label 'linux' }
    tools {
         maven 'v3.9.1'
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
    }
    
    post{
        always {
            sh 'mvn generate-test-resources process-test-resources'
        }
        success {
            sh 'mvn package'
            archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false, onlyIfSuccessful: true
        }
        failure {
            mail bcc: '', body: 'test failure', cc: '', from: '', replyTo: '', subject: 'build on pipeline1 failed', to: 'sebastien.dekeyser@acoss.fr'
        }
    }
    
    
    
}
