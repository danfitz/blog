---
layout: post
title:  "My Guide to Writing Good, Clean Code"
author: dan
categories: [coding thoughts]
tags: [clean code, code organization, organization, opinion, writing, coding]
image: "https://images.unsplash.com/photo-1517694712202-14dd9538aa97?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=750&q=80"
description: "This blog post serves to clarify for myself (and future me) all the things I'd like to live up to when writing code in any programming language."
featured: true
toc: true
---

I feel like one of the most valuable parts of personal blogging is that it serves as a kind of verbal time capsule of my thoughts in the same way that a photo album is a visual time capsule of my experiences.

With that in mind, this blog post serves to clarify for myself (and future me) all the things I'd like to live up to when writing code in any programming language.

This blog post is an **evolving** guide because I'm sure that my ideas about good, clean code will change as I grow as a developer. I'm still very young in this field!

## Universalize commonalities

This is a principle that I've found very useful in CSS, but I'm sure there are other areas like [object classes](https://en.wikipedia.org/wiki/Class_(computer_programming)) where the principle is useful. The idea is simple: things that share properties should be bundled together or **universalized**.

Code without universalization:

```css
h1 {
    font-weight: 300;
    color: red;
}
h2 {
    font-weight: 300;
    color: blue;
}
```

Code with universalization:

```css
h1, h2 { font-weight: 300; }
h1 { color: red; }
h2 { color: blue; }
```

In the above code blocks, `h1` and `h2` share the property `font-weight: 300;`. However, the first code block writes the property twice. Instead of writing twice and doubling your work, you can write the second code block that applies the property for both `h1` and `h2` at the same time.

### Why does universalization matter?

Universalizing your code* matters on a practical level because it **saves time when changes need to be made**.

Suppose you're building a website for a client, and they want to make all the headings bolder. Without universalization, you have to go to every heading with `font-weight: 300;` and change it to `font-weight: 400;`. With CSS files that might span 1000s of lines of code, that's a huge headache.

With code universalization, making the change for a client can be a simple toggle.

```css
h1, h2 { font-weight: 400; } /* Increased from 300 */
```

On a deeper level though, code universalization matters because it helps you develop a sense of conceptual organization, which is the next principle I'll be talking about.

**A lot of developers probably already know the idea of [DRY (Don't Repeat Yourself) code](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). This is it but framed differently.*

## Organize by distinct concepts

Many applications can be broken up into distinct concepts. For example, a personal website can have an about section, a contact section, and a blog section.

When I'm writing code, my goal is to try to break up my code into chunks, each chunk representing one of these distinct concepts.

Code without distinctions:

```css
.profile-pic { border: 1px solid blue; }
.email-form { background-color: red; }
.post { background-color: black; }
```

Code with distinctions:

```css
/* ABOUT SECTION */
.profile-pic { border: 1px solid blue; }

/* CONTACT SECTION */
.email-form { background-color: red; }

/* BLOG SECTION */
.post { background-color: black; }
```

The change here comes down to breaking one chunk of code into three chunks of code. Each chunk is for CSS pertinent to each section of the website: about, contact, and blog. 

### Why do distinctions matter?

Breaking down and organizing your code by distinct concepts matters, at least in part, because it's a **memory trick**.

Suppose I gave you the phone number 1603892063. Now suppose I give to you as 160-389-2063. For most people, the second number is going to be much easier to remember.

That's because when it comes to overwhelming groups of things, our ability to understand and recall what's going on will start to break down. (That's the entire basis of the need for calendars, productivity apps, etc.)

Similarly, if we walk into one giant mass of code—maybe it's something we wrote 3 months ago—we won't even know where to begin.

Organizing code by distinct concepts packages our code for us in ways that makes it easier for us to understand. With that in mind, let's move on to the last principle: modularization.

## Modularize (or think atomic)

Modularization is basically the process of organizing your code into its atomic parts and building things by combining those atomic parts as if they were LEGO pieces. As an analogy, think of a chair. In a factory setting, workers start by creating or obtaining the legs, the screws, the seat, and the back support. Then they combine those parts together to create the final product.

Suppose that I want a button on my application that, when pressed, disappears and displays an image in its place.

Code without modularization:

```js
const buttonPress = $("button").on("click", function() {
    $("button").css({"display": "none"});
    $("img").css({"display": "block"});
});
```

Code with modularization:

```js
const elementDisappear = function(element) {
    $(element).css({"display": "none"});
}
const elementAppear = function(element) {
    $(element).css({"display": "block"});
}

const buttonPress = $("button").on("click", function() {
    elementDisappear("button");
    elementAppear("img");
})
```

The difference between these two blocks of code is that the first treats the event as one atomic action: when the button is pressed, make the button disappear and make an image appear. In contrast, the second code block thinks of the button disappearing on the one hand and the image appearing on the other as two atomic actions.

### Why does modularization matter?

At first glance, the modularized code block looks worse because it's longer. However, the value comes down to **reuse**.

What if, as I'm building out my application, I realize that I need a lot of other things to disappear or appear? By creating an atomic action for `elementDisappear` and `elementAppear`, I've made it possible to reuse the code over and over again instead of having to rewrite it for every use.

On top of that, modularization has the same benefit as organizing code by distinct concepts: **manageability**.

When you're building an application that needs to do 1000 things, thinking about all 1000 things can feel overwhelming. But if you break it down into one thing at a time—the absolute smallest or atomic thing you can think of—the task of building out your application feels more manageable. In other words, modularization helps you see 1000 things as 1 thing + 1 thing + 1 thing + 1 thing...

## Summary

All of these principles matter at the end of the day because **they protect you against the unwieldiness of code as it grows and grows** into 1,000s or 10,000s or 100,000s of lines.

They're tricks and heuristics to **organize**. Without organization, at least for me, I could never wrap my head around everything I'm writing. I *need* organization, especially in a task like coding that gets very big very fast.