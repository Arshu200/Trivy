pipeline {
        agent any
        environment {
            DOCKER_IMAGE = 'arshad200/trivy'
        }
    
        stages {
            stage('Checkout') {
                steps {
                    checkout scm
                }
            }
    
            stage('Docker Build') {
                steps {
                    script {
                        sh "sudo docker build -t ${DOCKER_IMAGE}:${env.BUILD_ID} ."
                        echo "Docker image build successfully"
                        sh "sudo docker images"
                }
            }
            }

        stage("TRIVY"){
            steps{
                catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
                    sh "trivy image --no-progress --exit-code 1 --severity LOW,MEDIUM,HIGH,CRITICAL --format table ${DOCKER_IMAGE}:${env.BUILD_ID}"
                 }   
            }
        }   
        }
    }
