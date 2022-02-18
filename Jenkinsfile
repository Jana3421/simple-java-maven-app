pipeline{
    agent any 
    tools {
    maven 'Maven'
    }
    stages{
        stage("Checkout Code"){
            steps{
                echo "======== Code Checking Out ========"
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Jana3421/simple-java-maven-app.git']]])
            }
            post{
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage ("build") {
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "====++++only when successful++++===="
                }
                failure{
                    echo "====++++only when failed++++===="
                }
            }
        }    
          stage ("sonar scanning") {
            steps {
                script { 
                    def scannerHome = tool name: 'SonarScanner';
                    withSonarQubeEnv("SonarScanner") {
                        sh "${tool("SonarScanner")}/bin/sonar-scanner \
                        -Dsonar.projectKey=simple-java-maven-app \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://54.198.175.171:9000/ \
                        -Dsonar.login=2f60a4d498a222e03738eddeddc43ce5796ea491"
                    }
               }
            }
        stage ("Upload to Nexus") {
            steps {
                sh "mvn -gs ${WORKSPACE}/settings.xml deploy"
            }
      }
    }
  }
}
