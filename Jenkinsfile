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
            when{
                expression{
                    BRANCH_NAME=="master"
                }
            }
            steps{
                sh 'mvn package'
            }
        }
        stage("build docker image"){
            steps{
                echo "building image..."
                withCredentials([usernamePassword(credentialsId: "docker-cre",passwordVariable: 'PASS',usernameVariable: 'USER')]){
                    docker build -t imed1/demo:2.0 .
                    docker login -u $USER -p $PASS
                    docker push imed1/demo:2.0
                }
            }
        }
    }
}