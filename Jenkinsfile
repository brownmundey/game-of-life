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
				sh "sudo docker stop server"
				sh "sudo docker system prune -a -f"
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
				sh "sudo docker cp /mnt/weblight/gameoflife-web/target/gameoflife.war server:/usr/local/tomcat/webapps"
			}
		}
		stage ("restart t-server") {
		  steps {
				sh " sudo docker exec -it server bash"
				sh "cd /bin && ./startup.sh"
		  }
		}
  }
}
