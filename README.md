# coroutines

## personal notes

### setup

* kotlinx-coroutines-core: primary interface
* kotlinx-coroutines-android: ui thread support
* lifecycle-viewmodel-ktx: adds CoroutineScope to viewmodels

build.gradle (Module:app)

dependencies {

  ...

  implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:x.x.x"

  implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:x.x.x"

  implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:x.x.x"

}

### purpose

drawbacks in callback pattern
* does not permit exception handling
* can be less readable than sequential code

coroutines overcome both drawbacks and can be converted from callbacks

### function

coroutines mark functions with suspend modifier
* function execution is suspended until result is returned
* ui continues executing independent of suspended func
* suspend function does not specify thread of exec (could be main or bg)
* suspend similar to async Java keyword, except that await() is implicitly called in ktx

all coroutines run inside coroutine scope
* scope controls lifecycle of all contained coroutines
* useful for applying same action to all contained e.g. launch or cancel on user nav
* scope-wide dispatcher can be defined to apply to all contained coroutines
* for coroutines started by main thread, dispatcher is Dispatchers.Main
* lifecycle-viewmodel lib adds viewModelScope as function of ViewModel class
* viewModelScope default dispatcher is .Main and lifecycle is tied to that of ViewModel

launch method starts coroutine on a scope
* all coroutines cancelled with onCleared call from ViewModel dtor

testing
* InstantTaskExecutorRule: from JUnit, tells LiveData to execute tasks synchronously
* TestCoroutineDispatcher: from kotlinx-coroutines-test, provides virtual clock

room
* add suspend modifier to Dao method to make main-safe

retrofit
* to use suspend, add suspend modifier to method and remove call wrapper from return type

---

# Using Kotlin Coroutines in your Android app

[Kotlin Coroutines codelab](https://codelabs.developers.google.com/codelabs/kotlin-coroutines/index.html).

## License

    Copyright 2018 Google LLC

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
