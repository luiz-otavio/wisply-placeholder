# WPlaceholder
[![](https://jitpack.io/v/luiz-otavio/wisply-placeholder.svg)](https://jitpack.io/#luiz-otavio/wisply-placeholder)
Flexible library to replace placeholders inside messages/texts with Regex expressions.

## For what it's good for
Placeholder replacement is a common task in many languages. This library is a flexible and easy to use solution to replace texts/messages with new messages.

## Besides replacing placeholders
To understand how does it works, let's look at an example:
```java
public static void main(String[]args){
    String message = "Hello {name}, how are you?";
    String name = "John";
    String replacedMessage = message.replaceAll("\\{name\\}", name);
    System.out.println(replacedMessage);
}
```

It will print: `Hello John, how are you?`

The `\\{name\\}` is a placeholder. It's a special character that is used to replace a value.
That essentially means that the `\\{name\\}` will be replaced with the value of the `name` variable.

## Applying WPlaceholder
There are few ways to add WPlaceholder in your project like:

Gradle DSL:
```gradle
repositories() {
    maven {
        name = "jitpack"
        url = 'https://jitpack.io'
    }
}   

dependencies() {
    implementation 'com.github.luizotavio:<module-name: bukkit|bungee|common>:1.0.0-SNAPSHOT'
}
```

Kotlin DSL:
```kotlin

repositories() {
    maven("https://jitpack.io")
}

dependencies() {
    implementation("com.github.luizotavio:<module-name: bukkit|bungee|common>:1.0.0-SNAPSHOT")
}
```

Maven:
```xml
<repositories>
    <repository>
        <id>jitpack</id>
        <name>jitpack</name>
        <url>https://jitpack.io</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.github.luizotavio</groupId>
        <artifactId>bukkit|bungee|common></artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </dependency>
</dependencies>
```

## How to use it
```java
// Bukkit example:

public class Main {
    public static void main(String[] args) {
         PlaceholderDelegator.BukkitFacade facade = PlaceholderDelegator.createDelegator('%');
         
         facade.register(new BukkitPlaceholder("%name%") {
             @Override
             public String resolve(@Nullable Player player) {
                 return player == null ? "Unknown" : player.getName();
             }
         });
         
         String message = PlaceholderDelegator.replace("Hello %name%!", Bukkit.getPlayer("WizardBR_"));
         
         System.out.println(message);
    }
}
```
It will be: `Hello WizardBR_!`