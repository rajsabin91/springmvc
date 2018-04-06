pipeline {
  agent none
  
  	stage('build') {
      agent {
        label 'CentosSlave'
      }
      steps {
        sh 'echo"Now Bulding"'
        sh 'export M2_HOME=/opt/mvn'
		sh 'export M2=$M2_HOME/bin'
		sh 'export PATH=$M2:$PATH'
		sh 'cd /home/jenkins/svnmvc'
		sh 'mvn clean install'
      }
      post {
        success {
          archiveArtifacts artifacts: 'target/*.war', fingerprint: true
        }
      }
    }
    stage('deploy') {
      agent {
        label 'jenkins_tomcat'
      }
      steps {
        sh 'echo "delpoyment started"'
        sh 'cd ~'
		sh 'scp sabinraj893.mylabserver.com:/home/jenkins/svnmvc/target/spring-mvc-hibernate-example.war /home/jenkins'
		sh 'sudo cp spring-mvc-hibernate-example.war /opt/tomcat9/webapps/'
	    sh 'sudo service tomcat restart'
	       }
	   }
	  }