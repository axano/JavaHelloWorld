pipeline{
    agent any
    tools {
        jdk 'java'
        maven 'maven'
    }
    stages {
        stage("build"){
            steps{
                echo 'Building'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage("scanning"){
            steps{
                echo 'Security scanning'
                echo 'Scanning dependency check'
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

