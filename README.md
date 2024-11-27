Creating a simple booking app in React Native involves several components, including screens for booking details, a list of available options, and a simple navigation setup. Below is a basic example of how such an app could be structured.

### Step 1: Set Up Your React Native Project
If you haven't already set up a React Native project, you can do so using the following command:

```npx react-native init BookingApp
cd BookingApp
```
### Step 2: Install Necessary Packages
You may need to install React Navigation for handling navigation between screens:

```
npm install @react-navigation/native @react-navigation/native-stack
```
You'll also need to install the necessary dependencies:

```
npm install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```
### Step 3: Basic Project Structure
Here’s a simplified version of a booking app:

#### 1. App.js
This file sets up navigation for the app:

```
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import BookingList from './screens/BookingList';
import BookingDetails from './screens/BookingDetails';

const Stack = createNativeStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="BookingList">
        <Stack.Screen name="BookingList" component={BookingList} />
        <Stack.Screen name="BookingDetails" component={BookingDetails} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
```
#### 2. screens/BookingList.js
This screen displays a list of available bookings:

```
import React from 'react';
import { View, Text, Button, FlatList, StyleSheet } from 'react-native';

const bookings = [
  { id: '1', name: 'Booking A' },
  { id: '2', name: 'Booking B' },
  { id: '3', name: 'Booking C' },
];

const BookingList = ({ navigation }) => {
  return (
    <View style={styles.container}>
      <FlatList
        data={bookings}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <View style={styles.card}>
            <Text>{item.name}</Text>
            <Button
              title="View Details"
              onPress={() => navigation.navigate('BookingDetails', { bookingId: item.id })}
            />
          </View>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff',
  },
  card: {
    padding: 15,
    marginVertical: 10,
    backgroundColor: '#f9f9f9',
    borderRadius: 5,
    elevation: 2,
  },
});

export default BookingList;
```
#### 3. screens/BookingDetails.js
This screen shows the details of a selected booking:

```
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

const BookingDetails = ({ route, navigation }) => {
  const { bookingId } = route.params;

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Booking Details</Text>
      <Text>Details for booking ID: {bookingId}</Text>
      <Button title="Back to List" onPress={() => navigation.goBack()} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#fff',
  },
  title: {
    fontSize: 24,
    marginBottom: 20,
  },
});

export default BookingDetails;
```
### Step 4: Running Your App
After setting up the files, you can run your app with:

```
npx react-native run-android
```
or
```
npx react-native run-ios
```
