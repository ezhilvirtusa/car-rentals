pipeline{
    {  environment {
    registry = "http://35.153.67.88:8080/repository/car-rent-docker-snap/"
    registryCredential = 'Nexus;
    agent any
        tools{
        maven 'maven3'
    }
    stages{
        stage("Git"){
            steps{
               git credentialsId: 'Git', url: 'https://github.com/ezhilvirtusa/car-rentals.git' 
            }
        }
        stage("Build war"){
            steps{
                    sh 'mvn clean package'
            }
        }
        stage("Build image"){
            steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }

            }
        }
    }
}
