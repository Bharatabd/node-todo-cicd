pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
            echo "coding"
            git url: "https://github.com/Bharatabd/react_django_demo_app.git" , branch: "main"
            }
        }
        stage("Build"){
            steps{
                sh 'docker build . -t bharatdocker87/node-todo-test:latest'
            }
        }
        stage("Docker Push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockeHubCred',
                passwordVariable: 'dockerHubPass', usernameVariable: 'dockerHubUser')]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-todo-test:latest"
                }
            }
        }
        stage("Test"){
            steps{
            echo "testing"
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
