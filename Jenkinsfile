node{//node starting brace
    
def mvnHome= tool name: "maven3.8.5"
    timestamps{}
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])
    
    stage("1-getSCfromGit"){//stage1 starting brace
               git branch: 'development', credentialsId: '0b2294a7-f911-435d-8311-56b526a82904', url: 'https://github.com/vnr1986/maven-web-application.git' 
    }//stage1 ending brace

    stage("2-Build"){//stage2 starting brace
              sh "${mvnHome}/bin/mvn clean package"
    }//stage2 ending brace
    
    stage("3-SQreport"){//stage3 starting brace
              sh "${mvnHome}/bin/mvn sonar:sonar"
    }//stage3 ending brace
    
    stage("4-uploadToAR"){//stage4 starting brace
              sh "${mvnHome}/bin/mvn deploy"
    }//stage4 ending brace
    
    stage("5-Deploy"){
        sshagent(['e4d95cbf-3d67-41bd-8e57-1b0810dd9431']) {
            sh "scp -r target/maven-web-application.war ec2-user@172.31.13.206:/opt/apache-tomcat-9.0.63/webapps"
    }//ssh closing brace
 }//stage5 ending brace
}//node ending brace
