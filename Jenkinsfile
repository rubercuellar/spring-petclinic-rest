pipeline {
    // agent any
    // tools {
    //     maven 'maven3.9.16'
    // }

    agent {
        docker {
            image 'maven:3.9.16-eclipse-temurin-21'
        }
    }
    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=${WORKSPACE}/.m2/repository"
    }

    triggers {
        githubPush()
    }

    stages {
        // stage('Checkout SCM') {
        //     steps {
        //         git branch: 'master', url: 'https://github.com/rubercuellar/spring-petclinic-rest.git'
        //     }
        // }
        
       stage('Compile') {
        steps {
             bat 'mvn clean compile -B -ntp'
        }
    }

       stage('Test') {
        steps {
             bat 'mvn test -B -ntp'
        }
        post {
            success {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
       stage('Coverage') {
        steps {
             bat 'mvn jacoco:report -B -ntp'
        }
        post {
            success {
                recordCoverage(tools:[[parser: 'JACOCO']])
            }
        }
    }

       stage('Package') {
        steps {
            bat 'mvn package -DskipTests -B -ntp'
        }
       
    }

       
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint:true 
        }
        cleanup {
            cleanWs()
        }
    }
}