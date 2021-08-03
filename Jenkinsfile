node('ubuntunodeforgol') {
    stage('golbuild') {
        git 'https://github.com/asquarezone/game-of-life.git'
    }
    stage('build') {
        sh 'mvn clean package'
    }
    stage('postbuild') {
        junit '**/TEST-*.xml'
        archive '**/*.war'
    }
}
