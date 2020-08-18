## Introduction

Hi, and welcome to my Android course.

A video course that teaches you the basics to build mobile applications following modern development standards.



## Building modern mobile apps is too difficult.

Surfing on internet have you found many manuals, many courses but you don't know which path to follow?

**If you have also had these doubts, then you are in the right place!**

This is the course I would have preferred to follow when I started to get passionate about the Android world. A course created by an Android developer for anyone who wants to become a full-time mobile developer.

I have compiled a series of necessary topics to know, for those who enter the world of Android development. At the end of the course you will **not receive a certificate but knowledge!**

The strengths of my video course are:

- Clear
- Concise
- Learning to doing
- Beginner Friendly
- Open-Source Code



## Course overview.

Have you ever wondered how the large mobile applications you use on a daily basis are built? What are the main technologies, or what patterns are used?

We build a complete Android application using the full potential of the **Kotlin** programming language. You will learn how to use **Clean Architecture** on your projects to build robust, flexible and maintainable applications.

In this course I will show you how to build a real mobile application starting from **zero lines of code** until you get an app ready to be published on the **Google Play Store**.



- Clean Architecture
- Navigation Component
- Room database
- LiveData
- ViewModel
- Animation
- DiffUtil
- Dark mode
- more...


## The Mobile App

This is the app that we build during the course. An app that track the time that you spend on your activities and calculate your earnings.

It's composite by three view, Projects, Tasks and Categories.


## Create project

Create a new project with name Tintracker, package name com.tintracker, choose the save location and click finish.

The minSdkVersion is 21.



## Setup project and install dependencies

We install dependencies that will help us in the development of our application. 
During the course we will see in detail what each of them is for.

**Material Design**

```
implementation 'com.google.android.material:material:1.2.0'
```

**Room**

```
implementation 'androidx.room:room-runtime:2.2.5'
implementation 'androidx.legacy:legacy-support-v4:1.0.0'
kapt 'androidx.room:room-compiler:2.2.5'
implementation "androidx.room:room-ktx:2.2.5"
implementation 'androidx.paging:paging-runtime:2.1.2'
```

**Jetpack navigation**

```
implementation 'androidx.navigation:navigation-fragment-ktx:2.3.0'
implementation 'androidx.navigation:navigation-ui-ktx:2.3.0'
```

**Architecture components**

```
implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:2.2.0"
implementation "androidx.lifecycle:lifecycle-livedata-ktx:2.2.0"
```

**Coroutines**

```
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.5"
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.5"
```



# Navigation Component

### Create a Bottom navigation

Open `activity_main.xml` and change the layout to `CoordinatorLayout`. (??)

Then add a `BottomNavigationView` to `CoordinatorLayout`.

Bottom navigation bars make it easy for users to explore and switch between top-level views in a single tap. They should be used when an application has three to five top-level destinations.

Bottom navigation bar, represents a standard for the application. 

The code for BottomNAvigation

```xml
<com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottomNavigation"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom"
        android:background="#FFF"
        android:elevation="20dp"
        app:labelVisibilityMode="labeled"
        app:menu="@menu/navigation"/>
```

Create a new android resource that call `navigation.xml` in menu resource. 

Import the vector asset for menu (dashboard, list, av timer, start).

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/projectsFragment"
        android:icon="@drawable/ic_projects"
        android:title="@string/projects"/>

    <item
        android:id="@+id/tasksFragment"
        android:icon="@drawable/ic_tasks"
        android:title="@string/tasks" />

    <item
        android:id="@+id/statisticsFragment"
        android:icon="@drawable/ic_statistics"
        android:title="@string/statistics"/>

    <item
        android:id="@+id/categoriesFragment"
        android:icon="@drawable/ic_categories"
        android:title="@string/categories"/>

</menu>
```

Show the result in the emulator.

### Navigation component

The Navigation component consists of three key parts that are described below:

- Navigation graph: An XML resource that contains all navigation-related information in one centralized location. This includes all of the individual content areas within your app, called *destinations*, as well as the possible paths that a user can take through your app.
- `NavHost`: An empty container that displays destinations from your navigation graph. The Navigation component contains a default `NavHost` implementation, [`NavHostFragment`](https://developer.android.com/reference/androidx/navigation/fragment/NavHostFragment), that displays fragment destinations.
- `NavController`: An object that manages app navigation within a `NavHost`. The `NavController` orchestrates the swapping of destination content in the `NavHost` as users move throughout your app.

### Create Projects view

Create a new Empty Fragment, `ProjectsFragment` with ConstraintLayout. Remove the useless code.

In xml file update textView with the name of the fragment.

### Create Tasks view

Create a new Empty Fragment, `TasksFragment` with ConstraintLayout. Remove the useless code.

In xml file update textView with the name of the fragment.

### Create Statistics view

Create a new Empty Fragment, `StatisticsFragment` with ConstraintLayout. Remove the useless code.

In xml file update textView with the name of the fragment.

### Create Categories view

Create a new Empty Fragment, `CategoriesFragment` with ConstraintLayout. Remove the useless code.

In xml file update textView with the name of the fragment.

### Create Navigation graph

Create a a navigation graph that call `app_navigation.xml` and add the destinations (dashboardFragment, tasksFragment, statisticsFragment, categoriesFragment).

**Attention**: the `id` must be the same of the `id`  in menu -> navigation -> item.

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/app_navigation"
    app:startDestination="@id/projectsFragment">


    <fragment
        android:id="@+id/projectsFragment"
        android:name="com.tintracker.ProjectsFragment"
        android:label="@string/projects"
        tools:layout="@layout/fragment_projects" />
    <fragment
        android:id="@+id/tasksFragment"
        android:name="com.tintracker.TasksFragment"
        android:label="@string/tasks"
        tools:layout="@layout/fragment_tasks" >
    </fragment>
    <fragment
        android:id="@+id/statisticsFragment"
        android:name="com.tintracker.StatisticsFragment"
        android:label="@string/statistics"
        tools:layout="@layout/fragment_statistics" >

    </fragment>
    <fragment
        android:id="@+id/categoriesFragment"
        android:name="com.tintracker.CategoriesFragment"
        android:label="@string/categories"
        tools:layout="@layout/fragment_categories" >

    </fragment>
</navigation>
```

In `activity_main.xml` layout add the `navHostFragment`

```xml
    <fragment
        android:id="@+id/navHostFragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        app:defaultNavHost="true"
        app:navGraph="@navigation/app_navigation"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
```

In MainActivity setup navigation controller

```kotlin
val navController = findNavController(R.id.navHostFragment)

//val appBarConfiguration = AppBarConfiguration(setOf(R.id.dashboardFragment, 		   R.id.tasksFragment, R.id.statisticsFragment, R.id.categoriesFragment))

//setupActionBarWithNavController(navController, appBarConfiguration)

bottomNavigation.setupWithNavController(navController)
```

if would update the title bar with the name of the active fragment add:

```kotlin
val navController = findNavController(R.id.navHostFragment)

val appBarConfiguration = AppBarConfiguration(setOf(R.id.projectsFragment, 		   R.id.tasksFragment, R.id.statisticsFragment, R.id.categoriesFragment))

setupActionBarWithNavController(navController, appBarConfiguration)

bottomNavigation.setupWithNavController(navController)
```

and change the compile and kotlin options of the `build.gradle` 

```
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    kotlinOptions {
        jvmTarget = JavaVersion.VERSION_1_8.toString()
    }
```

now run the emulator and test it.


# Change color theme



# Room Database

Room provides an abstraction layer over SQLite to allow fluent database access while harnessing the full power of SQLite.

There are 3 major components in Room:

- [**Database:**](https://developer.android.com/reference/androidx/room/Database) Contains the database holder and serves as the main access point for the underlying connection to your app's persisted, relational data.

  The class that's annotated with [`@Database`](https://developer.android.com/reference/androidx/room/Database) should satisfy the following conditions:

  - Be an abstract class that extends [`RoomDatabase`](https://developer.android.com/reference/androidx/room/RoomDatabase).
  - Include the list of entities associated with the database within the annotation.
  - Contain an abstract method that has 0 arguments and returns the class that is annotated with [`@Dao`](https://developer.android.com/reference/androidx/room/Dao).

  At runtime, you can acquire an instance of [`Database`](https://developer.android.com/reference/androidx/room/Database) by calling [`Room.databaseBuilder()`](https://developer.android.com/reference/androidx/room/Room#databaseBuilder(android.content.Context, java.lang.Class, java.lang.String)) or [`Room.inMemoryDatabaseBuilder()`](https://developer.android.com/reference/androidx/room/Room#inMemoryDatabaseBuilder(android.content.Context, java.lang.Class)).

- [**Entity:**](https://developer.android.com/training/data-storage/room/defining-data) Represents a table within the database.

- [**DAO:**](https://developer.android.com/training/data-storage/room/accessing-data) Contains the methods used for accessing the database.

The app uses the Room database to get the data access objects, or DAOs, associated with that database. The app then uses each DAO to get entities from the database and save any changes to those entities back to the database. Finally, the app uses an entity to get and set values that correspond to table columns within the database.

### Create Category model class

In Room, an entity is a class that is our in-memory rapresentation of a SQLite table. Instances of the entity class represent rows in that table.

```kotlin
@Parcelize
@Entity(tableName = Category.TABLE_NAME)
class Category(
    @PrimaryKey(autoGenerate = true)
    var id: Int = 0,
    var name: String
):Parcelable {
    companion object {
        const val TABLE_NAME = "tintracker_categories"
    }
}
```

#### Parcelable

Basically **Parcelable** is a component of Android SDK, an Interface which is similar to JAVA Serializable. It is Android’s recommended way of passing your custom data structure between different components in your app, because Parcelable is processed relatively fast compared to the standard JAVA serialization.

### Create Dao

A Dao class says how I want read and write from that table. We define an interface or abstract class to descrive the API that we want to have for working with the database.

```kotlin
@Dao
interface CategoryDao {
    @Query("SELECT * FROM ${Category.TABLE_NAME}")
    fun getAllCategories(): Flow<List<Category>>

    @Insert(onConflict = OnConflictStrategy.REPLACE)
    suspend fun saveCategory(category: Category)

    @Delete
    suspend fun deleteCategory(category: Category)
}
```

@Insert, @Query, @Delete  are annotation that indicate what is the database operation that this method should apply.

In `getAllCategories()` our desired return values is a **Flow** from Kotlin's coroutines system.

In this circumstances Room will perform the query on a background thread and post the results to the Flow when ready, avoiding blocking the user interface until the operation is completed.

The keyword `suspend` indicates that these functions may run on a background thread, in such a fashion that callers may need to suspend their work waiting for these functions to return.

### Dependency injection with Koin

Many apps use dependency injection patterns for connecting different pieces of the app.

For this app i use KOIN. Add this to `build.gradle (app)` and click `Sync`

```
    implementation 'org.koin:koin-android:2.0.1'
    implementation 'org.koin:koin-androidx-viewmodel:2.0.1'
    implementation 'org.koin:koin-core:2.0.1'
```

### Create Database

```kotlin
@Database(
    entities = [Category::class],
    version = AppDatabase.DB_VERSION
)
abstract class AppDatabase : RoomDatabase() {

    abstract fun getCategoryDao(): CategoryDao

    companion object {
        const val DB_VERSION = 1
        const val DB_NAME = "tintracker_database"

        fun getInstance(context: Context): AppDatabase {
            return Room.databaseBuilder(context, AppDatabase::class.java, DB_NAME).build()
        }
    }
}
```

Usually, a Room database is a singleton. And since we are using Koin, we can have Koin supply our database to other classes via dependency injection.

This simply invokes our `getInstance()` function and exposes that instance as a `single` object. It uses `androidContext()` function, supplied by Koin, to get the Application singleton and supply that as a Context to our `getInstance()`

```kotlin
-->val databaseModule = module {
    single { AppDatabase.getInstance(androidContext()) }
    single { get<AppDatabase>().getCategoryDao() }
}

@Database(
    entities = [Category::class],
    version = AppDatabase.DB_VERSION
)
abstract class AppDatabase : RoomDatabase() {

    abstract fun getCategoryDao(): CategoryDao

    companion object {
        const val DB_VERSION = 1
        const val DB_NAME = "tintracker_database"

        fun getInstance(context: Context): AppDatabase {
            return Room.databaseBuilder(context, AppDatabase::class.java, DB_NAME).build()
        }
    }
}
```

### Create TintrackerApp

```kotlin
class TintrackerApp : Application() {

    override fun onCreate() {
        super.onCreate()
        startKoin {
            androidLogger()
            androidContext(this@TintrackerApp)
            modules(listOf(
                databaseModule,
            ))
        }
    }
}
```

### Create Repository

```kotlin
val categoryRepositoryModule = module {
    factory { CategoryRepository(get()) }
}

class CategoryRepository(private val categoryDao: CategoryDao) {

    fun gellAllCategories(): Flow<List<Category>> {
        return categoryDao.getAllCategories()
    }

    suspend fun saveCategory(category: Category) {
        categoryDao.saveCategory(category)
    }

    suspend fun deleteCategory(category: Category) {
        categoryDao.deleteCategory(category)
    }
}
```

then update the main application with this new module

```kotlin
class TintrackerApp : Application() {

    override fun onCreate() {
        super.onCreate()
        startKoin {
            androidLogger()
            androidContext(this@TintrackerApp)
            modules(listOf(
                databaseModule,
                -->categoryRepositoryModule
            ))
        }
    }
}
```

Now its time to build the Categories View.



### Create Insert Categories View

Let's start and create a new activity called `CategoryFormActivity` that I use for add or edit a category.

My `activity_form_category` contain:

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/windowBackground"
    tools:context=".ui.category.CategoryFormActivity">

    <TextView
        android:id="@+id/labelCategory"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="16dp"
        android:text="@string/category"
        android:textSize="@dimen/text_item"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/layoutCategory"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginEnd="16dp"
        android:textCursorDrawable="@null"
        app:hintTextAppearance="@style/AppTheme.CustomTextFloatAppearance"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/labelCategory">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/tvCategory"
            style="@style/AppTheme.CustomEditText"
            android:layout_width="match_parent"
            android:layout_height="48dp"
            android:lines="1"
            android:maxLines="1"
            android:paddingStart="10dp"
            android:paddingEnd="10dp"
            android:textColor="@color/textColor"
            android:textCursorDrawable="@null" />

    </com.google.android.material.textfield.TextInputLayout>


    <Button
        android:id="@+id/btnSave"
        style="@style/AppTheme.ButtonStyle"
        android:layout_width="match_parent"
        android:layout_height="48dp"
        android:layout_marginStart="16dp"
        android:layout_marginTop="24dp"
        android:layout_marginEnd="16dp"
        android:text="@string/save"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/layoutCategory" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

In this part I want to show how customize every single component of my interface. Like button, input and theme.

This is the final `style.xml` 

```xml
    <style name="AppTheme.ButtonStyle" parent="Widget.AppCompat.Button.Borderless">
        <item name="android:textColor">@color/white</item>
        <item name="android:textSize">@dimen/text_button</item>
        <item name="android:background">@drawable/round_button_blue</item>
        <item name="android:padding">0dp</item>
        <item name="android:textAllCaps">false</item>
    </style>

    <style name="AppTheme.CustomEditText" parent="Widget.AppCompat.EditText">
        <item name="colorControlActivated">@color/colorPrimary</item>
        <item name="colorControlHighlight">@color/colorPrimary</item>
        <item name="android:background">@drawable/input_rounded</item>
        <item name="android:paddingTop">3dp</item>
        <item name="android:paddingBottom">3dp</item>
        <item name="android:inputType">text</item>
        <item name="android:textSize">@dimen/text_item</item>
    </style>

    <style name="AppTheme.CustomTextFloatAppearance" parent="@android:style/TextAppearance">
        <item name="android:textSize">@dimen/text_item</item>
        <item name="android:textColor">@color/colorPrimary</item>
    </style>
```

this is `colors.xml` file

```xml
    <color name="colorPrimary">#6200EE</color>
    <color name="colorPrimaryDark">#3700B3</color>
    <color name="colorAccent">#03DAC5</color>
    <color name="white">#FFFFFF</color>
    <color name="grey">#9e9e9e</color>
    <color name="textColor">@android:color/black</color>
    <color name="windowBackground">#F3F3F3</color>
    <color name="red">#EB144C</color>
```

`round_button.xml` file in `drawable` folder

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <solid android:color="@color/round_button_clicked" />
    <corners android:bottomRightRadius="10dp"
        android:bottomLeftRadius="10dp"
        android:topRightRadius="10dp"
        android:topLeftRadius="10dp"/>
</shape>
```

`input_rounded.xml` file in `drawable` folder

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <item>
        <shape android:shape="rectangle">
            <solid android:color="@color/grey" />
            <corners android:radius="10dp" />
        </shape>
    </item>
    <item android:right="1.5dp" android:left="1.5dp" android:top="1.5dp" android:bottom="1.5dp">
        <shape android:shape="rectangle" >
            <solid android:color="@color/white" />
            <corners android:radius="10dp" />
        </shape>
    </item>
</layer-list>
```

`input_rounded_error.xml` file in `drawable` folder

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <item>
        <shape android:shape="rectangle">
            <solid android:color="@color/red" />
            <corners android:radius="10dp" />
        </shape>
    </item>

    <item android:right="1.5dp" android:left="1.5dp" android:top="1.5dp" android:bottom="1.5dp">
        <shape android:shape="rectangle" >
            <solid android:color="@color/white" />
            <corners android:radius="10dp" />

        </shape>
    </item>
</layer-list>
```



## Create View Model

### What is MVVM architecture?

MVVM architecture is a Model-View-ViewModel architecture that removes the tight coupling between each component. Most importantly, in this architecture, the children don't have the direct reference to the parent, they only have the reference by observables.

- **Model:** It represents the data and the business logic of the Android Application. It consists of the business logic - local and remote data source, model classes, repository.
- **View:** It consists of the UI Code(Activity, Fragment), XML. It sends the user action to the ViewModel but does **not** get the response back directly. To get the response, it has to subscribe to the observables which ViewModel exposes to it.
- **ViewModel:** It is a bridge between the View and Model(business logic). It does not have any clue which View has to use it as it does not have a direct reference to the View. So basically, the ViewModel should not be aware of the view who is interacting with. It interacts with the Model and exposes the observable that can be observed by the View.

Let's start to implement the `CategoryViewModel.kt`

```kotlin
import androidx.lifecycle.LiveData
import androidx.lifecycle.MutableLiveData
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import com.tintracker.data.models.Category
import com.tintracker.data.repository.CategoryRepository
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.flow.collect
import kotlinx.coroutines.launch
import org.koin.dsl.module

val categoryModule = module {
    factory { CategoryViewModel(get()) }
}

class CategoryViewModel(
    private val categoryRepository: CategoryRepository
):ViewModel() {

    fun saveCategory(category: Category) {
        viewModelScope.launch(Dispatchers.IO) {
            categoryRepository.saveCategory(category)
        }
    }

}
```

and add the new module to `TintrackerApp.kt`

Before to elaborate the CategoryFormActivity, enabled the **viewBinding**. 

*View binding* is a feature that allows you to more easily write code that interacts with views. Once view binding is enabled in a module, it generates a *binding class* for each XML layout file present in that module. An instance of a binding class contains direct references to all views that have an ID in the corresponding layout.

In most cases, view binding replaces `findViewById`.

In `build.gradle (app)` add and sync.

```
    buildFeatures {
        viewBinding = true
    }
```

### Create Category Form

Now start to code the `CategoryFormActivity.kt`

```kotlin
mport androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.MenuItem
import android.widget.Toast
import androidx.core.content.ContextCompat
import com.tintracker.R
import com.tintracker.data.models.Category
import com.tintracker.databinding.ActivityFormCategoryBinding
import kotlinx.android.synthetic.main.activity_form_category.*
import org.koin.androidx.viewmodel.ext.android.viewModel

class CategoryFormActivity : AppCompatActivity() {

    private val categoryViewModel: CategoryViewModel by viewModel()
    private lateinit var binding: ActivityFormCategoryBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityFormCategoryBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
        supportActionBar?.setDisplayHomeAsUpEnabled(true)

        binding.btnSave.setOnClickListener {
            saveCategory()
        }
    }

    private fun saveCategory() {
        val text = binding.tvCategory.text
        if (text.isNullOrEmpty()) {
            tvCategory.background = ContextCompat.getDrawable(applicationContext, R.drawable.input_rounded_error)
            return
        }

            val category = Category(name= text.trim().toString())
            categoryViewModel.saveCategory(category)
            Toast.makeText(this, getString(R.string.category_successfully_saved), Toast.LENGTH_SHORT).show()
        
        onBackPressed()
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        return when(item.itemId) {
            android.R.id.home -> {
                finish()
                true
            }
            else -> super.onOptionsItemSelected(item)
        }
    }
}
```

Run the emulator and insert some categories.

Now its time to list all categories that saved in my database.



# Create Row layout for RecyclerView

Define a layout resource to use for the rows in my category list.

In layout directory create a new resource file and assign the `category_item` name.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/layoutItemCategory"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="?android:attr/selectableItemBackground"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">


    <TextView
        android:id="@+id/tvName"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="16dp"
        android:layout_marginBottom="16dp"
        android:textColor="@color/textColor"
        android:textSize="@dimen/text_item"
        app:layout_constraintBottom_toTopOf="@+id/view"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:text="Item" />

    <View
        android:id="@+id/view"
        android:layout_width="match_parent"
        android:layout_height="0.5dp"
        android:background="@color/grey"
        app:layout_constraintBottom_toBottomOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### Create RecyclerView Adapter

`RecyclerView` is based on `RecyclerView.Adapter` and `RecyclerView.ViewHolder`. In particular `ViewHolder` is responsible for a single item in `RecyclerView`, such as a single row in a scrolling list. The `Adapter` is responsible for creating and populating the `ViewHolder` instances for each of our model objects.

So let's start by creating the `CategoryAdapter` and the `ViewHolder` classes.

In `onCreateViewHolder()` we are using `inflate()` to inflate the `category_item` layout.

 `onBindViewHolder()` is  called when `RecyclerView` wants us to update a `ViewHolder` to reflect data from some item in RecyclerView. We are given the `position` of that item that need to be updated and we pass that to `bind()`  function.

```kotlin
class CategoryListAdapter(
    private var listener: (Category) -> Unit
) : androidx.recyclerview.widget.ListAdapter<Category, CategoryListAdapter.CategoryHolder>(DiffCallback) {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): CategoryHolder {
        val layoutInflater = LayoutInflater.from(parent.context)
        val view = layoutInflater.inflate(R.layout.category_item, parent, false)
        return CategoryHolder(view)
    }

    override fun onBindViewHolder(holder: CategoryHolder, position: Int) {
        holder.bind(getItem(position))
    }

    inner class CategoryHolder(val view: View) : androidx.recyclerview.widget.RecyclerView.ViewHolder(view) {
        fun bind(category: Category) = with(view) {
            tvName.text = category.name
            layoutItemCategory.setOnClickListener {
                listener(category)
            }
        }
    }

    private object DiffCallback: DiffUtil.ItemCallback<Category>() {
        override fun areItemsTheSame(oldItem: Category, newItem: Category): Boolean {
            return oldItem.id == newItem.id
        }

        override fun areContentsTheSame(oldItem: Category, newItem: Category): Boolean {
            return oldItem.id == newItem.id && oldItem.name == newItem.name
        }
    }
}
```

**Tips**: The constructor parameter that we are missing to the `ListAdapter` constructor is an instance of `DiffUtil.ItemCallback` interface. This interface tells `ListAdapter` how to compare two model objects. In particular, it tells `ListAdapter` whether two model objects should be visually identical, so `RecyclerView` does not have to re-draw or move around view that have not changed their appearance.

- `areItemsTheSame()` needs to return true if two models are really the same thing, in our case determined using their unique IDs.
- `areContentsTheSame()` return true if the two models visual representation are the same.

### Display data in RecyclerView

`CategoriesFragment.kt` 

```kotlin
class CategoriesFragment : Fragment() {

    private var _binding: FragmentCategoriesBinding? = null
    private val binding get() = _binding!!
    private val categoryViewModel: CategoryViewModel by viewModel()
    private var adapter = CategoryListAdapter { item -> editCategory(item) }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        // Inflate the layout for this fragment
        _binding = FragmentCategoriesBinding.inflate(inflater, container, false)
        val view = binding.root
        addOnClickListener()

        binding.listCategory.hasFixedSize()
        binding.listCategory.adapter = adapter
        loadCategories()

        return view
    }

    private fun loadCategories() {
        categoryViewModel.getCategories()
        categoryViewModel.categoriesLiveData.observe(requireActivity(), Observer { items ->
            if (items.isNotEmpty()) {
                adapter.submitList(items)
            }
        })
    }

    private fun addOnClickListener() {
        binding.flbAdd.setOnClickListener{
            val intent = Intent(requireContext(), CategoryFormActivity::class.java)
            startActivity(intent)
        }
    }

    private fun editCategory(item: Category) {
        val intent = Intent(requireContext(), CategoryFormActivity::class.java)
        intent.putExtra("category", item)
        startActivity(intent)
    }

}
```

And then update the `CategoryFormActivity.ky`

```kotlin
mport androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.MenuItem
import android.widget.Toast
import androidx.core.content.ContextCompat
import com.tintracker.R
import com.tintracker.data.models.Category
import com.tintracker.databinding.ActivityFormCategoryBinding
import kotlinx.android.synthetic.main.activity_form_category.*
import org.koin.androidx.viewmodel.ext.android.viewModel

class CategoryFormActivity : AppCompatActivity() {

    private val categoryViewModel: CategoryViewModel by viewModel()
    private lateinit var binding: ActivityFormCategoryBinding
    private var tempCategory: Category? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityFormCategoryBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
        supportActionBar?.setDisplayHomeAsUpEnabled(true)

        if(intent.hasExtra("category")) {
            tempCategory = intent.getParcelableExtra("category") as Category
            if (tempCategory != null) {
                binding.tvCategory.setText(tempCategory?.name)
            }
            supportActionBar?.title = getString(R.string.edit_category)
        } else {
            supportActionBar?.title = getString(R.string.new_category)

        }

        binding.btnSave.setOnClickListener {
            saveCategory()
        }
    }

    private fun saveCategory() {
        val text = binding.tvCategory.text
        if (text.isNullOrEmpty()) {
            tvCategory.background = ContextCompat.getDrawable(applicationContext, R.drawable.input_rounded_error)
            return
        }

        if (tempCategory != null) {
            tempCategory?.name = text.trim().toString()
            categoryViewModel.saveCategory(tempCategory!!)
            tempCategory = null
            Toast.makeText(this, getString(R.string.category_successfully_updated), Toast.LENGTH_SHORT).show()
        } else {
            val category = Category(name= text.trim().toString())
            categoryViewModel.saveCategory(category)
            Toast.makeText(this, getString(R.string.category_successfully_saved), Toast.LENGTH_SHORT).show()
        }
        onBackPressed()
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        return when(item.itemId) {
            android.R.id.home -> {
                finish()
                true
            }
            else -> super.onOptionsItemSelected(item)
        }
    }
}
```



# Delete Single item from Database

`ItemTouchHelper` is a utility class to add swipe to dismiss and drag & drop support to RecyclerView.

It works with a RecyclerView and a Callback class, which configures what type of interactions are enabled and also receives events when user performs these actions.

Depending on which functionality you support, you should override `Callback#onMove(RecyclerView, ViewHolder, ViewHolder)` and / or `Callback#onSwiped(ViewHolder, int)`.

```kotlin
abstract class SwipeToDelete: ItemTouchHelper.SimpleCallback(0, ItemTouchHelper.LEFT) {
    override fun onMove(
        recyclerView: RecyclerView,
        viewHolder: RecyclerView.ViewHolder,
        target: RecyclerView.ViewHolder
    ): Boolean {
        return false
    }
}
```

### Swipe to delete

And then in `CategoriesFragment.kt` create a `swipeHandler()` function. 

Retrieve the item to delete and save in a temporary variable. 

Then call the `deleteCategory()` function and notify to adapter the position removed.

Add Toast to show the outcome of the operation and the possibility to cancel the operation.

```kotlin
private fun swipeHandler() {
        val swipeHandler = object : SwipeToDelete() {
            override fun onSwiped(viewHolder: RecyclerView.ViewHolder, direction: Int) {
                val tempItemToDelete = adapter.currentList[viewHolder.adapterPosition]
                categoryViewModel.deleteCategory(tempItemToDelete)
                adapter.notifyItemRemoved(viewHolder.adapterPosition)

                val snackbar = Snackbar.make(
                    requireActivity().findViewById(android.R.id.content),
                    R.string.category_successfully_deleted,
                    Snackbar.LENGTH_LONG
                )
                snackbar.setAction("Undo") {
                    categoryViewModel.saveCategory(tempItemToDelete)
                }
                snackbar.show()
            }
        }
        val itemTouchHelper = ItemTouchHelper(swipeHandler)
        itemTouchHelper.attachToRecyclerView(binding.listCategory)
    }
```

### Show no data views if database is empty

We improve our list and add a message and an icon to notify the user that our list is empty.

Import a new vector asset icon for no data. In my `fragment_categories` add an `ImageView` and a `TextView`

```xml
<ImageView
        android:id="@+id/no_data_imageView"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@drawable/ic_no_data"
        android:visibility="invisible"
        app:layout_constraintBottom_toBottomOf="@+id/listCategory"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="@+id/listCategory"
        app:layout_constraintTop_toTopOf="@+id/listCategory"
        app:layout_constraintVertical_bias="0.37" />

    <TextView
        android:id="@+id/no_data_textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="12dp"
        android:alpha="0.5"
        android:text="@string/no_data"
        android:textSize="16sp"
        android:visibility="invisible"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="@+id/listCategory"
        app:layout_constraintTop_toBottomOf="@+id/no_data_imageView" />
```

then in `CategoriesFragment.kt` class, update the `loadCategories()` function 

```kotlin
    private fun loadCategories() {
        categoryViewModel.getCategories()
        categoryViewModel.categoriesLiveData.observe(requireActivity(), Observer { items ->
            if (items.isNotEmpty()) {
                binding.listCategory.show()
                binding.noDataImageView.hide()
                binding.noDataTextView.hide()
                adapter.submitList(items)
            } else {
                binding.listCategory.hide()
                binding.noDataImageView.show()
                binding.noDataTextView.show()
            }
        })
    }
```





# Projects

### Create Project model class

Create the `Project.kt` class

```kotlin
@Parcelize
@Entity(tableName = TABLE_NAME)
data class Project (
    @PrimaryKey(autoGenerate = true)
    var id: Int = 0,
    @ColumnInfo(name = "client_name")
    var clientName: String? = null,
    @ColumnInfo(name = "project_name")
    var projectName: String? = null,
    var color: String? = null,
    @ColumnInfo(name = "hourly_rate")
    var hourlyRate: Float?  = 0f,
    var status: StatusProject? = StatusProject.ONGOING
): Parcelable {
    companion object {
        const val TABLE_NAME = "tintracker_projects"
        val colors = listOf(
            "orange",
            "yellow",
            "lightGreen",
            "green",
            "lightBlue",
            "blue",
            "grey",
            "red",
            "pink",
            "violet"
        )
    }
}
```

then create an enum that i call `StatusProject`

```kotlin
enum class StatusProject {
    ONGOING,
    CLOSED
}
```

then add the `Project` class to `AppDatabase`.

### Create Dao

```kotlin
@Dao
interface ProjectDao {
    @Query("SELECT * FROM ${Project.TABLE_NAME}")
    fun getAllProjects(): Flow<List<Project>>

    @Insert(onConflict = OnConflictStrategy.REPLACE)
    suspend fun saveProject(project: Project)

    @Delete
    suspend fun deleteProject(project: Project)
}
```

### Create the repository

```kotlin
val projectRepositoryModule = module {
    factory { ProjectRepository(get()) }
}

class ProjectRepository(private val projectDao: ProjectDao) {

    fun getAllProjects(): Flow<List<Project>> {
        return projectDao.getAllProjects()
    }

    suspend fun saveProject(project: Project) {
        projectDao.saveProject(project)
    }

    suspend fun deleteProject(project: Project) {
        projectDao.deleteProject(project)
    }
}
```

and the add the `ProjectDao` to `AppDatabase`.

### Create Insert Project View

Now lets start to create the form activity for insert a new project. Create a new empty activity that I call `ProjectFormActivity`.

Edit my xml file and add a `NestedScrollView`

### Create View Model



### Create layout for Recyclerview

### Create RecyclerView adapter

### Display data in RecyclerView



# Task



## Statistics



