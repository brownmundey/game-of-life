pipeline {
  agent {
	label {
		label "remote"
		customWorkspace "/mnt/weblight"
	}
  }
  stages {
		stage ("install tomcat") {
			steps {
				sh "sudo docker run -itdp 8081:8080 --name server tomcat:9"
			}
		}
		stage ("build") {
		  steps {
		    sh "mvn clean install"
		  }
		}
		stage ("copy and deploy") {
			steps {
				sh "docker cp /mnt/weblight/game-of-life/gameoflife-web/target/gameoflife.war server:/usr/local/tomcat/webapps"
			}
		}
		stage ("restart t-server") {
		  steps {
				sh "docker exec -it server bash"
				sh "cd /bin && ./startup.sh"
		  }
		}
  }
}
