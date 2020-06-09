Encryption &nbsp;&nbsp;[![](https://jitpack.io/v/ir.alirezaivaz/encryption.svg)](https://jitpack.io/#ir.alirezaivaz/encryption)
=====================

Encryption is a simple way to encrypt and decrypt strings on Android and Java project.

## How to use ##

1. Add [JitPack](https://jitpack.io/) to your build file
```gradle
allprojects {
  repositories {
    ...
    maven { url 'https://jitpack.io' }
  }
}
```

2. Add the gradle dependency
```gradle
dependencies {
  implementation 'ir.alirezaivaz:encryption:1.0'
}
```

3. Get an Encryption instance
```java
String key = "YourKey";
String salt = "YourSalt";
byte[] iv = new byte[16];
Encryption encryption = Encryption.getDefault(key, salt, iv);
```

4. Encrypt your text
```java
String encrypted = encryption.encryptOrNull("Text to be encrypt");
```

5. Decrypt your text
```java
String decrypted = encryption.decryptOrNull(encrypted);
```

## Custom usage ##

You can use you own builder
```java
Encryption encryption = new Encryption.Builder()
                .setKeyLength(128)
                .setKey("YourKey")
                .setSalt("YourSalt")
                .setIv(yourByteIvArray)
                .setCharsetName("UTF8")
                .setIterationCount(1)
                .setDigestAlgorithm("SHA1")
                .setBase64Mode(Base64.DEFAULT)
                .setAlgorithm("AES/CBC/PKCS5Padding")
                .setSecureRandomAlgorithm("SHA1PRNG")
                .setSecretKeyType("PBKDF2WithHmacSHA1")
                .build();
```

See more on Examples folder, there is an Android, a Java and a Kotlin project.

## FAQ ##

 - What is Encryption library?
	 - Encryption library is an Open Source library to help encryption routines in Android and Java applications, our target is to be simple and secure.
 - What is the "IV", what should be my `yourByteIvArray`
	 - Encryption 1.0+ uses by default the AES algorithm in CBC mode, so to encrypt and decrypt works you should have the same key and the same IV byte array to encrypt and to decrypt. An example of IV is `byte[] iv = {-89, -19, 17, -83, 86, 106, -31, 30, -5, -111, 61, -75, -84, 95, 120, -53};` like you can see, 16 bytes in a byte array. So if you want to use this library I recommend you create you own IV and save it :floppy_disk:.
 - I Don't like null returns when errors occurs, what to do to handle errors?
	 - You have the power to handle the exceptions, instead of uses `encryptOrNull` method just uses the `encrypt` method. The same for the `decryptOrNull`, just uses the `decrypt` method.
 - I'm getting problems with main thread, what to do?
	 - Encrypt routines can take time, so you can uses the `encryptAsync` with a `Encryption.Callback`to avoid ANR'S. The same for `decryptAsync`

### Want to contribute? ###

Fell free to contribute, We really like pull requests :octocat:


#### Third part ####

- Copyright (C) 2010 The Android Open Source Project, applied to:
	- Base64 (ir.android.encryption.Base64) original comes from [here](https://github.com/android/platform_frameworks_base/blob/ab69e29c1927bdc6143324eba5ccd78f7c43128d/core/java/android/util/Base64.java)
