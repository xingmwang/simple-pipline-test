pipeline {
    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                    steps {
                        sleep 120
                    }
                }
                stage('Test On Linux') {
                    steps {
                        sleep 180
                    }
                }
            }
        }
    }
}
