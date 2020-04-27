---
layout: post
title:      "The Music Library CLI - What I picked up what I thought was really  cool!"
date:       2020-04-27 09:32:45 -0400
permalink:  the_music_library_cli_-_what_i_picked_up_and_what_i_learned_about_myself
---


I have almost made it through the first major section of my training with Flatiron and am onto the final projects module, not far away from the opportunity to create my first app! I wanted to stop for a moment and write a little about how I've found things so far, then we can have a look through the Music Library CLI together.

It has been a very rewarding month or so since I started learning how to code. I'll be honest I'm pretty happy with how things are progressing. I am really enjoying the course, and find it very satisfying learning all these cool new things. It is great being able to do something creative, and Ruby is such a great language, it honestly has been a lot of fun. I've been thinking about my first project for the past week or so, but I won't get into that just yet, safe to say that I am excited about getting started with it.

<iframe src="https://giphy.com/embed/KxiRwO7tqXCTDVKobo" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/brooklynninenine-brooklyn-nine-99-heist-KxiRwO7tqXCTDVKobo">via GIPHY</a></p>

Before I can jump into my first app though, I have a few more challenges left to get through. I actually finished one of those last night and wanted to take you through how I approached it, the bits I found challenging, and how I'll use it to influence my work in the future.

What I was trying to build in this lab was a CLI that allowed me to browse through a library of music files I imported, and 'play' a song (it's a bit more complex than that but thats the main jist of it. The final product looked a little bit like this:
```
Welcome to your music library!
To list all of your songs, enter 'list songs'.
To list all of the artists in your library, enter 'list artists'.
To list all of the genres in your library, enter 'list genres'.
To list all of the songs by a particular artist, enter 'list artist'.
To list all of the songs of a particular genre, enter 'list genre'.
To play a song, enter 'play song'.
To quit, type 'exit'.
What would you like to do?
```
From here you can type in your commands and it will respond in kind (it worked aswell which was great):
```
What would you like to do?
list artist #I input this here
Please enter the name of an artist: #It then reponded with this!
Action Bronson #I input the artist I wanted to see
1. Larry Csonka - indie #Here you go, a song by Action Bronson, with its genre too
```

Pretty cool hey! 

To get to this point involved an awful lots of coding, neatly packed away into objects that collaborated and made the whole thing work. Now I don't want to run you through each individual method as that might not be the most thrilling way run through this. I wanted to give you a basic structure and then run through some of the cool (in my opinion) methods that linked the objects together and made the whole thing tick.

First things first there were 5 classes I created that made this run:
* Song
* Artist
* Genre
* MusicImporter
* MusicLibraryController

These all collaborated through has-many and has-many-through. Their relationships ran as follows: A Song has an Artist and an Artist has many songs; A song has a Genre and an Artist has many Genres through its Songs; A Genre has many Songs, and many Artists through its Songs. Simple stuff really (lol). I'll give you some examples of the methods that create the has-many relationships and the has-many-through relationships below:
```
def genres
  unique_genres = []
  songs.collect {|song| unique_genres << song.genre}
  unique_genres.uniq
end
```
This was situated in the Artist class and allows us to run `artist.genres`. Now through the artists songs we can see what genres it has. We use `.collect` to iterate through the artist's songs, and then shovel all of those songs genres into an array of `unique_genres` which we then call with .`uniq` so that it returns us a list of all of the different genres the artist has without doubling up on any. Cool right!

In the song class we have a couple cool examples of collaborative methods as well:
```
def artist=(artist)
  @artist = artist
  artist.add_song(self)
end
```

This is our `artist=` method. This allows us to assign the song an artist, and at the same time let the artist class know that it has a new song with `artist.add_song(self)`. We are calling another classes method on itself from with in the Song class. This sort of collaboration is what allows us to create the relationships we need to build meaningful and dynamic programs.

Now for us to be able to create a library of music to navigate through in the CLI we had to import a file of songs, and then work on the filenames and turn them into something more familiar. Basically so this: `'Action Bronson - Larry Conska - indie.mp3'` looked liked this `1. Action Bronson - Larry Conska - Indie` when we listed it in the CLI. A couple of the methods we used to do this are bellow. First of all we wanted to be able to instantiate a new song from the filename:
```
def self.new_from_filename(filename)
  array = filename.split(" - ")

  artist_name = array[0]
  song_name = array[1]
  genre_name = array[2].split(".mp3").join

  artist = Artist.find_or_create_by_name(artist_name)
  genre = Genre.find_or_create_by_name(genre_name)
  self.new(song_name, artist, genre)
end

```
We took the filename, and saved it into an array that we split using the .split method (check out some more info of the .split method here: https://www.thoughtco.com/using-the-split-method-2907756). We split it by the `-`. We then took the 3 sections of the filename and save them in variables `artist_name, song_name and genre_name`. We then passed `artist_name` and `genre_name` to our `.find_or_create_by_name` methods we defined in our `Concerns::Findable` module and instantiated a new song using the results of those methods! We did it, we created new song instances using the files we imported into the libary! 

Now a quick note of `Concerns::Findable`. Our aim as rubyists and developers in general is to make easy to understand beautiful code. We can do this through abstraction. To quote Edsger Dijkstra:

> "Being abstract is something profoundly different from being vague … The purpose of abstraction is not to be vague, but to create a new semantic level in which one can be absolutely precise."
> 

In this case, instead of repeating our `find_by_name` and `find_or_create_by_name` methods in both the genre and artist classes we have abstracted them away to a module called `Concerns::Findable` and then extended them into those classes, allowing them to benefit from their use (to get some more info on this topic checkout this blog https://medium.com/@leo_hetsch/ruby-modules-include-vs-prepend-vs-extend-f09837a5b073).

I think that's just about all for this blog post. I really enjoyed the Music Library CLI lab as it gave me an opportunity to test out my knowledge in a really wholistic way, what a long I've come from the start. To think over just a month a go I had no idea what a method even was! Thanks for reading guys.

<iframe src="https://giphy.com/embed/13Yjln8dW18nEA" width="480" height="408" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/13Yjln8dW18nEA">via GIPHY</a></p>


