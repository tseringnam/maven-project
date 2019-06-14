pipeline {
    agent any
    
    tools { maven 'mymaven'
            jdk 'jdk'
    }
    stages{
        stage('Build'){
            steps{
                
            sh 'mvn clean package'
            }
        }
    }
}
