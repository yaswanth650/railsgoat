pipeline {
    agent any
     stages {
        stage('BRAKEMAN') {
            steps {
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error --color'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error --color -o /dev/stdout -o output.json'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman  --no-exit-on-warn --no-exit-on-error -o output.html -o output.json'
                sh 'docker run -v "$(pwd)":/code presidentbeef/brakeman --no-exit-on-warn --no-exit-on-error -o brakeman_results.html'
            }
        }
    }
}
