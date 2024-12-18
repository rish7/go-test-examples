pipeline {
    agent none
    stages {
            stage('Test') {
                agent {
                    docker {
                        image 'golang:1.23'
                        //label 'golang:1.23'
                        //registryCredentialsId 'myPredefinedCredentialsInJenkins'
                    }
                }
            steps {
                // sh 'node --eval "console.log(process.platform,process.env.CI)"'
                script {
                    //Normal coverage profile
                    sh 'go mod tidy'
                    sh 'go test -v -coverprofile cover.out ./...'
                    sh 'go tool cover -html cover.out -o cover.html'
                    // go cover treemap
                    sh 'go install github.com/nikolaydubina/go-cover-treemap@latest'
                    sh 'go-cover-treemap -coverprofile cover.out > out.svg'
                    archiveArtifacts artifacts: 'cover.html', fingerprint: true
                    archiveArtifacts artifacts: 'out.svg', fingerprint: true
                    //junit
                    try {
                        sh 'go install github.com/jstemmer/go-junit-report/v2@latest'
                        sh 'go test -json 2>&1 -v ./... | go-junit-report -parser gojson > report.xml'
                    } finally {
                        if (fileExists('report.xml')) {
                            junit 'report.xml'
                        }
                    }
                }
            }
        }
    }
}
