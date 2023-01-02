node(""){
	withSonarQubeEnv(credentialsId: '2c069a5b-1119-4967-b5f4-0f2b232e26be') {
     stage ('checkout code'){
    	checkout scm
    }
    stage ('Build'){
    	sh "mvn clean install -Dmaven.test.skip=true"
    }
    stage ('Test Cases Execution'){
    	sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
    }
}
}
