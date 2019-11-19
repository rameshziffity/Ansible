pipeline {
  agent any
  options { 
    skipDefaultCheckout()
  }
  
  }
  stages {
    stage ('Launching Pipeline') {
      steps {
            script {
                    currentBuild.displayName = "${Magento_Branch}"
                }
                 }
                   

        checkout scm: [
        $class: 'GitSCM',
        branches: [[name: "*/${params.Magento_Branch}"]],
        doGenerateSubmoduleConfigurations: false,
        extensions: [ [$class: 'CloneOption', depth: 0, noTags: false, reference: '', shallow: true],
                      [$class: 'RelativeTargetDirectory', relativeTargetDir: 'magento']],
        submoduleCfg: [],
        userRemoteConfigs: [[credentialsId: '937d9d40-8f9c-4629-bedb-4b7e0a046999',
                             url: 'https://github.com/rameshziffity/devopsdemo.git']]]
                             
        checkout scm: [
        $class: 'GitSCM',
        branches: [[name: "*/${params.Ansible_Branch}"]],
        doGenerateSubmoduleConfigurations: false,
        extensions: [ [$class: 'CloneOption', depth: 0, noTags: false, reference: '', shallow: true],
                      [$class: 'RelativeTargetDirectory', relativeTargetDir: 'ansible']],
        submoduleCfg: [],
        userRemoteConfigs: [[credentialsId: '937d9d40-8f9c-4629-bedb-4b7e0a046999',
                             url: 'https://github.com/rameshziffity/Ansible.git']]]
      }
  
    } 
	
    
    stage ('Unit Test') {
      steps {
        script {
          if (fileExists('magento/tests')) {
            try {
              sh 'phpunit --log-junit test.xml magento/tests/*Test.php'
            } catch(err) {
            step([$class: 'JUnitResultArchiver', testResults: 'test.xml'])
            throw err
            }
          } 
		else {
              sh 'echo "No tests directory. Skipping Unit Test."'
          }     
        }
      }
    
    }
    stage("Code Analysis") {
      steps {
        script {
          if (fileExists('magento/tests')) {
            try {
              sh 'phpunit --log-junit test.xml magento/tests/*Test.php'
            } catch(err) {
            step([$class: 'JUnitResultArchiver', testResults: 'test.xml'])
            throw err
            }
          } 
		else {
              sh 'echo "No tests directory. Skipping Code Analysis."'
          }  
        }   
        
       }
      
      }
    
    stage ('Launching Server & Deploy') {
      steps {  
          sh 'curl -X POST -u z0057:Ziffity$$2323 http://ci.ziffity.com:8080/job/DEVOPS.DEMO.MAGE.DEPLOY/build'
   }
}
    
    stage ('Automation Testing') {
      steps {
        echo('Testing Completed')        
      }

    }
    stage ('Ready for QA') {
      steps {  
        echo('Ready For QA')
      }
    }
    
    
