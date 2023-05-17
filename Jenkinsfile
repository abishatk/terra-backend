pipeline {

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
    } 
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

   agent  any
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/abishatk/terra-backend.git']]])
            }
        }

        stage ("terraform init") {
            steps {
                bat ("terraform init -reconfigure") 
            }
        }
        
        stage ("plan") {
            steps {
                bat ('terraform plan') 
            }
        }

        stage (" Action") {
            steps {
                bat ('terraform ${action} --auto-approve') 
           }
        }
    }
}
    