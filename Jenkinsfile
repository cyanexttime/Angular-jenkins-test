pipeline{
    agent any

    tools{
        nodejs 'NODE22'
    }

    parameters{
        choice {
            name: 'ENV',
            choices: ['dev', 'preprod', 'prod']
        }
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
                sh 'export $(cat .env | xargs)'
                sh 'echo "Building for ENV=$ENV"'
                sh 'ng build'
                sh 'zip -r angular-dist-of-${ENV}.zip dist/'
                archiveArtifacts artifacts: 'angular-dist-of-${ENV}.zip'
            }
        }

        stage('Test')  {
            steps {
                sh 'ng test'
            }
        }
    }
}
