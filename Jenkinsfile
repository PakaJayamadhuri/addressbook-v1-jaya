pipeline{
    agent any

    parameters {
        string(name: 'Env', defaultValue: 'Test', description: 'version to deploy')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'decide to run it?')
        choice(name: 'APPVERSION', choices: ['1.1', '1.2'])
    }
    stages {
        stage('Compile') {
            steps {

                script {
                    echo "Compiling the code"
                    echo "Compiling in ${params.Env}"
                    sh "mvn compile"
                }
            }
        }

        stage("CodeReview") {
            steps {
                script {
                    echo "Code Review Using pmd plugin"
                    sh "mvn pmd:pmd"
                }
            }
        }
        stage('UnitTest') {
            when {
                expression { params.executeTests == true }
            }
            steps {
                script {
                    echo "UnitTest in junit"
                    sh "mvn test"
                }
            }
        }

        stage("CodeCoverage"){
            steps {
                script {
                    echo "Code Coverage using jacoco"
                    sh "mvn verify"
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    echo "Packaging the code"
                    sh "mvn package"
                }
            }
        }

        stage('PublishtoJFrog') {
            steps {
                script {
                    echo "Publish to JFrog"
                    sh "mvn deploy -U -s settings.xml"
                }
            }
        }
    }
}