[![Join the chat at https://gitter.im/manupsunny/PinLock](https://badges.gitter.im/manupsunny/PinLock.svg)](https://gitter.im/manupsunny/PinLock?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Maven Central](https://img.shields.io/maven-central/v/com.manusunny/pinlock.svg)](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22pinlock%22)
[![Download](https://api.bintray.com/packages/manupsunny/maven/PinLock/images/download.svg)](https://bintray.com/manupsunny/maven/PinLock/_latestVersion)
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-PinLock-orange.svg?style=flat)](http://android-arsenal.com/details/1/2824)
[![Circle CI](https://circleci.com/gh/manupsunny/PinLock.svg?style=shield&circle-token=851fc23d68f8848cd06350b82a8391b94b65c337)](https://circleci.com/gh/manupsunny/PinLock)
[![Codacy Badge](https://api.codacy.com/project/badge/grade/9889b3e5a1894ed8bdda28b078155807)](https://www.codacy.com/app/manupsunny/PinLock)
[![Hex.pm](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)

# PinLock

An Android library which can be used for implementing PIN lock mechanism in Android applications.

### Usage

First, add PinLock dependency to your `build.gradle`. PinLock is available in both Maven and jCenter.
```
compile 'com.manusunny:pinlock:+'
```

##### 1. Setting PIN

Create a new class by extending `SetPinActivity.java`. And implement method `onPinSet()`,
```java
public class SetPinActivitySample extends SetPinActivity {
    public void onPinSet(String pin){
        //Save 'pin' as SharedPreference
    }
}
```

That's it. Now you can start this activity using `startActivityForResult()`. And handle the results in `onActivityResult()`.
Activity will return one of these result codes:
1. `PinListener.SUCCESS`
2. `PinListener.CANCELLED`

##### 2. Confirming PIN

Create a new class by extending `ConfirmPinActivity.java`. And implement two methods,
```java
public class ConfirmPinActivitySample extends SetPinActivity {
    @Override
    public boolean isPinCorrect(String pin) {
        String currentPin = // get it from SharedPreferences
        return pin.equals(currentPin);
    }

    @Override
    public void onForgotPin() {
        // handle forgot PIN scenario
    }
}
```

Now you can start this activity using `startActivityForResult()`. And handle the results in `onActivityResult()`.
Activity will return one of these result codes:
1. `PinListener.SUCCESS`
2. `PinListener.CANCELLED`
3. `PinListener.FORGOT`

### Customizing the Plugin

##### 1. Customizing Styles

All styles in this library are configurable. Give required styles in `res/values/styles.xml`

Example:
```xml
<resources>
    <style name="PinLock" >
        <item name="pinLength">4</item>
        <item name="backgroundColor">#FFFFFF</item>

        <item name="keypadButtonShape">@drawable/rectangle</item>
        <item name="keypadTextColor">#000000</item>
        <item name="keypadTextSize">20</item>
        <item name="keypadWidth">200dp</item>
        <item name="keypadHeight">230dp</item>
        <item name="keypadVerticalSpacing">2dp</item>
        <item name="keypadHorizontalSpacing">2dp</item>
        <item name="keypadClickAnimationDuration">100</item>

        <item name="cancelForgotTextColor">#000000</item>
        <item name="cancelForgotTextSize">14</item>

        <item name="infoTextColor">#000000</item>
        <item name="infoTextSize">20</item>

        <item name="vibrateOnClick">true</item>
        <item name="vibrateDuration">20</item>

        <item name="statusEmptyBackground">@drawable/dot_empty</item>
        <item name="statusFilledBackground">@drawable/dot_filled</item>
        <item name="statusDotDiameter">8dp</item>
        <item name="statusDotSpacing">10dp</item>
    </style>
</resources>
```

##### 2. Customizing Labels

You can customize the messages and labels used in the library. Give new texts in `res/values/strings.xml`

Example:
```xml
<resources>
    <string name="message_enter_pin">Enter PIN</string>
    <string name="message_enter_new_pin">Enter new PIN</string>
    <string name="message_confirm_pin">Re enter PIN</string>
    <string name="message_invalid_pin">Invalid PIN. Try again</string>
    <string name="message_pin_mismatch">PIN mismatch. Try again</string>

    <string name="button_cancel">Cancel</string>
    <string name="button_forgot_pin">Forgot PIN</string>
</resources>
```

### Supporting Multiple Languages

You can support multiple languages by providing texts in different languages. If texts are not available for the selected language, English will be used as the fallback language. Add `res/values-<language_code>` folder for each new language, and provide tranlated contents in `strings.xml` file.

Folder Structure :

    |res
        |values       // Default language (en)
            |strings.xml
        |values-es    // Spanish
            |strings.xml
        |values-de    // German
            |strings.xml
            
Example: 

Sample file for Spanish `res/values-es/strings.xml`
```xml
<resources>
    <string name="message_enter_pin">Ingrese el PIN</string>
    <string name="message_enter_new_pin">Ingrese un nuevo PIN</string>
    <string name="message_confirm_pin">Confirme el PIN</string>
    <string name="message_invalid_pin">PIN inválido. Intente de nuevo</string>
    <string name="message_pin_mismatch">El PIN no coincide. Intente de nuevo</string>

    <string name="button_cancel">Cancelar</string>
    <string name="button_forgot_pin">Olvidé mi PIN</string>
</resources>
```

A list of languages which are currently supported by Android along with their codes are available [here](https://github.com/manupsunny/PinLock/blob/master/LangCodes.md).

### License

    Copyright 2016 © Manu Sunny

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

### Sample Screenshots

| SetPin | ConfirmPin | ChangePin |
| :----: | :--------: | :--------:|
| ![alt text](https://github.com/manupsunny/PinLock/blob/master/images/PinSet.gif "PinSet") | ![alt text](https://github.com/manupsunny/PinLock/blob/master/images/PinConfirm.gif "PinSet") | ![alt text](https://github.com/manupsunny/PinLock/blob/master/images/PinChange.gif "PinSet") |
