---
title: "App idea: Strava API + affiliate programs"
date: 2014-06-07 16:16:01 -0600
categories:
  - ideas
tags: 
  - strava 
  - affiliate 
  - running
---

I buy a lot of running shoes. Sometimes new models, now and then new brands, but most of the time I stick to the ones I know and trust. One such shoe is the Asics DS Trainer. A new model is released every year. The last one I bought was model #19. Before that pair I’ve had the DS Trainer 18, the 17, the 16 and the 15. Hey, it’s a great shoe.

## The problem

I want to know when the next model comes out and I want to know where I can get it for the best price.

Given that I love the DS Trainer, what other shoes should I try? What if I decide to switch to off-road running. Knowing that the DS Trainer is my favorite shoe on tarmac, and considering the width, support and quality of that shoe, which off-road shoe should I try?

## Data
There are a lot of apps for runners. RunKeeper, Nike+, Garmin Connect, Endomondo, Strava, MapMyRun and so on. They all share some common base features, but they also have extra features that set them apart. I like Strava due to the monthly challenges you can participate in, the segment feature, and the ability to log which shoes you are using for your runs.

[Strava](http://www.strava.com) has a free, public [API](https://strava.github.io/api/) for developers. I can authenticate with Strava, perform a REST call and retrieve the total mileage on all my shoes. Here’s an outtake of the data from my Strava profile page:

![Strava profile data](/images/060714_1540_AppideaStra1.png)

From this I can see that it’s about time to retire my DS Trainer 18’s. They’ve been heavily used so it’s fair to assume I like them and probably would buy something similar again. The app should detect this automatically on my behalf. I would like to be presented with the best price for this very model, it’s probably a bit dated and on sale somewhere in my area. Besides, running in worn out shoes can get me injured.

There are some shoes that I have only worn a couple of times. If this goes for other shoes from the same brand, it’s probably a brand I should avoid in the future. The app should not present me with any deals on this brand, and maybe even warn me to steer clear of this brand completely.

Combined with data about my runs, also available using the Strava API, I can see which shoes I have used for races, long runs or interval training. Any patterns here? Could the app recommend a certain shoe for me as it sees I have an upcoming race in 1 month and probably need a new pair of light-weight racing shoes?

## Mockups
My first idea was to use the data from Strava with the Amazon API, hence this quick sketch:

![Strava profile data](/images/060714_1540_AppideaStra2-198x300.png)

As I was playing around with the Bootstrap framework at the time, I also threw together this very rough sample web app (ignore the random heading):

![Strava profile data](/images/060714_1540_AppideaStra3-300x273.png)

The sample app was using mocked up data only, but I find getting some simple visuals help immensely when evaluating the idea. In this case, I realized a “passive” web site won’t work at all. There has to be some kind of notification system that actively notifies the user about a worn-out shoe or new models. A user may probably visit the website once, login with the Strava account and check out some of the targeted offers, but onwards from there a notification system has to take over. This could be in the form of email, tweets, push notifications to mobile device or any other channel, but I believe it has to be active for it to have any value.

## Monetization
Let’s say the data collection part of the app is done and the app has decided which shoes to look for deals on. How to find the deals?

Amazon is a given. Amazon has a free API where you can submit quite advanced queries and sort by “most discounted” or “lowest price”. You can also sign up for an affiliate account and get kickback when the users of the app buy shoes (or other things from Amazon).

[Skimlinks](http://www.skimlinks.com/) has a closed beta of a product API which looks very promising. Skimlinks has a huge collection of third-party monetizable products, including running shoes and other sports equipment. All available through a REST-based API. Read more about it [here](http://api-products.skimlinks.com/doc/).

Ads. Let Google do the job. Provide information and news about the shoes to the app users, set aside some room for Google ads, and trust that based on the content of the page, Google will find the best deals for your users.

## Conclusion
I won’t be taking this idea any further. At best, it’s a “feature” for strava.com, not a good enough idea to base a separate app off of. That said, I would probably use this myself if it was implemented well enough. I can also see this being a fun weekend project to learn a new tool or framework while working on something that may provide some value.