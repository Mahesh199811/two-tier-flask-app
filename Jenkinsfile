pipeline
{
    
    agent {label "dev"};
    stages{
        stage("Code Clone"){
            steps{
                git url:"https://github.com/Mahesh199811/two-tier-flask-app.git", branch:"master"
                
            }
        }
         stage("Code Build"){
            steps{
                sh "docker build -t flask-app:latest ."
                
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
    
    post{
        success{
            emailext(
                subject:"Build successful",
                body: "your build is successful",
                to:"maheshgadhave82@gmail.com"
                )
            
        }
        failure{
            emailext(
                subject:"Build Failed",
                body: "Error: Build Failed",
                to:"maheshgadhave82@gmail.com"
                )
            
        }
    }
}
