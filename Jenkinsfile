pipeline {
   agent {
        node {
            label 'maven'
         }
   }
   stages {
   stage("Tests") {
        steps {
             sh './mvnw clean test'
        }
   }
   stage("Packages") {
        steps {
             sh '''
                 ./mvnw package -DskipTests \
                 -Dquarkus.package.type=uber-jar
                '''
                archiveArtifacts 'target/*.jar'
             }
    }
    stage('Build Image') {
        environment { QUAY = credentials('QUAY_USER') }
        steps {
            sh '''
                ./mvnw quarkus:add-extension \
                -Dextensions="kubernetes,container-image-jib"
            '''
            sh '''
                ./mvnw package -DskipTests \
                -Dquarkus.jib.base-jvm-image=quay.io/redhattraining/do400-java-alpine-openjdk11-jre:latest \
                -Dquarkus.container-image.build=true \
                -Dquarkus.container-image.registry=quay.io \
                -Dquarkus.container-iamge.group=$afsanafaizi \
                -Dquarkus.container-image.name=do400-deploying-environments \
                -Dquarkus.container-image.username=$svkqzd \
                -Dquarkus.conatiner-image.password="$839fa0200e494e4e9eab" \
                -Dquarkus.container-image.push=true \
            '''
            }
        }
         
    }
 }
      
