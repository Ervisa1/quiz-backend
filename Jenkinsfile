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
                        withDockerRegistry (credentialsId: 'dockerhub-auth', url: "https://registry-1.docker.io/v2/") {
                              sh 'docker push ${Repo_TAG}'
                        }
                  }
             }
            stage('Deploy to Cluster') {
                  steps {
                        sh 'envsubst < ${WORKSPACE}/backend.yaml | kubectl apply -f -'
                  }
            }
      }
}



                        
                  
   
      
