pipeline {
    agent any
    parameters {
        string(name: 'SCRIPT_NAME', defaultValue: 'Products.jmx', description: 'Script name')
        string(name: 'THREADS', defaultValue: '5', description: 'Number of threads')
        string(name: 'RAMP_UP', defaultValue: '10', description: 'Ramp-up period')
    }
    stages {
        stage('Build') {
            steps {
                bat 'cd C:\\apache-jmeter-5.6.3\\bin && jmeter -n -t D:\\Hersann\\GitHub\\qa-performance-testing\\scripts\\Products.jmx -l C:\\apache-jmeter-5.6.3\\logs\\logs-${currentBuild.startTimeInMillis}.jtl -Jthreads=${params.THREADS} -Jramp_up=${params.RAMP_UP}'
            }
        }
    }
}