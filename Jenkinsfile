pipeline {
	agent any
	
	parameters {
		choice(name: 'ENV', choices: ['QA','UAT'], description: 'Pick Environment value')
	}
	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			  sh '/home/shivani/Documents/devops/apache-maven-3.9.6/bin/mvn install'
             }}
		stage('Deployment'){
		    steps {
			script {
			 if ( env.ENV == 'QA' ){
        	sh 'cp target/pink1.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps'
         echo "deployment has been done on QA!"
			 }
			elif ( env.ENV == 'UAT' ){
    		sh 'cp target/pink1.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps'
        echo "deployment has been done on UAT!"
			}
			echo "deployment has been done!"
			fi
			}}}
		stage('Slack') {
			steps {
				sh 'slackSend baseUrl: 'https://hooks.slack.com/services/', botUser: true, channel: 'pink1', color: 'good', message: 'pinkieee', teamDomain: 'devops', tokenCredentialId: 'pink1', username: 'pink1' '
					}}
	}}
