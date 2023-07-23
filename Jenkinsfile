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
            }
            steps {
                
                script {
                    dir('src') {
                        sh 'terraform init'
                        sh 'terraform apply --auto-approve'
                    }
                }
            }
        }
    }

}