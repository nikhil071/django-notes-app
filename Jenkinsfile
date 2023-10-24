pipeline{
    agent any
    
    stages{
        
        stage("code clone"){
            steps{
                 echo "cloning the code"
                 git url: "https://github.com/nikhil071/django-notes-app.git", branch: "main"
                
                
            }
            
        }
        stage("Build"){
            steps{
                
                echo "Building the code"
                sh "docker build -t my-notes-app ."
            }
            
            
        }
        stage("push-to-docekr-hub"){
            steps{
                 echo "push to docker hub"
                 withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                     sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                     sh "docker push ${env.dockerHubUser}/my-notes-app:latest "
                 }
                 
            }
            
        }
        stage("Deploy"){
            steps{
                 echo "deploying the code to hte container"
                 sh "docker-compose down && docker-compose up -d"
                
            }
            
            
        }
    }
}
