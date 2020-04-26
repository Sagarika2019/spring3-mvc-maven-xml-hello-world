pipeline {
   agent any

   tools {
      
      maven "maven3"
   }

   stages {
      stage('get_scm') {
         steps {
            
            git credentialsId: 'git-credentials', url: 'https://github.com/Sagarika2019/spring3-mvc-maven-xml-hello-world.git'
		}
	}
      stage ('build'){
	steps{
          script{
          
            sh "mvn clean package"
    	      }
	}  
	}
	 stage ('artifacts'){
	     steps{
	         archiveArtifacts '**/target/*.war'
	     }
	 }
	 stage('deploy') {
             steps{
                   withCredentials([usernameColonPassword(credentialsId: 'tomcat-credentials', variable: 'tomcat_credentials')]) 
                   {
                    sh "curl -v -u ${tomcat_credentials} -T /var/lib/jenkins/workspace/first_pipeline/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'ec2-54-209-237-49.compute-1.amazonaws.com:8080/manager/text/deploy?path=/pipeline_example&update=true'"
                   }
             }
             } 	 
    }   
      
 }
