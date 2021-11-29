pipeline {

    agent {
        node {
            label 'test'
        }
    }

    options {
        buildDiscarder logRotator(
                    daysToKeepStr: '16',
                    numToKeepStr: '10'
            )
    }
    parameters {
        string(name: 'DEPLOY_ARTIFICATE_VERSION', defaultValue: 'latest', description: 'Specify the artificate to deploy, defaults to latest')
        string(name: 'ENVIRONMENT_TAG', defaultValue: 'latest', description: 'Specify the artificate to deploy, defaults to latest')
        choice(name: 'START_FROM_STAGE', choices: ['Validate', 'Build', 'Deploy QA', 'Deploy PERF JP', 'Deploy PROD'], description: 'Build starting from the stage')
        choice(name: 'FORCE_RUN', choices: ['no', 'yes'], description: 'Force build if the packer images already exist (yes/no)')
        booleanParam(name: 'ENABLE_WORKER_ROLE', defaultValue: true, description: 'Enable worker role or not against non production environments')
    }

    stages {

        stage('Cleanup Workspace') {
            steps {
                sh """
                echo "Cleaned Up Workspace For Project"

                """
                print params.DEPLOY_ARTIFICATE_VERSION
                print params.ENVIRONMENT_TAG
                print params.START_FROM_STAGE
                print params.FORCE_RUN
                print params.ENABLE_WORKER_ROLE
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis" > testfile
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }
}
