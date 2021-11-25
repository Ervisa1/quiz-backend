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
            stage('Deploy to Cluster') {
                  steps {
                        sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
                  }
            }
      }
}



                        
                  
   
      
