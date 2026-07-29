piplien {
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
     }
 }
      
