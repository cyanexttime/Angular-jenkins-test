pipeline{
    agent any
	
    tools{
        nodejs 'NODE22'
    }

    // parameters {
    //     choice(
    //         name: 'ENV',
    //         choices: 'dev\npreprod\nprod',
    //         description: 'Select environment'
    //     )
    // }

    stages{
        stage('Fetch code') {
            // agent{
            //     label 'built-in'
            // }
            steps{
                git branch: 'main', url: 'https://github.com/cyanexttime/Angular-jenkins-test.git'
            }
        }
        stage('Install dependencies') {
            // agent{
            //     label 'built-in'
            // }
            steps {
                sh 'npm install'
                sh 'npm install @angular/cli'
            }
        }
        
        stage('Build') {
            // agent{
            //     label 'built-in'
            // }
            steps {
                echo "Branch name: ${env.BRANCH_NAME}"
                sh 'ng build'
                sh 'zip -r angular-dist-of-${env.BRANCH_NAME}.zip dist/'
                archiveArtifacts artifacts: "angular-dist-of-${env.BRANCH_NAME}.zip"
            }
        }

        stage('Test')  {
            // agent{
            //     label 'built-in'
            // }
            steps {
                sh 'ng test'
            }
        }
    }
}
