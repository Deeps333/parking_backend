pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/Deeps333/parking_backend.git'
		}
	}
	stage('Build') {
		steps {
			withSonarQubeEnv('sonar') {
				sh '/usr/share/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'
			}
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
                                flywayrunner commandLineArgs: '', credentialsId: 'flyway', flywayCommand: 'migrate', installationName: 'usr/local/bin/flyway', locations: '/flyway-6.3.2/sql', url: 'jdbc:mysql://35.154.66.159:3306/newfly'      
			}
		}
                stage ('Database Migration UAT'){
			steps {
				sh '/usr/share/maven/bin/mvn compile'
                                flywayrunner commandLineArgs: '', credentialsId: 'flyway', flywayCommand: 'migrate', installationName: 'usr/local/bin/flyway', locations: '/flyway-6.3.2/sql', url: 'jdbc:mysql://13.233.244.148:3306/flydb'      
			}
		}
}
	
}
