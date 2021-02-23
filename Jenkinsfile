//git凭证ID
def git_auth = "github-mysite"
//git的url
def git_url = "https://github.com/zxstar/mymvnweb.git/"

node {
        stage('pull code') {
            checkout([$class: 'GitSCM', branches: [[name: "*/${branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: ${git_aut}, url: "${git_url}"]]])
        }
}
