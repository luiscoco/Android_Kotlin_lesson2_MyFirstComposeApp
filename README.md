# How to create your first Compose App with Android (Jetpack Compose Basics)

https://developer.android.com/codelabs/jetpack-compose-basics

https://developer.android.com/static/codelabs/jetpack-compose-basics/img/8d24a786bfe1a8f2.gif

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d2beb612-54dc-48ac-ac5e-30cad6635f54)


## 1. 


## 2. 



## 3. 



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

These functions are used to preview the composables in Android Studio:

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

These functions allow you to see how the UI components will look without running the app




