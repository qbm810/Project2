pipeline{
      
    tools{
        maven 'mymaven'
    }
    
    
    agent any
    
     environment { 

        registry = 'https://hub.docker.com/repository/docker/qbm810/project2/' 

        registryCredential = 'Hub' 
        
    }
    stages{
        
        stage('Checkout Code'){
            steps{
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        
        
        stage('Build Code'){
            steps{
                sh 'mvn package'
                
            }
        }
        
        
        stage('Copy Build'){
            steps{
                sh 'cp /var/lib/jenkins/workspace/Project2/target/addressbook.war .'
            }
        }
        
        
        stage('Build Image'){
            steps{
                sh 'docker build -t project2:$BUILD_NUMBER .'
            }
        }
        
        
        stage('Push image to dockerhub'){
            steps{ 
                script{
                           
                    docker.withRegistry( '', registryCredential ) {    
                      sh 'docker push qbm810/project2:$BUILD_NUMBER'
                      }
                    }
            }
        }
        stage('Continuous Deployment'){
            steps{
                sh 'docker run -d -P project2:$BUILD_NUMBER'
            }
        }
  }
}
