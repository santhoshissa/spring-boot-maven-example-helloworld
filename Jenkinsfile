// Declarative //
pipeline {
    agent any
    stages {
        stage('Code Checkout') {
            steps {
                echo 'CheckOut SCM'
                //cleanWs()
                checkout scm
                //git 'https://github.com/santhoshissa/cucumber-java-selenium-webdriver-example.git'
            }
        }
        stage('SAST') {
            steps {
                echo 'Running SAST'
               // bat 'mvn verify'
                //bat 'mvn site'
                bat 'mvn test site'
                //bat 'mvn test site'
               
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
                bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000  -Dsonar.login=88e6f45f09066dcc8265bee6c084b18fcbf4960e'
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
        stage('Test Code Checkout') {
            steps {
                dir('web'){
                echo 'Checkout Test SCM'
                git 'https://github.com/sithagariajayreddy/Maven-Selenium-Cucumber-Java.git'
                }
            }
        }
        stage('Functional Test') {
            steps {
                dir('web'){
                bat 'mvn clean install'
                 bat 'mvn install'
                    bat 'mvn test'
            }
            }
        }
         stage('Non Functional Test') {
            steps {
                echo 'Non Functional Test'
                //git 'https://github.com/santhoshissa/cucumber-testing-framework-using-selenium-java-maven.git'
                bat 'C:\\apache-jmeter-5.4.2\\bin\\jmeter -j jmeter.save.saveservice.output_format=xml -n -t C:\\apache-jmeter-5.4.2\\bin\\JmeterTestCase.jmx -l C:\\apache-jmeter-5.4.2\\reports\\jmeterreport.jtl' 
            }
             post {
    always {
        perfReport filterRegex: '', showTrendGraphs: true, sourceDataFiles: 'C:\\apache-jmeter-5.4.2\\reports\\jmeterreport.jtl' 
    }
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
