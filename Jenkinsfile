pipeline{
    agent any

    tools{
        nodejs 'NODE22'
    }
    stages{
        stage('Fetch code') {
            steps{
                git branch: 'main', url: 'https://github.com/cyanexttime/Angular-jenkins-test.git'
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
                sh 'npm install -g @angular/cli'
            }
        }
        
        stage('Build') {
            steps {
                sh 'ng build'
                sh 'zip -r angular-dist.zip dist/'
                archiveArtifacts artifacts: 'angular-dist.zip'
            }
        }

        stage('Test')  {
            steps {
                sh 'ng test'
            }
        }
    }
}
