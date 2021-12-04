// Declarative //
pipeline {
    agent any
    stages {
        stage('Git pull') {
            steps {
                echo 'Git Pull'
              git 'https://github.com/santhoshissa/hello-world-spring-boot.git'
            }
        }
       stage('mvn actions') {
            steps {
                echo 'mvn actions'
                bat 'mvn clean'
                bat 'mvn install'
                bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000  -Dsonar.login=42b7fe4ecd92c27e96b3a2529d42c68f36144f9d'
            }
        }
      
       stage('deploy') {
            steps {
                echo 'deploy'
                bat 'cd'
                //bat 'copy "C:\Program Files\Apache Software Foundation\Tomcat 8.5\webapps"'
            }
        }
       
    }
       tools {
            jdk 'jdk'
            git 'git'
            maven 'mvn'
        }
}
// Script //
