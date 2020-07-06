pipeline{
    agent any
    tools {
  maven 'mavan'
}
 stages{
         stage('mavan build'){
            steps{
            sh 'mvn clean package'
            }
        }
        stage('tomcat deploy'){
            steps{
                library 'sharedlibrary'
                 tomcatDeploy credId:'tomcat',
                    ip:'172.31.9.71',
                    userName:'ec2-user',
                    tomcatHome:'/opt/tomcat8',
                    warName:'springmvc'
             }
        }
    }
}
