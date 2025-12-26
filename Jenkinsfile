pipeline{
    agent any
	
    tools{
        nodejs 'NODE22'
    }

    parameters {
        choice(
            name: 'ENV',
            choices: 'dev\npreprod\nprod',
            description: 'Select environment'
        )
    }

    stages{
        stage('Fetch code') {
            agent{
                label 'built-in'
            }
            steps{
                git branch: 'main', url: 'https://github.com/cyanexttime/Angular-jenkins-test.git'
            }
        }
        stage('Install dependencies') {
            agent{
                label 'built-in'
            }
            steps {
                sh 'npm install'
                sh 'npm install -g @angular/cli'
            }
        }
        
        stage('Build') {
            agent{
                label 'built-in'
            }
            steps {
                sh 'export $(cat .env | xargs)'
                sh 'echo "Building for ENV=$ENV"'
                sh 'ng build'
                sh 'zip -r angular-dist-of-${ENV}.zip dist/'
                archiveArtifacts artifacts: "angular-dist-of-${ENV}.zip"
            }
        }

        stage('Test')  {
            agent{
                label 'built-in'
            }
            steps {
                sh 'ng test'
            }
        }
    }
}
