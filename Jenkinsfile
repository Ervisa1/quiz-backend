pipeline {
      agent any
      environment {
            Service = "quiz-backend"
            Repo_TAG = "${dockerhubname}/${Service}:${BUILD_ID}"
      }
      stages {
            stage('Cloning the repository') {
                  steps {
                        git credentialsId: 'Github', url: "https://github.com/${githubname}/${Service}"
                  }
            }
            stage('Build') {
                  steps {
                        sh 'docker image build -t ${Repo_TAG} .'
                  }
            }
            stage('Push to the docker hub registry') {
                  steps {
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                              $(Repo_TAG).push()
                        }
                  }
            }
      }
}



                        
                  
   
      
