pipeline {
    agent any
    
    tools {
      nodejs 'nodejs21'
    }

    stages {
        
        stage('Checkout') {
            steps {
                git branch: 'main', url: "https://github.com/MM1132/KoodJohviCICD.git"
                echo "/kj_deployments/robert_${env.BRANCH_NAME}"
            }
        }

        stage('Install and Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh "mkdir -p /kj_deployments/robert_${env.BRANCH_NAME}"
                sh "mv dist/kood-johvi-cicd/browser/* /kj_deployments/robert_${env.BRANCH_NAME}"
            }
        }
    }

    post {
        always {
            discordSend description: "Jenkins Pipeline Build", 
            footer: "Status: ${currentBuild.currentResult}", 
            link: env.BUILD_URL, 
            result: currentBuild.currentResult, 
            title: env.JOB_NAME, 
            webhookURL: "https://discord.com/api/webhooks/1181556979337003029/1kbPvVQZqTNlD362WyMQjTPlGUPdMBTSqA6BWtkELZdRlOV_s9jfC9YwSp-6x89XGMKq"
        }
        
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed. Please check the logs for details.'
        }
    }
}
