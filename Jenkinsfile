node("master") {
    docker.withRegistry('https://hub.docker.com/r/lukeloresch/dockerized_node/', 'hub-lukeloresch') {
	//sh "docker pull lukeloresch/dockerized_node"    
        git url: "https://github.com/hub-lukeloresch/dockerized_node.git", credentialsId: 'hub-lukeloresch'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "lukeloresch/dockerized_node"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
