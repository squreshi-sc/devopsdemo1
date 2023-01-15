pipeline {
  agent any 
  tools {
    maven 'maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }

    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }


    stage ('Deploy to Tomcat') {
      steps {
        sshagent(['root']){
            sh 'sshpass -p "P@ssw0rd" scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webapp-cicd-pipeline/target/WebApp.war root@192.168.11.29:/root/prod/apache-tomcat-9.0.71/webapps/webapp.war'    
        
        }
       }
    }



    }
}
