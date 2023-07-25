pipeline {
    agent any

    stages {

        stage('Checkout source') {
            steps {
                git url: 'https://github.com/fabricioveronez/teste-jenkins.git', branch: 'main'
            }
        }

        stage('Criação ou atualização da infra') {
            environment {
                AWS_ACCESS_KEY_ID  = credentials('AWS_ACCESS_KEY_ID ')
                AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
                AWS_DEFAULT_REGION = credentials('AWS_DEFAULT_REGION')
                AWS_BUCKET = credentials('AWS_BUCKET')
                AWS_BUCKET_KEY = credentials('AWS_BUCKET_KEY')
            }
            steps {
                
                script {
                    dir('src') {
                        sh 'terraform init -reconfigure -backend-config="bucket=$AWS_BUCKET" -backend-config="key=$AWS_BUCKET_KEY"'
                        sh 'terraform apply --auto-approve -var="vpc_name=teste"'
                    }
                }
            }
        }
    }

}
