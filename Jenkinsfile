pipeline{
    agent any
    environment{
        path = "$PATH:/usr/share/maven"
    }
    stages
    {
        stage ('Checkout From SCM')
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/simple-app.git']]])
            }
        }
        stage ('BUILD')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage ('Push Artifact To Nexus')
        {
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'target/simple-app/3.0.0.war', type: 'war']], credentialsId: 'nexus-admin', groupId: 'in.javahome', nexusUrl: '13.234.110.38:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://13.234.110.38:8081/repository/maven-nexus-jenkins-repo/', version: '3.0.0'
            }
        }
    }
}