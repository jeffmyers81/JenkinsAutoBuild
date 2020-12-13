node {

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'jeffmyers81/devops_project'
    def registryCredential = 'dockerhub'

        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Building Image') {
 	    newApp = docker.build registry + ":$BUILD_NUMBER"     
            
        }
        stage('Registering Image') {
            docker.withRegistry( '', registryCredential ) {

    		newApp.push()

        }

	}

    stage('Removing image') {

        sh "docker rmi $registry:$BUILD_NUMBER"

        sh "docker rmi $registry:latest"

    }
}
