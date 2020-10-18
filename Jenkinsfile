def IP="ezhilc/petsapp"
pipeline{
    environment {
    registry = "ezhilc/petsapp"
    registryCredential = 'Docker'
    dockerImage=''
        }
  agent any
    tools{
        maven 'maven3'
    }
    stages{
    stage('Remote SSH') {
        steps {
   script {
    sshagent(["Node"]) {
        sh "ssh -oStrictHostKeyChecking=no ec2-user@18.208.211.106 'sudo docker run -d -p80:8080 ezhilc/petsapp:64'"
            }
                }
        }
    }
    }
}
