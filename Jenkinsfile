#!groovy

node() {

    currentBuild.result = "SUCCESS"

    env.TAG_REPO = "lukeloresch/dockerized_node/"
    env.DOCKER_HUB_CREDS = ""; //env.DOCKER_HUB_CREDS_DEV;
    
    try {
        docker.withRegistry("${env.DOCKER_HUB_REGISTRY_DEV}", "${env.DOCKER_HUB_CREDS}", {
            stage('Checkout') {
                checkout scm
                sh "git rev-parse --short HEAD > .git/commit-id"
                env.COMMIT_ID = readFile('.git/commit-id').substring(0, 6).toUpperCase()
                echo "Generating Docker Image tag based on commit id ${env.TAG_REPO}-${env.COMMIT_ID}"
                env.TAG_REPO = env.TAG_REPO + "-" + env.COMMIT_ID;
            }
            stage('Build Image') {
                echo 'build'
                sh "docker build --pull=true -t ${env.TAG_REPO} ."
            }
            stage('Deploy') {
                echo 'deploy'
                sh "docker push ${env.TAG_REPO}"
            }
            stage('Cleanup') {
                echo "Cleaning up build files"
                sh " rm -fr ./_book"
            }
        });
    }
    catch(err) {
        throw err;
    }
}
