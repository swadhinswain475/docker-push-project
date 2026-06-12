pipeline{
 tools{
  jdk 'JAVA_HOME_LINUX'
  maven 'MAVEN_HOME_LINUX'
 }
 agent{
  label 'linux-slave'
 }
 stages{
  stage("git checkout"){
   steps{
    git branch: 'main', url: 'https://github.com/swadhinswain475/docker-push-project.git'
   }
  }
  stage("maven package"){
   steps{
    sh 'mvn clean package'
   }
  }
  stage("docker image build"){
   steps{
    script{
	 sh 'docker build -t swadhinswain475/myimage .'
	}
   }
  }
  stage("docker image pull to docker hub"){
   steps{
    script{
	 withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pwd', usernameVariable: 'user')]) {
      sh 'docker login -u $(user) -p $(pwd)'
}
      sh 'docker push swadhinswain475/myimage'
	}
   }
  }
 }
}
