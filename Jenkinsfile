pipeline{
    agent any 
    tools{
        maven "maven-3.8"
    }
    stages{
        stage("fetch"){
            steps{
                git credentialsId: 'git-token', url: 'https://github.com/imededin/simple-java-maven-app.git'
            }

        }
        stage("build"){
            steps{
                sh 'mvn package'
            }
        }
    }
}