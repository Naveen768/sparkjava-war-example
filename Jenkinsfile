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
                                "target": "reddy/"
                            }
                        ]
                    }''',
                )
                buildName:'reddy',
                buildNumber:'1'
            }
        }
    }
}
