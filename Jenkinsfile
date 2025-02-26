pipeline
{
    
    agent any;
    stages{
        stage("Code Clone"){
            steps{
                git url:"https://github.com/Mahesh199811/two-tier-flask-app.git", branch:"master"
                
            }
        }
         stage("Code Build"){
            steps{
                sh "docker build -t maheshgadhave82/flask-app:latest ."
                
            }
        }
         stage("Code testing"){
            steps{
                echo "Testing"
            }
        }
         stage("Code push to Docker"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"dockerHubCreds",
                passwordVariable:"dockerHubPass",
                usernameVariable:"dockerHubUser")]){
                    
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag flask-app ${env.dockerHubUser}/flask-app"
                sh " docker push ${env.dockerHubUser}/flask-app:latest"
                }
            }
        }
         stage("Code Deploy"){
            steps{
               sh "docker compose up -d --build"
            }
        }
    }
}
