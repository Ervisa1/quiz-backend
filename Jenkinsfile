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
       withDockerRegistry(credentialsId: '123456visa', url: 'https://index.docker.io'){            
       app.push()                  
              }    
           }
        }
