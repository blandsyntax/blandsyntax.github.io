+++
title = "Android Intents"
date = 2025-07-24T15:00:00Z
[taxonomies]
categories = ["Android"]
tags = ["research", "concept"]
[extra]
subtitle = "Understanding intents in Android"
+++


Intents are how Android components—or apps—tell each other to do something, like open a screen, send data, or start a system action. It is more of like sending a letter with the intent mentioned, and Android delivers it where it's supposed to go (opening  a camera, navigating around system).

There are two types of intents mainly.
`Explicit Intents` & `Implicit intents`

> explicit intents : starts a specific component (own activity mainly) 
```java
Intent intent = new Intent(this, ProfileActivity.class);
startActivity(intent);
```

>implicit intents : invokes system or third-party actions
```java
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse("https://openai.com"));
startActivity(intent);
```

# Intent filters 
Defined in `AndroidManifest.xml` to allow other apps to call specific components
`intent filter` consists of 3 parts :
- action - type of intent? (like `"android.intent.action.VIEW"`)
- category - additional info telling how the component is supposed to be used (`"android.intent.category.DEFAULT"`)
- data - type of data to accept (`mimeType="text/plain"` or `scheme="http"`)

some common use cases are sharing text `ACTION_SEND`, picking image `ACTION_PICK`, open map `ACTION_VIEW`.

# Passing data

When using an Intent to start another Activity or Service, you can attach extra data to it using key-value pairs.

>attaching data to the intent (sender)
- `putExtra(key, value)` for simple types
- `putExtras(Bundle)` for multiple key-value paris on a single instance 

```java
Intent intent = new Intent(this, ProfileActivity.class);
intent.putExtra("username", "goober");
intent.putExtra("age", 51);
startActivity(intent);
```
this intent now carries `"username" = "goober"` and `"age" = 51`

>retrieving the data (receiver)
- inside `ProfileActivity`
```java
String username = getIntent().getStringExtra("username");
int age = getIntent().getIntExtra("age", -1); // -1 = default if not found
```

# Debugging intents
- use `adb shell am start` to trigger intents with manual ----------
- logcat is your saviour use the filters :p 

## Conclusion
**Passing data with Intent extras is like slipping notes between Android components — just don’t forget the key, or your app’s memory might ghost you.** 
