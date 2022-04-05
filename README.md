# React-Native_Docker-Image
Build and deploy react native from docker image without setting environment in system

# Motivation
Docker is a fantastic technology. With this, react native users can easily integrate ci to their code. Also you can easily debug react native code without setting up all the tools needed like android sdk and nodejs. 

# Dockerhub Image
see [https://hub.docker.com/r/reactnativecommunity/react-native-android/](https://hub.docker.com/r/reactnativecommunity/react-native-android/)

# Docker Pull
```
docker pull reactnativecommunity/react-native-android
```
# What's included:
React native, Create-React-Native-App, Android SKD, Gradle, Maven, Batteries

This container should run in any Unix/Unix Inspired system (Linux, Mac). Not tested on windows (you can let me know)

# How to use 

```
docker run -it --name rn-app -v "$pwd:/pwd" -w /pwd reactnativecommunity/react-native-android bash
```
-v flag is used for mounting location from source dir to in container dir 
-w will create /pwd dir in the container
This command will create a container named rn-app and u will be inside of the container -it flag insured of it

# Inside Container
 when you will be in container 
 
 ```
 root@a123640695ee:/pwd# 
 ```
inside container run following command to install react-native cli and expo cli

```
npm install -g yarn && yarn global add react-native-cli create-react-native-app expo-cli
```
After installing react-native cli run the following to create react-natvie project in the working dir
```
npx react-native init AwesomeProject 
```
AwesomeProject is the Project name you can change according to your project
# This step is optional 
cd to AwesomeProject and run the following to insure working dir is connected to container dir
```
touch file.txt
```
# Running the App

Firstly we have to connect adb to container .
before that we have to connect adb devcies to computer

Attach physical devices to pc then run the following to see attached devices 
``` 
adb devices
```
You will see all the connected devices 

```
List of devices attached

```
if you dont see your devices detachhed your device then attached it again
After that your will see your device

run the following to run adb port on 5555
```
adb tcpip 5555
```
after that detachhed your device then attached it again

***Make sure your device and your system is connected to the same network***

Go to mobile settings then mobile status and copy the ip address of the mobile 
ip addres will be used to connect the device to adb service with the following command
```
adb connect <ip-address>:5555
```
You will see device connected msg 

# Connecting Adb into container 
Run 
```
adb devices
```
You will see attached devices if dont see Dont worry there will be none 
You have to Attach Manually 
Run 
```
adb tcpip 5555
```
after that Run 
```
adb connect <ip-address>:5555
```
You will see devices connected msg

# Now its Time to Run your App

Cd to AwesomeProject

then run
```
npx react-native start
```
it will start your metro bundler in your terminal

After that create a new bash or terminal window and run the following
```
docker exec -it rn-app bash
```
This command will get u inside the container again 
type ``ls`` to see created app folder after that cd to app folder 
and create a random txt file to make sure same dir is connected ```touch random.txt```

Then Run 
```
npx react-native run-android
```
This will start running process of the react-native after that u will see the app in your mobile

## Referncess
Setting envirnment of react native


[https://reactnative.dev/docs/environment-setup](https://reactnative.dev/docs/environment-setup)

React-native-docker git repo 

[https://github.com/react-native-community/docker-android](https://github.com/react-native-community/docker-android)



























