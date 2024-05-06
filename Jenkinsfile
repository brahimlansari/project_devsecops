pipeline{
    agent {label 'master'}
    tools{
        jdk 'java17'
        maven 'Maven3'
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
                            sh 'mvn sonar:sonar
                            -Dsonar.projectKey=brahimlansari_project_devsecops
                            -Dsonar.organization=brahimlansari-github
                            -Dsonar.host.url=https://sonarcloud.io
                            -Dsonar.login=e79d8bbefe10385340dc71969d98f8a9db237c39
                        }
                    }
        }




    }

}