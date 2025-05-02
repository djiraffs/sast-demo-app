pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/djiraffs/sast-demo-app.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install --user bandit'
            }
        }

        stage('SAST Analysis') {
            steps {
                sh '~/.local/bin/bandit -f xml -o bandit-output.xml -r . || true'
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}
