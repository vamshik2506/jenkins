# **TO INSTALL JENKINS IN UBUNTU**

# **Update the package list and install Java (OpenJDK 17)**
sudo apt update
sudo apt install fontconfig openjdk-17-jre

# **Verify Java installation**
java -version

# **Expected output:**
# openjdk version "17.0.8" 2023-07-18
# OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
# OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)

# **Download and add Jenkins repository key**
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# **Add Jenkins repository to the package sources list**
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

# **Update the package list**
sudo apt-get update

# **Install Jenkins**
sudo apt-get install jenkins

# **Enable Jenkins to start on boot**
sudo systemctl enable jenkins

# **Start Jenkins service**
sudo systemctl start jenkins

# **Check the status of Jenkins service**
sudo systemctl status jenkins
```

Would you like me to add more details or format it differently? 🚀
