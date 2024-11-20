pipeline {
    agent any
    
    stages{
        stage("Clone code"){
            steps {
                echo "Cloning the code"
                git url: "https://github.com/Zub93-S/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("push to Docker Hub"){
            steps {
                echo"Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable:"dockerHubpass", usernameVariable:"dockerHubUser")]) {
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubpass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker run -d -p 8000:8000 zuber20j03/my-note-app:latest"
            }
        }
    }
}
    
        
        
    
