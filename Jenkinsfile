node {
    def app
    def project = 'trusty-drive-228822'
    def appName = 'hellonode'
    def imageTag = "gcr.io/${project}/${appName}:${env.BUILD_NUMBER}.latest"
    
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        //app = docker.build("gcr.io/trusty-drive-228822/hellonode")
        app = docker.build("gcr.io/${project}/${appName}")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
         
         
        
        docker.withRegistry('https://gcr.io/trusty-drive-228822/', 'gcr:trusty-drive-228822') {
            
            //app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
            app.push()
        }
        
        
        //sh("eval kubectl config current-context")

        
    }
}
