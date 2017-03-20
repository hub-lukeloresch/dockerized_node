node('master') {
	currentBuild.result = "SUCCESS" 
	env.TAG_REPO = "https://hub.docker.com/r/lukeloresch/dockerized_node/"
	
	try {
			stage('Checkout') {
				checkout scm
   		   		sh "git rev-parse HEAD > .git/commit-id"
				env.COMMIT_ID = readFile('.git/commit-id').substring(0, 7).toUpperCase()
				echo "Generating Docker Image tag based on commit id ${env.TAG_REPO}-${env.COMMIT_ID}"
				echo "${env.COMMIT_ID}"
			}
			stage ('Build Image') {
				echo 'build'
				sh "docker build -t ${env.TAG_REPO} ."
			}
			stage ('Deploy') {
				echo 'deploy'
				sh "docker push ${env.TAG_REPO}"

			}
		
	}
	catch(err) {
		throw err;
	}
}
