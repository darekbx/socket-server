# CARI (Console Android Resources Inspector)

Android tool used to view and edit resources like Preferences and Sqlite database.

#### Requirements
Installed Android Debug Bridge (adb), python3.

#### How to use
Connect Android device to the computer, and wait till device is ready, then run: 
> python3 cariclient.py

#### Options
  - **-d** provide a device
  - **-p** provide custom port for forward, default is 38300

#### Shell commands
  - **use** [resource|prefs_scope|sqlite_database]  - Use resource, scope or sqlite database for further actions
  - **clear**                                       - Clear used resource and scopes
  - **version**                                     - Print CARI Android SDK version

#### Resources
  - **prefs**, Android shared preferences wrapper, commands:
    - **scopes** - print all preferences scopes, related to the application context
    - **use** - select preferences scope for further actions
    - **dump** - print all preferences data (can be used with and without scope)
    - **list** - list all keys  (e.g. command: list)
    - **remove** - remove key with value  (e.g. command: remove KeyToDelete)
    - **set** - set value to key (e.g. command: set new_key KeyValue)
    - **get** - get key value (e.g. command: get my_key)
  - **sqlite**, Android SQLite wrapper, commands:
    - **databases** - print all databases, related to the application context
    - **use** - select sqlite database for further actions
    - **tables** - print all tables from selected database
    - **[query]** - execute SQLite query, when database is used (e.g. command: SELECT * FROM table or with prefix: q SELECT 1)

#### How to list keys from preferences scope:
  1. Run CARI: 
  > python3 cariclient.py
  2. In CARI shell type: 
  > use prefs
  3. Dump all scopes, by typing in shell: 
  > dump
  4. Use preferences scope (eg app_preferences), by typing in shell: 
  > use app_preferences   
  5. Type in shell to list all keys: 
  > list
  
#### How to execute an SQLite query:
  1. Run CARI: 
  > python3 cariclient.py
  2. In CARI shell type: 
  > use sqlite
  3. Print all databases, by typing in shell: 
  > databases
  4. Select database, by typing in shell: 
  > use room_db   
  5. Type in shell to execute an query: 
  > q SELECT * FROM table ORDER BY _id DESC

#### Android integration
  1. Download latest **.aar** lib from **./releases** dir and place in project **libs** directory
  2. Add to project **build.gradle** file those lines:
  ```groovy
  allprojects {
      repositories {
         flatDir {
             dirs 'libs'
         }
      }
  }
  ```
  3. Add to project **build.gardle** filr dependency:
  ```groovy
  implementation(name:'cari-sdk-release-1.0.0', ext:'aar')
  ```
  4. Initialize CARI in your Application class:
  ```kotlin
  class MyApplication : Application() {
      override fun onCreate() {
          super.onCreate()
          CARI.initialize(applicationContext)
      }
  }
  ```

<br />

### Any suggestions? Just add an issue.
