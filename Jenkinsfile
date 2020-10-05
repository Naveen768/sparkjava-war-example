pipeline{
    agent any
    stages{
        stage("code quality"){
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=red \
  -Dsonar.host.url=http://3.15.188.123:9000 \
  -Dsonar.login=ab71e348fe22672160ba4532e4228e32fc0d71a5
                '''
            }
        }
        stage('code build and publish'){
            steps{
                sh 'mvn clean package'
                rtUpload(
                    serverId:'artifactory',
                    spec: '''{
                        "files":[
                            {
                                "pattern": "**/sparkjava-hello-world-1.0.war",
                                "target": "project/"
                            }
                        ]
                    }''',
                    buildName: 'project',
                    buildNumber: '1'
                )
            }
        }
        stage('deployment') {
            steps {
                sh'''
                id
                pwd
                cd /home/ubuntu/
                ls -lrt
                curl -uadmin:APRhGXps7xAS2ZSuQrPpBJA1w5 -O "http://3.137.223.157:8082/artifactory/project/sparkjava-hello-world-1.0.war"
                cp sparkjava-hello-world-1.0.war /opt/tomcat/webapps/
                '''
            }
        }    

    }
}
