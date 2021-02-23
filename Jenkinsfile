//git凭证ID
def git_auth = "github-mysite"
//git的url
def git_url = "https://github.com/zxstar/mysite.git/"

node {
        stage('pull code') {
            checkout([$class: 'GitSCM', branches: [[name: "*/${branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: ${git_auth}, url: "${git_url}"]]])
		//checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-mysite', url: 'https://github.com/zxstar/mysite.git']]])
        }
}
