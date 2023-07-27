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
            steps {
                sshagent(['tomcat-dev']) {
                    // Copy war file to tomcat dev server
                    sh "scp -o StrictHostKeyChecking=no target/chatbot.war ec2-user@172.31.94.185:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/startup.sh"
                    }
                 }
            }
        // to Build the changes in Test environment
        stage("Maven Build"){
                when {
                    branch "test"
                     }
                steps {
                sh 'mvn clean package'
                     }
        }
         stage("Tomcat-dev"){
            //  install SSH Agent plugin 
            steps {
                sshagent(['tomcat-test']) {
                    // Copy war file to tomcat prod server
                    sh "scp -o StrictHostKeyChecking=no target/chatbot.war ec2-user@172.31.94.185:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/startup.sh"
                    }
                 }
            }
        // to Build the changes in Prod environment
        stage("Maven Build"){
                when {
                    branch "main"
                     }
                steps {
                sh 'mvn clean package'
                     }
        }
         stage("Tomcat-prod"){
            //  install SSH Agent plugin 
            steps {
                sshagent(['tomcat-prod']) {
                    // Copy war file to tomcat prod server
                    sh "scp -o StrictHostKeyChecking=no target/chatbot.war ec2-user@172.31.94.185:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.94.185 /opt/tomcat9/bin/startup.sh"
                    }
                 }
            }
        }
    }
