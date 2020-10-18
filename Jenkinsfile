pipeline{
    environment {
    registry = "ezhilc/petsapp"
    registryCredential = 'Docker'
    dockerImage=''
    secure = "ssh -oStrictHostKeyChecking=no ec2-user@52.23.206.10"
        }
  agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('Git'){
            steps{
                 git credentialsId: 'Github', url: 'https://github.com/ezhilvirtusa/car-rentals.git'  
            }
        }
        stage('Maven Build'){
            steps{
                sh "mvn clean package"  
            }
        }
        stage('Docker Build'){
            steps{
            script{
                dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }    
            }
        }
        stage('Docker Push'){
            steps{
            script{
                docker.withRegistry( '', registryCredential ){
                    dockerImage.push()
                }
            }
        }
        }
        stage('Remote SSH') {
            steps{
            script {
            sshagent(["Node"]) {
                sh "${secure} 'sudo docker rm -f petsapp  || true'" 
                sh "${secure} 'sudo docker run -d --name petsapp -p80:8080 ${registry}:${BUILD_NUMBER}'"
                    }
                }
            }
        }
    }
}

