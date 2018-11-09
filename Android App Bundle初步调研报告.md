# Android App Bundle初步调研报告
***
## Android App Bundle简介及其优势
Android App Bundle是一个新的应用上传格式，它允许开发者将应用按照自己所支持的屏幕密度，地区语言，ABI以及各种功能feature进行细粒度的划分，使得用户可以按需下载应用的不同部分，从而减少应用的体积大小
### Dynamic Delivery介绍
一种新的基于.aab文件格式的应用分发模型。在这种模型下，_**由Google Play使用.aab文件中的代码和资源**_来为用户生成特定于设备的屏幕密度，ABI以及地区语言的应用程序（APK文件）以及动态特性APK文件。并且如果开发者提供了动态特性的话，用户可以在第一次使用该特性的时候再下载动态特性apk文件，避免在第一次安装的时候就下载整个应用程序的代码和资源
#### Base APK
这是用户第一次下载应用的时候需要下载的基础APK文件。它包含了应用程序最基本功能的代码和资源，其中的代码和资源可能被以后下载的动态特性apk中的代码所引用。Base APK的manifest文件中声明了整个应用程序（包括可能会有的dynamic feature apks）中所需要的四大组件，并且包含了应用程序的版本控制以及所有的权限声明。这个APK文件中的代码和资源全部来自我们工程中的app module(或者叫base module)。此APK文件由Google Play从我们提供的.aab文件中生成

#### Dynamic feature APKs
动态特性APK。每一个这样的APK文件提供了所对应的动态特性所需要的代码和资源（也有可能会依赖Base APK中的代码和资源）。动态特性需要我们在IDE中显示地创建一个dynamic feature module，每一个这样的module都提供了对应功能的代码和资源。与Base APK同样地，当上传到Google Play之后，Google Play会从.aab文件中为每一个dynamic feature module分别生成一个dynamic feature apk
#### Configuration APKs
在以往每次下载应用程序的时候，无论用户的设备是什么配置，都会把应用程序针对所有配置的资源全部下载到设备上，造成了很多空间的浪费。在Dynamic Delivery下，Google Play从.aab文件中对每一种资源分别针对不同的设备配置都生成一个apk文件。比如对于drawable资源，针对不同的屏幕密度生成一系列的apk文件，每一个apk文件都包含了某一种屏幕密度下的所有drawable资源，叫做Density Configuration Split APKs。同理，对于ABI和Language都是一样的操作，分别叫做ABI Configuration Split APKs和Language Configuration APKs。当用户第一次下载应用的时候，除了下载一个Base APK文件以外，Goole play会根据用户设备的配置，分别从三个Split APKs中选择一个对应于设备配置的apk组成一个Configuration APKs。对于Base APK叫做Base Configuration APKs，对于Dynamic Feature APKs叫做Feature Configuration APKs。当用户切换了语言之后，会自动从Google Play下载一个新的Language Configuration APK。
#### Android App Bundle文件格式




## 构建一个Android App Bundle



## 从Android App Bundle部署，测试应用程序

### 使用bundletool在本地测试应用
### 使用Google Play测试应用



## 将Android App Bundle上传到Google Console




## 使用Play Core Library下载dynamic feature module
