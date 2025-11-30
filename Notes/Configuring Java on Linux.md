---
created-date: 2022-03-18
tags:
  - tech
---

- Install openjdk 

```sh
sudo apt install openjdk-25-jre-headless
```


- Install Maven
```jsx
sudo apt install maven
```

- Check Maven Version
```jsx
mvn -v
```

 - Check jdk directoy

```sh
ls /usr/lib/jvm/
```

- Open the profile file

```
cd /etc/
sudo vim profile
```

- Add to the file
```
JAVA_HOME=/usr/lib/jvm/java-1.25.0-openjdk-amd64
export JAVA_HOME
export PATH=$PATH:$JAVA_HOME
```

- Reboot the machine

- Print the JAVA_HOME to confirm if it is set
```sh
echo $JAVA_HOME
```

