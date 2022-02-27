pipeline {
    agent any 
    stages {
        stage('Code Build') {
            steps {
                 git credentialsId: 'git-nikhil-creds', url: 'https://github.com/nikhilreddysurya/nikbin_automobile.git'
                 sh 'mvn package'
            }
        }
        stage('Package upload') {
            steps {
                 sh '''aws s3 cp target/automobile.war s3://jenkins-practice/nikbin_automobile/automobile.war
                 sleep 5s
                 aws s3 cp target/automobile.war  s3://jenkins-practice/nikbin_automobile/automobile-$BUILD_NUMBER.war'''
            }
		}
        stage('node1-Deployment') {
	    agent node1
            steps {
                 sh 'aws s3 cp s3://jenkins-practice/nikbin_automobile/automobile.war /home/ubuntu/apache-tomcat-9.0.58/webapps/'
            }
        }
    }
    
}
