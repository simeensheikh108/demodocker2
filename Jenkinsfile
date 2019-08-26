node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'simeensheikh/firstdemo'
    def registryCredential = 'docker-hub'
	
	stage('Git') {
		git 'https://github.com/simeensheikh108/demodocker2.git'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Aqua MicroScanner'){
        steps{
            
        
        script{
        ADD https://get.aquasec.com/microscanner /
        RUN chmod +x /microscanner
        RUN /microscanner ZWNmZTU1ZWExNjI5
        }
        }
    }
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
