pipeline {
    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('sleep20') {
                    steps {
                        sleep 20
                    }
                }
                stage('sleep10') {
                    steps {
                        sleep 10
                    }
                }
            }
        }
    }
}
