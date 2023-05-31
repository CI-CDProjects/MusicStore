pipeline {
    agent { label ".NET_6.0"}
    triggers { pollSCM ('* * * * *') }
    stages {
        stage('VCS') {
            steps {
                git branch: 'declarative',
                    url: 'https://github.com/CI-CDProjects/MusicStore.git'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet restore ./MusicStore/MusicStore.csproj && dotnet build ./MusicStore/MusicStore.csproj'
            }
        }
        stage('Tests') {
            steps {
                sh 'dotnet test ./MusicStoreTest/MusicStoreTest.csproj --logger "junit;LogFilePath=TEST-musicstoretest.xml"'
                junit testResults: '**/TEST-*.xml'
            }
        }
    }
}