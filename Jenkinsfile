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
                echo 'Scanning dependency check'
                sh '/var/security/OwaspDependecyCheck/dependency-check/dependency-check/bin/dependency-check.sh --disableRetireJS -f XML --nvdApiKey 646a475b-3e7b-4b75-bd01-27b9c59d6e70  --out /tmp/ --scan /var/lib/jenkins/workspace/JavaHelloWorld_main/target/JavaHelloWorld-1.0-SNAPSHOT.jar'
                echo 'Scanning Trivy'
                echo 'Scanning Semgrep'
            }
        }
    }
    post{
        success{
            echo 'Build Success'
        }
    }
}

