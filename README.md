# Code improvments for Java Developers

## Summarie

## 1. The computeIfAbsent Pattern That Makes Maps Feel Like Python Dictionaries

<h3>Most developers still write code like this:</h3>

 ```java
 if (!map.containsKey(key)) {
    map.put(key, new ArrayList<>());
}
map.get(key).add(value);
```

This is fine, but it’s also unnecessary noise.

<h3>Java gives you a cleaner, safer pattern:</h3>

 ```java
map.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
```

<h3>Why this matters:</h3>

- No double lookup
- No risk of creating unused objects
- More readable and intentional
- This single method makes Map feel almost like Python’s defaultdict, which makes grouping or caching tasks much easier.


## 2. Want Faster Search? Use EnumMap Instead of HashMap for Enums

You might know this in theory, but most developers never apply it.

If your key is an enum:

```java
Map<Status, Integer> map = new HashMap<>();
```

…you’re leaving performance on the table.

The better choice:

```java
Map<Status, Integer> map = new EnumMap<>(Status.class);
```

<h3>Why this matters:</h3>

- Internally uses arrays
- No hashing
- Very compact memory layout
- This is one of those optimizations that costs nothing and gives you free speed.



## 3. Never Use RestTemplate Anymore — Use WebClient
```java
WebClient client = WebClient.builder()
    .baseUrl("https://api.example.com")
    .build();
```

<h3>Why?</h3>

- Non-blocking
- Handles backpressure
- Better performance under load
- Cleaner API

## 4. Iterate over Values MapString, Integer>
