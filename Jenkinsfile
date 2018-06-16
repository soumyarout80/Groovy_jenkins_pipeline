#!groovy

//Groovy pipeline code

 

pipeline {
agent { label ‘master’ }

stages{

stage(‘Clean Start’) {
steps {
dir(‘buildDIR’) {
deleteDir()
}
}
}

stage(‘Code Pull’) {
steps {
deleteDir()
// Get  code from a git repository
git url: ‘www.git/something.com’ branch: ‘something’
}
}

stage(‘Unit Testing’) {
steps {
// Unit testing
sh “””
something
“””
}
}

stage(‘code coverage’) {
steps {
// Code coverage report
sh “””
sudo python3 -m pytest –cov ./ –cov-report term-missing –cov-report xml
“””
step([$class: ‘CoberturaPublisher’, autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: ‘**/coverage.xml’, failUnhealthy: true, failUnstable: false,lineCoverageTargets: ’75, 60, 50′, maxNumberOfBuilds: 0, onlyStable: false, sourceEncoding: ‘ASCII’, zoomCoverageChart: false])
}
}

}
}

// Send email notification for each build for success and fail
post {
success {
emailext attachLog: true, body: ”’${FILE, path=”/var/lib/jenkins/email-template/my.html”}”’ , subject: “ALERT! [BuildResult][${currentBuild.currentResult}] – Job ‘${env.JOB_NAME}’ (${env.BUILD_NUMBER})” , to: ‘something@xyz.com’, from: ‘something@xyz.com’, mimeType: ‘text/html’;
}
failure {
emailext attachLog: true, body: ”’${FILE, path=”/var/lib/jenkins/email-template/my-template.html”}”’ , subject: “ALERT! [BuildResult][${currentBuild.currentResult}] – Job ‘${env.JOB_NAME}’ (${env.BUILD_NUMBER})” , to: ‘something@xyz.com’, from: ‘something@xyz.com’, mimeType: ‘text/html’;
}
}
}
