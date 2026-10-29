pipeline {
    agent any
    
    tools {
        maven 'maven3.9.16'
    }

    stages {
        // stage('Checkout SCM') {
        //     steps {
        //         git branch: 'master', url: 'https://github.com/rubercuellar/spring-petclinic-rest.git'
        //     }
        // }
        
       stage('Build') {
        steps {
             bat 'mvn clean package -DskipTests -B -ntp'
        }
    }

       
    }
}