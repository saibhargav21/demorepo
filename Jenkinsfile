pipeline {
   agent any

   stages {
      stage('Cloning the repo') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/saibhargav21/demorepo.git']]])
         }
      }
   
       stage("build the repo"){
           steps{
               sh label: '', script: '''mvn clean package'''
           }
       }
       stage("deploy the code"){
           steps{
               sh label: '', script: 'sudo systemctl stop tomcat'
               sh label: '', script: 'sudo rm -rf /opt/tomcat/tomcat1/webapps/mvn-hello-world*'
               sh label: '', script: 'sudo cp -f target/mvn-hello-world.war /opt/tomcat/tomcat1/webapps/'
               sh label: '', script: 'sudo systemctl start tomcat'
           }
       }
       
      /*stage("credentials"){
           steps{
               withCredentials([usernamePassword(credentialsId: '', passwordVariable: 'paswd', usernameVariable: 'usernme')]) {
    
             echo "username is :${usernme}"
             echo "passwd is :${passwd}"
               } 
           }
       }*/
    stage("access parameters"){
        steps{
            script{
                print env.name
                print env.countrylist
            }
        }
    } 
   }
  
   
}
