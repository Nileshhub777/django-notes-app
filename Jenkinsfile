pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "cloning the code.."
                git branch: 'main', url: 'https://github.com/Nileshhub777/django-notes-app.git'
            }
            
            
        }
        
        stage("Build"){
            steps{
                echo "Building the image."
                sh "docker build -t my-note-app ."
            }
        }
        
        stage("Push to docker hub "){
            steps{
                echo "pushing to the image to docker hub"
                 withCredentials([usernamePassword(credentialsId: 'myId', passwordVariable: 'dockerHubPass', usernameVariable: 'dockerHubUser')]) {
                 sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                 sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }

            }
        }
        
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
}

    
}
