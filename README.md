# Build a Responsive Nav using mainly JavaScript!

With a better understanding of JavaScript, I decided play around and see if I could create
a nav with the bare minimum of HTML and CSS.  I inadvertantly learned even more in this process, 
which is another thing I was hoping to accomplish.
<br>
<br>
Not only is the Nav bar responsive, but you can also add/remove Nav items simply altering the parameters
in the `createNav()` function.  This saves time having to type out each Nav item in the html, and then style them in the css.
<br>
<br>
One point of functionality I will add soon is the ability to truncate the Nav item overflow into a nested Nav list.
<br>
<br>
So let's get to the code now!
<br>

---

### HTML:

<br>
You'll want to start with the normal boilerplate html.
<br>

Then within the `<body>` tags add a `<header>`. <br>
<br>
Now with flexbox, I always add containers around the things I want to position.<br>
So add a `<div>` with a class of "navContainer".<br>
Then inside the `<div>` add a `<nav>` with a class of.... you guess it, nav! ^-^<br>
And then finally, withint the `<nav>` you'll need a single `<ul>` with a class of "navList".
<br>
<br>
The final code looks like :
<br>
<br>
```html
    <header>
      <div class="navContainer">
        <nav class="nav">
          <ul class="navList"></ul>
        </nav>
      </div>
    </header>
    
```
<br>

Then don't forget to link your JS file `<script src="./app.js"></script>` to your html right before your `</body>` tag.

<br>

#### And that's all the HTML you need for this!

---

### CSS:

I decided to keep some of the styling in the CSS so that it can be changed easily to suit whomever's preference, but the majority of the sizing and fixed styling is declared in the JS so each Nav item is uniform.
<br>
<br>

I'll simply post the code here, but if you have any questions on CSS styling feel free to DM me on [Twitter](https://twitter.com/stacksantos)!

```css

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
header {
    width: 100%;
    height: 5rem;
    background-color: black;
}
.navContainer {
    display: flex;
    justify-content: center;
}
.navItems {
    color: white;
    font-size: 1.5rem;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    text-transform: uppercase;
    background-color: black;
}

```

If you haven't noticed, there's a `.navItems` class in the CSS.  "But that's weird, why isn't there one in the HTML?", you might ask.
<br>
<br>
**That's because we build the "Nav items" in the JS!**  Which is pretty cool if I do say so myself.
<br>
<br>
So now that the CSS is out of the way, we can get to the good stuff!

---

### JavaScript:

<br>

Alright, so the first thing we'll want to do is name our function.... this one took me a couple weeks to do but eventually I settled on `createNav` (makes sense right?).

<br>
<br>

Inside the function we'll need to pass it 3 different arguments.<br>
These are `(param, array, links)` .

<br>

The start of the function looks a little like this: <br>

` const createNav = (param, array, links) => { ` .

<br>
<br>

That's the only function we're going to use, so we might as well "call" it at the bottom, then fill in the function so we can see what's happening as we code it.<br>
The code will look like this at first: <br>
<br>

```javascript
const createNav = (param, array, links) => {

};

createNav("insert param", "insert array", "insert links");
```

<br>
I'll explain what you'll be passing into the function real soon. For now lets get started on filling out the function.
<br>
<br>

The first thing I did was grab the `.navList` which is the `ul` 's class and stick it in a variable right after the opening of the function `{`.

<br>

```javascript
const navList = document.querySelector(".navList");
```

<br>
<br>

### Then... I made it flex. 

<br>
<br>

![flex](https://user-images.githubusercontent.com/100369086/175751551-77ea4b03-3ff2-4f44-8e3b-62a907e6d32e.gif)

<br>
Simply grab the "navList", then target it's display which is under 'style'<br> (similar to if you were using inline styles in your html)<br> and set it to = "flex".
<br>
<br>

The code:<br>
<br>

```javascript 
navList.style.display = "flex";
``` 
(don't forget your semicolons!)

<br>
<br>
Moving on to the fun stuff.  Now we'll start creating, assigning, and styling each link all within ONE 'for' loop.<br> It's like a little link factory pumping out however many you need for your Nav!

<br>
<br>

Here's where `param` comes into play.  Because param can be anything, and we'll be passing in a number there, we can use it in the 'for' loop to tell it how many times to run!

<br>
<br>

The start of the code looks like this:<br>
<br>

```javascript 
for (let i = 0; i < param; i++) { 
```

Now that we've got our factory running, lets give it something to make.
<br>
<br>
We'll first start pumping out some anchor links `<a>`.  So define a variable and set it to create an element. Tell it to create "a".
<br>

```javascript
const navLink = document.createElement("a");
```

<br>

Then your anchor links will need something to hook to so next we have to define their urls.<br>
This is where the `links` argument comes into play that we fed into our function earlier. And we'll also want them to open under a different tab as well.

<br>
<br>
The code:
<br>

```javascript
navLink.href = `${links[i]}`;
navLink.target = "_blank";
```
We use a template literal to target `links` and also target which "iteration" `[i]` (the navLink) is being made this time. We also target the ....target, and set it to `"_blank";` so the link opens up in a new tab.

<br>
<br>

Now we need to create the `<li>` inside of the `<a>`.  The process is the same as before.  Define your variable and tell it what to create.

<br>
<br>
The code:
<br>

```javascript
const navItem = document.createElement("li");
```

<br>
For future styling purposes you'll want to give them a class, individual Id's, and also what their text displays. That's where the `array` argument comes into play now.
<br>
<br>
The code:
<br>

```javascript
navItem.classList.add("navItems");
navItem.id = array[i];
navItem.innerHTML = array[i];
```

<br>

The `array[i]` will take the text of each respective Nav item and add it to their Id's and display text each time they are made.

<br>

### And with that we have defined all of our arguments!


Now we can finish off styling them and putting them together!
<br>
Like I mentioned earlier, this can also be done in CSS, but I wanted them to be out of the way so there's less code to write.  Of course you can always just delete these and stick them in the CSS if that's your preference.  Or you can modify them in the JS instead.  It's completely up to you!
<br>
<br>
I'm just going to post the code because I've explained how to style things earlier (if you were actually reading!):
<br>

```javascript
navItem.style.listStyle = "none";
navItem.style.marginLeft = "1rem";
navLink.style.textDecoration = "none";
navLink.style.cursor = "pointer";
navLink.style.padding = "1.5rem";
```
<br>
<br>
Now all that's left is to nest them properly!  The navLinks are nested under the navList, and the navItems are nested inside of the navLinks.
<br>
<br>

The code:
<br>

```javascript
navList.append(navLink);
navLink.append(navItem);
```
<br>

Then close the function off
<br>

```javascript
  }
};
```

### AND YOU'RE DONE!

## Almost...

<br>

You have to call the function otherwise it won't work!<br>
And inside you'll want to pass in your arguments which hold the parameters you want to pass through.<br>
<br>
**With that information the factory can run and start pumping out Nav items to your hearts content!**
<br>
<br>
The syntax is pretty simple.  First tell it how many Nav items you want (param). Use a number...or it won't work.
<br>
Then give the array an array of the names of each Nav item.
<br>
Then also give it an array of the links to those Nav items.
<br>
<br>
**Make sure everything is in order though or your users will get lost!**<br>
<br>
<br>
Here's an example:

```javascript
createNav(
  3,
  ["Instagram", "Facebook", "Twitter"],
  ["https://instagram.com", "https:facebook.com", "https://twitter.com"]
);
```
<br>

If you change the number and don't put the required number of names and links, it will return undefined but not break. Go ahead and try it out!
<br>
<br>
The full function is here:
<br>

```javascript
const createNav = (param, array, links) => {

  const navList = document.querySelector(".navList");

  navList.style.display = "flex";

  for (let i = 0; i < param; i++) {

    const navLink = document.createElement("a");

    navLink.href = `${links[i]}`;
    navLink.target = "_blank";

    const navItem = document.createElement("li");

    navItem.classList.add("navItems");
    navItem.id = array[i];

    navItem.innerHTML = array[i];

    navItem.style.listStyle = "none";
    navItem.style.marginLeft = "1rem";
    navLink.style.textDecoration = "none";
    navLink.style.cursor = "pointer";
    navLink.style.padding = "1.5rem";

    navList.append(navLink);
    navLink.append(navItem);
  }
};


createNav(
  3,
  ["Instagram", "Facebook", "Twitter"],
  ["https://instagram.com", "https:facebook.com", "https://twitter.com"]
);
```
<br>
And NOW we're done.  With that you have a convoluted way of building out a Nav if ever you decided it was something you just HAD to do...<br>
Truth be told I only did it this way to see if I could.  And I can... and also now you can.
<br>
<br>

## HAPPY HACKING!
