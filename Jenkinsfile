//Notes
// Owasp dependency check plugin needs to be added to jenkins installation
// https://sudheer-baraker.medium.com/integrate-owasp-dependency-check-in-jenkins-pipeline-748d8aefc2b7

pipeline{
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("build"){
            steps{
                echo 'Building'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage("run"){
            steps{
                echo 'Executing app'
                sh 'java -jar /var/lib/jenkins/workspace/JavaHelloWorld_main/target/JavaHelloWorld-1.0-SNAPSHOT.jar'
            }
        }
        stage("scanning"){
            steps{
                echo 'Security scanning'
                echo 'Scanning Owasp dependency check'
                // First time will take ~20 mins
                // need to make jenkins able to execute depcheck with sudo
                //jenkins ALL= NOPASSWD: /var/security/OwaspDependecyCheck/dependency-check/dependency-check/bin/dependency-check.sh
                // report name will be dependency-check-report.xml
                sh 'sudo /var/security/OwaspDependecyCheck/dependency-check/dependency-check/bin/dependency-check.sh --disableRetireJS -f XML --nvdApiKey 646a475b-3e7b-4b75-bd01-27b9c59d6e70  --out ~/ --scan /var/lib/jenkins/workspace/JavaHelloWorld_main/target/JavaHelloWorld-1.0-SNAPSHOT.jar'
                // follow https://semgrep.dev/docs/getting-started/quickstart first incl login. THIS HAS TO BE DONE AS JENKINS USER
                echo 'Scanning Semgrep'
                sh 'semgrep scan --config auto --json --output ~/semgrep.json /var/lib/jenkins/workspace/JavaHelloWorld_main/src/'
                // follow https://aquasecurity.github.io/trivy/v0.18.3/installation/
                echo 'Scanning Trivy'
                sh 'trivy image --timeout 1h --format json python:3.4-alpine > ~/trivy.json'
            }
        }
        // stage("pushing to defectdojo"){
          //  steps{
            //}
         //}
    }
    post{
        success{
            echo 'Build Success'
        }
    }
}

