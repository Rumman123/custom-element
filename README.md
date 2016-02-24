# custom-element

The basic Idea is if you have to  create an element that perform the same role and same set of properties throught the web.Like we have video tag simply you add an tag into your html and it present you whole video controls and its UI.A lot of element desribe their own function.

So,let better understand it with a example like you have to add a css customized loader to around 5-10 what you do you simply insert its html to every respective  page.If I give you a suggestion that make loader a tag and wherever you want to use the loader simply give its tag name and loader appears there.You surely think that I am mocking you and if not you think how can I acheive this.

To acheive this we have to make a custom element of loader and we can use it wherever we want.The document.registerElement() method is used to create a custom HTML element.Like we are here creating a loader and embedding into web page

```javascript
var loader = document.registerElement('x-loader');
document.body.appendChild(new loader());
```
This would add a tag to our HTML page

`<x-loader></x-loader>`

####Naming Rules
`you have to give atleast - between the name if you use _ or any other sign it will result in an error.`

Here we add an custom element it was doing nothing but just residing in html page.So,In order to add features to a custom element, you first need to create a basic prototype object by calling Object.create() with HTMLElement.prototype as an argument. This gives you an empty prototype object with the basic HTML element feature set in its prototype chain. Add any functions and properties you want to the prototype object, then pass your prototype to document.registerElement as shown below:

```javascript
var createProto=Object.create(HTMLElement.prototype);
var loader=document.registerElement('x-loader',{
prototype:createProto})
var dom=new loader();
document.body.appendChild(dom);
```
After adding this code our tag can inherit HTML functionalities however we are here to create an loader So.to do this we have to create HTML & CSS of loader and embed it in template tag with an id.

`<template id="template">`
    `<style>`
       

        .container {
            height: 100vh;
            width: 100vw;
            font-family: Helvetica;
        }
        .loader {
            height: 20px;
            width: 250px;
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            margin: auto;
        }
         
        .loader--dot {
            animation-name: loader;
            animation-timing-function: ease-in-out;
            animation-duration: 3s;
            animation-iteration-count: infinite;
            height: 20px;
            width: 20px;
            border-radius: 100%;
            background-color: black;
            position: absolute;
            border: 2px solid white;
        }
        .loader--dot:first-child {
            background-color: #8cc759;
            animation-delay: 0.5s;
        }
        .loader--dot:nth-child(2) {
            background-color: #8c6daf;
            animation-delay: 0.4s;
        }
        .loader--dot:nth-child(3) {
            background-color: #ef5d74;
            animation-delay: 0.3s;
        }
        .loader--dot:nth-child(4) {
            background-color: #f9a74b;
            animation-delay: 0.2s;
        }
        .loader--dot:nth-child(5) {
            background-color: #60beeb;
            animation-delay: 0.1s;
        }
        .loader--dot:nth-child(6) {
            background-color: #fbef5a;
            animation-delay: 0s;
        }
        .loader--text {
            position: absolute;
            top: 200%;
            left: 0;
            right: 0;
            width: 4rem;
            margin: auto;
        }
        .loader--text:after {
            content: "Loading";
            font-weight: bold;
            animation-name: loading-text;
            animation-duration: 3s;
            animation-iteration-count: infinite;
        }

        @keyframes loader {
            15% {
                transform: translateX(0);
            }
            45% {
                transform: translateX(230px);
            }
            65% {
                transform: translateX(230px);
            }
            95% {
                transform: translateX(0);
            }
        }
        @keyframes loading-text {
            0% {
                content: "Loading";
            }
            25% {
                content: "Loading.";
            }
            50% {
                content: "Loading..";
            }
            75% {
                content: "Loading...";
            }
        }

    </style>
    <div class='loader'>
        <div class='loader--dot'></div>
        <div class='loader--dot'></div>
        <div class='loader--dot'></div>
        <div class='loader--dot'></div>
        <div class='loader--dot'></div>
        <div class='loader--dot'></div>
        <div class='loader--text'></div>
    </div>
`</template>`

Next you define a function for the createdCallback, which is fired when the element is created.

```javascript
createProto.createdCallback=function(){}
```
###Combine custom element with shadow DOM and Template

So,for achieving this we have to create shadow DOM for our element to limit its styles,Ids to its scope of itself and template as I discussed earlier that it is used to make our code reusable and eaisier to handle.

```javascript

  var createProto=Object.create(HTMLElement.prototype);
        createProto.createdCallback=function(){
           var root=this.createShadowRoot();
            var template=document.querySelector('#template');
            var clone=document.importNode(template.content,true);
            root.appendChild(clone);
        }
        var loader=document.registerElement('x-loader',{
            prototype:createProto});
```

By adding this script you'll see that now loader is working fine on our page. 
