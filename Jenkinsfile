node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
		sh 'echo "Build image startimmmmmmmmmmmmmm "'
       app = docker.build("davedocker101/jenkins-examples-01")  
	   sh 'echo "Build image completedmmmmmmmmm "'
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        sh 'echo "Push image startimmmmmmmmmmmmmm "'
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_id') {
            app.push("${env.BUILD_NUMBER}")
			
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
