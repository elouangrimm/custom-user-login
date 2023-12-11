> The code snippets in this post are untested. I did it from memory and probably got stuff wrong.

# Putting data in the cloud

It's remarkably hard to put data up there in the cloud.

## Dream scenario

My dream scenario would be a simple javascript function I can call.

```js
putDataInTheCloud({
  key: "favourite-food",
  value: "pasta",
  password: "my-super-secret-password",
})
```

And to get it back...

```js
getDataFromTheCloud({
  key: "favourite-food",
  password: "my-super-secret-password"
})
```

## Key

The `key` option lets me get back the same value later on. 

## Value

The `value` is what I store up there.

## Password

The `password` is a secret that I've configured on my rented cloud. It means that other people can't use it - just me.

I wouldn't actually pass it over as a string literal. That would mean that other people could view source and steal my password. Instead, there would be a password field in the user interface. To use the program, I would need to type in my password.

```html
<input type="password" />

<script>
const input = document.querySelector("input")

const setFavourite = (food) => {
  putDataInTheCloud({
    key: "favourite-food",
    value: food,
    password: input.value,
  })
}
</script>
```

## Local storage

You can even store the password locally. That way, you don't need to type it in each time.

```html
<input type="password" />

<script>
const input = document.querySelector("input")

const setFavourite = (food) => {
  putDataInTheCloud({
    key: "favourite-food",
    value: food,
    password: input.value,
  })
}
</script>
```

## Local storage

You can even store the password locally. That way, you don't need to type it in each time.

```html
<input type="password" oninput="handleInput()" />

<script>
const input = document.querySelector("input")

input.value = localStorage.getItem("password") ?? ""

const handleInput = () => {
  localStorage.setItem("password", input.value)
}

const setFavourite = (food) => {
  putDataInTheCloud({
    key: "favourite-food",
    value: food,
    password: input.value,
  })
}
</script>
```

## But but cross-site scripting!!

If someone has access to your browser, it's already game over. They could just read the password out of the input as you type it, or log your key presses.

A simple "save password to local storage" toggle would let the user choose.

```html
<input type="password" oninput="handleInput()" id="password" />
<input type="checked" onchange="handleToggle()" id="save" />

<script>
const input = document.querySelector("#password")
const checkbox = document.querySelector("#save")

checkbox.checked = localStorage.getItem("save") ?? false

if (checkbox.checked) {
  input.value = localStorage.getItem("password") ?? ""
}

const handleInput = () => {
  if (checkbox.checked) {
    localStorage.setItem("password", input.value)
  }
}

const handleToggle = () => {
  localStorage.setItem("save", checkbox.checked)

  if (checkbox.checked) {
    localStorage.setItem("password", input.value)
  } else {
    localStorage.removeItem("password")
  }
}

const setFavourite = (food) => {
  putDataInTheCloud({
    key: "favourite-food",
    value: food,
    password: input.value,
  })
}
</script>
```

## Two factor authentication

A better form of security would be two-factor authentication. When you login from a browser that looks different, your cloud server could email you to ask if it's really you. 

## Val town

I reckon all of this is possible on [val.town](https://val.town).

## Rented server

I reckon it's also possible on a server that you rent. For example, I rent a server that sits in a room in Nuremberg. I could use that!

But I reckon it would take a bit more work than val town, so I might try that first.

## Any other ideas?

How else could I do this?

No, I don't want to set up something bulky like supabase. No, I don't want to lock myself into a stack like deno. No, I don't want to use node, or vercel, or anything like that.

Tally of people who suggested these things anyway: 0

<br>

Back to the [wikilocoucvhhbvv](/wikiblogarden).