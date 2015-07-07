---
layout: post
title: Simple Scala habits saved us on launch
---

Months after it happened, the launch of Egraphs still feels like a blur. There was the crazy rush to finish the site in the weeks leading up, publishing the site from Tropicana Field as the Rays played the Red Sox, and watching baseball fans show up and actually start spending money.

I would have preferred to avoid any development death marches, but we were committed to July 12 because we were working with external partners including the MLB, the Rays, and an initial lineup of celebrity partners including David Ortiz and Pedro Martinez. How many startups out can say that they have so much support on day one?

One thing that naturally occurred is that we stopped writing tests in the six weeks leading up to launch. It’s not something I’m proud of, but amazingly the site didn’t croak when customers started using it. We saw zero null pointer exceptions and very few logic bugs, and I attribute that to easy Scala habits we adopted to great effect.

For example, to achieve null-safety, we avoided calling Option.get like the plague. Scala allows you to access objects that might or might have been instantiated with map, or match, or for-comprehension. That one habit is responsible for the rarity of NPEs for us.

Secondly, we relied on type-safety as much as possible. If branching on the state of something to determine which logic path to execute, we got specific with types. It’s a beautiful thing to be able to write a lot of code and feel confident that if it compiles, then it likely works.
