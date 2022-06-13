node{//node starting brace
    
def mvnHome= tool name: "maven3.8.5"
    
    stage("1-getSCfromGit"){//stage1 starting brace
               git branch: 'development', credentialsId: '0b2294a7-f911-435d-8311-56b526a82904', url: 'https://github.com/vnr1986/maven-web-application.git' 
    }//stage1 ending brace

    stage("2-Build"){//stage2 starting brace
              sh "${mvnHome}/bin/mvn clean package"
    }//stage2 ending brace
    
}//node ending brace
