pipeline {
  agent none
  stages {
    stage('build') {
      steps {
        echo 'build done1'
        sh './gradlew clean build'
      }
    }

    stage('upload') {
      steps {
        echo 'upload done2'
        sh 'aws s3 cp build/libs/application.war s3://springboot-cicd-shuwang/application.war --region us-east-2'
      }
    }

    stage('deploy') {
      steps {
        echo 'deploy done3'
        sh 'aws elasticbeanstalk create-application-version --region us-east-2 --application-name springboot-cicd-shuwang --version-label ${BUILD_TAG} --source-bundle S3Bucket="springboot-cicd-shuwang",S3Key="application.war"' 
        sh 'aws elasticbeanstalk update-environment --region us-east-2 --environment-name Springbootcicdshuwang-env-1 --version-label ${BUILD_TAG}'
      }
    }

  }
}