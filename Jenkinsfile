node{
    
def mavenHome = tool name: "maven3.9.2"

echo "The node name is: " ${env.NODE_NAME}
echo "The job name is: " ${env.JOB_NAME}
stage('get the code from scm'){
git credentialsId: '290dbc8c-2d9e-426b-85c5-656b00f282fb', url: 'https://github.com/anillagudu/maven-web-application.git'
}

stage('build the code'){
sh "$mavenHome/bin/mvn clean package"
} 

stage('code coverage'){

sh "$mavenHome/bin/mvn sonar:sonar"

}
/*
stage('deployed artifactory'){
sh "$mavenHome/bin/mvn deploy"
}
*/
stage('deployed to tomcat server'){
sshagent(['8e09da8f-7bcf-4fde-8902-384448820bef']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@52.55.16.89:/opt/apache-tomcat-8.5.89/webapps"
	}
}

}
