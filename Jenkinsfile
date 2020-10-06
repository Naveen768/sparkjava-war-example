pipeline{
    agent any
    stages{
        stage("code quality"){
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=project \
  -Dsonar.host.url=http://3.17.160.211:9000 \
  -Dsonar.login=16c5880572ce353aeadaab3a4eff504e97306909
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
                curl -uadmin:APAUKBb5JeroF2zDsNs9a83m5aF -O "http://3.137.192.125:8081/artifactory/project/sparkjava-hello-world-1.0.war"
                cp sparkjava-hello-world-1.0.war /opt/tomcat/webapps/
                '''
            }
        }    
    }
}
