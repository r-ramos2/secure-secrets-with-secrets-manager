<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Secrets with Secrets Manager

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-secretsmanager)

**Author:** R  


---

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-security-secretsmanager_r7s8t9u0)

---

## Introducing Today's Project!

In this project, I will demonstrate how to identify and eliminate hardcoded credentials in code by using AWS Secrets Manager. I'm doing this project to learn secure, scalable methods for managing secrets in cloud applications.

### Tools and concepts

Services I used were AWS Secrets Manager, GitHub, and Git. Key concepts I learnt include securely managing credentials, using Git rebase to rewrite commit history, resolving merge conflicts, and integrating cloud-based secrets with Python apps.

### Project reflection

This project took me approximately a 1 hour to complete. The most challenging part was resolving the merge conflicts during rebase. It was most rewarding to see my code push successfully without exposing any credentials.

I did this project to learn secure practices for handling secrets in cloud-based applications. It absolutely met my goals.

---

## Hardcoding credentials

In this project, a sample web app is exposing AWS credentials in config.py. It is unsafe to hardcode credentials because anyone with access to the code can misuse them to access, modify, or destroy resources in your AWS account.

I've set up the initial configuration with placeholder AWS credentials in config.py. These credentials are just examples because they simulate real ones without exposing a real AWS account to security risks.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

---

## Pushing Insecure Code to GitHub

Once I updated the web app code with credentials, I forked the repository because I wanted to create a version of the project under my own GitHub account that I could push changes to and share publicly. A fork is different from a clone because a fork lives on GitHub and lets others view or collaborate on your version, while a clone is just a local copy on your computer.

To connect my local repository to the forked repository, I used `git remote set-url origin <forked-repo-url>` to point the local project to my fork on GitHub. Then I used `git add .` and `git commit -m "Updated config.py with hardcoded credentials"` to stage and save my changes locally. Finally, `git push -u origin main` uploaded my committed changes to the main branch of my forked repository on GitHub.

GitHub blocked my push because it detected hardcoded AWS credentials in my `config.py` file. This is a good security feature because it prevents developers from accidentally exposing sensitive information like access keys, which could be exploited by malicious users to gain unauthorized access to cloud resources and cause financial or data loss.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

Secrets Manager is a secure AWS service for storing and managing sensitive information like API keys, credentials, and tokens. I'm using it to store my AWS Access Key ID and Secret Access Key so they aren't hardcoded in my application code. Other common use cases include storing database credentials, OAuth tokens, and rotating secrets automatically for better security.

Another feature in Secrets Manager is secret rotation, which means automatically changing secrets at regular intervals. It's useful for high-risk credentials, like database passwords, where rotating secrets reduces the risk of exploitation if compromised.

Secrets Manager provides sample code in various languages, like Python, Node.js, and Java, to show developers how to retrieve stored secrets securely in their applications. This is helpful because it simplifies integration, reduces the risk of misconfigurations, and ensures that credentials are accessed securely without hardcoding them in the codebase.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I updated the `config.py` file to retrieve AWS credentials securely from AWS Secrets Manager instead of hardcoding them. The `get_secret()` function will connect to Secrets Manager using the `boto3` client, request the secret named `"aws-access-key"`, and return the decrypted credentials for use in the application.

I also added code to `config.py` to extract the individual credential values from the retrieved secret. This is important because our application expects `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_REGION` to be available as variables, and now they are securely set using the values retrieved from AWS Secrets Manager.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is a way to rewrite a repository’s commit history. I used it to remove the commit that contained hardcoded AWS credentials by interactively editing and dropping that specific commit. This was necessary because even though the credentials were deleted from the current code, they still existed in the repository’s history, and GitHub's secret scanning blocks pushes if sensitive data is found anywhere in that history.

A merge conflict occurred during rebasing because the commit I removed had hardcoded credentials in `config.py`, and the subsequent commit also modified the same file. Git wasn't sure whether to delete the changes from the removed commit or keep the newer changes. I resolved the merge conflict by removing the section with the hardcoded credentials and retaining the updated version of the `config.py` file with the Secrets Manager integration. This allowed me to cleanly rewrite the commit history without exposing any credentials.

Once the merge conflict was resolved, I verified that my hardcoded credentials were removed by checking the `config.py` file in my GitHub repository. I ensured that the file now only contains the code to retrieve credentials from AWS Secrets Manager, and there were no hardcoded credentials left in the file. This confirmed that the commit history had been properly rewritten, and no sensitive data was exposed in the repository.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
