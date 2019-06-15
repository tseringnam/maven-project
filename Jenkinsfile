pipeline {
    agent any
    
    tools { maven 'mymaven'
            jdk 'jdk'
            docker 'mydocker'
    }
    stages{
        stage('Build'){
            steps{
                
            sh 'mvn clean package'
            sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}
