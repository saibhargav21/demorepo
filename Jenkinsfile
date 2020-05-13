pipeline {
   agent any

   stages {
      stage('CLoning the repo') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/sudhfree/demorepo.git']]])
         }
      }
      
      stage("build the code")
      {
          steps{
               sh label: '', script: 'mvn clean package'
          }
      }
      
      stage("deploy the code")
      {
          steps{
          echo "stopping the service"
    sh label: '', script: 'sudo systemctl stop tomcat'
    echo "deleting the old code"
    sh label: '', script: 'sudo rm -rf /opt/tomcat/webapps/mvn*'
    echo "copying the new code"
    sh label: '', script: 'sudo cp -f target/mvn-hello-world.war /opt/tomcat/webapps/'
    echo "resatrting the service"
    sh label: '', script: 'sudo systemctl start tomcat'
          }
      }
      
     
      
   }
}
