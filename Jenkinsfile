
	
node(){

    def mvnHome = tool 'MavenBuildTool'
    def sonarScanner = tool name: 'ForSonarQubeScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'

 

    
    try {
        stage('Checkout Code'){
            checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '60d8691b-71cc-4878-8c54-0ab3f3debec0', url: 'https://github.com/shrth7/MavenBuild.git']])
        }

        stage('Maven Build'){
            sh "${mvnHome}/bin/mvn clean install -Dmaven.test.skip=true"
        }

        stage('Test Cases Execution'){
            sh "${mvnHome}/bin/mvn test"
        }

        stage('SonarQube Analysis'){
            withSonarQubeEnv(credentialsId: '2c069a5b-1119-4967-b5f4-0f2b232e26be') {
    		sh "${sonarScanner}/bin/sonar-scanner"
	    }
	}



    }
    catch (Exception e){
        currentBuild.result = 'FAILURE'
        echo currentBuild.currentResult
    }finally{
        emailext body: '''Hello Sharath ,
The build was successful''', subject: 'Build Status!!', to: 'shrth7777@gmail.com'
    }
}
