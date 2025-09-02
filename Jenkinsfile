pipeline {
  agent {
    label 'test'
  }
  tools {
    maven 'MAVEN_3.9.6'
    jdk 'JDK_21'
  }
  // environment {
  //   JAVA_HOME = "${tool 'JDK_21'}"
  //  PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
  // }
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/harish1416/tomcat.git', branch: 'main'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
  stage('Deploy to Tomcat') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat', url: 'http://ec2-3-26-16-58.ap-southeast-2.compute.amazonaws.com:8080/')], war: '**/*.war'
      }
    }
  }
}
