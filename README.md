# What is it?

After looking at the reference materials below, I tested the construction of an environment that develops iOS, Android and Web simultaneously using react-native-cli.

Reference : https://retool.com/blog/how-to-make-your-react-native-apps-work-on-the-web/

# How?

1. Create react native project.

   ```shell
   npx react-native init (ProjectName)
   ```

2. Move to project folder.

   ```shell
   cd (ProjectName)
   ```

3. Create the necessary files and folders.

   ```
   mkdir src
   
   mkdir public
   
   touch public/index.html
   
   mv App.tsx src
   
   mv app.json src
   
   cp index.js src
   
   mv index.js index.native.js
   ```

4. Install dependencies using npm or yarn.

   ```
   npm install react-dom react-native-web
   npm install -dev react-scripts
   ```

   or

   ```
   yarn add react-dom react-native-web
   yarn add --dev react-scripts
   ```

5. Modify each file as follows.

- `public/index.html`

  ```html
  <!DOCTYPE html>
  <html lang="ko">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>WebTest</title>
    </head>
    <body>
      <div id="root"></div>
    </body>
  </html>
  ```

- `index.native.js`

  ```JavaScript
  import {AppRegistry} from 'react-native';
  import App from './src/App';
  import {name as appName} from './src/app.json';

  AppRegistry.registerComponent(appName, () => App);
  ```

- `src/index.js`

  ```JavaScript
  import {AppRegistry} from 'react-native';
  import App from './App';

  AppRegistry.registerComponent('App', () => App);
  AppRegistry.runApplication('App', {rootTag: document.getElementById('root')});
  ```

- `src/App.tsx`

  ```TypeScript
  import React from 'react';
  import {SafeAreaView, StatusBar, Text, View} from 'react-native';

  const App = () => {
  return (
     <SafeAreaView>
        <StatusBar />
        <View>
        <Text style={{fontSize: 24}}>Hello World!!</Text>
        </View>
     </SafeAreaView>
  );
  };

  export default App;
  ```

6. Edit `package.json` and add the following line to the scripts section.

   ```json
   "web": "react-scripts start"
   ```

7. Run apllication on all platforms using npm or yarn.
   ```Shell
   npm run ios && npm run android && npm run web
   ```
   or
   ```Shell
   yarn ios && yarn android && yarn web
   ```

# Result

![Result](https://github.com/Yuhyeon0516/ReactNative-Run-iOS_Android_Web-Test/assets/120432007/65a3f35b-302f-451e-8cef-27f4a24e3e6c)

