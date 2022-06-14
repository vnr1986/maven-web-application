node{//node starting brace
    
def mvnHome= tool name: "maven3.8.5"
    timestamps{}
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])
    properties([parameters([choice(choices: ['development master test qa'], description: 'please select an branch to run the build', name: 'selectBranch')]), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])

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
    
}//node ending brace
