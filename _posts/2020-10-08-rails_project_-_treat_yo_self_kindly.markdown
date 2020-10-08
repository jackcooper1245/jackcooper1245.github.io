---
layout: post
title:      "Rails Project - Treat Yo Self (kindly)!"
date:       2020-10-08 10:27:18 +0000
permalink:  rails_project_-_treat_yo_self_kindly
---


Hey guys, I wanted to put down a few thoughts about my rails project. 

First things first I wanted to tell you how relieved I am to have got this done. Its not easy balancing full time employment with trying to build a full on web app. Not only that but I had a self imposed deadline as I am away on a much needed holiday with my girlfriend tomorrow. I found myself spending so much time in front of the computer these past couple weeks that I genuinely can't wait for a nice break away from a screen! What I've learnt is that I need to get better at taking breaks, rather than just powering through. With web development, the project isn't over until you've built it, but that doesn't mean you can't give yourself a break. Treat yourself kindly.

Anyway... So my app I built is a budgeting app called Treat-Yo-Self.  Its essentially an app to help you budget, but with a twist, it helps you budget your spending on the things you break out of your budget for. Its hard work to stick to a budget, so this helps you control your spending when you sneak outside your budget.

<iframe src="https://giphy.com/embed/gVv0K9mssfJao" width="480" height="294" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/night-stop-her-gVv0K9mssfJao">via GIPHY</a></p>

Honestly building my first rails app was really hard. It took a lot of going back through old lessons and a lot of reading the documentation to get it all working. One thing I think I really had to work on was Active Record Associations, and working in the many to many relationship. I'll talk about that first.

My Many to Many relationship was between my Lists and Treats models. I created a jointable called 'Lts'. 


 `class Lt < ApplicationRecord
    belongs_to :list
    belongs_to :treat
end
`

So when I wanted to add a Treat to a Treat Cycle I assigned a `treat_id` and a `list_id`  and a `start_time` through a form with hidden fields.

```
  <%current_user.treats.each do |treat|%>
    <div><%= link_to treat.name, user_treat_path(current_user, treat)%> 
    <%= form_for(@lt) do |f|%>
    <%= f.date_select :start_time%>
    <%= f.hidden_field :list_id, value: @list.id%>
    <%= f.hidden_field :treat_id, value: treat.id%>
    <%=f.submit "Add to cycle"%>
    <%end%>
    <%end%>

```

This form created an Lt object that we displayed through the calendar on the apps homepage. I generated the calendar using a really cool gem called simple_calendar. Definitely check it out. It allowes you to render a simple calendar using the following code:

```
 <%= week_calendar start_data: Time.now, events: @lts do |date, lts| %>
        <%= date.day %>

        <% lts.each do |lt| %>
          <div>
            <%=link_to lt.treat.name, treat_path(lt.treat) %>
          </div>
        <% end %>
      <% end %>
```

The first 2 lines of code render the calendar, I then passed the join table model through an instance variable `@lt`. Lt object had a start_time, which allows you to render them on the simple_calendar gem. I then chained the Lt object treat name via its treat_id and that displayed when and what treat you were planning on using on a given day on the calendar.

Pretty neat huh!
 
 
I learnt a lot on this build and am very much looking forward to Front End!

<iframe src="https://giphy.com/embed/XtUPfbJIltIaY" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/zach-galifianakis-cheers-the-hangover-part-iii-XtUPfbJIltIaY">via GIPHY</a></p>



