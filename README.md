# How to create your first Compose App with Android (Jetpack Compose Basics)

https://developer.android.com/courses/jetpack-compose/course

https://github.com/android/codelab-android-compose

https://developer.android.com/codelabs/jetpack-compose-basics

https://m3.material.io/get-started

## 1. Introduction 

**Jetpack Compose** is a modern toolkit designed to simplify **UI** development

It combines a **reactive programming** model with the conciseness and ease of use of the **Kotlin** programming language

It is fully **declarative**, meaning you **describe** your **UI** by calling a series of functions that transform data into a UI hierarchy

When the underlying **data changes**, the framework **automatically re-executes** these **functions**, updating the UI hierarchy for you

A Compose app is made up of **composable functions** - just regular functions marked with **@Composable**, which can call other composable functions

A function is all you need to create a new UI component

The annotation tells Compose to add special support to the function for updating and maintaining your UI over time

By making small reusable composables, it's easy to build up a library of UI elements used in your app

With Compose, an **Activity** remains the **entry point** to an **Android app**

In our project, **MainActivity** is launched when the user opens the app (as it's specified in the **AndroidManifest.xml** file)

You use **setContent** to define your **layout**, but instead of using an **XML file** as you'd do in the traditional **View system**, you **call Composable functions** within it

## 2. Starting a new Compose project

To start a new Compose project, open Android Studio

Select **File > New > New Project** from the menu bar

For a new project, choose **Empty Activity** from the available templates

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/b3c0c003-d7d3-4ad0-a5a2-34fc04556a9b)

Click **Next** and configure your project

When choosing the **Empty Activity** template, the following code is generated for you in your project:

The project is already configured to use Compose

The **AndroidManifest.xml** file is created

The **build.gradle.kts** and **app/build.gradle.kts** files contain options and dependencies needed for Compose

After syncing the project, open **MainActivity.kt** and check out the code

**MainActivity.kt**

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            BasicsCodelabTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Greeting("Android")
                }
            }
        }
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    BasicsCodelabTheme {
        Greeting("Android")
    }
}
```

## 3. Application UI 

https://developer.android.com/static/codelabs/jetpack-compose-basics/img/8d24a786bfe1a8f2.gif

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/523e404b-7715-400f-bb7d-9cbd8927af03)

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d5bbd54e-27b5-41e3-82d9-2939f3deb44e)

Now compare your code with the solution:

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/17c3406a-f449-4acc-b4be-0acb430f9365)

```kotlin
import androidx.compose.foundation.layout.fillMaxWidth

@Composable
fun MyApp(
    modifier: Modifier = Modifier,
    names: List<String> = listOf("World", "Compose")
) {
    Column(modifier = modifier.padding(vertical = 4.dp)) {
        for (name in names) {
            Greeting(name = name)
        }
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(
        color = MaterialTheme.colorScheme.primary,
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        Column(modifier = Modifier.fillMaxWidth().padding(24.dp)) {
            Text(text = "Hello ")
            Text(text = name)
        }
    }
}
```

In the next step you'll **add a clickable buttont** that expands the Greeting Card

The goal is to create the following layout:

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/9abc1275-5985-4668-bcda-53d8a868356a)

```kotlin
import androidx.compose.foundation.layout.Row
import androidx.compose.material3.ElevatedButton
// ...

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Surface(
        color = MaterialTheme.colorScheme.primary,
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        Row(modifier = Modifier.padding(24.dp)) {
            Column(modifier = Modifier.weight(1f)) {
                Text(text = "Hello ")
                Text(text = name)
            }
            ElevatedButton(
                onClick = { /* TODO */ }
            ) {
                Text("Show more")
            }
        }
    }
}
```

To **add internal state to a composable**, you can use the **mutableStateOf** function, which makes Compose recompose functions that read that **State**

**State** and **MutableState** are interfaces that hold some value and trigger UI updates (**recompositions**) whenever that value changes

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    val expanded = remember { mutableStateOf(false) }
    val extraPadding = if (expanded.value) 48.dp else 0.dp
    Surface(
        color = MaterialTheme.colorScheme.primary,
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        Row(modifier = Modifier.padding(24.dp)) {
            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(bottom = extraPadding)
            ) {
                Text(text = "Hello ")
                Text(text = name)
            }
            ElevatedButton(
                onClick = { expanded.value = !expanded.value }
            ) {
                Text(if (expanded.value) "Show less" else "Show more")
            }
        }
    }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d1f1f305-39a8-486d-8232-ac262ae46c65)


## 4. Code explanation

This code is a simple Android application built using **Jetpack Compose**, which is a modern toolkit for building **native Android UI**

The application displays a **greeting card with expandable content**

Here’s a step-by-step explanation of the code:

### 4.1. MainActivity Class

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            BasicsCodelabTheme {
                MyApp(modifier = Modifier.fillMaxSize())
            }
        }
    }
}
```

**MainActivity** extends **ComponentActivity** and overrides the **onCreate** method

In **onCreate**, it calls **setContent** to set the **layout** using **Compose**

The layout is wrapped in a **custom theme** (BasicsCodelabTheme) and calls the **MyApp** composable function

### 4.2. MyApp Composable

```kotlin
@Composable
fun MyApp(modifier: Modifier = Modifier) {
    var shouldShowOnboarding by rememberSaveable { mutableStateOf(true) }

    Surface(modifier) {
        if (shouldShowOnboarding) {
            OnboardingScreen(onContinueClicked = { shouldShowOnboarding = false })
        } else {
            Greetings()
        }
    }
}
```

MyApp is the main composable function

It uses a state variable shouldShowOnboarding to track whether the onboarding screen should be shown

If shouldShowOnboarding is true, it shows OnboardingScreen. Otherwise, it shows Greetings

### 4.3. OnboardingScreen Composable

```kotlin
@Composable
fun OnboardingScreen(
    onContinueClicked: () -> Unit,
    modifier: Modifier = Modifier
) {
    Column(
        modifier = modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text("Welcome to the Basics Codelab!")
        Button(
            modifier = Modifier.padding(vertical = 24.dp),
            onClick = onContinueClicked
        ) {
            Text("Continue")
        }
    }
}
```

OnboardingScreen displays a welcome message and a "Continue" button

When the button is clicked, it calls onContinueClicked, which changes the state in MyApp to show the greetings

### 4.4. Greetings Composable

```kotlin
@Composable
private fun Greetings(
    modifier: Modifier = Modifier,
    names: List<String> = List(25) { "$it" }
) {
    LazyColumn(modifier = modifier.padding(vertical = 4.dp)) {
        items(items = names) { name ->
            Greeting(name = name)
        }
    }
}
```

Greetings displays a list of greeting cards using LazyColumn

Each card is created by the Greeting composable

### 4.5. Greeting Composable

```kotlin
@Composable
private fun Greeting(name: String, modifier: Modifier = Modifier) {
    Card(
        colors = CardDefaults.cardColors(
            containerColor = MaterialTheme.colorScheme.primary
        ),
        modifier = modifier.padding(vertical = 4.dp, horizontal = 8.dp)
    ) {
        CardContent(name)
    }
}
```

Greeting creates a card for each name

The card's content is defined by the CardContent composable

### 4.6. CardContent Composable

```kotlin
@Composable
private fun CardContent(name: String) {
    var expanded by rememberSaveable { mutableStateOf(false) }

    Row(
        modifier = Modifier
            .padding(12.dp)
            .animateContentSize(
                animationSpec = spring(
                    dampingRatio = Spring.DampingRatioMediumBouncy,
                    stiffness = Spring.StiffnessLow
                )
            )
    ) {
        Column(
            modifier = Modifier
                .weight(1f)
                .padding(12.dp)
        ) {
            Text(text = "Hello, ")
            Text(
                text = name, style = MaterialTheme.typography.headlineMedium.copy(
                    fontWeight = FontWeight.ExtraBold
                )
            )
            if (expanded) {
                Text(
                    text = ("Composem ipsum color sit lazy, " +
                            "padding theme elit, sed do bouncy. ").repeat(4),
                )
            }
        }
        IconButton(onClick = { expanded = !expanded }) {
            Icon(
                imageVector = if (expanded) Filled.ExpandLess else Filled.ExpandMore,
                contentDescription = if (expanded) {
                    stringResource(R.string.show_less)
                } else {
                    stringResource(R.string.show_more)
                }
            )
        }
    }
}
```

CardContent contains the actual content of the card

It includes a Row with a Text element to greet the user and another Text element to display the name

The card can expand and collapse to show more content. The expansion state is managed by the expanded variable

The IconButton changes the expansion state and updates the icon accordingly

### 4. 7. Preview Functions

These functions allow you to **see** how the **UI** components will look **without running the app**:

```kotlin
@Preview(showBackground = true, widthDp = 320, heightDp = 320)
@Composable
fun OnboardingPreview() {
    BasicsCodelabTheme {
        OnboardingScreen(onContinueClicked = {}) // Do nothing on click.
    }
}

@Preview(
    showBackground = true,
    widthDp = 320,
    uiMode = UI_MODE_NIGHT_YES,
    name = "GreetingPreviewDark"
)
@Preview(showBackground = true, widthDp = 320)
@Composable
fun GreetingPreview() {
    BasicsCodelabTheme {
        Greetings()
    }
}

@Preview
@Composable
fun MyAppPreview() {
    BasicsCodelabTheme {
        MyApp(Modifier.fillMaxSize())
    }
}
```






