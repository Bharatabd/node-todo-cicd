pipeline{
     agent any
    
    stages{
        stage("Code Clone"){
            steps{
                echo "Code Clone Stage"
                git url: "https://github.com/Bharatabd/node-todo-cicd.git", branch: "master"
            }
        }
         stage("Install Dependencies"){
            steps{
                echo "installing dependencies"
                sh "npm install"
            }
        }
         stage("Run Tests"){
            steps{
                sh "npm test"
            }
        }
        stage("Code Build"){
            steps{
                echo "Code Build Stage"
                sh "docker build -t node-app ."
            }
        }
        stage("Push To DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockeHubCred",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker image tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d --build"
            }
        }
    }
}
