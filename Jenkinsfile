//git凭证ID
def git_auth = "github-mysite"
//git的url
def git_url = "https://github.com/zxstar/mysite.git/"

node {
        stage('pull code') {
            checkout([$class: 'GitSCM', branches: [[name: "*/${branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: "${git_auth}", url: "${git_url}"]]])
		//checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-mysite', url: 'https://github.com/zxstar/mysite.git']]])
        }
	
	stage('代码审查') {
		sh "echo '代码审查'"
		//定义当前Jenkins的SonarQubeScanner工具
		//def scanerHome = tool 'sonar-scanner'
		//withSonarQubeEnv('sonarqube') {
		//	sh """
		//		cd ${project_name}
		//		$(scanerHome}/bin/sonar-scanner
		//}
	}
}
