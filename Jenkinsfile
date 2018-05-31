node {
    stage('SCM') {
        git 'https://github.com/vinaysandela/game-of-life.git'
    }
    stage('Build & Package') {
        sh 'mvn package'
    }
    stage('Results') {
        archive 'gameoflife-web/target/gameoflife.war'
        junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
}