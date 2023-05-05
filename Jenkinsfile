pipeline{
    agent { label 'agent-node1'}
    stages{
        stage('Clone Code...'){
            steps{
                git url: 'https://github.com/Anuj7495/django_todo_project.git', branch: 'master'
            }
        }
        stage('Build and test Code...'){
            steps{
                sh 'docker build . -t anujsaini/todo-app:latest'
            }
        }
        stage('Login and push image to dockerhub'){
            steps{
                echo 'logging into docker hub and pushing image'
                withCredentials([usernamePassword(credentialsId:'DockerHub',passwordVariable:'DockerhubPassword',usernameVariable:'dockerhubUser')]){
                    sh "docker login -u ${env.dockerhubUser} -p ${env.DockerhubPassword}"
                    sh "docker image push anujsaini/todo-app:latest"
                }
            }
        }
        stage('Deploy Code.. '){
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d --no-deps --build'
            }
        }
    }
}
