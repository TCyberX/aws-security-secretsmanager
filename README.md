

# Secure Secrets with Secrets Manager

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-secretsmanager)

**Author:** Albert  
**Email:** tapcyberx@gmail.com

---

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_r7s8t9u0)

---

## Introducing Today's Project!

In this project, I’ll demonstrate how to use AWS Secrets Manager for secure credentials management. 

The goal is to learn how to protect sensitive data like (database credentials and API keys) when connecting live applications to AWS services and environments. This is a critical step in building secure, production-ready cloud systems.

### Tools and concepts

Services I used were Secret Manager, GitHub, S3 , IAM.

Key concepts I learnt include GitHub secret scanning, the risks of hardcoding credentials, using git rebase to rewrite the commit history of a repository, forking a repository. 

### Project reflection

This project took me approximately took me around more or less 5 hours. 
The most challenging part was pushing the code resolving errors and also playing with repository.

I did this project today to learn more about protecting/securing the code using services like AWS Secrets Manager. This project met my goals in using the best practise credentials management, and helped us build the skills in Git (e.g rebasting) along the way.

---

## Hardcoding credentials

In this project, the sample app exposes the developer’s AWS access keys and access key ID directly in the code. This is highly insecure because once that code is made public (e.g. on GitHub), anyone can extract those credentials and gain access to the AWS environment. This could lead to data theft, resource deletion, or unauthorized billing.

This example highlights the importance of using tools like AWS Secrets Manager to securely manage credentials and keep them out of source code.

In this step, I’ve set up the initial configuration of the web app using a sample Access Key and Secret Access Key. These are test credentials, not linked to my real AWS account. This approach ensures I can safely demonstrate how the app handles credentials without risking exposure of sensitive data or compromising my actual AWS environment.



![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

As an extension for this project, I also decided to run the web app locally using my own AWS credentials to set up my virtual environment, I installed packages like boto3, uvicorn and  fast-api, which are packages the app.py uses to connect the web app to AWS.

When I first ran the app, I ran into an error (InvalidAccessKeyId) because I was using test credentials - Not real AWS Account.



To resolve the 'InvalidAccessKeyId' error, I updated the (config.py) file to use my account access key ID and secret access key. Let's test in real excenario (no more test credentials). 

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_wghjteykut)

---

## Pushing Insecure Code to GitHub

In this step of my cloud security project, I updated the web app code with sample credentials and then forked the repository to simulate what it’s like to push insecure code to a public repo.

A fork creates a new repository under my GitHub account, allowing me to experiment independently. This is different from a clone, which only copies the code to my local machine without creating a separate GitHub project.

This exercise demonstrates how easily AWS credentials can be exposed, and why secrets should never be hardcoded a critical lesson for any developer or cloud engineer.

 I connected my local project to my forked GitHub repository using the git remote set-url origin command. Then I used git add, git commit, and git push to upload my changes, including the config file with test credentials.

This step helped me simulate what happens when sensitive data is accidentally pushed to a public repo. It was a great hands-on way to understand the risks of hardcoding credentials and why secure practices like using AWS Secrets Manager are so important.

GitHub blocked my push because of secret scanning features detected that we hardcoding AWS credentials This is a good security feature because prevent from revealing personal information in a public repository.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

Secrets Manager is an AWS service that help us with securely storing and retrieving secrets e.g. database credentials, API keys, and anything I deem sensitive. I using it to store AWS access key ID and secret access key .Other common use cases include OAuth keys and even account IDs or URLs I don't want people to see our code.

Another great feature I explored in AWS Secrets Manager is secret rotation . This means your keys or credentials can be automatically changed on a regular schedule.

It’s super useful in high-risk environments if an attacker ever gets hold of your credentials, secret rotation helps limit how long they have access. Secrets Manager handles generating and updating the values for you, adding an extra layer of security without extra work! 

 AWS Secrets Manager makes it easy for developers to integrate secure credential access into their applications. 

 It provides sample code in multiple languages like Python, Java, and more so instead of hardcoding credentials, you can use these snippets to securely retrieve secrets.
 I used the sample code in my config.py file to build a function that connects directly to Secrets Manager and fetches credentials when needed.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I just updated the config.py file to securely retrieve secrets from AWS Secrets Manager programmatically! 

Using a custom get_secret() function, I set up a connection with Secrets Manager through boto3. This function grabs the secret we created earlier by name and stores its value in a variable called secret. 

Now, instead of hardcoding credentials, my app fetches them securely at runtime a major step toward safer cloud development!

I took it a step further by updating config.py to extract the individual values (Access Key ID and Secret Access Key) from the secret stored in AWS Secrets Manager. 

Now, instead of hardcoding credentials, the config file uses the recommended function from AWS’s sample code to securely split and assign the values to variables the same ones app.py relies on. 

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is the process of changing the commit history of the repository that we created. I used it drop the commit where I hardcode the AWS credential. This was necessary becuase the AWS credentials are still living somewhere in the repository commit history otherwise (and if it's living in the commit history, it's still discoverable to attackers). 

Start your answer with 'A merge conflict occurred during rebasing because Git is now confused about whether it should also remove all the changes to config.py I made in a commit  AFTER the commit we wanted to drop. I resolved the merge conflict by going directly into the config.py file, and manually removing all the parts I want to remove (hardcode credentials), and keeping the code from Secrets Manager.

Once I updated config.py. I verified that GitHub is not exposing any of our credentials. I visited the config.py file in the forked repository, and cansee that uses code to extract the credentials instead of any hardcode. We also successfulle pushed the code without any blocking from GitHub Secrets Scanning.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
