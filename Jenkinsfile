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
        sh 'scp -o StrictHostKeyChecking=no  /var/lib/jenkins/workspace/my-app2021/target/.war ec2-user@10.0.1.66:/optt/tomcat/apache-tomcat-8.5.68/webapps/'
    }
      }
    }
    stage('dev-deploy'){
      when {
        branch "develop"
      }
      steps{
        echo "deploy to dev environment"
      }
    }

    stage('uat-deploy'){
      when {
        branch "uat"
      }
      steps{
        sh "curl -u admin:admin -X GET 'http://65.0.19.206:8081/service/rest/v1/repositories'"
        // How do you get latest artifact from nexus?
        echo "deploy to uat environment"
      }
    }

    stage('prd-deploy'){
      when {
        branch "master"
      }
      steps{
        // How do you get latest artifact from nexus?
        echo "deploy to prod environment"
      }
    }
  }
}
