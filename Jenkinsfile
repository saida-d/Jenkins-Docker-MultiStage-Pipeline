pipeline{
  // if you want to run jenkins master/slave architecture just make this value none 
  // and proceed required slave labels further  
  agent none
  
  stages{
      
    stage('Checkout'){
        // execute in staging node, make sure you have configured jenkins master/slave architecture
        agent {label 'Staging'}
        steps{
            git branch: 'main', url: 'https://github.com/saidasoft/Jenkins-Docker-MultiStage-Pipeline.git'
        }
        
    }
    stage('Build'){
        // execute in staging node, make sure you have configured jenkins master/slave architecture
        agent {label 'Staging'}
        steps{
            sh 'docker rm -f $(docker ps -a -q)'
            sh 'docker build /home/ec2-user/jenkins_node_02/workspace/Webapp-Multi-Stage-Groovy/ -t mywebapp'
            echo "Build completed"
        }
    }
    stage('Test'){
        // execute in staging node, make sure you have configured jenkins master/slave architecture
        agent {label 'Staging'}
        steps{
            sh 'docker run -it -d -p 80:80 mywebapp'
            echo "Ready to test"
        }
    }
    stage('Production Deploy'){
        // execute in production node, make sure you have configured jenkins master/slave architecture
        agent {label 'Production'}
        steps{
            // checkout same code
            git branch: 'main', url: 'https://github.com/saidasoft/Jenkins-Docker-MultiStage-Pipeline.git'
            
            // execute above steps together here
            sh 'docker rm -f $(docker ps -a -q)'
            sh 'docker build /home/ec2-user/jenkins_node_01/workspace/Webapp-Multi-Stage-Groovy/ -t myprodwebapp'
            sh 'docker run -it -d -p 80:80 myprodwebapp'
            echo "Deploy in production"
        }
    }
  }

}
