pipeline {
    agent any
     stages {
        stage('BRAKEMAN') {
            steps {
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error --color'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error --color -o /dev/stdout -o output1.json'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman  --no-exit-on-warn --no-exit-on-error -o output.html -o output.json'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error -o brakeman_results.html'
                sh ' docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error -c ./brakeman.yml  -o brakeman_results2.html'
            }
        post {
         always {
                 recordIssues tools: [
                      brakeman(id: 'brakeman1', pattern: 'output.json'),
                      brakeman(id: 'brakeman2', pattern: 'output1.json')
                    ]
                 publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '/var/lib/jenkins/workspace/BRAKEMAN',
                    reportFiles: 'brakeman_results.html',
                    reportName: 'BRAKEMAN1'
                    ])
                 publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '/var/lib/jenkins/workspace/BRAKEMAN',
                    reportFiles: 'brakeman_results2.html',
                    reportName: 'BRAKEMAN2'
                    ])
                }
            }
        }
    }
}
