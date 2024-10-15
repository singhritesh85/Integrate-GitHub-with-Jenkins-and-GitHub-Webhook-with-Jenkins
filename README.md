# Integrate-GitHub-with-Jenkins-and-GitHub-Webhook-with-Jenkins

To integrate GitHub with Jenkins we can follow two methods

1. Using SSH Keys
2. Using Personal Access Token.

For this to achieve you must install two pluging **GitHub** and **Git** in Jenkins.

### 1. Integrating GitHub with Jenkins using SSH Keys.

To achieve this Go to **Manage Jenkins > System** then GitHub Servers and do the configuration as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/e44ae6ce-6361-4e1e-97cb-af696b00ff43)
![image](https://github.com/user-attachments/assets/21459b3c-af93-46e5-a3f0-af4ebd2d00d7)

Go to User's **Setting > SSH and GPG Keys** and provide SSH Public Key here as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/8b09d40a-ca21-4635-ad0e-59a3be1bbd09)
![image](https://github.com/user-attachments/assets/b778ae11-27ed-4368-8d56-9c1b893d710b)

Create credential with the Option SSH Username with private key as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/5ccdd4f8-6a84-4f5d-a037-090795894c27)
![image](https://github.com/user-attachments/assets/8b32ecce-c3c0-48de-a0c5-b228005a68b7)

![image](https://github.com/user-attachments/assets/45d1df97-6994-44dd-8514-df5c1e6795e3)

Here I am using SSH Keys for Authentication and the Git Repo URL will be as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/169bb6e8-41d9-44fd-ad6a-1933181c6f9f)

The SSH Private and Public Keys which I had used was present on the Jenkins Slave Node as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/d786084d-21f5-4785-800b-1641bf37a812)

The Jenkins Job has been created as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/bdc90020-aa30-4339-9ddb-6699be4a28e3)
![image](https://github.com/user-attachments/assets/8742a5f0-7db1-48b3-98bc-c09fab4b019a)

The declarative pipeline is as written below.

```
pipeline{
    agent{
        node{
            label "Slave-1"
            customWorkspace "/home/jenkins/demo"
        }
    }
    parameters { 
        string(name: 'COMMIT_ID', defaultValue: '', description: 'Provide Commit ID') 
    }
    stages{
        stage("clone-code"){
            steps{
                cleanWs()
                checkout scmGit(branches: [[name: "${COMMIT_ID}"]], extensions: [], userRemoteConfigs: [[credentialsId: 'github-cred', url: 'git@github.com:singhritesh85/hello-world2.git']])
            }
        }
    }
}
```

Finally while running the Jenkins Job I provided Commit ID and Jenkins Job ran successfully.

### 2. Integrating GitHub with Jenkins Using Personal Access Token.

Created Jenkins credential with username and password as shown in the screenshot attached below. For username provide the username for GitHub and Password as Personal Access Token (PAT).

![image](https://github.com/user-attachments/assets/c594f715-f531-4870-8edd-05cbd6670c80)

Create Jenkins Job as shown in the screenshot attached below with webhook.

![image](https://github.com/user-attachments/assets/bd545f68-ef44-47fd-9143-7b5893b49033)

```
pipeline{
    agent{
        node{
            label "Slave-1"
            customWorkspace "/home/jenkins/demo"
        }
    }
    stages{
        stage("clone-code"){
            steps{
                cleanWs()
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/singhritesh85/hello-world2.git']])
            }
        }
    }
}
```

Configuration in GitHub Repository setting is as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/90e4cfd6-f7c8-4e86-8380-bcd88b386e7f)
![image](https://github.com/user-attachments/assets/2a003b37-0d4d-4220-afd3-55204ec49967)
![image](https://github.com/user-attachments/assets/a973969f-975c-477d-88b8-bee1d2c84d35)

I did some changes in Dockerfile and webhook triggered as shown in the screenshot attached below and Jenkins Job ran successfully. 

![image](https://github.com/user-attachments/assets/32b5dcb6-ca3e-4db7-8dc7-3ca8884797be)
![image](https://github.com/user-attachments/assets/91f08fd2-0970-4f1e-aab9-def8cc59419b)

The source code is present in GitHub Private Repo as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/5f8d2760-4781-4f72-9c73-f4810f6a4f89)





