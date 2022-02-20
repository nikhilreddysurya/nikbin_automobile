pipeline {
    agent any 
    stages {
        stage('Code Build') {
            steps {
                 git credentialsId: 'git-nikhil-creds', url: 'https://github.com/nikhilreddysurya/welcomeApp.git'
                 sh 'mvn package'
            }
        }
        stage('Package upload') {
            steps {
                 sh '''aws s3 cp target/welcomeapp.war s3://jenkins-practice/welcomeapp-war-files/welcomeapp.war
                 sleep 5s
                 aws s3 cp target/welcomeapp.war  s3://jenkins-practice/welcomeapp-war-files/welcomeapp-$BUILD_NUMBER.war'''
            }
		}
        stage('Deployment') {
            steps {
                 sh 'aws s3 cp s3://jenkins-practice/nikbin_automobile/automobile.war /home/ubuntu/apache-tomcat-9.0.58/webapps/'
            }
        }
	}
    
}
