node("master") {
#    docker.withRegistry('lukeloresch/dockerized_node', 'hub-lukeloresch') {
	sh "docker pull lukeloresch/dockerized_node"    
        git url: "https://github.com/hub-lukeloresch/dockerized_node.git", credentialsId: 'hub-lukeloresch'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "test"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}