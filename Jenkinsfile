pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'

    }
    environment{
        ArtifactId = readMavenPom().getArtifcatId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
    }
    
    stages {
        // Specify various stage with in stages

        //stage 1 : Build
        stage ('Build') {
            steps {
                sh 'mvn clean install package'
        }
    }

    // Stage2 : Testing
    stage ('Test') {
        steps {
            echo ' testing......'
        }
    }
    // Stage 3: Publish the artificate to nexus
    stage ('Publish to Nexus'){
        steps {
            nexusArtifactUploader artifacts: [[artifactId: '${ArtifactId}', 
            classifier: '', 
            file: 'target/AnitDevOpsLab-0.0.4-SNAPSHOT.war',
            type: 'war']],
            credentialsId: '61f10800-a30c-4b4f-a507-be8e393a7b06',
            groupId: '${GroupId}',
            nexusUrl: '172.20.10.193:8081',
            nexusVersion: 'nexus3',
            protocol: 'http', 
            repository: 'AnitDevOpsLab-SNAPSHOT', 
            version: '${Version}'
        }
    }

    //Stage 4 : Print Env vars 
    stage ('Print Environments Variables') {
        steps() {
            echo "Artifact ID is '${ArtifactId}'"
            echo "Version is '${Version}'"
            echo "GroupID is '${GroupId}'"
            echo "Name is '${Name}'"
        }
    }

    // Stage5 : Deploying
    stage ('Deploy') {
        steps {
            echo 'deploying.....'
        }
    }

    }

}