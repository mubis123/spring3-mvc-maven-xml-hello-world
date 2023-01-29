pipeline{
        agent any
        tools{
                jdk 'java11'
                maven 'maven3'
            }
        stages{
            stage('clone'){
                steps{
                    git credentialsId: 'git_credentials', url: 'https://github.com/mubis123/spring3-mvc-maven-xml-hello-world.git'
                    
                }
            }
             stage('Build'){
                steps{
                    sh "mvn clean package"
                    
                }
            }
            stage('Deploy'){
                steps{
                    //Deploy A New Application Archive (WAR) Remotely
                    //example: http://localhost:8080/manager/text/deploy?path=/foo -->foo means filename 
                   // one method: with credentials
                   //sh "curl -v -u admin:admin -T /var/lib/jenkins/workspace/spring3/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://99.79.54.80:8081/manager/text/deploy?path=/pipeline2_spring_curl&update=true'"
                 //second method: hiding credentials
                 withCredentials([usernameColonPassword(credentialsId: 'tomcat_cred', variable: 'tomcat_pipeline')]) 
                 {
                  sh "curl -v -u ${tomcat_pipeline} -T /var/lib/jenkins/workspace/spring3/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://99.79.54.80:8081/manager/text/deploy?path=/pipeline2_spring_curl&update=true'"
                  }
                    
                    
                }
                 
            }
        }
    
}
