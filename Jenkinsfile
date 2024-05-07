pipeline{
    agent {label 'master'}
    tools{
        jdk 'java17'
        maven 'Maven3'
    }
    environment{
        APP_NAME = 'Projet-devsecops'
        RELEASE_VERSION = '1.0.0'
        DOCKER_USER = 'brahim02'
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = 'brahim02/projet-devsecops'
        IMAGE_TAG = "${RELEASE_VERSION}-${BUILD_NUMBER}"
    }
    stages{
        stage("nettoyage"){
            steps{
                cleanWs()
            }
        }
        stage("Checkout SCM"){
            steps{
                git branch: 'master' , credentialsId: 'github' , url: 'https://github.com/brahimlansari/project_devsecops.git'
            }
        }
        stage("Build"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("Test"){
            steps{
                sh 'mvn test'
            }
        }
        stage('SonarQube analysis') {
                    steps {
                        withSonarQubeEnv('SonarCloud') {
                            sh 'mvn sonar:sonar -Dsonar.projectKey=brahimlansari -Dsonar.organization=brahimlansari -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=e79d8bbefe10385340dc71969d98f8a9db237c39'
                        }
                    }
        }
        stage("Build & Push Docker Image"){
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_PASS){
                        docker_image = docker.build("${IMAGE_NAME}")
                    }

                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_PASS){
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push("latest")
                    }

                }
            }
        }




    }

}