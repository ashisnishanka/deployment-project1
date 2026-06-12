pipeline {
    agent {
    docker {
      image 'abhishekf5/maven-abhishek-docker-agent:v1'
	  image 'maven:3.9.6-eclipse-temurin-17'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
    
    stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        git branch: 'main', url: 'https://github.com/ashisnishanka/deployment-project1.git'
      }
    }

  stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        // build the project and create a JAR file
         sh 'mvn clean package'
		
      }
    }
//   stage('Static Code Analysis') {
//     // environment {
//     //     SONAR_HOST_URL = 'http://65.0.181.39:9000'
//     //     SONAR_AUTH_TOKEN = credentials('sonarqubeserver')
//     // }

//     // steps {
//     //     sh '''
//     //     mvn sonar:sonar \
//     //     -Dsonar.projectKey=demo \
//     //     -Dsonar.host.url=$SONAR_HOST_URL \
//     //     -Dsonar.token=$SONAR_AUTH_TOKEN
//     //     '''
//     // }
// 	  withSonarQubeEnv('sonarqubeserver') {
//     sh 'mvn sonar:sonar'
// }
// }
stage('Static Code Analysis') {
    steps {
        withSonarQubeEnv('sonarserver') {
            sh 'mvn sonar:sonar'
        }
    }
}
		
}
}

