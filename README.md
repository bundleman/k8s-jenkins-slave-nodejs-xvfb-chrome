<img src="https://cloutainer.github.io/documentation/images/cloutainer.svg?v5" align="right">

# k8s-jenkins-slave-nodejs-xvfb-chrome

Kubernetes Docker image providing Jenkins Slave JNLP and Node.JS.


-----
&nbsp;

### Preinstalled Tools

 * yarn, nodejs, npm, cloudfoundry-cli, git, curl, wget, Xvfb, chrome

-----
&nbsp;

### Usage

Use with Kubernetes Jenkins Plugin like so:

```groovy
podTemplate(
  name: 'nodejs-xvfb-chrome-v17',
  label: 'k8s-jenkins-slave-nodejs-xvfb-chrome-v17',
  cloud: 'mycloud',
  nodeSelector: 'failure-domain.beta.kubernetes.io/zone=eu-west-1a',
  containers: [
    containerTemplate(
      name: 'jnlp',
      image: 'cloutainer/k8s-jenkins-slave-nodejs-xvfb-chrome:v17',
      privileged: false,
      alwaysPullImage: false,
      workingDir: '/home/jenkins',
      resourceRequestCpu: '500m',
      resourceLimitCpu: '1',
      resourceRequestMemory: '3000Mi',
      resourceLimitMemory: '3000Mi'
    )
  ]
) {
  node('k8s-jenkins-slave-nodejs-xvfb-chrome-v17') {
    stage('build and test') {
      sh 'yarn -version'
      sh 'git clone https://github.com/clouless/angular-4-unit-test-dummy.git code'
      dir('code') {
        sh 'yarn && yarn test'
      }
    }
  }
}
```


-----
&nbsp;

### License

[MIT](https://github.com/cloutainer/k8s-jenkins-slave-nodejs-xvfb-chrome/blob/master/LICENSE) © [Bernhard Grünewaldt](https://github.com/clouless)
