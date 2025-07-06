---
created-date: 2022-03-18
tags:
  - tech
---

## Linux

```jsx
sudo apt install openjdk-11-jdk
```
Verificar caminho:
```jsx
sudo update-alternatives --config java
```
Configurar JAVA_HOME:
```jsx
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export JAVA_HOME
export PATH=$PATH:$JAVA_HOME
```
Instalar Maven:
```jsx
sudo apt install maven
```
Verificar Versão:
```jsx
mvn -v
```