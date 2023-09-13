
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
                    runPipeline(environmentName, lambdaName)
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
                    runPipeline(environmentName, lambdaName)
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
                    runPipeline(environmentName, lambdaName)
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
                    runPipeline(environmentName, lambdaName)
                }
            }
        }
    }
}

def runPipeline(environmentName, lambdaName)
{
   if ("$environmentName" == 'dev' )
    {
            sh "mv my_deployment.zip ${environmentName}_deployment.zip"
            withCredentials([string(credentialsId: 'access_key', variable: 'ACCESS_KEY'), string(credentialsId: 'secret_key', variable: 'SECRET_KEY')]) {
				sh "aws lambda update-function-code --function-name ${lambdaName} --zip-file fileb://./${environmentName}_deployment.zip"
			}
    }
	if ("$environmentName" == 'qa' )
    {
            sh "mv my_deployment.zip ${environmentName}_deployment.zip"
            withCredentials([string(credentialsId: 'access_key', variable: 'ACCESS_KEY'), string(credentialsId: 'secret_key', variable: 'SECRET_KEY')]) {
				sh "aws lambda update-function-code --function-name ${lambdaName} --zip-file fileb://./${environmentName}_deployment.zip"
			}
    }
	if ("$environmentName" == 'staging' )
    {
            sh "mv my_deployment.zip ${environmentName}_deployment.zip"
            withCredentials([string(credentialsId: 'access_key', variable: 'ACCESS_KEY'), string(credentialsId: 'secret_key', variable: 'SECRET_KEY')]) {
				sh "aws lambda update-function-code --function-name ${lambdaName} --zip-file fileb://./${environmentName}_deployment.zip"
			}
    }
	if ("$environmentName" == 'master' )
    {
            sh "mv my_deployment.zip ${environmentName}_deployment.zip"
            withCredentials([string(credentialsId: 'access_key', variable: 'ACCESS_KEY'), string(credentialsId: 'secret_key', variable: 'SECRET_KEY')]) {
				sh "aws lambda update-function-code --function-name ${lambdaName} --zip-file fileb://./${environmentName}_deployment.zip"
			}
    }
}

