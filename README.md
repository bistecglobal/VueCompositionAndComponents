# VueCompositionAndComponents
Vue Composition API and Components using Nuxt JS




# Vue Composition API and Components using Nuxt JS

Vue 3 Composition API, provide a new approach to organize data models and functions. Previous options of API don’t provide features to organize models or business logic in logical manner. Composition API provides great feature to organize codes, in a more reusable manner and it improves the readability of big components.

Option API distributes codes among data block, computed blocks methods and watch functions. Code has been spread in all the places there is no logical fragmentation. That structure is what makes it difficult to understand and maintain a complex component.

However, when we are working with bigger code blocks it’s convenient to fragment code blocks based on the logical concerns. It would be much nicer if we could collocate code related to the same logical concern. And this is exactly what the Composition API enables us to do.

  
The Problem  
If you have experience with Vue js 2, you must have seen the Option API, where the codes are not fragmented in a logical manner based on its functionality. A component might look like this.  

![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure1.png)

If we apply different color code for code fragments according to the Vue Composition API RFC showing how code fragments will be.

![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure2.png)

# How Composition API resolves

Here, goals are to fragment codes based on its feature / logical functionality.  Using Composition API we can extract these logic and place in separate files. And we can consume those inside the Setup method in Composition API. The separation of options obscures the underlying logical concerns. In addition, when working on a single logical concern, we have to constantly "jump" around option blocks for the relevant code.

## Composition API Using Nuxt Js

Nuxt Js provide Composition function using Nuxt Composition API. @nuxtjs/composition-api module that brings first-class Composition API support to Nuxt. The @nuxtjs/composition-api package is a wrapper over a @vue/composition-api plugin which means that along with Nuxt-specific utilities it contains all “standard” Composition API functions like ref or computed.

Before starting the feature of the Composition, first we will look into how Nuxt Composition API addons facilities to us to work with Composition in Nuxt Project. To enable Composition in Nuxt project we have to setup NuxtJs Composition API.

The installation is straightforward, just like with every other Nuxt module. First, we have to install the package:

> npm install @nuxtjs/composition-api –save

And register the module in our nuxt.config.js

> {
> buildModules: ['@nuxtjs/composition-api' ]
> }

The module is registering @vue/composition-api plugin under the hood so we can immediately use its features in our project without any additional code.

**Server-side**

The @nuxtjs/composition-api provide SSR capabilities within Composition.

useFetch which is a Composition API wrapper for a well-known Nuxt fetch that is commonly used to fetch asynchronous data (both on a server and client side)

It does two things:

It makes sure that the asynchronous function that was passed as its argument was resolved. Then the result is conveyed into client-side through window.__NUXT__ object and picked up by your client-side code as its initial state.

It’s preventing the client-side execution if navigation has been made on a server-side. Because of that we’re not performing unnecessary network calls if we already have the data from the server-side fetch.

To make use of useFetch in our composable we just need to wrap it around our asynchronous code:

> import { ref, useFetch } from '@nuxtjs/composition-api' import {
> defineComponent } from '@nuxtjs/composition-api'
> 
> function getEntrolment (id) {   const entrolment = ref({});   const {
> fetch: fetchEntrolment } = useEntrolment(async () =>
> fetch('https:entrolment /' id).then(response => response.json())  }

## Using Nuxt Context in your composable

Among with data related server capabilities, Nuxt composition API is delivering a set of composables to interact with other composable api. One of the most helpful feature is useContext.  As represented in the name, it facilitates us to access Nuxt context inside our composable. We can use this instance to access router, store and properties via Nuxt Modules.

In Vue 3 Composition, Vue Context is accessible inside the Setup() method only. It’s not allowed to access outside. Therefore, if we want to access the Context in different Compose files we have to pass context as a parameter to the specific file. With the help of useContext() method we can access Context Object inside  any Composition API.

# How to Modularize Components

Let’s see how we can organize our component by feature and reuse our code across other components. In this below example it’s a Student Portal it has three main feature area, those are Course Enrolment, Showing Progress Report, Showing Student Profile.  If we see the functionality of the student portal, we can clearly identify that it has three modules as follows.

 - Enrollment
 - Progress Report
 - Student Profile

Let see how we can organize the code using Composition API.  
![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure3.png)

Here Enrollment, Progress Report and Student Profile has been moved to different files. It’s related fields and methods are also placed in the same file. Therefore, it’s more human readable and mean time maintainable. And we can use the above compose section anywhere in our application as used in this page.

# Building Reusable UI Vue Component

There are two approaches alleviable to build reusable component in the Vue application. Both have their strength and weakness. Those are using Property and using Slot. We have to select the correct approach based on the needs.

# Using Props

For an example there is an Address Component which is used to capture address of the student. The same component has been used to capture local address and foreign address as well. So based on the country, the address fields have to be changed. This has been achieved using Props for the component. The component has multiple props to change the behavior of the component.

![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure4.png)

![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure5.png)

This approach is suitable for small components. If number of props increases it’s difficult to manage the component because as we are introducing logic inside the component to maintain the state. It’s difficult to understand.

To handle this scenario with Vue 2.6 Slot directive has been introduced. Through this we can distribute the content to the component. So rather than keeping the HTML content in a component and changing the behavior based on the props. We can set the HTML content to the component from outside.

# Slot Directive

So, we understand the whole concept from the definition of slots it’s about making components reusable. Now, we’re going to dive in with some examples showcasing Vue slots and talk about how to make use of them.

We will take the same example and see how we can use Slot instead of Props.

![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure6.png)

You can notice in the above picture that we have removed Drop down from Postal code and we have placed <Slot name=”PostalCode”> This is going to work as a place holder and when we are using this component we have to define the HTML Content for this Slot as given below.

![enter image description here](https://raw.githubusercontent.com/bistecglobal/VueCompositionAndComponents/main/doc/img/Figure7.png)

Through this we can distribute the content to outside of the component.  Therefore, we are able to control the component behavior from the outside.

# Conclusion

We have seen how we can use Nuxt Composition API to fragment code in a logical manner and how we can reuse them among the components. Mean time we can create reusable UI Components using Slot directives.  The goal of the Composition API is to increase readability and facilitate us to create components in more reusable manner.
