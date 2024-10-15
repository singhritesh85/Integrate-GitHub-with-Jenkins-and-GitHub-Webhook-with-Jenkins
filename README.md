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

![image](https://github.com/user-attachments/assets/81bc952a-4c15-4fd2-b9aa-f796f0a83b75)
![image](https://github.com/user-attachments/assets/e6744a99-5231-4fc1-8178-df5de4a018cd)


