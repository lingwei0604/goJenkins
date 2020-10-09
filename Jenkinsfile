pipeline {
    agent any

    stages {
        stage('UnitTest') {
            steps {
               sh 'chmod +x rununittest.sh; ./rununittest.sh'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x buildapp.sh;./buildapp.sh'
            }
        }
        stage('Deploy') {
            steps {
                sh 'chmod +x deployapp.sh; ./deployapp.sh'
            }
        }
    }
    post {
        failure {
            mail bcc: '', body: "<b>gopro build failed</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset    : 'UTF-8', from: 'yunwei-monitor@donews.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "mawencheng@donews.com";
        }
        success {
            mail bcc: '', body: """
                                <div id="content">
                                  <h1>CI报告</h1>
                                  <div id="sum2">
                                      <h2>Jenkins 运行结果</h2>
                                      <ul>
                                      <li>Job URL : <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></li>
                                	  <li>jenkins的执行结果 : <a>jenkins 执行成功</a></li>
                                	  <li>jenkins的Job名称 : <a id="url_1">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></li>
                                	  <li>jenkins的URL : <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></li>
                                	  <li>jenkins项目名称 : <a>${env.JOB_NAME}</a></li>
                                      </ul>
                                  </div>
                                  <div id="sum0">
                                  <h2>GIT 信息</h2>
                                  <ul>
                                	<li>GIT项目的地址 : <a>${git_url}</a></li>
                                	<li>GIT项目当前的分支名 : ${git_branch}</li>
                                	<li>GIT最后一次提交的commitID : ${git_project_commitID}</li>
                                  </ul>
                                  </div>
                                <div id="sum0">
                                  <h2>运行环境</h2>
                                  <ul>
                                	<li>项目发布的环境:  ${params.build_env}</li>
                                	<li>项目环境访问地址: ${params.mail_project_url} </li>
                                	<li>项目运行环境的IP : ${params.mail_project_ip}</li>
                                	<li>项目运行环境的jar路径 : ${params.project_path}</li>
                                  </ul>
                                  </div>
                                  </div>
                                    """, cc: '', charset: 'UTF-8', from: 'yunwei-monitor@donews.com', mimeType: 'text/html', replyTo: '', subject: "SUCCESS CI: Project name -> ${env.JOB_NAME}", to: "mawencheng@donews.com";
        }
    }
}