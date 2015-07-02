---
layout: post
title:  "Developer Portal is Now Online!"
date:   2015-07-01 19:12:30 +0800
categories: announcement
---
We would like to announce the availability of our SDK Portal. Hopefully we could help you build that stellar app through the tools we will provide soon!

We would like to thank the Jekyll development team for sharing tools that allows us to build this developer portal.

## Jekyll
Jekyll is a static site generator developed in ruby that generates websites from markdown and many other formats. The benefit of this is that you can have a highly customisable blog where you can generate posts by writing easy markdown code whilst still retaining the small memory imprint that Jekyll has. 

### Code Snippets
Code Snippets are one of the main reasons why I love Jekyll and I think you will too. All code snippets become highlighted with great colours when you write the code in markdown. Here is an example of highlighted Ruby code in a weather application that I have made.
{% highlight ruby %}
#!/usr/bin/env ruby

require 'json'
require 'net/http'
require 'libnotify'

def parsejson
    file = "http://api.openweathermap.org/data/2.5/find?q=London&mode=json"
    response = Net::HTTP.get_response(URI.parse(file))
    weatherjson = response.body
    actual = JSON.parse(weatherjson)

    # check for errors
    if actual.has_key? 'Error'
        raise "error with the url"
    end

    results = []

    actual["list"].each do |listitem|
        weather = listitem["weather"]
        weather.each do |weath|
            results.push(weath["description"])
        end
        main = listitem["main"]
        temp = main["temp"] - 273.15
        results.push ("%.2f" % temp)
    end

    return results
end

def notify(summary)
    Libnotify.show(:body => "Current temperature is: #{summary[1]} degrees celsius.\nCurrent description of conditions: #{summary[0]}", :summary => "Weather Update", :timeout => 10)
end

notify(parsejson())
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com


Stay tunes for more updates!