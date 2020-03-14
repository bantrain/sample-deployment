pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']
                ]) {
                    setupGithubSSH()
                    sh "AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID} AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY} AWS_DEFAULT_REGION=eu-west-1"
                    sh "aws eks --region ${env.CLUSTER_REGION} update-kubeconfig --name ${env.CLUSTER_NAME}"
                    sh 'helm upgrade --atomic --install chart ./chart'
                }
            }
        }
    }
}