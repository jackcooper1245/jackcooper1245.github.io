---
layout: post
title:      "Forms, twitter storms and lockdown norms!"
date:       2020-06-29 13:04:22 +0000
permalink:  forms_twitter_storms_and_lockdown_norms
---


Hey guys. Another installment of my blog today. I'll be honest it has been a while since I've written one, and I feel strangely guilty about it. My circumstances have changed recently and I'm still trying to to refind the balance I had when I first started at Flat Iron. Not only have I started a full time (non-technical) new job, I've also moved to the Netherlands. The move has been great and as Lockdown eases here there has been a lot more to do than when I was in the UK so I've been making the most of it and doing all sorts of Dutch things. Lots of cycling and sitting in Cafes. Its honeslty been a delight.

Enough about that. I wanted to discuss a few things in this post. I've started getting into Front End and am really enjoying it! One things I've been trying to really focus on is RESTful routes and sticking to conventions. After that I wanted to dive quickly into the other aspect of my course at Flat Iron, the end goal, finding a job and how I've been going about it recently.

**Sinatra RESTful routes:**

Lets face it. The internet would be a very confusing place without convention. This is why RESTful routes allow a design pattern that allows for easy manipulation of data. It makes the whole thing a lot easier, web development that is. What is a RESTful route you ask? 

> A RESTful route is a route that provides mapping between HTTP verbs (get, post, put, delete, patch) to controller CRUD actions (create, read, update, delete). Instead of relying solely on the URL to indicate what site to visit, a RESTful route also depends on the HTTP verb and the URL.
> 

Lets take a look at the individual routes that relate to each of the different elements of CRUD (Create, Read, Update, Delete).

<iframe src="https://giphy.com/embed/l3V0mgFspVuDAJK9y" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/gotham-fox-l3V0mgFspVuDAJK9y">via GIPHY</a></p>

**Create - or the ``/new`` route:**

If we use the example of a magazine website: 

```
get '/articles/new' do
  erb :new
end
 
post '/articles' do
  @article = Article.create(:title => params[:title], :content => params[:content])
  redirect to "/articles/#{@article.id}"
end
```

The first controller action loads the form for a new article, this is a `get` request. This action responds to a ``post`` request and creates a new article based on the params from the form and saves it to the database. Once the item is created, this action redirects to the show page.

**Read - or the `/show` route**

```
get '/articles/:id' do
  @article = Article.find_by_id(params[:id])
  erb :show
end
```

In order to show a single article we need a `/show` action. We use symbols (`:id`) to make the URL dynamic, which means we can access the article id throught the params hash. This controller responds to a `get` request. 

**Update - or the` /edit `route**

```
get '/articles/:id/edit' do  #load edit form
    @article = Article.find_by_id(params[:id])
    erb :edit
  end
 
patch '/articles/:id' do #edit action
  @article = Article.find_by_id(params[:id])
  @article.title = params[:title]
  @article.content = params[:content]
  @article.save
  redirect to "/articles/#{@article.id}"
end
```

The first controller action above loads the edit form in the browser by making a `get` request to `articles/:id/edit`.

The second controller action handles the edit form submission. This action responds to a `patch` request to the route `/articles/:id`. First, we pull the article by the ID from the URL, then we update the title and content attributes and save. The action ends with a redirect to the article show page.


**Delete - or the `/delete` route**

```
delete '/articles/:id' do #delete action
  @article = Article.find_by_id(params[:id])
  @article.delete
  redirect to '/articles'
end
```

On the article show page, we have a form to delete it. The form is submitted via a `delete` request to the route `/articles/:id`. This action finds the article in the database based on the ID in the url parameters, and deletes it. It then redirects to the index page `/articles`.

```
<form action="/articles/<%= @article.id %>" method="post">
  <input id="hidden" type="hidden" name="_method" value="delete">
  <input type="submit" value="delete">
</form>
```

As you can see if we stick to these convetions across the web, things will be an awful lots easier to navigate, not only for developers but also for users! Neat right.


Before I wrap this up I wanted to discuss some of the techniques I've been trying to build me network and get my name out there. Twitter, it turns out, is full of developers, chock a block to the top full of them. The Tech twitter community is very active and tends to be very inclusive. I sent up a tweet recently that got a fair bit of traction in the community and I thought "I've got to capitalise on this audience reach". I went through a few of the people who have engaged in my tweets and reached out to them directly to ask their advice on getting into the industry as a junior. You know what it really worked. I managed to get a video intro to an entrepeneur in Berlin who wanted to ask my thoughts on his new project and I've also got a face to face coffee with a Senior Developer for a major e-commerce organisation out of it as well. If you can take anything away from this is don't be afraid to ask people for their advice. Most people are very friendly and more than that, most people want to help juniors like myself get into the industry. It is worth tweeting them and asking them, you never know what may come of it. That twitter storm could lead to the next step in your career!

<iframe src="https://giphy.com/embed/nbax9PrgJBBuSPdWFK" width="480" height="204" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/nbax9PrgJBBuSPdWFK">via GIPHY</a></p>

That's all for now. Starting my Sinatra project soon, so will be posting about that once it's complete. If you want to chat about anything just hit my up on twitter @normal_name12. 
