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
                sh '/var/security/OwaspDependecyCheck/dependency-check/dependency-check/bin/dependency-check.sh --out /tmp/ --scan /var/lib/jenkins/workspace/JavaHelloWorld_main/target/JavaHelloWorld-1.0-SNAPSHOT.jar'
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

