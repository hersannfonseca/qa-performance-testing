pipeline {
    agent any

    parameters {
        string(name: 'JMeterFile', defaultValue: 'Products.jmx', description: 'JMeter test plan file')
        string(name: 'JMeterPath', defaultValue: 'C:\\apache-jmeter-5.6.3\\bin', description: 'JMeter path')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/hersannfonseca/qa-performance-testing.git'
            }
        }
        stage('Run test') {
            steps {
                bat 'cd %JMeterPath% && jmeter -n -t %JMeterFile% -l results.csv'
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