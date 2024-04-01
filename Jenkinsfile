pipeline{
    agent{ label 'Jenkins-Agent'}
    tools{
        jdk 'Java17'
        maven 'Maven3'
    }
    stages{
        stage("nettoyage){
            steps{
                netoyer()
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

    }


}