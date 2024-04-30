pipeline {
    agent any

    parameters {
        choice(name: 'ENV', choices: ['QA', 'UAT'], description: 'Pick Environment value')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '/home/shivani/Documents/devops/apache-maven-3.9.6/bin/mvn install'
            }
        }

        stage('Deployment') {
            steps {
                script {
                    if (env.ENV == 'QA' || env.ENV == 'UAT') {
                        sh "cp target/pink1.war /home/shivani/Documents/devops/apache-tomcat-9.0.88/webapps"
                        echo "Deployment has been done on ${env.ENV}!"
                    } else {
                        error "Invalid environment selected: ${env.ENV}"
                    }
                }
            }
        }

        stage('Slack') {
            steps {
                script {
                    slackSend baseUrl: 'https://hooks.slack.com/services/',
                              botUser: true,
                              channel: 'pink1',
                              color: 'good',
                              message: "Deployment to ${env.ENV} environment completed successfully!",
                              teamDomain: 'devops',
                              tokenCredentialId: 'pink1',
                              username: 'pink1'
                }
            }
        }
    }
}
