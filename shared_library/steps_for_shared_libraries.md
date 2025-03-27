# Jenkins Shared Libraries

## What are Jenkins Shared Libraries?
Jenkins Shared Libraries allow you to create reusable functions and workflows that can be used across multiple Jenkins pipelines. They help in maintaining DRY (Don't Repeat Yourself) principles, improving maintainability, and streamlining pipeline development.

## Setting Up a Shared Library

### 1. Create a Git Repository for the Library
Jenkins Shared Libraries are usually stored in a version control system like GitHub.

- Create a new Git repository (e.g., `jenkins-shared-lib`).
- Inside the repository, create a directory structure:
  ```
  jenkins-shared-lib/
  ├── vars/
  │   ├── example.groovy
  │   ├── notifySlack.groovy
  ├── src/
  ├── resources/
  ├── README.md
  ```

### 2. Writing a Shared Library Function
Shared library functions are stored inside the `vars/` directory as Groovy scripts.

#### Example: Deploy Web App Using Ansible
Create `vars/deployWebApp.groovy`:
```groovy
// vars/deployWebApp.groovy
void call(String server, String playbook) {
    stage('Deploy Web App') {
        sh "ansible-playbook -i ${server}, ${playbook}"
    }
}
```

#### Example: Send Slack Notification
Create `vars/notifySlack.groovy`:
```groovy
// vars/notifySlack.groovy
void call(String message, String channel = '#general') {
    stage('Send Slack Notification') {
        sh "curl -X POST --data-urlencode 'payload={\"text\": \"${message}\", \"channel\": \"${channel}\"}' https://hooks.slack.com/services/YOUR_SLACK_WEBHOOK"
    }
}
```

## Configuring Jenkins to Use the Shared Library
1. Go to **Manage Jenkins > Configure System**.
2. Find **Global Pipeline Libraries**.
3. Add a new library:
   - Name: `jenkins-shared-lib`
   - Default version: `main` (or specify a branch)
   - Retrieval Method: Git
   - Enter your Git repository URL.

## Using the Shared Library in a Pipeline

```groovy
@Library('jenkins-shared-lib') _

pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                deployWebApp('myserver.com', 'playbook.yml')
            }
        }
        stage('Notify') {
            steps {
                notifySlack('Deployment Successful!')
            }
        }
    }
}
```


