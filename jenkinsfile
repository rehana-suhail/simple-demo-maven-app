//This is the Jenkins file created from the pipeline syntax
node ('mvn-label') {
    def mvnHome
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/rehana-suhail/Hello_Java.git'
        // Get the Maven tool.
        // ** NOTE: This 'M3' Maven tool must be configured
        // **       in the global configuration.
        mvnHome = tool 'maven-3.5.2'
        //latest maven tool
        //hello
    }
    stage('Build') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                //sonar added just try
                //deploy the repo to jfrog
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy sonar:sonar -Dsonar.host.url="http://ec2-52-66-236-162.ap-south-1.compute.amazonaws.com:9000"'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
        //slackSend channel: '#devops-training', teamDomain: 'devops-6wb2537', tokenCredentialId: '07a2a721-597a-47fe-b879-68ea6bf08ce0'
        //Slack has been added
        //slackSend channel: '#devops-training', message: 'Hello_Java Successfully Deployed', teamDomain: 'devops-6wb2537', tokenCredentialId: '07a2a721-597a-47fe-b879-68ea6bf08ce0', username: 'hussain.rehana@gmail.com'
    }
}
