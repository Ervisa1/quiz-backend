pipeline {
      environment {
            Service = "quiz-backend"
            Repo_TAG = "${dockerhubname}/${Service}:${BUILD_ID}"
      agent { 
            docker {
                  image 'ervisa/backend_locally:11'
                  registryUrl 'https://ervisa/backend_locally'
                  registryCredentialsId 'dockerhub-auth'
                  args '-v /var/jenkins/.m2:/root/.m2'
            }
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
            stage('Push image') {
                  steps {
                        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-auth') {            
                              Repo_TAG.push("${env.BUILD_ID}")            
                        }
                  }
            }
             stage('Push to the docker hub registry') {
                  steps {
                        withDockerRegistry (credentialsId: 'dockerhub-auth', url: "https://index.docker.io/v1/") {
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



                        
                  
   
      
