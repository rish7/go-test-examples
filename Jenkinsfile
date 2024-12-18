pipeline {
    agent {
        docker {
            image 'node:latest'
            //label 'node-22.12.0'
            //registryCredentialsId 'myPredefinedCredentialsInJenkins'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --eval "console.log(process.platform,process.env.CI)"'
            }
        }
    }
}
