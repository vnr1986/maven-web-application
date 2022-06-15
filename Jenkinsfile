node{//node starting brace
    
def mvnHome= tool name: "maven3.8.5"
    timestamps{}
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])
    
    stage("SCfromGit"){//stage1 starting brace
               git branch: 'development', credentialsId: '0b2294a7-f911-435d-8311-56b526a82904', url: 'https://github.com/vnr1986/maven-web-application.git' 
    }//stage1 ending brace

    stage("Build"){//stage2 starting brace
              sh "${mvnHome}/bin/mvn clean package"
    }//stage2 ending brace
    
    stage("SQreport"){//stage3 starting brace
              sh "${mvnHome}/bin/mvn sonar:sonar"
    }//stage3 ending brace
    
    stage("UploadToAR"){//stage4 starting brace
              sh "${mvnHome}/bin/mvn deploy"
    }//stage4 ending brace
    
    stage("Deploy"){
        sshagent(['83a58225-9391-4f13-a312-79adefbadd35']){
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.13.206:/opt/apache-tomcat-9.0.63/webapps/"
        }//ssh closing brace
    }//stage5 ending brace
}//node ending brace
