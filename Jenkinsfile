pipeline {
    agent { label 'docker' }
    environment {
        S3_RESOURCES_CREDENTIALS = credentials('S3_RESOURCES_CREDENTIALS')
    }

    stages {
        stage('upload') {
            agent {
                docker {
                    image 'amazon/aws-cli:2.13.12'
                    args """
                    -e AWS_ACCESS_KEY_ID=${S3_RESOURCES_CREDENTIALS_USR}
                    -e AWS_SECRET_ACCESS_KEY=${S3_RESOURCES_CREDENTIALS_PWD}
                    -v ${PWD}:/aws s3 cp zalando.yml s3://resources.exentra.io
                    """
                    reuseNode true
                }
            }
        }
    }
}