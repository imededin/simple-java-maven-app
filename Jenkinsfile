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
             when {
                branch '*/master'
            }
            
            steps{
              
                sh 'mvn package'
            }
        }
        stage("build docker image"){
            steps{
                echo "building image..."
                withCredentials([usernamePassword(credentialsId: "docker-cre",passwordVariable: 'PASS',usernameVariable: 'USER')]){
                    sh "docker build -t $USER/demo:2.0 ."
                    sh "docker login -u $USER -p $PASS"
                    sh "docker push imed1/demo:2.0"
                }
            }
        }
    }
}
