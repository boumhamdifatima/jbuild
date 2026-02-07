def pipelineContext = [:]
node {

   def registryProjet='ghcr.io/boumhamdifatima/jbuild'
	 def IMAGE="${registryProjet}:version-${env.BUILD_ID}"

	 echo "IMAGE = $IMAGE"

    stage('Clone') {
    			checkout scm
		}

		def img = stage('Build') {
					docker.build("$IMAGE",  '.')
		}
	
		stage('Run') {
					img.withRun("--name run-$BUILD_ID -p 80:80") { c ->
						sh 'sleep 5'
						sh 'curl localhost'
          }					
		}

		stage('Push') {
					docker.withRegistry('https://ghcr.io', 'registrygithub') {
							img.push 'latest'
              img.push()
					}
		}
 
}

