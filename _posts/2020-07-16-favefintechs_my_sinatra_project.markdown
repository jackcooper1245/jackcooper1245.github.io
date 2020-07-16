---
layout: post
title:      "FaveFintechs! My Sinatra Project."
date:       2020-07-16 17:12:12 -0400
permalink:  favefintechs_my_sinatra_project
---


Wow where to start. I have just wrapped up the build of my first full stack web app and it feels great. I feel so much more capable now than I did a few days ago. Let me talk you through the project and what I learned.

So FaveFintechs (there might be a theme here) is essentially a website where you can rate and review Fintech Companies. It has all the bells and whistles, error messages, and full on encrypted login system and it does what is supposed to which is great! My personal favourite parts about it are the search bar (which just looks cool and it works which is even better) and the fact that the whole site is responsive, so it looks good on your phone too. I built the site using Sinatra, Ruby and ERB as well as my new best friend .... Bootstrap! If you haven't seen or heard of it, its an open source tool that will revolutionize your front-end! Check it out here https://getbootstrap.com/.

<iframe src="https://giphy.com/embed/l4FGlrnsf6xR3U2EU" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/csssandbox-changethestory-imaginationbuildspower-l4FGlrnsf6xR3U2EU">via GIPHY</a></p>

Firstly lets have a quick look at my search bar. I built it into the layout of the site, so you could see it on every page! Here is the code below:

```   
<form class="form-inline my-2 my-lg-0" action="/search" method="post">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" name="search">
      <button class="btn btn-outline-primary my-2 my-sm-0" type="submit">Search</button>
</form>
```

and here is how it looks irl:

  <form class="form-inline my-2 my-lg-0" action="/search" method="post">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" name="search">
      <button class="btn btn-outline-primary my-2 my-sm-0" type="submit">Search</button>
  </form>
	
	
Pretty damn sexy right! Thanks too bootstrap it certainly looks that way! Honeslty I can't stress enough how great a resource bootstrap is. Check it out!
	
To get the search bar to actually work was a little challenging to start with. It turns out it just a basic ```post``` method that is passed the params of the search bar. I set it so you can only search for Company names stored in the SQLite database. If they didn't exist it took you to a page where you had the opportunity to create that very company. Check out the code below:

```

	post "/search" do
		@fintechs = Fintech.all
		if
		@fintech = @fintechs.find_by(name: params[:search])
		redirect to "/fintechs/#{@fintech.id}"
		else
			redirect to '/error'
		end
	end
	```
	
	It really is as simple as passing the params from the search bar and iterating through my Fintech class to see if the params matched any of the Fintech names. If they matched it took me to the company profile. Its not much but getting it to work was incredibly satisfying!
	
Another part of the build I love was making everything responsive. The site looks good on my mac and it'll look good on my iPhone as well! How did I manage this..... that's right you guessed it: Bootstrap. Simple little things like ```<div>```s and the magic assigning them classes like ```container-fluid``` or creating a table and assigning it the class of ```table-responsive``` is all it take for you containers to adjust themselves automatically to fit the screen size! Honeslty Bootstrap... you're a god send (you might think I've got shares in Bootstrap with all this banging on about it, but like I said its opensource and totally free!!!!). 

Combining the above with the magic of<a href="https://medium.com/@salmaeng71/understanding-yield-and-layouts-in-sinatra-659b40dc52bb"> ```<%=yield%>```</a> will allow you to build great looking, consistent websites with eaze.

Finally a few words on my learning journey throughout this project. I can honeslty say that I was surprised with how prepared I was to get through this. When I first started I was pretty nervous (don't believe me check out this  <a href="https://twitter.com/normal_name12/status/1282290750441619456">tweet</a>) and honeslty didn't know if I was capable of creating something from scratch. But the more I got into it  I realised I had been very well prepared by what I've learnt so far with Flatiron! Can't wait for Rails, bring it on.

<iframe src="https://giphy.com/embed/Me1YYAwaMz09zU2UaB" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/MeanGirlsBway-Me1YYAwaMz09zU2UaB">via GIPHY</a></p>

