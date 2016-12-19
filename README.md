# tipsi-twitter

[![build status](https://img.shields.io/travis/tipsi/tipsi-twitter/master.svg?style=flat-square)](https://travis-ci.org/tipsi/tipsi-twitter)

React Native component for auth with twitter

## Requirements

### iOS

* Xcode 8+
* iOS 10+
* [CocoaPods](https://cocoapods.org) 1.1.1+

### Android

* Minimum SDK 16

## Installation

Run `npm install --save tipsi-twitter` to add the package to your app's dependencies.

### iOS

 .............................. ....... ..... ..... .... ... . . . .....

### Android

##### react-native cli

Run react-native link tipsi-twitter so your project is linked against your Android project

##### Manual

1. In your app build.gradle add:
```gradle
...
dependencies {
 ...
 compile project(':tipsi-twitter')
 compile "com.facebook.react:react-native:+"  // From node_modules
}
```
2. In your settings.gradle add:
```gradle
...
include ':tipsi-twitter'
project(':tipsi-twitter').projectDir = new File(rootProject.projectDir, '../node_modules/tipsi-twitter/android')
```

3. In your AndroidManifest.xml add:
```xml
    <application
    ...
        <meta-data
            android:name="io.fabric.ApiKey"
            android:value="YOUR_FABRIC_API_KEY" />
    </application>
```

## Usage

```js
...
import { TPSTwitterModule } from 'tipsi-twitter'

TPSTwitterModule.init({
  twitter_key: '<TWITTER_KEY>',
  twitter_secret: '<TWITTER_SECRET>',
})
...

  onTwitterLoginFinished = async () => {
    try {
      const result = await TPSTwitterModule.login()
      this.setState({
        errorMessage: '',
        twitterUserId: result.userId,
      })
    } catch (error) {
      this.setState({
        errorMessage: error.message,
      })
    }
  }
...
  render() {
    return (
      <View style={styles.container}>
        <Button
          title="Twitter Login Button"
          onPress={this.onTwitterLoginFinished}/>
      </View>
    );
  }
...
```

### Result

A `result` object will be returned after successful Twitter auth.

##### `token`

An object with the following keys:

* `userName` _String_ - Twitter user name.
* `userId` _String_ - Twitter user id.
* `isCancelled` _Boolean_ - true if user has canceled Twitter auth.
* `authToken` _Object_ - object with token data.

##### `authToken`

An object with the following keys:

* `token` _String_ - Twitter token for auth in your app.
* `secret` _String_ - Twitter secret for auth in your app.
* `describeContents` _Number_ - For Twitter auth usualy 0.
* `isExpired` _Boolean_ - Always true. Twitter does not expire OAuth1a tokens.

## Tests

#### Local CI

To run `example` app e2e tests for all platforms you can use `npm run ci` command. Before running this command you need to specify `TWITTER_KEY`, `TWITTER_SECRET`,
and `TWITTER_USER`, `TWITTER_PASS` environment variables:

```bash
TWITTER_KEY=<...> TWITTER_SECRET=<...> TWITTER_USER=<...> TWITTER_PASS=<...> npm run ci
```

#### Manual

1. Go to example folder `cd example`
2. Install CocoaPods dependencies (iOS only) `pod install --project-directory=ios`
3. Install npm dependencies `npm install`
4. Configure project before build `TWITTER_KEY=<...> TWITTER_SECRET=<...> npm run configure`
5. Build project:
  * `npm run build:ios` - for iOS
  * `npm run build:android` - for Android
  * `npm run build` - for both iOS and Android
6. Open Appium in other tab `npm run appium`
7. Run tests:
  * `npm run test:ios` - for iOS
  * `npm run test:android` - for Android
  * `npm run test` - for both iOS and Android

#### Troubleshooting

You might encounter the following error while trying to run tests:

`An unknown server-side error occurred while processing the command. Original error: Command \'/bin/bash Scripts/bootstrap.sh -d\' exited with code 1`

This can be fixed by installing `Carthage`:

```bash
brew install carthage
```

## Example

To see more of the `tipsi-twitter` in action, check out the source at [example](https://github.com/tipsi/tipsi-twitter/tree/master/example) folder.

![Eample](https://cloud.githubusercontent.com/assets/4946753/21184163/dec7bb12-c213-11e6-8034-6ac839629838.png)

## License

tipsi-twitter is available under the MIT license. See the [LICENSE](https://github.com/tipsi/tipsi-twitter/tree/master/LICENSE) file for more info.
