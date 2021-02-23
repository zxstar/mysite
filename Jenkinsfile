//git凭证ID
def git_auth = "github-mysite"
//git的url
def git_url = "https://github.com/zxstar/mysite.git/"

//docker tag
def tag="latest"
//harbor url
def harbor_url = "8.136.189.162:80"
//harbor project
def harbor_project = "mysite"

def image_name = "mysite"

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
	
	stage('镜像制作上传') {
		sh "tar zcf mysite.tar.gz *.html"
		sh "docker build -t ${harbor_url}/${harbor_project}/${image_name}:${tag} ."
		
		withCredentials([usernamePassword(credentialsId: 'harbor', passwordVariable: 'password', usernameVariable: 'username')]) {
		    // some block
			sh "docker login -u ${username} -p ${password} ${harbor_url}"
			//镜像上传
			sh "docker push ${harbor_url}/${harbor_project}/${image_name}:${tag}"
			
			sh "echo '镜像上传成功'"
		}
	}
	
	stage('镜像部署') {
		//sshPublisher(publishers: [sshPublisherDesc(configName: 'app', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '/opt/jenkins_shell/deploy.sh $harbor_url $harbor_project $image_name $tag', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
		// 测试public over ssh
		sshPublisher(publishers: [sshPublisherDesc(configName: 'app', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'mkdir /root/overssh', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
	
	}
}
