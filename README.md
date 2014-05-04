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

## Users

(Recognize [Jina][] or anyone else? Crazily enough, I just grabbed these avatars from [UIFaces.com][uif].)


[re-thinking]: https://www.youtube.com/watch?v=DgVS-zXgMTk&src_vid=x7cQ3mrcKaY&feature=iv&annotation_id=annotation_3048311263
[think]: http://facebook.github.io/react/docs/thinking-in-react.html
[mockup]: http://cl.ly/1E0C2H0M2J3Z
[Jina]: https://twitter.com/jina
[uif]: http://uifaces.com/authorized
[fid]: http://jsfiddle.net/alanhogan/2mVWk/