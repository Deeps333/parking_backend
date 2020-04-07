pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/Deeps333/parking_backend.git'
		}
	}
	
	
	stage ('Release') {
		steps {
			sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'
		}
	}
		stage ('Database Migration'){
			steps {
				
                               sh '/usr/share/maven/bin/mvn compile'
                                flywayrunner commandLineArgs: '', credentialsId: 'flyway', flywayCommand: 'migrate', installationName: 'usr/local/bin/flyway', locations: 'filesystem:/var/lib/jenkins/workspace/MigrateDB/src/main/resources/db/migration', url: 'jdbc:mysql://13.127.63.205:3306/newfly'
			}
		}
                stage ('Database Migration UAT'){
			steps {
				sh '/usr/share/maven/bin/mvn compile'
                                flywayrunner commandLineArgs: '', credentialsId: 'flyway', flywayCommand: 'migrate', installationName: 'usr/local/bin/flyway', locations: 'filesystem:/var/lib/jenkins/workspace/MigrateDB/src/main/resources/db/migration', url: 'jdbc:mysql://13.232.190.244:3306/flydb'      
			}
		}
}
	
}
