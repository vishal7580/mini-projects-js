
# 🧠 Why `let i = 0` Outside Loop Doesn't Work (and What Does)

## ❓ Problem

You tried this:

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

It seems like it should work, but it doesn't. All buttons play the same sound — usually the last one.

---

## 💥 Why It Breaks

You're using one shared `i` for all buttons.

- Each `click` handler is remembering the **same variable** (`i`).
- When the loop finishes, `i` has been incremented to the final value.
- Now **all click handlers use that final value**, so all buttons play the last sound.

---

## ✅ The Correct Way

Use the `i` provided by `forEach`:

```js
btns.forEach((button, i) => {
  button.addEventListener('click', () => {
    console.log(i);
    animalSounds[i].play();
  });
});
```

This works because:

- JavaScript gives **each button its own version** of `i`.
- When the click event is created, that `i` is **locked** into memory — this is called a **closure**.

---

## 🧠 What’s a Closure?

A **closure** is when a function “remembers” the variables it had access to when it was created.

Each button's `click` function remembers its own `i`, **not a shared one**.

---

## 📦 Summary

| Your Way (❌) | Problem |
|--------------|---------|
| `let i = 0` outside loop | All buttons **share** this one `i`. After loop finishes, `i` = last value, so all buttons click same sound. |

| Correct Way (✅) | Why it works |
|------------------|--------------|
| `forEach((btn, i) => { ... })` | JS gives each button its own `i`, and remembers it when you attach the `click` event. |

---

### 🎯 TL;DR

- All buttons pointing to the same changing `i` = ❌
- Each button getting its own fixed `i` = ✅
