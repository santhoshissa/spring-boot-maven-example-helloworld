// Declarative //
pipeline {
    agent any
    stages {
        stage('Code Checkout') {
            steps {
                echo 'CheckOut SCM'
                cleanWs()
                checkout scm
                //git 'https://github.com/santhoshissa/spring-boot-maven-example-helloworld.git'
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
                bat 'del ..\\target\SpringBootMavenExample-1.3.5.RELEASE.war'
                bat 'copy "C:\\Users\\Sanu\\Desktop\\spring-boot-maven-example-helloworld-master\\target\\SpringBootMavenExample-1.3.5.RELEASE.war" ..\\target\'
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
