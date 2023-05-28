node {
    docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2'){
        stage('Build') {
		sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
		sh 'mvn test -Dmaven.test.failure.ignore=true'
		junit 'target/surefire-reports/*.xml'
        }
	stage('Manual Approval') {
		input message: 'Lanjutkan ke tahap Deploy?'
	}
	stage('Deploy') {
		sh './jenkins/scripts/deliver.sh'
	}
    }
}
