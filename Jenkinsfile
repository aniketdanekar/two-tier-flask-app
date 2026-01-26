pipeline{
    
    agent any;
    stages{
        stage("Code"){
            steps{
              git url: "https://github.com/LondheShubham153/two-tier-flask-app.git", branch: "master" 
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test"){
            steps{
                echo "Tester Will give the test commands.."
            }
        }
        stage("Push To Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: "dockerhubcreds",
                                                  passwordVariable: "dockerHubPass",
                                                  usernameVariable: "dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app:latest"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
