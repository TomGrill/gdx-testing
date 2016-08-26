# gdx-testing

This is a skeleton for libGDX projects which require testing with JUnit and Mockito.

## Updates & News
Follow me to receive release updates about this and my other projects (Promise: No BS posts)

https://twitter.com/TomGrillGames and https://www.facebook.com/tomgrillgames

I will also stream sometimes when developing at https://www.twitch.tv/tomgrill and write a blog article from time to time at http://tomgrill.de 

## Installation

Asuming that you already did setup a libGDX project:

* Copy the **tests** folder of this project into your libGDX root directory.

* Edit the **settings.gradle** file and add the **'tests'** subproject to the includes like this:

```gradle
include 'desktop', 'android', 'ios', 'html', 'core', 'tests'
```

* Edit **build.gradle** file, and add these lines:

```gradle
project(":tests") {
    apply plugin: "java"

    sourceSets.test.java.srcDirs = ["src/"]
    		
    dependencies {
	
		/**
		 * If you do have some classes to test in os specific code you may want to uncomment
		 * some of these lines.
		 * 
		 * BUT: I recommend to create seperate test sub projects for each platform. Trust me :)
		 * 
		 */
	
//        compile project(":android")
//        compile project(":html")
//        compile project(":desktop")
        
        
//        if(System.getProperty("os.name").toLowerCase().indexOf("mac") >= 0) {
//        	compile project(":ios")
//        }
        
        compile project(":core")
        
        compile "junit:junit:4.+"
        compile "org.mockito:mockito-all:1.9.+"
        
        compile "com.badlogicgames.gdx:gdx-backend-headless:$gdxVersion"
        compile "com.badlogicgames.gdx:gdx:$gdxVersion"        

        testCompile 'junit:junit:4.+'
        testCompile "org.mockito:mockito-all:1.9.+"

        testCompile "com.badlogicgames.gdx:gdx-backend-headless:$gdxVersion"
        testCompile "com.badlogicgames.gdx:gdx:$gdxVersion"
        testCompile "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-desktop"
    }
}
```

* Import the project to your IDE
* Refresh your gradle dependencies. 

## Run the tests
```php
./gradlew tests:test
```

Note: gradle caches passed tests. So if you rename/move/delete badlogic.jpg and run the tests again it will pass. Run from time to time (especially when working with tests against filesystem or anything else that has changed but did not affect the compiled tests):
```php
./gradlew clean tests:test
```

Whenever you require a headless libGDX environment for your tests to pass, copy the [tests/src/de/tomgrill/gdxtesting/GdxTestRunner.java](tests/src/de/tomgrill/gdxtesting/GdxTestRunner.java) file to your tests project and annotate your test class with:

```java 
@RunWith(GdxTestRunner.class)
public class MySuperTestClass {
	@Test
	public void bestTestInHistory() {
	
	}
}
```

Happy testing!

##License

The gdx-testing project is licensed under the Apache 2 License, meaning you can use it free of charge, without strings attached in commercial and non-commercial projects.

##Source & inspired by

http://shahmirj.com/blog/getting-junit-working-with-libgdx-in-gradle

http://badlogicgames.com/forum/viewtopic.php?f=17&t=1485
