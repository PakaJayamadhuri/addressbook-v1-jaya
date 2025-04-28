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
                echo "Deploying in ${params.Env} environment"
            }
        }
        stage('UnitTest') {
            when {
                expression { params.executeTests == true }
            }
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying version ${params.APPVERSION}"
            }
        }
    }
}