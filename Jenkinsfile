pipeline{
    agent any 
      stages{
        stage("Code clone"){
            steps{
                sh "whoami"
            clone("https://github.com/ManishSingh-01/two-tier-flask-app.git","main")
            }
        }
        stage("Code Build"){
            steps{
            dockerbuild("notes-app","latest")
            }
        }
        stage("Push to DockerHub"){
            steps{
                dockerpush("dockerHubCreds","notes-app","latest")
            }
        }
        stage("Deploy"){
            steps{
                deploy()
            }
        }
        
    }
}
