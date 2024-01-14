pipeline {

    agent any

    stages {

        stage("configure") {
            steps {
                echo "Create python environment"
            }
        }

        stage("build") {
            steps {
                echo "build the app"
            }
        }

        stage("test") {
            steps {
                echo "Testing the application"
            }
        }

        stage("after") {
            steps {
                echo "After every step"
            }
        }

    }
}