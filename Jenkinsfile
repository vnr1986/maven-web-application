node{

stage("1-getSCfromGit"){
       git branch: 'development', credentialsId: '0b2294a7-f911-435d-8311-56b526a82904', url: 'https://github.com/vnr1986/maven-web-application.git'    
}
   
stage("2-Build"){
      sh "${mvnHome}/bin/mvn clean package"
}
}
