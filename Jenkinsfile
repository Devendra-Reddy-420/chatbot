pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World-Jenkins Pipeline'
            }
        }
        stage("Maven Build"){
                when {
                    branch "develop"
                     }
                steps {
                sh 'mvn clean package'
                     }
        }
         stage("Tomcat-dev"){
            //  install SSH Agent plugin 
             when {
                    branch "develop"
                     }
            steps {
                sshagent(['tomcat-dev']) {
                    // Copy war file to tomcat dev server
                    sh "scp -o StrictHostKeyChecking=no target/chatbot.war ec2-user@172.31.94.185:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/startup.sh"
                    }
                 }
            }
        // to Build the sample changes in Test environment
         stage("test-deploy"){
             when {
                    branch "test"
                     }
            steps {
                    echo "Test Deploy"
                    }
         }
        // to Build the sample changes in Prod environment
         stage("prod-deploy"){
                     when {
                         branch "main"
                         }
                            steps {
                                 echo "Test Deploy"
                             }
                }
            }
        }
