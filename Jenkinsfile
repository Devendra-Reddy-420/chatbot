pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World-Jenkins Pipeline'
            }
        }
        stage("Maven Build"){
                steps {
                sh 'mvn clean package'
                     }
        }
         stage("Tomcat-dev"){
            //  install SSH Agent plugin
            steps {
                sshagent(['tomcat-dev']) {
                    // Copy war file to tomcat dev server
                    sh "scp -o StrictHostKeyChecking=no target/chatbot.war ec2-user@172.31.30.26:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.30.26 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.30.26 /opt/tomcat9/bin/startup.sh"
                    }
                 }
            }
      }
}
