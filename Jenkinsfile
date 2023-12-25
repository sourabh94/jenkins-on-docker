pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                
                script{
                    sh 'rm -rf * && rm -rf .git'
                    sh 'git clone https://github.com/sourabh94/jenkins-on-docker.git .'
                    sh 'ls -la'
                    sh 'docker build -t testimage -f Dockerfile.sample .'
                }
            }
            
        }
        
        stage('Push'){
            steps {
                
                script{
                    
                    withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'pass', usernameVariable: 'user')]) {
                        // the code here can access $pass and $user
                        sh 'docker login -u $user -p $pass '
                    }
                    
                    sh 'docker tag testimage devopskey/jenkins-sample'
                    sh 'docker push devopskey/jenkins-sample'
                    
                    
                }
            }
        }
        
    }
}
