@Library("shared-libraries") _

pipeline {

	agent any

    stages {
        stage('Build') {
            steps {
                 sh "zip my_deployment.zip lambda_function.py"
            }
        }
        stage('Deliver for development') {
            when {
                branch 'dev'
            }
            steps {
                script
                {
                    environmentName = "dev"
                    lambdaName = "dev_function"
                    lambda1.runPipeline(environmentName, lambdaName)
                }
            }
        }
        stage('Deploy for qa') {
            when {
                branch 'qa'
            }
            steps {
                script
                {
                    environmentName = "qa"
                    lambdaName = "qa_function"
                    lambda1.runPipeline(environmentName, lambdaName)
                }
            }
        }
		stage('Deploy for staging') {
            when {
                branch 'staging'
            }
            steps {
                script
                {
                    environmentName = "staging"
                    lambdaName = "staging_function"
                    lambda1.runPipeline(environmentName, lambdaName)
                }
            }
        }
		stage('Deploy for production') {
            when {
                branch 'master'
            }
            steps {
                script
                {
                    environmentName = "master"
                    lambdaName = "master_function"
                    lambda1.runPipeline(environmentName, lambdaName)
                }
            }
        }
    }
}


