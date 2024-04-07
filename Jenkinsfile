pipeline{
    tools{
        maven 'mymaven'
    }
    agent any
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
                sh 'cp /var/lib/jenkins/workspace/DockerJenkinsPipeline/target/addressbook.war .'
            }
        }
        stage('Build Image'){
            steps{
               sh 'docker build -t project2:$BUILD_NUMBER .'
            }
        }
        stage('Push image to dockerhub'){
            steps{
                sh 'docker tag project2 edu123/project2:$BUILD_NUMBER'
                sh 'docker login --username edu123 --password Edureka@123'
                sh 'docker push edu123/project2:$BUILD_NUMBER'
            }
        }
        stage('Continuous Deployment'){
            steps{
                sh 'docker run -d -P project2:$BUILD_NUMBER'
            }
        }
    }
}
