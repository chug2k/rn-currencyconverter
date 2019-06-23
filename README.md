# Week 2 - **Currency 💵💴💶💷 Converter**

## Introduction 🌟

Let's build a new app 📱 using [React Native](https://facebook.github.io/react-native/) & [Expo](https://expo.io/).  Our app will help users convert currency 💵 from USD 🇺🇲 to VND 🇻🇳 as well as vice versa!

![pwd](./assets/intro.png)

### Features 🎯 🥅🥇🏆

- [ ] User sees instructions advising them what to do
- [ ] User can input data to our application, hint, `TextInput`.
- [ ] User can see a placeholder text in the input indicating an expected value to be entered by the user
- [ ] User can only enter numbers into the input
- [ ] User can see centered text in the input
- [ ] User can see two buttons indicating
  - VND to USD
  - USD to VND
- [ ] User can see a prompt showing the current value they've entered
- [ ] User can see a prompt showing the current value's converted value
- [ ] User can see both values formatted correctly for their regionale
- [ ] User can switch from VND to USD or USD to VND

### Learning Objectives ✍️📚📝 📈🙌 ️

1. Learn more about passing props.

2. Learn how to build our own components which consume props.

3. Learn how to compose our functional components with internal functions.

4. Learn how to [useState()](https://reactjs.org/docs/hooks-state.html) in our applications.

5. Learn that we can listen for user inputs using components such as `TouchableOpacity` and props such as `onPress`.

> **Tip** 💡: As we move forward we'll have smaller and smaller code snippets. We do this to encourage you to think about what the code does and where it is it needs to go.

### **Milestone 1 🛣🏃 Get up and running**

Create a new application using what we learned last week. This knowledge gives us a **sky 🛫🌤️** of possibilities.

**A)**  Use `expo init currencyConvert` to generate a new project. Remember, it contains many folders 📂 and files 📑. Afterwards start the simulator.

![pwd](./assets/1a.png)

**B)** Prompt the user. Update the body of the return with instructions.

```jsx
  return (
    <View style={styles.container}>
      <Text>Please enter the value of the currency you want to convert</Text>
    </View>
  );
```

![pwd](./assets/1b.png)

**C)** Grab a `TextInput` component from React Native so we can get the users desired conversion value.

```jsx
import {
  TextInput,
} from 'react-native'
```

**D)** Nest the `TextInput` inside of the body of the return.

```jsx
<View style={styles.container}>
  <Text>
    Please enter the value of the currency you want to convert
  </Text>
  <TextInput />
</View>
```

![pwd](./assets/1c.png)

#### Different Styles 💋👔⌨

We show you different ways to write the same code so you can be aware of them.

<details>

<summary>Option 1</summary>

```jsx
<View style={styles.container}>
  <Text>Please enter the value of the currency you want to convert</Text>
  <TextInput></TextInput>
</View>
```

</details>

<details>

<summary>Option 2</summary>

```jsx
<View style={styles.container}>
  <Text>Please enter the value of the currency you want to convert</Text>
  <TextInput />
</View>
```

</details>

We nested the `TextInput` inside of the `View` below the `Text`, but we don't see anything. That's because we need to add a **prop** to the `TextInput` component.

**E)** Pass a style 💅 prop.

```jsx
<TextInput
  style={{
    height: 60,
    padding: 5,
    width: 300,
    fontSize: 35,
    borderWidth: 1,
    borderColor: 'lightblue'
  }}
/>
```

![name](./assets/1d.png)

**F)** Now enable your simulator's **Keyboard**. 

![name](./assets/1e.png)

> **Tip** 💡: We need to account for the keyboard in the layout when building for mobile. Failing to do this can be deadly ☠️❗🚫.

**G)** Everythings bunched at the bottom. There's a lot of wasted space at the top. Move everything toward the top by updating the styles at the bottom of the file.

```jsx
const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    marginTop: 50,
    alignItems: 'center',
    backgroundColor: '#fff',
    justifyContent: 'flex-start',
  },
});
```

![name](./assets/1f.png)
Everything starts at the top of the screen now. Nice.

**H)** Since were building a currency converter, it would be appropriate that the user should only be able to enter numbers. Pass the `TextInput` a new prop which makes the keyboard numpad type.

```jsx
<TextInput
  keyboardType="number-pad"
/>
```

![name](./assets/1g.png)

Now we see that the keyboard is a number pad. Excellent.

**I)** Exceptional apps will take anticipatory steps on behalf of users. Focus the `TextInput` when our app loads by adding a new prop.

```jsx
<TextInput
  autoFocus // autoFocus === autoFocus={true}
/>
```

![name](./assets/1h.png)
We should now see the `TextInput` focus immediately. The keyboard should also reveal.

**J)** Center the text in the input so it looks better.

```jsx
<TextInput
  textAlign="center"
/>
```

![name](./assets/1i.png)

**K)** Let's add a `placeholder` **prop** as well to be super explicit to the user on our expectations.

```jsx
<TextInput
  placeholder="100,000,000 VND"
/>
```

![name](./assets/1j.png)

**L)** Choose a custom color for the cursor. Add the prop `selectionColor`.

```jsx
<TextInput
  selectionColor="red"
/>
```

![name](./assets/1k.png)
If your screen looks like this then good work. We indicated to the user what we want. We've also made some sensible decisions in terms of user experience. The `TextInput` component is auto focused, the keyboard is of type `Number`, the placeholder is a value which shows an appropriate input.

---
> Key Points 🔑📝

- There is a `TextInput` component provided for free from React Native.
- There are many different properties we can pass `TextInput`. The properties can be of datatype `String`, `Boolean`, `Object`, and spoiler, `Function`.

---

### **Milestone 2 🛣🏃 Complete layout by creating our own component**

Let's create a component which highlights the **from** and **to** currencies. It will also handle the user choosing between which currencies to convert as well. I advise we create a component because we want to reuse the logic which handles these use cases.

**A)** Import a `TouchableOpacity` component from React Native.

```jsx
import {
  TouchableOpacity,
} from 'react-native'
```

Remember, we get a lot of free components from React Native out the box. This component will handle user events soon.

**B)** Let's go ahead and add some style to the `TouchableOpacity` component.

```jsx
const styles = StyleSheet.create({
  button: {
    height: 35, 
    width: 200, 
    margin: 10,
    borderWidth: 2,
    borderRadius: 20,
    alignItems: 'center',
    borderColor: 'lightblue',
    justifyContent: 'center',
  }
})
```

**C)** Now define the component above the `App` component.

```jsx
const ConversionTypeButton = () => {
  return (
    <TouchableOpacity style={styles.button}>
      <Text>VND to USD</Text>
    </TouchableOpacity>
  )
}
```

**D)** Nest the `ConversionTypeButton` component in the body of our `App` components body.

```jsx
return (
    <View style={styles.container}>
      <ConversionTypeButton />
    </View>
  )
```

![name](./assets/2a.png)
We can see a VND to USD button now. This one will handle VND to USD conversion for the user. Now the power of React is going to shine. Let's use this component again in order to add a USD to VND button.

**E)** Add a second `ConversionTypeButton` for USD to VND

```jsx
return (
    <View style={styles.container}>
      <ConversionTypeButton />
      <ConversionTypeButton />
    </View>
  )
```

![name](./assets/2d.png)
We have two buttons but we have a problem. The buttons say the **exact same thing**.

#### How can we fix this?

We can fix this by applying a concept we learned last week. We can pass props to our component.

**D)** Pass two new props `from` & `to` to our `ConversionTypeButton` component when we nest it in the body of `App`. Contemplate  the value of these properties.

```jsx
return (
  <View style={styles.container}>
    <ConversionTypeButton
      to="usd"
      from="vnd"
    />
    <ConversionTypeButton
      to="vnd"
      from="usd"
    />
  </View>
)
```

Now we've got two props passed to our `ConversionTypeButton`. That isn't enough though we need to take these props and do additional work.

**E)** Refactor `ConversionTypeButton` to behave correctly based on these new props, `to` & `from`.

The result is the component rendering the appropriate flags based on the props sent to it.

```jsx
const ConversionTypeButton = (props) => {
  const fromFlag = props.from === 'usd' ? '🇺🇲' : '🇻🇳'
  const toFlag = props.to === 'usd' ? '🇺🇲' : '🇻🇳'
  return (
    <TouchableOpacity style={styles.button}>
      <Text>{fromFlag} to {toFlag}</Text>
    </TouchableOpacity>
  )
}
```

![name](./assets/2e.png)
We should now see our buttons render with the appropriate flags. Nice.

#### Different Styles 💋👔⌨

Here's a couple different ways we could have refactored `<ConversionTypeButton />`

<details>

<summary>Option 1</summary>

```jsx
const ConversionTypeButton = ({ from, to }) => {
  const fromFlag = from === 'usd' ? '🇺🇲' : '🇻🇳'
  const toFlag = to === 'usd' ? '🇺🇲' : '🇻🇳'
  return (
    <TouchableOpacity style={styles.button}>
      <Text>{fromFlag} to {toFlag}</Text>
    </TouchableOpacity>
  )
}
```

</details>

<details>

<summary>Option 2</summary>

```jsx
const ConversionTypeButton = ({ from, to }) => {
  let toFlag
  let fromFlag

  if (from === 'usd') {
    toFlag = '🇻🇳'
    fromFlag = '🇺🇲'
  } else {
    toFlag = '🇺🇲'
    fromFlag = '🇻🇳'
  }

  return (
    <TouchableOpacity style={styles.button}>
      <Text>{fromFlag} to {toFlag}</Text>
    </TouchableOpacity>
  )
}
```

</details>

**F)** Add the two prompts and values below what we have so far.

We need to help the user understand what the input and conversion values are as well as which is which. This is how they'll know which number represents which value, `from` or `to`.

1. First lets add a new style to the bottom.

```jsx
const styles = StyleSheet.create({
  currencyText: {
    fontSize: 30,
    color: 'green',
    fontWeight: 'bold'
  }
})

```

2. Now let's add some components & styles of the correct composition to the body of the return from `App`.

```jsx
return (
  <View>
    <Text>
      Current currency:
    </Text>
    <Text style={styles.currencyText}>
      0.00
    </Text>
    <Text>
      Conversion currenecy:
    </Text>
    <Text style={styles.currencyText}>
      0.00
    </Text>
  </View>
)
```

![name](./assets/2f.png)

We should see the two prompts above the two `from` & `to` now.

---
> Key Points 🔑📝

- `TextInput` & `TouchableOpacity` aree components provided for free. We will use them often. `TextInput` & `TouchableOpacity` take a `style` prop like most components we'll use.

- Creating components help us reuse logic. Consider the `ConversionTypeButton` component we created.

- We can pass our components props like we did for `TextInput` & `TouchableOpacity`. Consider the `from` and `to` props we passed to `ConversionTypeButton`.

- The props given to a component determine how the components will behave. Contemplate how `ConversionTypeButton` shows different flags becaused of the different props.

---

### **Milestone 3 🛣🏃 Add statefulness to our application to implement behavior**

One of the most important concepts in React is state. There have been many ways to handle state developed over the years. We'll use [hooks](https://reactjs.org/docs/hooks-intro.html) in our class.

State will allow us to encapsulate logic into our applications from whether or not a user is signed in, if we have movies to show, or what currency a user wants to convert `from` & `to`.

State can represent anything we can imagine.

**A)** Add a new piece of state to the app, `currentCurrencyValue`.

1. Grab two new dependencies from React, `useState` & `useEffect`. These two functions are introduced to handle state.

```jsx
import React, { useState, useEffect } from 'react'
```

2. Use state in the body of the `App` component's definition. Call the function `useState` with an argument of `0`.

    - The return value of this function call is an array.
    - We need the first two items in the array, `currentCurrencyValue` & `setFromCurrencyValue`.
    - The `0` is the initial value of `currentCurrencyValue`.
    - `setFromCurrencyValue` is how we'll update the variable.

#### This is how we'll get access state in our app. We define the name of the `variable`, the `initial value`, and the `setter` method in one line. This all comes from a function call to `useState`

```jsx
const [currentCurrencyValue, setFromCurrencyValue] = useState(0)
```

3. Add the `currentCurrencyValue` variable we just got from the `useState` function call to our return.

```jsx
<Text style={styles.currencyText}>
  {currentCurrencyValue}
</Text>
```

![name](./assets/3a.png)

You should now see a `0` underneath 'Current currency'

**B)** Implement current currency updating.


Pass as a new property to our `TextInput` component. The value is the second index value from the array we get from `useState`.

```jsx
<TextInput
  onChangeText={setFromCurrencyValue}
>
```

![name](./assets/3b.png)

We should now see that the current currency value follows that of the `TextInput`.

**C)** We need to do the same thing for the converted currencies value. Follow the same steps to have access to a new piece of state. We'll call this variable `convertedCurrencyValue`.

```jsx
const [convertedCurrencyValue, setConvertedValue] = useState(0)
```

```jsx
<Text style={styles.currencyText}>
  {convertedCurrencyValue}
</Text>
```

![name](./assets/3c.png)
We should now see a `0` underneath 'Convesion Currency'. However, if you look closely, when the user enters 100,000 VND, the converted currency value does not change.

**D)** Implement converted currency behaving as expected from VND to USD.

1. Define a new function, `convertCurrency`, in the body of our `App` component.

This function will look at the state of our app, specifically the 
`currentCurrencyValue` value, then decide by 23000. This is the calculation to convert from VND to USD.

```jsx
const convertCurrency = () => {
  setConvertedValue(currentCurrencyValue / 23000)
}
```

2. Use the `useEffect` hook provided by React in `App`'s body as well. Pass it the function we want to run on state change, the one we just defined, `convertCurrency`.

```jsx
useEffect(convertCurrency)
```

![name](./assets/3d.png)

We should now see that the current and conversion values change.

---
> Key Points 🔑📝

- We will represent real world concepts in our apps using `state`.
- We can access state in React via a call to the function `useState`.
- The argument to `useState`'s call is the initial value of the variable.
- The return value of `useState` is an array. The first index of the array is the variable we get, the second is the `setter` function.

---

### **Milestone 4 🛣🏃 Implement final touches**
Our app works alright... But I think we could add some polishing touches.

**A)** Add two new pieces of state, `toCurrency` & `fromCurrency`. These values will represent which currencies the user wants to exchange `from` & `to` respectively.

```jsx
const [toCurrency, setToCurrency] = useState('usd')
const [fromCurrency, setFromCurrency] = useState('vnd')
```

**B)** Define a new function which will handle the user changing the conversion they want to make.

```jsx
const setConversionCurrencies = (from, to) => {
  setFromCurrency(from)
  setToCurrency(to)
}
```

**C)** Pass these values to our `ConversionTypeButton` component as props.

```jsx
<ConversionTypeButton
  toCurrency={toCurrency}
  fromCurrency={fromCurrency}
  setConversionCurrencies={setConversionCurrencies}
/>
```

**D)** Refactor our `ConversionTypeButton` component. Implement it to look at the `fromCurrency` and `toCurrency` props passed to it and to behave accordingly.

1. Style button based on comparsions of it's `to` & `from` props to it's `fromCurrency` and `toCurrency` props. This will result in th button having a blue background is that conversion it the current state of the application.

2. Pass the style, `buttonStyle`, as the second element in an array passed to the `style` prop of `TouchableOpacity`.

3. Forward the `setConversionCurrencies` prop we sent to `ConversionTypeButton` as a prop to it's `onPress`. This will allow to use to change which conversion they want to make.

```jsx
const ConversionTypeButton = (props) => {
  const backgroundColor = props.fromCurrency === props.from && props.toCurrency === props.to ? 'lightblue' : null
  const buttonStyle = { backgroundColor: backgroundColor  }

  const fromFlag = props.from === 'usd' ? '🇺🇸' : '🇻🇳'
  const toFlag = props.to === 'usd' ? '🇺🇸' : '🇻🇳'

  return (
    <TouchableOpacity
      style={[styles.button, buttonStyle]}
      onPress={() => props.setConversionCurrencies(props.from, props.to)}
    >
      <Text style={styles.buttonText}>{fromFlag} to {toFlag}</Text>
    </TouchableOpacity>
  )
}
```

#### Different Styles 💋👔⌨

We show you different ways to write the same code so you can be aware of them.

<details>

<summary>Option 1</summary>

```jsx
const ConversionTypeButton = ({ fromCurrency, toCurrency, from, to, setConversionCurrencies}) => {
  const backgroundColor = fromCurrency === from && toCurrency === to ? 'lightblue' : null
  const buttonStyle = { backgroundColor: backgroundColor  }

  const fromFlag = from === 'usd' ? '🇺🇸' : '🇻🇳'
  const toFlag = to === 'usd' ? '🇺🇸' : '🇻🇳'

  return (
    <TouchableOpacity
      style={[styles.button, buttonStyle]}
      onPress={() => setConversionCurrencies(from, to)}
    >
      <Text style={styles.buttonText}>{fromFlag} to {toFlag}</Text>
    </TouchableOpacity>
  )
}
```

</details>

<details>

<summary>Option 2</summary>

```jsx
const ConversionTypeButton = ({
  to,
  from,
  toCurrency,
  fromCurrency,
  setConversionCurrencies,
}) => {
  const isSelectedConversionType = fromCurrency === from && toCurrency === to
  const backgroundColor = isSelectedConversionType ? 'lightblue' : null
  const buttonStyle = { backgroundColor: backgroundColor  }

  const fromFlag = from === 'usd' ? '🇺🇸' : '🇻🇳'
  const toFlag = to === 'usd' ? '🇺🇸' : '🇻🇳'

  return (
    <TouchableOpacity
      style={[styles.button, buttonStyle]}
      onPress={() => setConversionCurrencies(from, to)}
    >
      <Text style={styles.buttonText}>{fromFlag} to {toFlag}</Text>
    </TouchableOpacity>
  )
}
```

</details>

**E)** Refactor our `convertCurrency` function to behave according to the current state of the applications `fromCurrency` value. If the `fromCurrency` is vnd we divide by 23,000, if not, we multiply by 23,000. Computer Science!

Afterwards, we call the function we got for free `setConvertedValue` with the argument of thee new converted currenciees value.

```jsx
const convertCurrency = () => {
  let value
  if (fromCurrency === 'vnd') {
    value = currentCurrencyValue / 23000
  } else {
    value =  23000 * currentCurrencyValue
  }
  setConvertedValue(value)
}
```

![name](./assets/4e.gif)