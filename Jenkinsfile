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
				nexusPublisher nexusInstanceId: 'nsx01', nexusRepositoryId: 'taller4', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/jenkins_home/workspace/tallerm4-nexus/build/DevOpsUsach2020-1.0.0.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '1.0.0']]]
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
