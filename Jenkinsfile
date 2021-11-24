node {    
      def app     
      stage('Clone repository') {               
             
            checkout scm    
      }     
      stage('Build image') {         
       
            app = docker.build("ervisa/backend_locally")    
       }     
      stage('Test image') {           
            app.inside {            
             
             sh 'echo "Tests passed"'        
            }    
        }     
       stage('Push image') {
       docker.withRegistry('https://index.docker.io', 'dockerhub') {            
       app.push("${env.BUILD_NUMBER}")                  
              }    
           }
        }
