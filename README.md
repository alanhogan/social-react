# Learning React.js to solve this coding challenge

<!-- Markdown. Convert it for optimal readability! -->

I’ve been hearing some good things about React.js, the new “JavaScript library for building interfaces” from Facebook. Intrigued, I watched [their introductory video][re-thinking] — and not only did I find their reasoning compelling, but my jaw actually dropped when I saw the effects they were producing at 60fps using just React.js' declarative-style approach. (Specifically, a 3D Cover Flow-esque interface with perfect touch tracking.)

Thanks to a 2011 success of mine involving a combination of a state machine with Knockout.js data binding, I’m not a stranger to how powerful, DRY, and reliable code written in a declarative paradigm can be, so this was sounding pretty good.

And having used Angular professionally in the past, well, it seemed less intriguing an option for this challenge.

## How to Think with React

Boy, do I love good technical writing like [this introduction to thinking with React][think].

Essentially, they encourage developers to start with the mockup and data model to small "components." Well, we already have a [Balsamiq mockup][mockup], but no data, so let’s reverse-engineer some JSON.

    // JSON + comments for the feed.
    {
      "posts": [
        {
          "id": "89765466856", // IDs as strings avoids the maxint problem
          "authorId": "59876",
          "postTimeStr": "5h ago", // it's a prototype; don't calc at runtime
          "content": "\"Would you eat them with a hat?\" Are you kidding me? I am never trying green eggs and ham!",
          "comments": [
            // Each comment will have the same format as a post, since they have the same data, with the exception of having "comments" themselves
          ]

        } // , ...
      ]
    }

    // JSON for a user/author
    {
      "id": "89765466856",
      "displayName": "Teddy Geisel",
      "aviThumbUrl": "avatars/1.jpg"
    }

Okay, so let’s take this info and draw onto our mockup, identifying candidates to be React components.

![Mockup with components outlined](http://f.cl.ly/items/111G352A0s2I1R2c2r0S/Screen%20Shot%202014-05-03%20at%209.34.40%20PM.png)

The components that were identified (leaving aside the delete/modal screen for now) are:

- Toolbar (not outlined)
- BackBtn (pink; only visible in second screen)
- CurrentUserIndicator (gray)
- Feed (green)
- Post (orange)
- DeletePostBtn (red)
- AuthorThumb (purple)
- AuthorName (golden)
- PostTime (pink)
- PostContent (teal)
- CommentLink (navy blue)
- CommentComposer (gray)

Although, on second thought, a lot of the components in a post don’t really have any behavior or complexity to them — yet — so we’re probably *not* going to make AuthorThumb, AuthorName, PostTime, and PostContent their own components just yet.

And we can recognize that these components will have a an obvious sort of hierarchy.

## Start Static

Next, I followed the suggestion of implementing a completely static version of the interface using React components.

I did this by forking the handy jsFiddle template the React developers set up. You can take a look at [my fork here][fid].

Well, I did first screen of the interface, anyway. Since comments are not shown in the main feed, I wasn’t sure how to mock them up while being static, so I looked ahead to the next part of the guide.

## Identifying state within our app

React doesn’t seem to ship with any sort of router concept (being more limited in its scope than many popular frameworks), so I think that may mean considering our “place” within the app to be part of our state.

This means I have a way to finish statically creating the rest of the app, however; I’ll use a top-level component which handles rendering (and eventually animating) the different parts  of the app. In the spirit of starting static, I can set the state of this component as needed to preview the different parts of my app.

State will be needed to handle:

- Whether we are looking at a feed or just one post
- Which post, if applicable, is being shown
- Whether the delete modal is shown or not, and which post to delete if the deletion is confirmed

So at the top-level component, I have named “Social” for lack of a better name; now I am creating and using a getInitialState() function. By changing its values, I am able to build and test the post detail view (which is how I’m thinking of the screen that shows comments on a post).

## Can we navigate? Part 1: “Add inverse data flow.”

In React, there is no two-way binding. To change data or state, you have to explicitly throw it back up the view hierarchy. (“React makes this data flow explicit to make it easy to understand how your program works, but it does require a little more typing than traditional two-way data binding.”)

What I want to handle next is navigation (sans animation, at first). But the guide is lending itself more towards handling the automatic enabling of the Post button when the user enters comment text, so I think I’ll take a detour for that.

## Handle change: 

I hadn’t actually added the comment box yet, so I did that next. I added state to the DetailView to track whether or not text has been entered, and instructed React to set that state (as calculated on string length — I’d use trim in production, of course — whenever the input field changes. We will see if React's concept of changing is more immediate than the laggardly browser `change` event.)

## Finally navigating 



## Users

(Recognize [Jina][] or anyone else? Crazily enough, I just grabbed these avatars from [UIFaces.com][uif].)


[re-thinking]: https://www.youtube.com/watch?v=DgVS-zXgMTk&src_vid=x7cQ3mrcKaY&feature=iv&annotation_id=annotation_3048311263
[think]: http://facebook.github.io/react/docs/thinking-in-react.html
[mockup]: http://cl.ly/1E0C2H0M2J3Z
[Jina]: https://twitter.com/jina
[uif]: http://uifaces.com/authorized
[fid]: http://jsfiddle.net/alanhogan/2mVWk/