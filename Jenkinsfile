node('slave') {
    
     stage('test pipeline') {
        sh(script: """
            echo "hello"
           git clone https://github.com/steflaarman/deploy-examples.git
           cd ./golang
           
           docker build . -t test
        """)
    }
}