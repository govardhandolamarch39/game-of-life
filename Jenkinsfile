pipeline {
    agent { label 'MAVEN_JDK8' }
    trigger { cron ('H/15 * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['testing', package', 'install', 'clean'] , description: 'Maven_Goal' )
    }
    stages {  
        stage('vcs') {
            steps {
            git url: 'https://github.com/govardhandolamarch39/game-of-life.git',
                branch: 'declarative'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_8_UBUNTU'
            steps {
                sh "mvn testing"
            }
        }
        stage('post build') {
            steps {    
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST*-.xml',
            }
        }
        post {
            success {
                mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is success",
                    body: "Use this URL ${BUILD_URL} for more info",
                    to : "team-all-dhola@dhola.com",
                    from: 'durga.td44@gmail.com'
            }
            failure{
                mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is success",
                body: "Use this URL ${BUILD_URL} for more info",
                to: "${GIT_AUTHOR_EMAIL}",
                from: 'durga.td44@gmail.com
        }    
    }
}
    
    

