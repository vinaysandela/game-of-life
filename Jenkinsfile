node {
    stage('SCM') {
        git 'https://github.com/vinaysandela/game-of-life.git'
    }
    stage('Build & Package') {
	withSonarQubeEnv('Sonar') {
	        sh 'mvn clean package Sonar:Sonar'
	}	
    }
    stage("Quality Gate") {
	timeout(time: 1, unit: 'HOURS') {
		def qg = waitForQualityGate()
		if (qg.status != 'OK') {
			error "Pipeline aborted due to quality gate failure: ${qg.status}"
		}
	  }
	}
    stage('Results') {
        archive 'gameoflife-web/target/gameoflife.war'
        junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
}