---
layout: post
title:      "Top50fintechs - My CLI Data Gem"
date:       2020-05-06 19:58:49 +0000
permalink:  top50fintechs_-_my_cli_data_gem
---


This blog post I am going to run you through my CLI Data Gem project. I have spent the last week (almost) battling away at my first original creation. First things first I wanted to run through some of the methods I used to create the Gem.

The gem essentially scrapes info from fintech50.com and allows you to easily browse all of the top FinTech companies from the past few years. The first issue I ran into was how to scrape the right amount of information at a given time without slowing down the program. At first I tried to start the program and scrape all of the information I needed, store it as objects and then access that information as required. This didn't work. I was essentially asking my program to scrape information from 164 different web pages at the same time, it was too much for my slow countryside internet connection. I changed my strategy, I would only scrape information when it was specifically requested. So I split my scraping into 2 methods ``scrape_companies_titles_and_urls`` and ``self.scrape_by_name``. The first scraped the index pages from the website and saved the companies names and a  link to more information about the company. The second then allowed you to enter the name of the company you wanted more info on and then scrape the information about it. You can check out those 2 methods below:

```
def scrape_companies_titles_and_urls
    array = []
    @doc = Nokogiri::HTML(open(@category_url))
    @doc.search('div[class=margin-wrapper]').each do |company|
      company_hash = {
        :name => company.search('a').attribute('href').value.split('/').join.gsub("-", " ").capitalize,
        :company_url => "https://thefintech50.com#{company.search('a').attr('href').text}"}
          array << company_hash
        end
    array
end

def self.scrape_by_name(input)
  url = Company.select_by_name(input)
  profile_array = []
  html = Nokogiri::HTML(open(url))
  profile_hash = {}

  profile_hash[:name] = html.css('h2')[0].text
  profile_hash[:website] = html.css('div.sqs-block-content p:first a').attribute('href')

  html.css('.sqs-block-content p').each do |el|
    if el.text.include?("Founders")
      profile_hash[:founders] = el.text
    elsif
      el.text.include?("Founded")
      profile_hash[:founded] = el.text
    elsif
      el.text.include?("Last funding")
      profile_hash[:last_funding] = el.text
    elsif
      el.text.include?("HQ")
      profile_hash[:HQ] = el.text
    elsif
      el.text.include?('t:')
      profile_hash[:twitter] = el.text
    elsif
      el.text.include?("Keyword")
      profile_hash[:keywords] = el.text
    end
  end

  profile_array << profile_hash
  profile_array
end
```

We then took the information from  ``self.scrape_by_name`` and displayed it with display_company in the CLI class. To give you an example, if you wanted to get some info on Revolut, the program would go to https://thefintech50.com/revolut and scrape the information, and then display it like this:
```
Name: Revolut
-------------------------
Company website: http://www.revolut.com
Founders:  Nikolay Storonsky (CEO), Vlad Yatsenko
Founded: 2015
HQ: UK, London
t: @RevolutApp
Keywords: Digital Banking
-------------------------
```

Its not much but I think its pretty neat.

The CLI itself is also something I am kinda proud of. It took me ages to get it to work the way I wanted it to. To get it to seamlessly jump in and out of levels without it crashing. You pick a category, choose a company you want to learn about, return to the list of companies, choose another company, jump back to the main menu, pick another category and run through it again. Its really cool. Some of the methods that allowed this are below:

```
def menu
  puts "To return to a previous menu at any point please type 'back'"
  input = " "
  while input != 'exit'
    input = gets.strip
    case input
    when "1"
     make_companies('https://thefintech50.com/the-fintech50-2019-50-fintechs-to-watch-in-2019')
     Company.print_all
     enter_next
    when "2"
      make_companies('https://thefintech50.com/the-hot-ten-2019')
      Company.print_all
      enter_next
    when "3"
      make_companies('https://thefintech50.com/the-fintech50-2018-list')
      Company.print_all
      enter_next
    when "4"
      make_companies('https://thefintech50.com/the-fintech-50-2017')
      Company.print_all
      enter_next
    when "back"
      Company.destroy
      lists_categories
    when "return"
      Company.print_all
      enter_next
    when "exit"
      goodbye
    else
      error_assitance
   end
  end
end


def enter_next
  puts "Please enter the name of the company you would like to know more about or type 'back' to return to the previous menu."
  input = gets.strip
  if input == "back"
    lists_categories
  elsif
    input == "exit"
    lists_categories
  elsif
    Scraper.scrape_by_name(input)
    display_company(input)
  end
end
```

The ``menu`` allows you to navigate the top layer of the program.  ``enter_next`` then allows you to run the program successfully.  Cool huh! You can see the whole thing in the github repo here https://github.com/jackcooper1245/top50fintechs

