pipeline {
    agent {
        docker {
            image 'golang:1.23'
            //label 'golang:1.23'
            //registryCredentialsId 'myPredefinedCredentialsInJenkins'
        }
    }
    stages {
        stage('Test') {
            steps {
                // sh 'node --eval "console.log(process.platform,process.env.CI)"'
                script {
                    sh 'go test -v ./01-normal'
                }
            }
        }
    }
}
