 #**What's a Closure?**
## In JavaScript, a closure just means:

### A function remembers the variables it saw when it was created — even after those variables are outside its scope.

### Like, imagine if a button remembers a snapshot of a variable it saw when it was born.

 ```js
 let i = 0;

    btns.forEach((button) => {
    button.addEventListener('click', () => {
        console.log(i);
        animalSounds[i].play();
    });
    i++;
    });
```

# You are saying:

### “Make all the buttons remember this i — and I’ll just keep changing it.”

#### So all the buttons are looking at the same i. But since you keep increasing it (i++), by the time you're done looping, i is, say, 5. Now every button remembers i, which is 5. That’s why all buttons play the same last sound.

```js

btns.forEach((button, i) => {
  button.addEventListener('click', () => {
    animalSounds[i].play(); // now each one uses the correct i
  });
});
```

##### Here, i is given fresh for every button — each button gets a new mini copy of i, and it locks it into memory when the click function is created.

#### So button 1 remembers i = 0,button 2 remembers i = 1,and so on.

#### They don’t share anything. Each click knows its own correct index.


| Your Way (❌)Problem  | Correct Way (✅) Why it works 
| -----------------------|------------------------- | 
| `let i = 0` outside loop All buttons **share** this one `i`. After loop finishes, `i` = last value, so all buttons click same sound. | `forEach((btn, i) => { ... })` JS gives each button its own `i`, and remembers it when you attach the `click` event. |
