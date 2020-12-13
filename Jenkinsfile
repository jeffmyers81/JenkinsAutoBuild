node {

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'jeffmyers81/devops_project'
    def registryCredential = 'dockerhub'

        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Building Image') {
            docker.withRegistry('https://' + registry, registryCredential) {
                def buildName = registry + ":$BUILD_NUMBER"
                    newApp = docker.build buildName
                    newApp.push()
            }
        }
        stage('Registering Image') {
            docker.withRegistry( 'https://' + registry, registryCredential ) {

    		newApp.push 'latest2'

        }

	}

    stage('Removing image') {

        sh "docker rmi $registry:$BUILD_NUMBER"

        sh "docker rmi $registry:latest"

    }

}
