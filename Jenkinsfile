pipeline {
    agent {
        kubernetes {
            // Rather than inline YAML, in a multibranch Pipeline you could use: yamlFile 'jenkins-pod.yaml'
            // Or, to avoid YAML:
            // containerTemplate {
            //     name 'shell'
            //     image 'ubuntu'
            //     command 'sleep'
            //     args 'infinity'
            // }
            yaml '''
                apiVersion: v1
                kind: Pod
                spec:
                  containers:
                  - name: maven
                    image: maven:alpine
                    command:
                    - cat
                    tty: true
                  - name: node
                    image: node:lts-alpine3.18
                    command:
                    - cat
                    tty: true
                '''
            defaultContainer 'maven'
        }
    }
    stages {
        stage('Run maven') {
            steps {
                container('maven') {
                    sh 'mvn -version'
                    sh 'echo Hello > hello.txt'
                    sh 'ls -last'
                }
                container('node') {
                    sh 'npm version'
                    sh 'cat hello.txt'
                    sh 'ls -last'
                }
            }
        }
    }
}
