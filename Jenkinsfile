pipeline {
      agent any
      environment {
            Service = "quiz-backend"
            Repo_TAG = "${dockerhubname}/${githubname}-${Service}:${BUILD_ID}"
      }
      stages {
            stage('Cloning the repository') {
                  steps {
                        git credentialsId: '', url: "https://github.com/${githubname}/${Service}"
                  }
            }
            stage('Build') {
                  steps {
                        sh 'docker image build -t %{Repo_TAG} .'
                  }
            }
      }
}
                        
                  
   
      
