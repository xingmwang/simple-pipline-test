pipeline {

    agent {
        node {
            label 'master'
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
        choice(name: 'START_FROM_STAGE', choices: 'Validate\nBuild\nDeploy QA\nDeploy PERF JP\nDeploy PROD', description: 'Build starting from the stage')
        choice(name: 'FORCE_RUN', choices: 'no\nyes', description: 'Force build if the packer images already exist (yes/no)')
        booleanParam(name: 'ENABLE_WORKER_ROLE', defaultValue: true, description: 'Enable worker role or not against non production environments')
    }
  //  triggers {
  //       upstream(upstreamProjects: 'multibranch-pipeline-demo/develop', threshold: hudson.model.Result.SUCCESS)
  //  }

    stages {

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"

                """
                print params.DEPLOY_ARTIFICATE_VERSION
                print param.ENVIRONMENT_TAG
                print params.START_FROM_STAGE
                print params.FORCE_RUN
                print params.ENABLE_WORKER_ROLE
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                sleep 3
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
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
