pipeline {

    agent any

    environment {
        SOLUTION_FILE = 'SeleniumBasicExercise.sln'
        TEST_PROJECT_2_PATH = 'TestProject2/TestProject2.csproj'
        TEST_PROJECT_3_PATH = 'TestProject3/TestProject3.csproj'
    }

    stages {
        stage('Checkout repo') {
            steps {
                checkout scm
            }
            
        }

        stage('Restore Dependencies') {
            steps {
                bat "dotnet restore ${SOLUTION_FILE}"
            }
        }

        stage('Build') {
            steps {
                bat "dotnet build ${SOLUTION_FILE} --no-restore"
            }
            
        }

        stage('Run tests') {
            parallel {
                stage('TestProject2') {
                    steps {
                        bat "dotnet test ${TEST_PROJECT_2_PATH} --no-build"
                    }
                }

                stage('TestProject3') {
                    steps {
                        bat "dotnet test ${TEST_PROJECT_3_PATH} --no-build"
                    }
                }

            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        unstable {
            echo 'Tests failed!'
        }

    }

}