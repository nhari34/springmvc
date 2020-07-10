currentBuild.displayName = currentBuild.projectName +"-${para}#" +currentBuild.number
pipeline{
    agent any
    parameters {
  choice choices: ['dev', 'uat', 'prod'], description: 'choose deployment environment', name: 'para'
}

    tools {
  maven 'mavan'
}

    stages{
        stage('paramstage'){
            steps{
                echo "this is from ${params.para} environment"
            }
        }
        stage('parallel'){
            parallel{
                stage('one'){
                    steps{
                 echo  "1"
                sleep   2
                echo   "2"
                sleep   2
                echo    "3"
                sleep   2
                echo   "4"
                    }
                }
            
        stage('two'){
            steps{
                 echo "a"
                sleep  2
                echo  "b"
                sleep  2
                echo "c"
                sleep 2
                echo "d"
                }
              }
            }
        }
        stage('displayname'){
            steps{
            echo currentBuild.displayName
           
}
}
  
        stage('git checkout'){
            steps{
                git credentialsId: 'github', url: 'https://github.com/chnaveen112/springmvc'
            }
        }
        stage('mvn build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('tomcat deploy'){
            steps{
                sshagent(['tomcat']) {
    // some block
    sh "scp target/springmvc.war ec2-user@172.31.9.71:/opt/tomcat8/webapps/"
          }        
        }
    }
  }
}
