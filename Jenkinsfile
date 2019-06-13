pipeline {
    agent any
    
    tools { maven 'mymaven'
            jdk 'jdk'
    }

    parameters {
         string(name: 'tomcat_dev', defaultValue: '3.95.155.196', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.233.163.158', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i /Users/tsering/Download/MyNewKeyPair.pem  **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i  /Users/tsering/Download/MyNewKeyPair.pem  **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                    }
                }
            }
        }
    }
}
