node {
    def app

    stage 'checkout' {
checkout([$class: 'GitSCM', branches: [[name: '*/${BRANCH_NAME}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '5a02a237-d956-42c5-bdcc-866e9579480f', url: 'https://github.com/yogeshdeepti/mavenproject2.git']]])

    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        env.DIRPATH=pwd()
        sh "echo ${env.DIRPATH}"
        env.BRANCH=env.BRANCH_NAME
        sh "echo ${env.BRANCH}"
        app = docker.build("${env.DIRPATH}/example")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }         
    
}
