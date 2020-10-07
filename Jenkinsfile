pipeline{

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
                    sh 'docker build -t myimage .'
            }
        }
    }
}
