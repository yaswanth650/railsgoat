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
                      brakeman(pattern: 'output.json'),
                      brakeman(pattern: 'output1.json'),
                      brakeman(pattern: 'brakeman_results.html'),
                      brakeman4(pattern: 'brakeman_results2.html')
                    ]
                }
            }
        }
    }
}