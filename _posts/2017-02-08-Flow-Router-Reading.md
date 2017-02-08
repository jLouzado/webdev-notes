---
layout: post
title: "Into to Flow Router (with Blaze)"
date: 2017-02-08 09:00:00 +0530
categories: meteor flowrouter blaze getting-started
description: Getting started with Flow Router, BlazeLayout and Meteor
---

# Routing with FlowRouter

## [Introduction to Flowrouter](https://kadira.io/academy/meteor-routing-guide/content/introduction-to-flow-router)

### Introduction 

- flowrouter *only* focuses on Routing.
    - rendering etc is handled separately, which allows you to plug other renderers into your app 
    - also means that flow router can be simpler and, hence, more stable.

#### Creating a route is simple

```
FlowRouter.route('/blog/:postId', {
    name: 'blogPost',
    action: function(params) {
        console.log("This is my blog post:", params.postId);
        //other actions, like rendering a template, etc.
    }
});
```

If the path is `/blog/kadira/getting-started?comments=show` the above params and queryParams objects will look like this:

```
params = {category: "kadira", postId: "getting-started"};
queryParams = {comments: "show"}
```

#### Group Routes

Group routes allow for defining structures and doing common tasks with [Triggers](https://kadira.io/academy/meteor-routing-guide/content/triggers)

```
var adminSection = FlowRouter.group({
    prefix: "/admin"
});
```

And then add a sub route by:

```
adminSection.route('/', {
    action: function() {}
});
```

And nested groups can be defined as:

var SuperUser = adminSection.group({
    prefix: "/super"
});

### [Rendering With Blaze](https://kadira.io/academy/meteor-routing-guide/content/rendering-blaze-templates)

TODO: Right now I don't see why this has to be mixed with meteor Blaze. Just use that, I think.

### [Subscriptions and Data Mgmt](https://kadira.io/academy/meteor-routing-guide/content/subscriptions-and-data-management)

- with iron-router, data subscriptions were done in the router and then handed off to the view.
    - This is now considered bad practice; an anti-pattern.
- Why?
    - client has no control of the data and also needs to be reactive, this leads to unpredictability. Also requires more work with loading screens, etc.
    - template reuse becomes harder because the data requirement in the router now also needs to be repeated.
- So now, subscription mgmt is just done at the template-level (with Blaze) and at a similar lvl with React, etc.

#### With (Meteor Blaze)

Let's load the data for our blog post:

```js
Template.blogPost.onCreated(function() {
  var self = this;
  self.autorun(function() {
    var postId = FlowRouter.getParam('postId');
    self.subscribe('singlePost', postId);  
  });
});
```

- an autorun() function means that old subs are automatically closed as new ones are made.
- Note that the postID is gotten using `FlowRouter.getParam` instead of getting via Blaze context.
    - this minimizes unwanted rendering.

Use a helper to get the data:

```js
Template.blogPost.helpers({
  post: function() {
    var postId = FlowRouter.getParam('postId');
    var post = Posts.findOne({_id: postId}) || {};
    return post;
  }
});
```

this keeps the content correct as the postId changes in the URL.

Finally the template:

```html
<template name="blogPost">
  <a href="/">Back</a>
  {{#if Template.subscriptionsReady}}
    {{#with post}}
      <h3>{{title}}</h3>
      <p>{{content}}</p>
    {{/with}}
  {{else}}
      <p>Loading...</p>
  {{/if}}
</template>
```

Also, [Manipulating URL & link generation](https://kadira.io/academy/meteor-routing-guide/content/manipulating-the-url-and-link-generation) and [accessing url state](https://kadira.io/academy/meteor-routing-guide/content/accessing-the-url-state) are important.


# Further Reading

* Contrasting patterns for auth and permissions- [Flow Router for Auth & Permissions](https://medium.com/@satyavh/using-flow-router-for-authentication-ba7bb2644f42) vs [Official Documentation](https://kadira.io/academy/meteor-routing-guide/content/implementing-auth-logic-and-permissions) vs [FlowRouter and Subscription Mgmt](https://meteorhacks.com/flow-router-and-subscription-management/)
* [FlowRouter Boilerplate](https://medium.com/meteor-js/starting-meteorjs-with-flow-router-cb7803ee7234)


