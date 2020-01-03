node {

    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.

    def server = Artifactory.server "SERVER_ID"

    // Create an Artifactory Gradle instance.

    def rtGradle = Artifactory.newGradleBuild()

    def buildInfo



    stage('Clone sources') {

        git url: 'https://github.com/Mugundhanp2497/gradle-build1.git'

    }



    stage('Artifactory configuration') {

        // Tool name from Jenkins configuration

        rtGradle.tool = "Gradle-2.4"

        // Set Artifactory repositories for dependencies resolution and artifacts deployment.

        rtGradle.deployer repo:'ext-release-local', server: server

        rtGradle.resolver repo:'remote-repos', server: server

    }



    stage('Gradle build') {

        buildInfo = rtGradle.run rootDir: "/Users/Y509477/Downloads/gradle-6.0.1/bin", buildFile: 'build.gradle', tasks: 'clean artifactoryPublish'

    }



    stage('Publish build info') {

        server.publishBuildInfo buildInfo

    }

}
