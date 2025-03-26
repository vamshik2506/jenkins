# Installing Jenkins on Ubuntu

## **Step 1: Install Java**  
Jenkins requires Java to run. Install OpenJDK 17 using the following commands:  

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
```
This verifies the installation of Java. The expected output should display the installed Java version:  
```
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```

---

## **Step 2: Install Jenkins**  
Jenkins is not available by default in Ubuntu repositories, so we need to add its repository manually.  

### **Add Jenkins Repository Key and Source**  
Run the following commands to download the key and add the Jenkins repository:  

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

Update the package list:  

```bash
sudo apt-get update
```

---

## **Step 3: Install Jenkins**  
Now, install Jenkins using:  

```bash
sudo apt-get install jenkins
```

---

## **Step 4: Start and Enable Jenkins**  
Enable Jenkins to start on boot and start the service immediately:  

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

To check if Jenkins is running, use:  

```bash
sudo systemctl status jenkins
```

If Jenkins is running correctly, the output will show `active (running)`.  

---

## **Access Jenkins Web Interface**  
Jenkins runs on port `8080` by default. Open a browser and navigate to:  

```
http://<your-server-ip>:8080
```

To get the initial administrator password, run:  

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy this password and paste it into the Jenkins setup page to proceed with the installation.  

---

### 🎉 **Jenkins Installation is Complete!**  
You can now set up Jenkins, install required plugins, and create your first pipeline! 🚀  
