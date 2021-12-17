// Declarative //
pipeline {
    agent any
    stages {
        stage('Code Checkout') {
            steps {
                echo 'CheckOut SCM'
                //cleanWs()
                checkout scm
                //git 'https://github.com/santhoshissa/spring-boot-maven-example-helloworld.git'
            }
        }
        stage('SAST') {
            steps {
                echo 'Running SAST'
                bat 'mvn spotbugs:spotbugs'
               
            }
        }
       stage('Build and Package') {
            steps {
                echo 'Build and Package'
                bat 'mvn clean'
                bat 'mvn install'
            }
        }
        
         stage('Code Quality') {
            steps {
                echo 'Code Quality Check'
                bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000  -Dsonar.login=42b7fe4ecd92c27e96b3a2529d42c68f36144f9d'
            }
        }
        stage('Deploy approval'){
            steps {
                input "Deploy to prod?"
            }
        }
      
       stage('deploy') {
            steps {
                echo 'deploy'
                bat 'cd'
                bat 'del "C:\\Program Files\\Apache Software Foundation\\Tomcat 8.5\\webapps\\SpringBootMavenExample-1.3.5.RELEASE.war"'
                bat 'copy target\\SpringBootMavenExample-1.3.5.RELEASE.war "C:\\Program Files\\Apache Software Foundation\\Tomcat 8.5\\webapps\\"'
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
