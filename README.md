# Jenkins File Syntax

## Items To Learn

1.  Jenkins File Structure
2.  Jenkins Pipeline Structre
3.  Jenkins Pipeline Django

## Jenkins Installation Process

## Jenkins File Template

```
pipeline {

    agent any

    stages {

        stage("Create python environment") {
            steps {
                
            }
        }

    }
}
```

## Scoping In Jenkins

Scoping per stage is also applicable in Jenkins

```
pipeline {
    agent any
    environment {
        RELEASE="22.23"
    }

    stages {
        
        stage("Build"){
            agent any
            environment{
                LOG_LEVEL="INFO"
            }
            steps{
                echo "Build release ${RELEASE} on log level ${LOG_LEVEL}"
            }
        }

        stage("Test"){
            steps{
                echo "Testing release ${RELEASE} on absent or invisible log level"
                //  ${LOG_LEVEL}
            }
        }
    }
}
```

## Running Stages In Parallel

```Jenkinsfile

pipeline {
    agent any
    environment {
        RELEASE='20.04'
    }
    stages {
        stage('Build') {
            environment {
                LOG_LEVEL='INFO'
            }
            parallel {
                stage('linux-arm64') {
                    agent any
                    steps {
                        echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}..."
                        sh 'sleep 10'
                    }
                }
                stage('linux-amd64') {
                    agent any
                    steps {
                        echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}..."
                        sh 'sleep 20'
                    }
                }
                stage('windows-amd64') {
                    agent any
                    steps {
                        echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}..."
                        sh 'sleep 30'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo "Testing release ${RELEASE}..."
            }
        }
        stage('Deploy') {
            input {
                message 'Deploy?'
                ok 'Do it!'
                parameters {
                    string(name: 'TARGET_ENVIRONMENT', defaultValue: 'PROD', description: 'Target deployment environment')
                }
            }
            steps {
                echo "Deploying release ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
            }
        }        
    }
    post{
        always {
             echo 'Prints whether deploy happened or not, success or failure'
        }
    }
}

```