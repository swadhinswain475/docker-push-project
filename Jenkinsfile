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
	 sh 'docker build -t swadhinswain475/dockerimage'
	}
   }
  }
  stage("docker image pull to docker hub"){
   steps{
    script{
	 withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
      sh 'docker login -u swadhinswain475 -p $(dockerhubpwd)'
}
      sh 'docker push swadhinswain475/MyBuildImage'
	}
   }
  }
 }
}
