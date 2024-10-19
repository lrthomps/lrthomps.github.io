---
title:  "Site overhaul to get <strike>rid of</strike> Jekyll"
subtitle: "...and get things working again!"
categories: ["other"]
date:   2020-09-07
description: If you know html+css, why use a framework? Turns out, a few reasons.

---


<p>I had great intentions last summer to add more regular posts: more paper summaries, worked through ideas, etc. But [excuses]. Fast forward to now, I have notes to put up but have since switched entirely from a mac to Ubuntu, discovered a far better app to edit markdown with math, <a href="https://www.typora.io/">Typora</a> (not freeware but so good I'll pay once it's out of beta [looking back in 2024: I did!]), and I couldn't get the new post to render properly (some strange auto-scaling was happening).</p>
<p>After I wasted over nearly two days debugging Jekyll (cause stuff happened outside of my template files), I gave up. In a couple of hours, I was rid of Jekyll, rid of frameworks and down to raw html+css. Gotta say, html5 once you give in to it, is damn nice compared to circa 2004 wed development (my work is still <a href="https://pitp.phas.ubc.ca/">live</a> [*still* live in 2024], don't look). </p>
<p>A few  things to share to anyone who's thinking of doing the same:</p>
<ul>
<li><p>before you do, keep in mind it worked for me because</p>
<ul>
<li>I know html+css but not Jekyll</li>
<li>I don't need a real blog (with feed, commenting, auto-generated file structure etc); though all I'm missing is the feed.xml file (except... see the next section)</li>

</ul>
</li>
<li><p>I copied code snippets from other sites, kept some css from the Jekyll minima theme, but my goal was to strip it back to the simplest it could be</p>
</li>
<li><p><a href="https://gist.github.com/">gist</a> for syntax highlighting of code, and let Github host and render</p>
</li>
<li><p>mathjax for latex math: I try to keep formulas from going too wide but if they must I choose to let them run over the page edge on small devices. It's better than squinting at scaled down math</p>
</li>
<li><p>colours: again, simple is best. Think of all the wonderful people that use a dark mode: does half your content disappear? It seems the majority of pages still have a white(ish) background, so I went with that too: it means the simplest dark modes that invert colours works for my site (e.g. Firefox iOS app).</p>
</li>

</ul>
<p>My favourite find to convert a picture of myself that didn't feel so [...]: cartoonize <a href='https://github.com/SystemErrorWang/White-box-Cartoonization'>project/paper</a> + <a href='https://cartoonize-lkqov62dia-de.a.run.app/'>demo</a>. It's another style transfer GAN, predominantly trained on <code>scenery images are collected from Shinkai Makoto, Miyazaki Hayao and Hosoda Mamoru films</code>. The cityscapes are the best, especially those with clouds. I used a picture from the approach on Mount Rainier: love what it did to the rocks, grass, trees and background hills!</p>

<h2>...and bringing Jekyll back</h2>

I considered getting the feed working manually, adding posts manually hereon, updating posts.html manually. But finally, I accepted the challenge of just getting Jekyll working after all. It was too much like installing a GPU for ML only &mdash; fighting against the grain &mdash; except in this case, why bother?

Main takeaways:

* no theme is required: I kept fighting the theme, elements kept not looking like they should. Overall, I failed the theme. But! no theme required! I had all the layout files anyway. Lesson learned. No theme.

* the theme I got rid of wanted assets in \_assets but normal Jekyll wants them in assets

* math: use \vert for pipes; \star for complex conjugate. Otherwise, pipes are interpreted as part of a table and stars italicize

* posts didn't have to get buried in folder hell: specify the file structure in \_config.yml: 

	```yml
	permalink: /posts/:title.html
	```

* feed.xml doesn't make it easy to *sign up* in the first place (though it does provide the actual feed): add to the header of the root layout 

	```html
	<link href='{{ "feed.xml" | relative_url }}' rel='alternate' type='application/atom+xml'>
	```
	For some reason, to sign up with <a href="https://feedly.com/">Feedly</a>, I have to enter `https://lrthomps.github.io/posts.html` to be found (not `feed.xml`). 

My Jekyll configuration is bare bones. By all means, <a href="https://github.com/lrthomps/lrthomps.github.io">copy</a> as much as you like!