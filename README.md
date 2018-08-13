# react-native-fixed-demo
Hello! This repository, *made in 13 August 2018*, is what you would get by typing `react-native init newproj` in your shell, with some tweaks and a **checklist of things to do to ensure your project runs correctly**. This is not so trivial!

I decided to made this repository after following the *'Getting started'* page of React Native: [The React Native page](https://facebook.github.io/react-native/docs/getting-started.html).

There are some informations that aren't very clear when it comes to error reporting and I have to thank StackOverflow users if I found fixes to run the demo project.

Here is the checklist.

## Avoid [Expo](https://expo.io/). Follow "Building Projects with Native Code" instead of using Expo
This can be a subjective topic; Expo makes life easier for you and many things are implemented and supported out of the box. You literally just download the Expo app, start an Expo project on their website, scan a QR code, use Tunnel or LAN mode and you're ready to make awesome apps.

Some people might not like it and finds Expo just another boilerplate layer that adds more complexity in the long run; **an alternative is just to use React Native *as it is*, the native way**. This is a little trickier, but it has its advantages, as shown below.

There are **objective points** addressed from the [Expo documentation itself (Why not Expo?)](https://docs.expo.io/versions/v27.0.0/introduction/why-not-expo) but in particolar from [this medium post from paulsc](https://medium.com/@paulsc/react-native-first-impressions-expo-vs-native-9565cce44c92).

To sum them:
- If you want to add **custom native components, you can't with Expo**. You must [eject](https://github.com/react-community/create-react-native-app/blob/master/EJECTING.md) which means you **convert your Expo project into a "native-like" version of your project which seems to be indipendent from Expo itself but it's not really**, plus you can't uneject unless you wanna `git checkout`; going **native** doesn't have this problem;
- If you need a **finer control** over your build, **it's better to go native**. One advantage of doing this for example is that you don't need to submit your apk through Expo servers while programming;
- In the long run it makes things easier as **Expo seems to be unnecessary for some expert React Native developers**, considering that Expo wasn't always around before;
- In **Expo**, **size** of the app can **increase of some MBs due to Expo APIs** (And you **can't** trim them as for now if you don't need them);
- In **Expo**, building in iOS might not be **reliable**;
- In **Expo**, there is **no support for background code execution, Bluetooth, WebRTC and other non-implemented technologies**;
- In **Expo**, there is **no support for other kind of push notification systems** except the one provided by Expo;
- In **Expo**, you must be connected to internet to use JS assets stored in Google Cloud Platform / AWS.

## Setup your machine for Native Code
1. (Install NodeJS)[https://nodejs.org/it/download/].
2. Install `React Native CLI` globally.
`npm install -g react-native-cli`.

Make sure it's typed correctly: at beginning I typed `react-native` instead of `react-native-cli`, which does **NOT** have `react-native` process.
3. **Fork** this project (**Recommended**):
`git clone https://github.com/fabnicolas/react-native-fixed-demo`

*(You can rename it later by using [this tool](https://github.com/junedomingo/react-native-rename).)*

*In alternative you can use `react-native` command: `react-native init mainproj`.*

## Run your project
1. **CD into**.
`cd react-native-fixed-demo`

2. **Run** it (For example on Android):
`react-native run-android`

Make sure your Android device is connected and that `adb devices` shows it.

3. **In theory**, you should be done. **However I have encountered some errors and that's why I made this repository. Here is below a checklist that can help you during installation and use of React Native for the first time.**

## Errors & Fixes
### 1. Problems with JVM, output similar to: `Could not determine java version`, or `Failed to notify project evaluation listener. > javax/xml/bind/annotation/XmlSchema`.

**Solution**: *React Native* uses *Gradle* which uses **JDK**. To build React Native files for android, you need **JDK 8**. Other versions such as JDK 9 and JDK 10 are not supported at moment.

You have two ways for Windows users:
#### Windows: uninstall **JDK/JRE 9/10**, install **JDK 8**.
As simple as it is. This method automatically fixes `PATH` environment variable in Windows systems.

#### Windows: change PATH variable
If you want to **keep multiple java versions** in your Windows machine, this is the right solution for you.

- **Change** your `PATH` variable by **removing all Java versions and add**:

`;%JAVA_HOME%\bin`

- **Make** a new environment variable called `JAVA_HOME` and set it to **JDK 8 path**, for example:

`C:\Program Files\Java\jdk1.8.0_181`
*You can download JDK 8 [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).*

- **Reboot** your machine (Yeah... we love Windows).

### Linux, using brew
If you are a Linux user, simply do this:
```
brew cask uninstall java
brew tap caskroom/versions
brew cask install java8
```

### 2. Problems with SDK, output similar to: `Failed to notify project evaluation listener. > Could not initialize class com.android.sdklib.repository.AndroidSdkHandler`.

**Solution**: This is an Android-related problem and it basically means that the **SDK folder** is NOT correct or specified.

#### Set SDK folder
1. `cd` into `android` folder;
2. **Make** a `local.properties` file with the following content *(Example for Windows)*:

```
sdk.dir=C:\\Users\\YOUR_NICKNAME\\AppData\\Local\\Android\\sdk
```

Where `YOUR_NICKNAME` is your **Windows username**. *Too bad we can't just use `%APPDATA%`.*

On Linux, just set the path accordingly to your Android SDK installation folder.

### 3. Problems with react-native, output similar to: `Unable to resolve module 'AccessibilityInfo'`.

**Solution**: this repository automatically fixes this problem, however if you did not fork this project but made a `react-native init` installation - you should follow these steps below.

#### Fix dependency `react-native`
1. **Delete** `node_modules` folder.
2. **Change** `package.json` by downgrading `react-native` dependency to version 0.55.4. Well, version 0.56.0 is not compatible with `react` for some reasons...
```
...
"react-native": "0.55.4"
...
```
3. **Reinstall packages by executing** `npm install`.

### 4. Problems with react-native, output similar to: `error: bundling failed: "TransformError [...] (While processing preset: node_modules [... \\babel-preset-react-native\\index.js")"`

**Solution**: this repository automatically fixes this problem, however if you did not fork this project but made a `react-native init` installation - you should follow these steps below.
1. **Delete** `node_modules` folder.
2. **Execute** `npm install babel-preset-react-native@2.1.0 --save-dev`
3. **Reinstall packages by executing** `npm install`.