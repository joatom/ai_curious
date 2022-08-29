# Art and Diffusion
Some thoughts about ML/AI and art.
## Human-machine interaction

In summer 2016 I spent a day with [my brother](http://www.maximilian-tomasoni.com/) at his studio in [Monastery of Bentlage](https://www.kloster-bentlage.de/en/kunst-kultur-en/bentlage-print-society) to try out fine art printing. The monastery is located in the country side and is a very calming place to escape from everyday life.
As preparation for the workshop my brother asked us to prepare a drawing. I'm not a good drawer, my hands are shaky and whatever comes out of the pencil never looks like what I intended to draw. Luckily, I was experimenting with edge-detecting algorithms at that time. The algorithm I was implementing was suitable to create an image that looked like a drawing. I took a picture of my son where he was playing with the Neato and run my program to extract the contours of my son and the vacuum robot. The setting of me generating a drawing with an algorithm and the motive of my son playing with a robot was very appealing.
In the workshop we used the drawing as template for our artwork. The printing technique we applied to create the artwork is called etching. The classical look and feel of this centuries old technique was a nice contrast to the rather modern motive - a kid playing with a smart robot. Yet, it made the interaction between humans and robots look pretty normal. And I was proud of my amateurish accomplishments.

<p align="center">
	<img width=50% src=":/9a2f182d41a14e53926efb624bf7ded9"/>
</p>

A few weeks later I was attending a TEDx event in Münster. One of the [talks](https://www.youtube.com/watch?v=oVE5rRJa0D8) was given by an artist called [Roman Lipski](https://www.romanlipski.com/) and an art collective called [YQP](http://www.yqp.computer/). Surprisingly, they introduced their concept of art where the artist interacts with an Artificial Muse. The Muse (an algorithm) learned Lipski’s style from his paintings and generated images in his style. The painter than used the generated image as inspiration (Muse) to paint a new picture on canvas.
This was in 2016 right after google shared there [Deep Dream](http://ai.googleblog.com/2015/06/inceptionism-going-deeper-into-neural.html) accomplishments and [Style Transfer](http://arxiv.org/abs/1508.06576) was a hot topic in the tech community. Lipski and his team envisioned the natural interaction between AI and humans to create art.
In 2016 I was not practicing ML yet, nor was I heavily involved into art, besides seeing my brother every now-and-than. But, after this TED talk it was obvious that computer generated images will have a high impact on arts in the future. But will it be interruptive?

## What is art? Or, why is art?

There are countless definitions and strong opinions about *What is Art* and what not. Let’s ignore this question for now and rather raise the question:
*Why does Art exists?*
As said I’m not an art professional, but a few answers are obvious:

Art exists because of,
- the human nature:
    - people love to be creative,
    - people love beauty,
    - people use different forms to express feelings,
    - people love stories and imagination
- political and sociological activities:
    - people, who are suppressed, can hide critics in art,
    - people can visualize opinions,
    - people use art to defame opponents
…

There certainly are many more categories and reasons. However, a few things stands out.

- Art is an highly influential medium to form opinions using the imaginary power of the viewer. To the point where the viewer’s imagination can go way beyond the obvious object. For example, if you look at a picture with a house in a landscape and the rich and shiny oil colors take your imagination from the museum right to Toscana.
- People also practice art for their own sake.

So why do we get confused about the question *What is art?* Some of the techniques that are used in art are also used for other purpose.
Let’s take drawing. An architect uses drawing technics to plot a diagram of a house. The plot may including information about wall measures, plug-ins for water and electricity, etc. Usually you wouldn’t consider that kind of plot as a piece of art, though it still requires a bit of imagination from the viewer. The technical drawing intends to be easy accessible for the interpreter and thus provides the obvious information (e.g. measures of the wall in centimeters). At some point however, the technical drawing diffuses into art. - It still can serve the original purpose, though. - A technical drawing can be of such of an elegance that it my raise strong feelings in the viewer - or the drawer. Than it becomes art. Don’t you feel joy or fascination when you are looking at Christo’s drawings?

Back to the question, *will advancements in AI/ML disrupt Art?* No! Every argument I used for my definition of art includes the humans at some point. There is no perception of beauty or expression of feelings without humans nor is there any political or social implications without humans.
*Will AI/ML heavily influence the arts and creativity?* Yes! We will gain an impressive tool set and techniques. And we can see that Computers are already being creative in certain environment (e.g. generative ML-models).

## Diffusion

Computers are magical and support you being creative. I remember in the 90’s when we used to create flyers for our parties. The visual effects of the graphic programs were so fascinating that we had to use almost all of them. That always ended up looking like flyers of psychedelic 70’s parties rather then flyers of cool underground techno parties.
25 years later the algorithms are getting very sophisticated. Images can be created out of noise or text. Existing images can be transformed to adapt the style of another painter or to look totally different.
At the time that I’m writing this article Diffusion Models are trending. Their strength is to modify existing images by adding noise to the image and then transforming the image while reducing the added noise again. The models can be combined with text encoders that you can basically tell the Computer how you want a given image to change.

This summer my brother called me up because someone spontaneously dropped out of a workshop he was offering that weekend and if I wanted to join. I signed up for the two day offside and since I missed the first day I needed to come up with a good template quickly. I decided to use one of the publicly available Diffusion Models to get started. I picked [Disco Diffusion](https://colab.research.google.com/github/alembics/disco-diffusion/blob/main/Disco_Diffusion.ipynb), where a handy [tutorial](https://www.youtube.com/watch?v=wIw59kAU6u8) was available. I added one of my favorite photos of the kids to the model and as text input I asked the model to change the model into something like “*Three children waiting for a bus in a photorealistic cyberpunk town. Red, blue, black, dark cyberpunk scheme.*”. I did a bit of parameter tuning and after two hours I had a few templates to work with on the workshop.

<table>
	<tr>
		<td><img src=":/d5d42071d7994f58bba60d0e85681920"/></td>
 		<td><img src=":/f81328a33a1d4e3f9aab2ed954fc4ca7"></td>
	</tr>
	<tr>
		<td>Original photo (censored)</td>
		<td>Combination of two generated images</td>
	</tr>
</table>

On this workshop we applied screen printing technique and due to time restrictions were limited to two (color) layers. I used the original photo and the generated images as inspiration for the print. I wouldn’t call it Muse in my case because it was rather a template I abstracted from. But if I’d be a professional artist I would definitely use the algorithms somehow.

<table>
	<tr>
		<td><img src=":/ce16b57c6f464c5e99f167f484d980ed"/></td>
 		<td><img src=":/b3f2c261a30e40718c451ce6a1cf6e5f"/></td>
 		<td><img src=":/19fbf71613f447d49c5d00140ee8f083"/></td>
 		<td><img src=":/da6357f75ece4277b7ebca7ca953c9c7"/></td>
 		<td><img src=":/ef26c8e1e2b44fe9b0bd5007f2c4c669"/></td>
		<td><img src=":/89128c0352a043edae940e5c4a9cc517"</td>
	</tr>
</table>

For me as an amateur the fulfillment lays rather in the relaxing hours, escaping routines, chatting with people, while hand crafting some little artwork to use as Christmas cards or to hang on the walls at home.

![](:/4b3cf5e245144cfdabd642c8bc1b3959)
