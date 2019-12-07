---
description: A backyard made with loads of CSS.
---

# Ming's Backyard: A teaching material for Girls Who Code Club, Millbrae \(Dec. 7\)

[Ming's Backyard](https://codepen.io/tslmy/pen/yLLWXgE)

A backyard made with loads of CSS.

I don't actually have a backyard in real life.

:\(

_Disclaimer: I did not create most of the images that are used in this session. Although the images may be subject to copyright, since I am using and distributing the images for teaching, my usage of these images may qualify as a fair use. Do not use whatever images you find on the Internet -- you might infringe someone else's rights._

## Welcome to my backyard!

It's a bit basic for now...

```markup
<sky>
</sky>
<ground>
</ground>
```

### Big things I have in my backyard

I have a `barn`, a `garden`, and a `picnic table` in my backyard. They are placed **on the ground**, rather than _in the sky_:

```markup
<sky>
</sky>
<ground>

  <barn>
  </barn>

  <garden>
  </garden>

  <picnic-table>
  </picnic-table>

</ground>
```

### Some touch-ups

There's a `fence` in my garden, and there's `grass` growing on the ground:

```markup
<sky>
</sky>
<ground>

  <barn>
  </barn>

  <garden>
    <fence></fence> <!-- -->
  </garden>

  <picnic-table>
  </picnic-table>

  <grass></grass> <!-- -->

</ground>
```

## Add more things

I have lots of interesting things I want to put in my backyard. They are:

| Picture | Name | What is this? |
| :--- | :--- | :--- |
| ![](https://i.pinimg.com/originals/7a/57/d8/7a57d80a5f120fe10f55e176c7be4687.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://library.transylvaniacounty.org/wp-content/uploads/2016/12/harry-potter-on-broom-clipart.png) | _Potter_ | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](http://www.pngall.com/wp-content/uploads/2017/01/Fog-PNG.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](http://www.pngpix.com/wp-content/uploads/2016/10/PNGPIX-COM-Cloud-PNG-Transparent-Image.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://i.pinimg.com/originals/00/bf/7f/00bf7f101f82f08c2fb3cd150714019a.gif) | _Jose_ | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](http://www.republicbike.com/images/republic_gbike_angle.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://ph-files.imgix.net/229aeee9-ad6c-4bfd-ba94-cc3db9ebd7a0?auto=format) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://i.pinimg.com/originals/3f/18/80/3f1880697a9910f7b61ab0f9e06d019c.gif) | _Sausage_ | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://img.itch.zone/aW1nLzc3NjkzNC5naWY=/original/OXf8zn.gif) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](http://www.pngpix.com/wp-content/uploads/2016/11/PNGPIX-COM-Fruit-Basket-PNG-Transparent-Image-500x416.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://www.childrens-museum.org/media/uploads/teddybear2.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |
| ![](https://data2.polantis.com/image1000/data/562/26287/Cutout%20Tree%2034_3D_p.png) |  | wizard, cloud, airplane, food, toy, pet, bike, horse, tree |

Put in a less exciting format: [here](https://gist.github.com/tslmy/c6ca6b163166b066095add427693ce59).

I only named **3** of them!

> _A recap:_
>
> $1+1+1=3$

### Do I have space to put them?

Find some place where I can put these things!

* In the **sky**?
* On the **table**?
* On the **ground**?
* In the **barn**?
* In the **garden**?

### Where should I put each type of things?

Complete the association!

| Type | Where to put this type of things? |
| :--- | :--- |
| 🧙 wizard | sky, table, ground, barn, garden |
| ☁️ cloud | sky, table, ground, barn, garden |
| ✈️ airplane | sky, table, ground, barn, garden |
| 🍲 food | sky, table, ground, barn, garden |
| 🧸 toy | sky, table, ground, barn, garden |
| 🐕 pet | sky, table, ground, barn, garden |
| 🚲 bike | sky, table, ground, barn, garden |
| 🐎 horse | sky, table, ground, barn, garden |
| 🌳 tree | sky, table, ground, barn, garden |

CLICK ME let map = { wizard: "sky", cloud: "sky", airplane: "sky", food: "picnic-table", toy: "picnic-table", pet: "ground", bike: "ground", horse: "barn", tree: "garden" };

#### Notice that you can have **repeating values on the right** side of the colons, but **not on the left** side!

A dictionary may tell you:

> * "`Splendid`" means "good".
> * "`Marvelous`" means "good".
> * "`Devastating`" means "bad".

However, it makes no for a dictionary to say:

> * "`Splendid`" means "good".
> * "`Splendid`" means "good". **\(I know that already!\)**
> * "`Devastating`" means "bad".

Or, worse:

> * "`Splendid`" means "good".
> * "`Splendid`" means "bad". **\(Which one???\)**
> * "`Devastating`" means "bad".

### Now let's actually put the things to where they belong!

```javascript
// For each thing in `things`... oh wait, instead of "thing", let's call each "thing" "info" (for "information").
things.forEach(info => {

  // `info` has a `type` attribute that is something like "food", "toy", ...
  // "Let type be info's type."
  let type = info.type;

  // Consult our `map` about which location I should put this type of things to.
  // "Let location be whatever map points this type to."
  let location = map[type];

  // Use a tool called "jQuery" (What else tech stuff is capitalized on the second letter?) to locate the container inside that location.
  // "Let space be the container element at that location."
  let space = $(location + " > container");

  // Create an image element.
  // "Let thing be a new image element created on the HTML document's root."
  let thing = document.createElement("img");
  // Tell the image element to load this particular image.
  thing.src = info.image;
  // Tell the image element to draw ("render") the image at this particular width given.
  thing.width = info.size;
  // Actually put this element there.
  space.append(thing);
});
```

## Quiet!

There's too much going on in my backyard :weary:

I want to remove everything that makes a noise!

2 questions:

1. **What makes noise?** wizard, cloud, airplane, food, toy, pet, bike, horse, tree. Let's call them `noisyTypes`:

   ```javascript
   let noisyTypes = ['', '', ''];
   ```

2. **How to make them disappear?** There's many ways to do that:
   1. **Remove these things** from the `things` list.
   2. Before adding them to my backyard \(`things.forEach(info => {`\), **filter out things** whose `type` is in `noisyTypes`.

      ```javascript
      let quietThings = things.filter(info => {return noisyTypes.contains(info.type);});
      ```

      Let's see if the result makes sense:

      ```javascript
      console.log(quietThings);
      ```

      \(Alternatively, we can do: `quietThings.map(info => {return info.type;}).join(', ')`.\)

## Line up by height!

Small-&gt;large:

```javascript
let sortedThings = things.sort((a,b)=>{return a.size-b.size;});
```

Large-&gt;small:

```javascript
b.size-a.size
```

