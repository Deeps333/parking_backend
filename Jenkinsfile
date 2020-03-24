pipeline {
   agent any
	options {
             skipDefaultCheckout true
	}
       stages {
      stage('Git Checkout') {
         steps {
           checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Deeps333/parking_backend.git']]])
		}
	}
	stage ('Build')
	   
	    {steps{
                sh '/usr/share/maven/bin/mvn clean package -Dmaven.test.skip=true'
	    }    }
        stage ('Update the Version')
		{ steps {
                sh '/usr/share/maven/bin/mvn --batch-mode release:clean release:prepare release:perform -DreleaseVersion-4.1.1 -DdevelopmentVersion-2.6.2-SNAPSHOT -Dmaven.test.skip=true'
	        sh 'sudo git add .'
                sh 'sudo git commit -m "Updated pom" pom.xml'
                sh 'sudo git push https://Deeps333:Deepanshu333@github.com/Deeps333/parking_backend.git HEAD:master'
                }       }
      }
          
   }
