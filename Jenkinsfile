pipeline{
    agent any;
    
    stages{
        stage("Code Clone"){
            steps{
                git url: "https://github.com/mohdayan123/jenkins-cicd-project.git", branch: "main"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test Case"){
            steps{
                echo "Test Checking Code. "
            }
        }
        stage("Docker Hub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId: "dockerHubCreds",
                usernameVariable: "dockerHubUser",
                passwordVariable: "dockerHubPass"
                )]){
                    
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
            sh "docker push ${env.dockerHubUser}/two-tier-flask-app"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
