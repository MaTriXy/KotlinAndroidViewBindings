# KotlinAndroidViewBindings

Bindings for properties with Kotlin types (Boolean, String) to layout traits (visibility, text).

[![](https://jitpack.io/v/MarcinMoskala/KotlinAndroidViewBindings.svg)](https://jitpack.io/#MarcinMoskala/KotlinAndroidViewBindings)

Library allows to bind properties of basic types (String, Int, functional) to view element properties. Example:

```kotlin
var email: String by bindToTextView(R.id.emailView)
val emailRequestFocus: ()->Unit by bindToRequestFocus(R.id.emailView)
var emailErrorId: Int? by bindToErrorId(R.id.emailView)
```

This allows to make clear and simple MVP. Example:

LoginView.kt
```kotlin
interface LoginView {
    var progressVisible: Boolean
    
    var email: String
    val emailRequestFocus: ()->Unit
    var emailErrorId: Int?
 
    var password: String
    val passwordRequestFocus: ()->Unit
    var passwordErrorId: Int?
    
    var loginButtonClickedCallback: ()->Unit
}
```

LoginActivity.kt
```kotlin
class LoginActivity : AppCompatActivity(), LoginView {
    
    override var progressVisible by bindToLoading(R.id.progressView, R.id.loginFormView)
    
    override var email by bindToTextView(R.id.emailView)
    override val emailRequestFocus by bindToRequestFocus(R.id.emailView)
    override var emailErrorId by bindToErrorId(R.id.emailView)
    
    override var password by bindToTextView(R.id.passwordView)
    override val passwordRequestFocus by bindToRequestFocus(R.id.passwordView)
    override var passwordErrorId by bindToErrorId(R.id.passwordView)
    
    override var loginButtonClickedCallback by bindToClick(R.id.loginButton)
    
    //...
}
```

Presenter.kt
```kotlin
class LoginPresenter(val view: LoginView) {

    fun onCreate() {
        view.loginButtonClickedCallback = { attemptLogin() }
    }
    
    //...
}
```

This makes presenters fully unit-testable while keeping Activities short and simple. Full example [here](https://github.com/MarcinMoskala/KotlinAndroidViewBindings/tree/master/sample/src/main/java/com/marcinmoskala/kotlinandroidviewbindings/login). Library usage in wider context [here](https://github.com/MarcinMoskala/SimpleKotlinMvpBoilerplate).

## Other libraries

If you like it, remember to leave the star and check out my other libraries:
 * [ActivityStarter](https://github.com/MarcinMoskala/ActivityStarter/blob/master/README.md) - Simple Android Library, that provides easy way to start and save state of Activities, Fragments, Services and Receivers with arguments.
 * [PreferenceHolder](https://github.com/MarcinMoskala/PreferenceHolder) - Library for simple SharedPreference management in Kotlin
 * [ArcSeekBar](https://github.com/MarcinMoskala/ArcSeekBar) - Good looking curved Android SeekBar
 * [VideoPlayView](https://github.com/MarcinMoskala/VideoPlayView) - Custom Android view with video player, loader and placeholder image

License
-------

    Copyright 2017 Marcin Moskała

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

