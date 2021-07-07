pipeline{
  agent any

  stages{
    stage('Maven Build'){
      steps{
        sh "mvn clean package"
      }
    }
    stage('Upload To tomcat'){
      steps{
         sshagent(['tomcatec2']) {
        sh 'scp -o StrictHostKeyChecking=no  /var/lib/jenkins/workspace/my-app2021/target/ myweb-0.0.1.war ec2-user@10.0.1.66:/optt/tomcat/apache-tomcat-8.5.68/webapps/'
    }
      }
    }
    
  }
}
