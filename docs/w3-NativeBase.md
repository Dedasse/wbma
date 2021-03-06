class: center, middle

# NativeBase

## 3/2020

---
  **Note!**

  When using NativeBase you should import the [`<Image>` component](https://facebook.github.io/react-native/docs/images.html#network-images) still from `react-native` library to avoid issues with network sourced images.

### Setup

1. Continue last exercise. Create a new branch 'nativebase' with git.  
1. Study [this article](https://blog.bitsrc.io/11-react-native-component-libraries-you-should-know-in-2018-71d2a8e33312) and [NativeBase](https://nativebase.io/)
1. Convert the app we've made so far to use NativeBase
1. Install NativeBase
    - `npm i native-base`
    - `expo install expo-font`
1. Note: Remove all styling from the files where you use NativeBase components:

   ```jsx harmony
   // remove this part:
   const styles = StyleSheet.create(...
   ```

    - You can customise NativeBase components later
1. [NativeBase components](https://docs.nativebase.io/Components.html#Components)
   - Some components you may find useful for the task: `Body`, `Button`, `Card`, `CardItem`, `Container`, `Content`, `Header`, `Icon`, `List`, `ListItem`, `Left`, `Right`, `Thumbnail`, `Text`, `Title`...    
   - By default you can use [Ionicons](https://ionicons.com/) as value for name attribute of [Icon](https://docs.nativebase.io/Components.html#icon-def-headref)
1. In our app there are already `ListItem` component so if you want to use the ListItem of [List](https://docs.nativebase.io/Components.html#list-def-headref) component of NativeBase you need to use `import as` syntax:

   ```jsx harmony
   ...
   import {ListItem as NBListItem} from 'native-base';
   ...
   return (
         <NBListItem thumbnail>
               <Left>
                 <Thumbnail>
         etc...
     );
   ```
   
   **Note:** native-base `List` is deprecated, use FlatList (which we already have in List.js)

1. [Adding icons to bottom tabs](https://reactnavigation.org/docs/material-bottom-tab-navigator/#example)

1. In Android devices you might need to [load the NativeBase fonts](https://docs.nativebase.io/docs/GetStarted.html) ([example](https://github.com/GeekyAnts/NativeBase-KitchenSink/blob/CRNA/src/boot/setup.js)) before you can use them. It can be done by using useEffect hook in the _App.js_:

```jsx harmony
import React, { useState, useEffect } from 'react';
import {AuthProvider} from './contexts/AuthContext';
import Navigator from './navigators/Navigator';
import * as Expo from "expo";
import * as Font from 'expo-font';

const App = () => {
  const [fontReady, setFontReady] = useState(false);
  const loadFonts = async () => {
    await Font.loadAsync({
      Roboto: require("native-base/Fonts/Roboto.ttf"),
      Roboto_medium: require("native-base/Fonts/Roboto_medium.ttf"),
    });
    setFontReady(true);
  }
  useEffect(() => {
   loadFonts();
  }, []);

  if (!fontReady) {
    console.log('Waiting for fonts...');
    return (
      <Expo.AppLoading />
    );
  }

  return (
    <AuthProvider>
      <Navigator />
    </AuthProvider>
  );
};

export default App;

```
### Task A: Convert the app we've made so far to use NativeBase

1. Try to make the app look like these images:

![Login screen](images/login.png)

![Home screen](images/home.png)

![Single screen](images/single.png)


### Task B: Develop profile page

1. Add avatar image to the user
    - Use postman to upload image and add a [tag](http://media.mw.metropolia.fi/wbma/docs/#api-Tag-PostTag) 'avatar_CurrentUserId' to it (e.g avatar_85)
    - When fetching avatars, you can use _CurrentUserId to limit the amount of fetched data.
1. Display users avatar image, name and email in profile page
   - You'll need to use existing or add more methods to 'ApiHooks.js' to achieve this

![Profile screen](images/profile.png)
  
