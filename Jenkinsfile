       properties([parameters([choice(choices: 'Dev\nQa\nProd', description: 'Select the branch name', name: 'branch')])])
pipeline {
    agent any
    stages {
        stage('checkout SCM'){
            steps{
                echo "Fetching changes from selected ${params.branch} branch"
                git url:'https://gitlab.com/indie3/jenkins.git', branch: "$params.branch"
            }
        }
        stage('test AWS credentials') {
            steps {
                withAWS(credentials: 'get1', region: 'us-east-1') {
                    sh 'aws secretsmanager list-secrets'
                }
            }
        }
    }
}
    
