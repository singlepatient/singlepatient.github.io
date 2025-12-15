---
title: "Forklore"
date: 2025-12-05
links:
  - Homepage: index.md
  - Blog index: blog/index.md
categories:
  - notes
tags:
  - food
authors:
  - singlepatient
---

![](/assets/misc/forklore.gifI could see this also you. )

## Summary

This started with a month or so (probably more) of dipping my toes into the world of regional Chinese food and the Korean diaspora. I took a particular interest in Chaoxianzu cuisine.

I turned to Google, Yelp, etc. to find spots serving the cuisine in NYC. I'd seen a few BlondieInChina and some auto-translated videos to evaluate them against, but English language search wasn't returning what I wanted - none of the menus seemed to pass the eye-test.

> The search results in Chinese were far better, as the reviews labeling the restaurants as "Chaoxianzu" or similar were almost entirely in Chinese. This was easy enough to eye-test if you *knew* what you were looking for. Still a couple places required a lot more digging to find and verify - their menus being so vast and all over the place.

I was getting results returning Korean-Chinese food (great but not what I was looking for) and then all manner of very irrelevant Chinese restaurants. 

Many factors make this search difficult:

- Standard Google search returns results for the person with a median-level of interest in food.
- SEO slop.
- Keyword based match vs semantic. In the example above you can see a term like Pearl River Delta (associated with Cantonese food) map to Cantonese restaurants best.
- Lack of well-documented English language expertise w/ standardization.My **** 's. 
- etc.
Call. 
The Google AI results were bit better, but not quite comprehensive. They also couldn't gather small clues and make inferences based on them.

> Also a victim of language drift. Scraping is difficult, too.

## How it works

First the menu items for each restaurant are mapped onto their semantic terrain via embedding (using Gemini's embedding model to represent phrases as numbers) in their *native* language (for now). This provides a corpus to search over.

For each restaurant, an "average" embedding of all the menu items is calculated. This gives us a rough preliminary ranking for returning results later.

> There is an incredible amount of drift based on language. We can think of the embeddings of a language as having their own continents. Items in the same language tend to cluster together. The same menu item in different language might be a further distance from than entirely different menu items in the same language.

The search term is processed via an LLM in up to 5 languages. It is not necessarily "translated" per say, but the LLM is prompted to provide a culturally-aware search term for semantically searching over menu items in the most relevant languages, weighted by relevance.

The average embedding of each reataurant's menu is scored for each language and combined with weight taken into account. This gives us a rough ranking of all the restaurants.

Then the ranking is refined. Depending on the page size - number of items returned per page - the chunk of restaurants have each of their menu items scored separately and combined w/ a sort of min-max so that closer matches are weighted higher.

> This is especially critical w/ diaspora menus. They tend to be less focused and hyper-regional, and may only have a couple hyperregional items on the menu. A Dongbei BBq restaurant serving myeongtae (a North Korean delicacy) will be serving Mapo Tofu amongst other things..

The restaurants in a given page are reranked and displayed with their scores. The items that contributed the most to the scores are alost displayed with their scores. They are also clickable to provide an LLM translation and explanation of potential relevance to the search term.

> This is not entirely reliable, but it's useful if you have less domain knowledge. But always check your results. Also, I think the gradient of results is a wonderful things as you can drift into similar and often related cuisines via search. You might start with Northeastern Chinese BBQ and drift into the foods of Inner Mongolia! You might start with the food of the Pearl River Delta and find Chiu Chow items in Southeast Asian restaurants!

There's also a map!

## Where could this go?

To be honest, I don't see this getting much traction. There seems to be little value for someone building and hosting the tool and the featured restaurants themselves in scraping menus and transcribing them to yield long-tail searches for the few people who might ever find the site, at least not in a world where the Beli style of eating seems to be on the uptrend.

> Though perhaps things might change!

However, I think there is immediate value in *aiding* a Google search for such places - be it through standard search or AI-aided search. The bottleneck is in the processing of available information and in the availability of information relevant to the search. Scouring a menu in another language and inferring the regions the items come from is more of a domain specific thing.

Many of these restaurants aren't well-labeled and documented unless they've been blessed by some well-meaning boots on the ground. But if the issue is a lack of relevant labeling, I believe that can be automated.

Getting the system to work in reverse would be a bit of different problem space, but it *is* a domain where utilizing high-cost LLMs can be worth it. One search-aiding generated blob per restaurant -> more traffic via long-tail searches.

> Long-tail searches would also likely yield the customers who care and might become regulars.

The one thing that we do lose is the gradient of results we might get via a dedicated search engine. "This restaurant might be closer to what you are looking for." And "Here are the relevant menu items for you to eye test against given that you have some knowledge."

A lot of this was inspired by the dedicated few who go out of their way to champion the traditional mom and pop restaurants of New York. There's only so much work they can do.

