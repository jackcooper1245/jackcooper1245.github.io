---
layout: post
title:      "A few tips for getting started with Ruby!"
date:       2020-04-16 07:44:53 -0400
permalink:  a_few_tips_for_getting_started_with_ruby
---


I have been studying with the flatiron school now for a few weeks and have made my way through the basics of Ruby and Procedural Ruby. Now that I am focussing on Object Oriented Programming I thought I would spare a few minutes and write about my experiences. It can feel pretty daunting getting started with programming and I thought it might be helpful to hear someone new to its thoughts, just in case like me you were unsure whether you'd be up to the task of getting started. Trust me there will be times you are totally lost, I was, but its all about using the right methods to find the right solution.

<iframe src="https://giphy.com/embed/3EiNpweH34XGoQcq9Q" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/3EiNpweH34XGoQcq9Q">via GIPHY</a></p>

I thought I'd use the first major challenge I was tasked with, building a CLI Application, and how I made life easier for myself working through it. Tic Tac Toe, as our friends across the pond call it, or Noughts and Crosses if you're from my rainy little island.  It is definitely challenging figuring out some of the methods and I know personally I had to ask a lot of questions to make my way through it. Learning a new language is difficult, and learning to code in that new language is even harder. So don't feel like you need to be able to immediately recognise the answer to the complex solutions you're faced with. If you knew all the answers right away there would be no challenge in this undertaking, and where is the fun in that. 

<iframe src="https://giphy.com/embed/YoQqbNpEF39SpI7deq" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/abcnetwork-stumptownabc-not-fun-wheres-the-YoQqbNpEF39SpI7deq">via GIPHY</a></p>

From my brief glimpse into the field and my conversations with coaches and people with world's more experience than me, we, as programmers are not expected to know the solution for everything off the top of our head.

What will help you get through the uphill challenge of learning to code is getting good at looking for solutions. Google is your best friend and there are some awesome sites that can give you a fresh perspective on the issue you are facing.

A few of my personal favourites are:

1 https://stackoverflow.com/

I can almost guarantee you that any issue you are facing with your code someone has faced before. Here you can post your issues and crowd source solutions with the community or look up answers to similar problems to yours that have previously been discussed. Its a lifesaver.

2 https://www.geeksforgeeks.org/

Geeks for Geeks is very helpful in explaining the process and syntax of different methods in Ruby. Definitely a go to for me if I want to get an explanation on an unfamiliar method. If you're struggling with your loops like I did at first check out their tutorial on them here https://www.geeksforgeeks.org/ruby-loops-for-while-do-while-until/.

3 https://medium.com/

The website itself is pretty general, but it does have some really good blogs on learning Ruby. Here I found some really well written articles explaining issues that I was facing. Not only that but the site itself has really nice asthetics. Check out a couple of blogs I've found useful so far: https://medium.com/@christine_tran/tic-tac-toe-game-ruby-style-cli-7bf619021e5d, https://medium.com/the-renaissance-developer/learning-ruby-from-zero-to-hero-2cf06da45396




Finally before I sign off I thought I'd run you through one of the topics I found particularly interesting. Object Oriented Programming is awesome! The fact that you can create these objects and teach them all these amazing tricks is really cool. I thought I would run you through one subtopic and give you some tips on how to learn them: Instance Methods!

First things first what is an instance method? An instance method is a method than can be called on every instance of a class. It is what gives our instances the power to the interesting things that we program them to do. All objects respond to methods and we can use this power to create things out of thin air and then get them to do the things we want them to do.

```
class Puppy
end

daisy = Puppy.new
```

Here we see that we have created a class called Puppy. We then go on to create an **instance** of this class called daisy. We can teach our Puppy daisy to do some cool things by inserting instance methods into the Puppy class. Say we wanted daisy to know how to bark for example.

```
class Puppy

def bark
puts "Woof!"
end

end

daisy = Puppy.new
```

Now if we ran this program and asked daisy to bark, she would!

```
daisy.bark
Woof!
=> nil```

Pretty cool huh! But this just seems like daisy is responding to a normal method. The cool thing about instance methods is that we can create as many new puppies as we'd like and they'll all know how to bark. This is because we have written the bark method inside the Puppy class where these instances come from. 

```
jaffa = Puppy.new
jaffa.bark
Woof!
=> nil
```

That's cool right! Thinking about the objects as actual things rather than some imaginary thing the computer facilitates made wrapping my head around object oriented programming a lot easier than it would have been. If you think about the instances of the class Puppy as actual puppies you want to learn things it makes things a little easier.

<iframe src="https://giphy.com/embed/lqwcYeLIvQSUcSf6nP" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/memecandy-lqwcYeLIvQSUcSf6nP">via GIPHY</a></p>
Don't bang you head against your table. Ask for help and use the right resources to find it and you'll be on your way.

Okay that's all for this time. Thanks for reading and I hope this helped in some form or another.







