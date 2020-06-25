pipeline{
    agent any
    stages{
        stage("build"){
            agent{docker'maven:3-alpine'}
            steps{
                sh"mvn clean package"
                rtUpload (
    serverId: 'artifactory',
    spec: '''{
          "files": [
            {
              "pattern": "**/sparkjava-hello-world-1.0.war",
              "target": "project/"
            }
         ]
    }''',
 
    // Optional - Associate the uploaded files with the following custom build name and build number,
    // as build artifacts.
    // If not set, the files will be associated with the default build name and build number (i.e the
    // the Jenkins job name and number).
    buildName: 'project',
    buildNumber: '1'
)
curl -uadmin:APASfQaa9ckVm7xtrFxAepxV1QE -O "http://18.225.35.16:8082/artifactory/project/sparkjava-hello-world-1.0.war"
scp sparkjava-hello-world-1.0.war ubuntu@3.21.168.71:/opt/tomcat/webapps/

            }
        }
    }
}
