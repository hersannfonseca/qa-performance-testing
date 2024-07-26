pipeline {
    agent any

    parameters {
        string(name: 'JMeterFile', defaultValue: 'Products.jmx', description: 'JMeter test plan file')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/hersannfonseca/qa-performance-testing.git'
            }
        }
        stage('cd') {
            steps {
                bat 'cd scripts'
            }
        }
        stage('Build') {
            steps {
                bat 'jmeter -n -t %JMeterFile% -l results.csv'
            }
        }
        stage('Publish Report') {
            steps {
                publishPerformanceTestReport(target: [
                    reportFile: 'results.csv',
                    format: 'JMeter'
                ])
            }
        }
    }
}