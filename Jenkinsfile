pipeline {

    agent any


    parameters {

        string(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'Environment to deploy to')

        booleanParam(name: 'RUN_TESTS', defaultValue: 'true', description: 'Run tests?')

        choice(name: 'DEPLOY_SERVER', choices: ['dev', 'test', 'prod'], description: 'Choose deployment server')

    }


    stages {

        stage('Dev Stage') {

            steps {

                echo "Deploying to ${params.ENVIRONMENT} environment"

            }

        }

        stage('Test Stage') {

            when
    {
    
                    expression { params.RUN_TESTS == true }
    
                }
            steps {

                echo 
                    "Running tests in ${params.ENVIRONMENT} environment"

                }

            }

        }

        stage('Prod Stage') {

            steps {

                script {

                    if (params.DEPLOY_SERVER == 'prod') {

                        echo "Deploying to production server"

                    } else {

                        echo "Deploying to ${params.DEPLOY_SERVER} server"

                    }

                }

            }

        }

}

