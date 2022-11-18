pipeline {
    agent any
	stages {
        stage('Compile') {
            steps {
                echo 'Compile..'
                sh "./mvnw clean compile -e"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
				sh "./mvnw clean test -e"
            }
        }
		stage('Building') {
            steps {
                echo 'Testing..'
				sh "./mvnw clean package -e"
            }
        }
		stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('Sonar') {
					sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

stage('uploadNexus') {
            steps {
                echo 'Uploading Nexus'
<<<<<<< HEAD
				nexusPublisher nexusInstanceId: 'nexus01', nexusRepositoryId: 'ejemplo-maven-taller3', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/jenkins_home/workspace/multi-taller3-mod4_feature-nexus/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
=======
				nexusPublisher nexusInstanceId: 'nexus1', nexusRepositoryId: 'ejemplo_Maven_taller3_lmrclo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/jenkins_home/workspace/Multibranch_lmrclo_feature-nexus/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
>>>>>>> bdc524d2011b8212cb745bb4c0457ca4f9f8b92c
            }
        }
   
		stage ('Clean'){
            steps
                {
                    cleanWs()
                }
        }

    }
}
