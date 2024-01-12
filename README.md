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