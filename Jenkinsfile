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




    }


}