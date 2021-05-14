# Android-Project-Guidelines

## General Guidelines

### Keeping it simple

There are many different ways to develop an Android app.  It's hard to nail down "best practices", but generally one should aim to do their best to write code that is easy to understand, maintain, and change if there are new features/requirements to add in the future.  When the goal is to get a product out as quickly as possible, it is very easy to cut corners and make things "work" while creating future tech debt that can make development on the project painful in the future.  Our development process values speed, but take a bit more time to create a feature if it means that it is maintainable in the future.  

### Programming languages and tools
Use Kotlin and leverage its features.  Avoid pulling in libraries like RxJava when you can utilize features like coroutines and flow. Try to follow [this](https://developer.android.com/kotlin/style-guide) style guide the best you can.  Make sure to develop with the latest stable builds of Android Studio and Gradle.  

### Minimum SDK
Unless told otherwise by a client, use min SDK 26 to target devices on Android 8.0 and above.  This avoids the headache of needing to test on ancient devices that probably should not be used anymore. 

### Libraries

Avoid reinventing the wheel when possible.  Leverage the following libraries in order to save time:
* [Android Jetpack Libraries](https://developer.android.com/jetpack)
* [Retrofit](https://square.github.io/retrofit/) - Networking
* [Glide](https://github.com/bumptech/glide) - Image loading and caching
* [Moshi](https://github.com/square/moshi) - JSON parsing
* [Timber](https://github.com/JakeWharton/timber) - Logging

### Fragments and Activities
There are many opinions on how to use fragments and activities.  It seems that things are moving towards using one activity and multiple fragments when developing.  If possible, follow this pattern.  There may be times when adding another activity is ideal, but in general use fragments with Jetpack navigation.  Using fragments with shared viewmodels is preferred over passing data from activity to activity with intents.  Jetpack Compose is exciting, but this will not be used until it becomes the established standard.

### Accessing views
Use the [view binding](https://developer.android.com/topic/libraries/view-binding) library to access views.  Avoid outdated methods like findViewByID and Kotlin synthetics.  

### MVVM
Use the [recommended](https://developer.android.com/jetpack/guide) architecture to separate UI from logic.  Activities and fragments should hold as little logic, state, and code as possible.  Viewmodels should hold live data that the UI classes can observe and use to change state. 

### UI Responsiveness

It's imperative that the app's UI remain responsive during all aspects of the app's lifecycle. In general, any delay greater than 200 ms will be immediately noticeable by the user and could cause them to question whether or not the system registered their tap.

* Reserve the main thread for UI work. Move as much work to background threads as possible. Follow [best practices](https://developer.android.com/kotlin/coroutines/coroutines-best-practices) for handling coroutines and scope.

### Styling
Unfortunately, many apps are developed and designed with iOS in mind.  When working with app designs, strive to make the app look and feel like a native Android app instead of an iOS clone.  Give UX designers constructive feedback if you feel that a design does not translate well to Android.  




### Some Best Practices Guidelines we like from Google
**Avoid designating your app's entry points—such as activities, services, and broadcast receivers—as sources of data.**

Instead, they should only coordinate with other components to retrieve the subset of data that is relevant to that entry point. Each app component is rather short-lived, depending on the user's interaction with their device and the overall current health of the system.

**Create well-defined boundaries of responsibility between various modules of your app.**

For example, don't spread the code that loads data from the network across multiple classes or packages in your code base. Similarly, don't define multiple unrelated responsibilities—such as data caching and data binding—into the same class.

**Assign one data source to be the single source of truth.**

Whenever your app needs to access this piece of data, it should always originate from this single source of truth.

## Architectural Guidelines

When working on a new project it is imperative that all developers understand the scope and significance of any technical decision they make. In general, the more junior the developer, the more guidance and the less architectural decision making power the developer has. This is primarily to protect the customer as well as Strides Development from “rogue” developers making a poor technology or other architecturally significant decision that would impact our ability to meet customer expectations.

In general, if a developer has to make a decision between development technologies (e.g. languages, tools, 3rd party components, complex implementations, etc.) then this is an architecturally significant decision that requires director level approval and notification. The sole intent of this guideline is to protect the client and Strides Development, not to create an artificial bottleneck.
