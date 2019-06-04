node ('master') {

	stage('SCM') {
		checkout scm		
	}

    stage('Build') {
        sh """            
            docker build -t rafaelfmezquita/demo-k8s .             
        """
    }

	stage('Push') {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')]) {
            sh """
                docker login -u ${docker_user} -p ${docker_pass}
                docker push rafaelfmezquita/demo-k8s
            """
        }
	}

	stage('Deploy') {
        configFileProvider([configFile(fileId: 'hosts_k8s', targetLocation: "${env.WORKSPACE}/hosts_k8s")]) {    
            sh """
                ls -ltrha
                ansible-playbook demo-k8s-playbook.yml
            """
        }        
	}

	stage('Notify'){
        emailext( 
            attachLog: true, 
            body: "Check console output at ${env.BUILD_URL} to view the results.", 
            compressLog: true, 
            subject: "demo-k8s - Build #${env.BUILD_NUMBER} - completed!", 
            to: 'rafaelf.mezquita@gmail.com'
        )
	}
}
