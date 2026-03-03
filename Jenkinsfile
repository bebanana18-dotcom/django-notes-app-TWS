@Library("Shared") _
pipeline {
    agent { label 'agent'}

    stages {
        stage('Hello') {
            steps{
                script{
                    hello()
                }
            }
        }
        stage('code clone') {
            steps {
                // echo 'this is cloning code'
                // git url: "https://github.com/bebanana18-dotcom/django-notes-app-TWS.git",branch: "dev"
                // echo 'code clone complete'
                script{
                    clone("https://github.com/bebanana18-dotcom/django-notes-app-TWS.git" , "dev")
                }
            }
        }
        stage('code Build') {
            steps {
                echo 'building code'
                // sh 'docker build -t notes-app:latest .'
                script{
                    docker_build("notes-app" , "latest" , "himanshumaurya1920")
                }
                echo 'build complete'
            }
        }
        stage('PUSH-TO-DOCKER-HUB') {
            steps {
                echo 'pushing to docker-hub registry after-renaming'
                // withCredentials([usernamePassword(
                //     credentialsId:"dockerHubCredential",
                //     usernameVariable:"dockerHubUser",
                //     passwordVariable:"dockerHubPass")]){
                        
                //         sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass} "
                //         sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                //         sh "docker push ${env.dockerHubUser}/notes-app:latest"
                //     }
                script{
                    docker_push("notes-app" , "latest" , "himanshumaurya1920")
                }
                echo 'test complete'
            }
        }
        stage('code deploy') {
            steps {
                echo 'code deploying'
                // sh 'docker compose down && docker compose up -d --build'
                script{
                    docker_compose()
                }
                echo 'code deployed successfully '
            }
        }
    }
}
