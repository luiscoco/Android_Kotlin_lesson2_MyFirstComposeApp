# How to create your first Compose App with Android (Jetpack Compose Basics)

https://developer.android.com/courses/jetpack-compose/course

https://github.com/android/codelab-android-compose

https://developer.android.com/codelabs/jetpack-compose-basics

https://m3.material.io/get-started

https://github.com/philipplackner

https://www.youtube.com/playlist?list=PLQkwcJG4YTCSpJ2NLhDTHhi6XBNfk9WiC

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

### 1.1. Create Android Composable application

Let's create a simple Android Composable basic application:

See this youtube video: https://www.youtube.com/watch?v=xv2ZUuO3wwk&list=PLAzlSdU-KYwXYL1V9F-NkCy9MaNial-sm&index=5

```kotlin

class MainActivity: ComponentActivity() {
     override fun onCreate(savedInstanceState: Bundle?) {
         super.onCreate(savedInstanceState)
         setContent{
             Text("Hello World!")
         }
     }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/2fb9f466-5fde-43c9-bfcc-69d5fcab4856)

The **MainActivity** class is the **entry point of the application**, and the **onCreate** method **sets up the UI** content using Compose's setContent function

### 1.2. Create a Compose function

We can now create out first **Compose function**

```kotlin

class MainActivity: ComponentActivity() {
     override fun onCreate(savedInstanceState: Bundle?) {
         super.onCreate(savedInstanceState)
         setContent{
             GreetingsMessage()
         }
     }
}

@Composable
fun  GreetingsMessage(){
     Text("Hello World!")
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/81f8d72a-e186-426e-91e4-9c94e9b377d3)

### 1.3. Send a parameter in a function call and crea a Preview Composable

Now we can **send a parameter** in the function call

We can also create a **Preview Composable** to show the UI without running the application

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.tooling.preview.Preview

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MensajeTarjeta("Daniel")
        }
    }
}

@Composable
fun MensajeTarjeta(name: String) {
    Text(
        text = "Hello $name!"
    )
}

@Preview
@Composable
fun PreviewMensajeTarjeta() {
    MensajeTarjeta("Daniel")
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/292ad8dd-c61d-4315-b01c-74bffeb1b3f2)

### 1.4. Create a Column

To visualize two texts one above the other we use the **Column** component

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Column
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Column {
                NombreTarjeta("Daniel")
                MensajeTarjeta()
            }
        }
    }
}

@Composable
fun NombreTarjeta(name: String) {
    Text(
        text = "Hello $name!"
    )
}

@Composable
fun MensajeTarjeta() {
    Text(
        text = "Hello esta es una descripcion con Compose"
    )
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/ff8439ad-25e1-4fe1-8c7f-5d175bfcdfc3)

### 1.5. Create a Column containing three Rows

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.material3.Text

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Column() {
                Row {
                    Text(text = " Celda 1.1 ")
                    Text(text = " Celda 1.2 ")
                    Text(text = " Celda 1.3 ")
                }
                Row {
                    Text(text = " Celda 2.1 ")
                    Text(text = " Celda 2.2 ")
                    Text(text = " Celda 2.3 ")

                }
                Row {
                    Text(text = " Celda 3.1 ")
                    Text(text = " Celda 3.2 ")
                    Text(text = " Celda 3.3 ")
                }
            }
        }
    }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/a24e5f25-84f3-4d0f-9aec-2d95f280cbd3)

### 1.6. Create a Row containing an Image and a Column

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.res.painterResource

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Row() {
                Image(
                    painter = painterResource(id = R.drawable._d_burger),
                    contentDescription = "Foto"
                )
                Column() {
                    NombreTarjeta("Daniel")
                    MensajeTarjeta()
                }
            }
        }
    }

    @Composable
    fun NombreTarjeta(name: String) {
        Text(
            text = "Hello $name!"
        )
    }

    @Composable
    fun MensajeTarjeta() {
        Text(
            text = "Hello esta es una descripcion con Compose"
        )
    }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/a6964470-80b6-46b0-8ab2-8c26207f122a)

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/08402964-3c20-417f-af68-8936550fca8a)

### 1.7. Create three columns with widths in the ratio 1:2:3

The first column will be the narrowest, the second will be wider, and the third will be the widest

To create three columns with different widths in a Jetpack Compose layout, you can use the Row composable along with Modifier.weight to distribute the available space among the columns

Each column can be given a different weight to control its width proportionally

Here's an example of how to achieve this:

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.unit.dp

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Column() {
                Row() {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto"
                    )
                }
                Row() {
                    Column() {
                        ThreeColumns()
                    }
                }
            }
        }
    }

    @Composable
    fun ThreeColumns() {
        Row(modifier = Modifier.fillMaxWidth()) {
            // First column with weight 1 (smallest width)
            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(8.dp)
            ) {
                Text("Col 1", style = MaterialTheme.typography.bodyLarge)
            }

            // Second column with weight 2 (medium width)
            Column(
                modifier = Modifier
                    .weight(2f)
                    .padding(8.dp)
            ) {
                Text("Col 2", style = MaterialTheme.typography.bodyLarge)
            }

            // Third column with weight 3 (largest width)
            Column(
                modifier = Modifier
                    .weight(3f)
                    .padding(8.dp)
            ) {
                Text("Col 3", style = MaterialTheme.typography.bodyLarge)
            }
        }
    }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/dbc50eb6-f57d-45ca-8803-4c46ea62397f)

**Explanation**

Row(modifier = Modifier.fillMaxWidth()): Creates a horizontal layout that fills the available width of the parent

Column(modifier = Modifier.weight(xf).padding(8.dp)) { ... }:

Each Column is given a weight modifier. The weight determines how much of the available space each column should take relative to the others

The padding(8.dp) adds some spacing around the content of each column

**Weights**:

The first column has a weight of **1f**, meaning it will take up one part of the available space

The second column has a weight of **2f**, meaning it will take up two parts of the available space

The third column has a weight of **3f**, meaning it will take up three parts of the available space

Text("Column X", style = MaterialTheme.typography.bodyLarge): Displays text in each column

You can replace this with any other composable content

## 1.8. Adding a function to a Composable

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d2aba0fd-81e4-4b8d-8604-dd4f3d171673)

## 1.9. Clip an image with a circularShape and we add a border with a color

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/6414c406-b12f-4ac9-a677-e564c0310496)

How to change a Text Color

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/16f670cd-efe6-4bcd-98f4-b9dde91c3835)

## 1.10. Modify the Text Typography

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/5fd1d19c-3763-4f49-923e-257755b5e2d6)

## 1.11. Adding a form and a padding around a Text

```kotlin
shadowElevation = 1.dp
```

```kotlin
modifier = Modifier.padding(all = 4.dp),
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d86b9b85-5232-4cc2-92a5-04973d2c16f7)

## 1.12. Create a Row with Horizontal Scroll and serveral images and a Column with different size

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyRow
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.unit.dp

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Column {
                LazyRow(
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(8.dp)
                ) {
                    item(1) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                    item(2) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                    item(3) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                    item(4) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                    item(5) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                    item(6) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                    item(7) {
                        Image(
                            painter = painterResource(id = R.drawable._d_burger),
                            contentDescription = "Foto",
                            modifier = Modifier.padding(8.dp)
                        )
                    }
                }
                Row {
                    Column {
                        ThreeColumns()
                    }
                }
            }
        }
    }

    @Composable
    fun ThreeColumns() {
        Row(modifier = Modifier.fillMaxWidth()) {
            // First column with weight 1 (smallest width)
            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(8.dp)
            ) {
                Text("Col 1", style = MaterialTheme.typography.bodyLarge)
            }

            // Second column with weight 2 (medium width)
            Column(
                modifier = Modifier
                    .weight(2f)
                    .padding(8.dp)
            ) {
                Text("Col 2", style = MaterialTheme.typography.bodyLarge)
            }

            // Third column with weight 3 (largest width)
            Column(
                modifier = Modifier
                    .weight(3f)
                    .padding(8.dp)
            ) {
                Text("Col 3", style = MaterialTheme.typography.bodyLarge)
            }
        }
    }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/09eba6df-470b-4a4d-8849-f673c14a7dbe)

## 1.13. We also add two screens with a top bar with a navigation button to go back to the home screen

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyRow
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.unit.dp
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController
import androidx.navigation.NavHostController

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            val navController = rememberNavController()
            NavHost(navController = navController, startDestination = "main") {
                composable("main") { MainScreen(navController) }
                composable("new_screen1") { NewScreen1(navController) }
                composable("new_screen2") { NewScreen2(navController) }
            }
        }
    }

    @Composable
    fun MainScreen(navController: NavHostController) {
        Column {
            LazyRow(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(8.dp)
            ) {
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier
                            .padding(8.dp)
                            .clickable {
                                navController.navigate("new_screen1")
                            }
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier
                            .padding(8.dp)
                            .clickable {
                                navController.navigate("new_screen2")
                            }
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
            }
            Row {
                Column {
                    ThreeColumns()
                }
            }
        }
    }

    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun NewScreen1(navController: NavHostController) {
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("New Screen1") },
                    navigationIcon = {
                        IconButton(onClick = { navController.navigateUp() }) {
                            Icon(painter = painterResource(id = android.R.drawable.ic_menu_revert), contentDescription = "Back")
                        }
                    }
                )
            },
            content = { innerPadding ->
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(innerPadding)
                        .padding(16.dp)
                ) {
                    Text(text = "This is New Screen1", style = MaterialTheme.typography.bodyLarge)
                }
            }
        )
    }

    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun NewScreen2(navController: NavHostController) {
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("New Screen2") },
                    navigationIcon = {
                        IconButton(onClick = { navController.navigateUp() }) {
                            Icon(painter = painterResource(id = android.R.drawable.ic_menu_revert), contentDescription = "Back")
                        }
                    }
                )
            },
            content = { innerPadding ->
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(innerPadding)
                        .padding(16.dp)
                ) {
                    Text(text = "This is New Screen2", style = MaterialTheme.typography.bodyLarge)
                }
            }
        )
    }

    @Composable
    fun ThreeColumns() {
        Row(modifier = Modifier.fillMaxWidth()) {
            // First column with weight 1 (smallest width)
            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(8.dp)
            ) {
                Text("Col 1", style = MaterialTheme.typography.bodyLarge)
            }

            // Second column with weight 2 (medium width)
            Column(
                modifier = Modifier
                    .weight(2f)
                    .padding(8.dp)
            ) {
                Text("Col 2", style = MaterialTheme.typography.bodyLarge)
            }

            // Third column with weight 3 (largest width)
            Column(
                modifier = Modifier
                    .weight(3f)
                    .padding(8.dp)
            ) {
                Text("Col 3", style = MaterialTheme.typography.bodyLarge)
            }
        }
    }
}
```

When we click on the first Burger image or in the second we navigate to another screen

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d31cc38a-9c6b-4090-b296-85cad93da596)

This is the Screen 1. We navigate to this screen when we click on the first burger image

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/598b15b5-a140-4031-9d7f-abbb609170eb)

## 1.13. We also add three Tabs in the HomeScreen, a Top Navigation Bar, a Bottom Navigation bar and a DropDown Menu

```kotlin
package com.example.myfirstapp_text_only

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyRow
import androidx.compose.material.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.unit.dp
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.currentBackStackEntryAsState
import androidx.navigation.compose.rememberNavController
import androidx.navigation.NavHostController
import com.google.accompanist.pager.*
import kotlinx.coroutines.launch

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            val navController = rememberNavController()
            Scaffold(
                topBar = { TopBar(navController) },
                bottomBar = { BottomNavigationBar(navController) }
            ) { innerPadding ->
                NavHost(navController = navController, startDestination = "main", modifier = Modifier.padding(innerPadding)) {
                    composable("main") { MainScreen(navController) }
                    composable("new_screen1") { NewScreen1(navController) }
                    composable("new_screen2") { NewScreen2(navController) }
                }
            }
        }
    }

    @Composable
    fun TopBar(navController: NavHostController) {
        var expanded by remember { mutableStateOf(false) }

        TopAppBar(
            title = { Text("My App") },
            actions = {
                IconButton(onClick = { expanded = true }) {
                    Icon(painter = painterResource(id = android.R.drawable.ic_menu_more), contentDescription = "More")
                }
                DropdownMenu(
                    expanded = expanded,
                    onDismissRequest = { expanded = false }
                ) {
                    DropdownMenuItem(onClick = {
                        navController.navigate("main")
                        expanded = false
                    }) {
                        Text("Main")
                    }
                    DropdownMenuItem(onClick = {
                        navController.navigate("new_screen1")
                        expanded = false
                    }) {
                        Text("Screen 1")
                    }
                    DropdownMenuItem(onClick = {
                        navController.navigate("new_screen2")
                        expanded = false
                    }) {
                        Text("Screen 2")
                    }
                }
            }
        )
    }

    @Composable
    fun BottomNavigationBar(navController: NavHostController) {
        BottomNavigation {
            val navBackStackEntry by navController.currentBackStackEntryAsState()
            val currentRoute = navBackStackEntry?.destination?.route

            BottomNavigationItem(
                icon = { Icon(painter = painterResource(id = android.R.drawable.ic_menu_view), contentDescription = "Main") },
                selected = currentRoute == "main",
                onClick = {
                    navController.navigate("main") {
                        popUpTo(navController.graph.startDestinationId) { saveState = true }
                        launchSingleTop = true
                        restoreState = true
                    }
                },
                label = { Text("Main") }
            )
            BottomNavigationItem(
                icon = { Icon(painter = painterResource(id = android.R.drawable.ic_menu_add), contentDescription = "Screen 1") },
                selected = currentRoute == "new_screen1",
                onClick = {
                    navController.navigate("new_screen1") {
                        popUpTo(navController.graph.startDestinationId) { saveState = true }
                        launchSingleTop = true
                        restoreState = true
                    }
                },
                label = { Text("Screen 1") }
            )
            BottomNavigationItem(
                icon = { Icon(painter = painterResource(id = android.R.drawable.ic_menu_agenda), contentDescription = "Screen 2") },
                selected = currentRoute == "new_screen2",
                onClick = {
                    navController.navigate("new_screen2") {
                        popUpTo(navController.graph.startDestinationId) { saveState = true }
                        launchSingleTop = true
                        restoreState = true
                    }
                },
                label = { Text("Screen 2") }
            )
        }
    }

    @OptIn(ExperimentalPagerApi::class)
    @Composable
    fun MainScreen(navController: NavHostController) {
        val tabs = listOf("Tab 1", "Tab 2", "Tab 3", "Tab 4")
        val pagerState = rememberPagerState()
        val coroutineScope = rememberCoroutineScope()

        Column {
            // LazyRow with images
            LazyRow(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(8.dp)
            ) {
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier
                            .padding(8.dp)
                            .clickable {
                                navController.navigate("new_screen1")
                            }
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier
                            .padding(8.dp)
                            .clickable {
                                navController.navigate("new_screen2")
                            }
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier.padding(8.dp)
                    )
                }
            }

            // Tabs and HorizontalPager
            TabRow(selectedTabIndex = pagerState.currentPage) {
                tabs.forEachIndexed { index, title ->
                    Tab(
                        selected = pagerState.currentPage == index,
                        onClick = {
                            coroutineScope.launch {
                                pagerState.animateScrollToPage(index)
                            }
                        },
                        text = { Text(title) }
                    )
                }
            }
            HorizontalPager(state = pagerState, count = tabs.size) { page ->
                when (page) {
                    0 -> Tab1Screen(navController)
                    1 -> Tab2Screen()
                    2 -> Tab3Screen()
                    3 -> Tab4Screen()
                }
            }

            // ThreeColumns content
            Row {
                Column {
                    ThreeColumns()
                }
            }
        }
    }

    @OptIn(ExperimentalMaterialApi::class)
    @Composable
    fun NewScreen1(navController: NavHostController) {
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("New Screen1") },
                    navigationIcon = {
                        IconButton(onClick = { navController.navigateUp() }) {
                            Icon(painter = painterResource(id = android.R.drawable.ic_menu_revert), contentDescription = "Back")
                        }
                    }
                )
            },
            content = { innerPadding ->
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(innerPadding)
                        .padding(16.dp)
                ) {
                    Text(text = "This is New Screen1", style = MaterialTheme.typography.h4)
                }
            }
        )
    }

    @OptIn(ExperimentalMaterialApi::class)
    @Composable
    fun NewScreen2(navController: NavHostController) {
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("New Screen2") },
                    navigationIcon = {
                        IconButton(onClick = { navController.navigateUp() }) {
                            Icon(painter = painterResource(id = android.R.drawable.ic_menu_revert), contentDescription = "Back")
                        }
                    }
                )
            },
            content = { innerPadding ->
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(innerPadding)
                        .padding(16.dp)
                ) {
                    Text(text = "This is New Screen2", style = MaterialTheme.typography.h4)
                }
            }
        )
    }

    @Composable
    fun Tab1Screen(navController: NavHostController) {
        Column {
            LazyRow(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(8.dp)
            ) {
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier
                            .padding(8.dp)
                            .clickable {
                                navController.navigate("new_screen1")
                            }
                    )
                }
                item {
                    Image(
                        painter = painterResource(id = R.drawable._d_burger),
                        contentDescription = "Foto",
                        modifier = Modifier
                            .padding(8.dp)
                            .clickable {
                                navController.navigate("new_screen2")
                            }
                    )
                }
                // Add more items as needed
            }
            Row {
                Column {
                    ThreeColumns()
                }
            }
        }
    }

    @Composable
    fun Tab2Screen() {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(16.dp)
        ) {
            Text("This is Tab 2", style = MaterialTheme.typography.h4)
        }
    }

    @Composable
    fun Tab3Screen() {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(16.dp)
        ) {
            Text("This is Tab 3", style = MaterialTheme.typography.h4)
        }
    }

    @Composable
    fun Tab4Screen() {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(16.dp)
        ) {
            Text("This is Tab 4", style = MaterialTheme.typography.h4)
        }
    }

    @Composable
    fun ThreeColumns() {
        Row(modifier = Modifier.fillMaxWidth()) {
            // First column with weight 1 (smallest width)
            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(8.dp)
            ) {
                Text("Col 1", style = MaterialTheme.typography.subtitle1)
            }

            // Second column with weight 2 (medium width)
            Column(
                modifier = Modifier
                    .weight(2f)
                    .padding(8.dp)
            ) {
                Text("Col 2", style = MaterialTheme.typography.subtitle1)
            }

            // Third column with weight 3 (largest width)
            Column(
                modifier = Modifier
                    .weight(3f)
                    .padding(8.dp)
            ) {
                Text("Col 3", style = MaterialTheme.typography.subtitle1)
            }
        }
    }
}
```

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/31a8bd90-78c0-4663-af4e-fba35fd5fd94)

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/d07159d8-c8b5-48a4-b0f0-9a23af9af46b)

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/677487e9-b3c6-49d3-99e9-b4c34ae9e36f)

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/24dbde33-21bc-438c-9202-43589603e1d8)

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

![image](https://github.com/luiscoco/Android_Kotlin_lesson2_MyFirstComposeApp/assets/32194879/068dbb5c-133b-4cc8-9fd0-1b23f037f364)

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






