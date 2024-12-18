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
                    sh 'go test -v -coverprofile cover.out ./01-normal'
                    sh 'go tool cover -html cover.out -o cover.html'
                    sh 'cat cover.html'
                    archiveArtifacts artifacts: 'cover.html', fingerprint: true
                }
            }
        }
    }
}
