# interface-buoy

Kotlin and groovy provide very convenient operators, the operator `?.` is only invoked when the reference object is not empty, but unfortunately, this utility operator is not provided in java.

I wrote a [blog]() to analyze the principles of the `?.` operators in kotlin and groovy. The kotlinc and groovyc compilers compile the `?.` to the same effect as `if (callback != null) {} ` bytecode.

**Interface-buoy** is an Android gradle plugin that uses ASM to dynamically modify java bytecode during the build process. Combine dynamic proxies and reflections to achieve the same effect as the '?.' effect.

Note that we only modify the method defined in the java interface, that is which will trigger the [invokeinterface](https://cs.au.dk/~mis/dOvs/jvmspec/ref--32.html) instruction at runtime.


Blog link : [在Java 中安全使用接口函数]()

## Usage

#### Command Line

```bash
$ git clone git@github.com:SmartDengg/interface-buoy.git
$ cd interface-buoy/
$ ./gradlew build
```


#### AGP

Add Android gradle plugin dependency to your any application or library module's build.gradle.


```groovy
buildscript {
    repositories {
        maven { url 'https://jitpack.io' }
    }
    dependencies {
        
    }
}

apply plugin: 'com.android.application' // or apply plugin: 'com.android.library'
apply plugin: 'com.smartdengg.interfacebuoy' // or apply plugin: 'interfacebuoy'

dependencies {
  implementation fileTree(include: ['*.jar'], dir: 'libs')
  implementation 
}

```

#### Optional

In the java code you can use `InterfaceBuoy.loggable = true` to control whether to print the log, the default is not to print the log.


#### Unsupport

If the invoked interface method has a return type but not a `void` type, its bytecode will not be modified. Currently only the `void` return type is supported.


## About me

email : hi4joker@gmail.com

blog  : [小鄧子](https://www.jianshu.com/u/df40282480b4)

weibo : [-小鄧子-](https://weibo.com/5367097592/profile?topnav=1&wvr=6)


## License

See the [LICENSE](LICENSE) file for license rights and limitations (MIT).