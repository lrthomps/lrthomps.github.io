---
layout: post
use_math: false
use_carousel: true
title:  "How Hard Do You Climb?"
subtitle: "and can a model help you climb harder?"
tags: ["machine learning", "climbing"]
date:   2021-11-01
summary: Analysis of a climbing survey dataset to test the wisdom of the crowd in how best to improve at climbing. 

---

I've been on and off climbing for nearly two decades, beginning with years of mountaineering and easy (<5.9) trad, building up to a lead of Exasperator 5.10c (in two pitches) and a lone V2 in the Squamish grandwall boulders. This summer was the first that I devoted to bouldering and the first time that I did any kind of training. After a few months with a weekly training session[^summertraining], I started getting "<a href="https://hiveclimbing.com/start-here/#explained">4-hex</a>" routes regularly at the Hive, a V5 on the kilter board[^kilter], started getting outdoor V2s more easily (including a 12 yr later repeat of that first V2) and got my first outdoor V3[^v3]. 

[^summertraining]: An intensive core series (~30-45min) followed by max strength training for pull-ups and push-ups (5 sets of 5 reps of progressively difficult variations).

[^kilter]: Writing this post is what pushed me to try V5 at all! When the models said I was underperforming I had to consider: am I not trying hard often enough? And yes, if I try hard, I can climb harder!

[^v3]: &hellip;followed by another three V3s while visiting the Okanagan! I guess the edgier basalt columns and gneiss rock are closer to indoor bouldering. For local granite, I need to work on sloper strength and tricky mantels!

Being data minded, as a runner, I've already been tracking my runs and rest heart rate (for recovery stats) with a Garmin watch, so of course I tracked all my training sessions but, beyond noting new grades climbed, I wasn't tracking anything else. But what metrics are most relevant to climbing? Number of pull-ups? How small an edge I can hang from? Or how steep a sloper? From that, can I estimate what grade I should be climbing at?

The <a href="https://gripped.com/indoor-climbing/how-close-are-you-to-climbing-5-15d/">9c "ultimate" climbing test</a>[^9ctest] is everywhere on social media and estimates your highest achievable[^9ctestgap] grade given max finger strength, max (single) pull-up strength, core strength and endurance (hanging from a bar). I get a very lopsided score of 14 dominated nearly entirely by core strength. Should the scores be more equal? Does a 6 in one really make up for a 2 in another?

[^9ctest]: Magnus Midtb&oslash;&rsquo;s <a href="https://www.youtube.com/watch?v=UOBB4wkTdxQ">video</a> of getting assessed by the test creators, Martin Mobr&aring;ten and Stian Christophersen (authors of The Climbing Bible), set off endless posts and videos of climbers everywhere doing the 9c test&mdash;if I feel ambitious and bored someday, I'll compile results.

[^9ctestgap]: The gap between your actual grade and this predicted grade can apparently be attributed to lack of technique and/or mobility, poor strategy or lacking mental strength. Aka, everything we can't really measure. 

The <a href="https://strengthclimbing.com/finger-strength-analyzer/">Climbing Finger Strength Analyzer 2.0</a> takes finger strength and pull-up strength as inputs and estimates your V grade. I get a V3 estimate with a 36% probability of climbing V5 and the assessment that my "upper body strength is quite high compared to [my] finger strength" and to stop training it in favour of improving finger strength. That's with pull up strength roughly on par to finger strength (in the common protocols); if I increase finger strength by 1.5x then my "upper body strength is on par with [my] finger strength" and, up to 2x then my "upper body strength is slightly low compared to [my] finger strength". We'll come back to this ratio.

Lattice Training does another <a href="https://latticetraining.com/product/my-fingers/">finger assessment</a>: given your finger strength in your preferred grip (half crimp or open hand) for a 7s on a 20mm hang, they'll "compare your data to [their] models so you can find out how your finger strength compares to other similar climbers". [and I get?] Ok, but I want to build my own models and include more than just finger strength. 

The <a href="https://docs.google.com/spreadsheets/u/0/d/1J6d45EqIlIsIqNdi2X-Zl-EGFxf9d9T3R_W55xrpEAs/edit">dataset</a> that I'll use includes many strength metrics, training habits and basic climber attributes[^otherdata]. I'll focus on bouldering and ask questions like: which metrics are important for bouldering? how balanced should a strength profile be? what progression of strength is most common in going from V-low to V-med to V-hi? 

Megan, better known as <a href="https://www.instagram.com/fearlesstofu/">@fearlesstofu</a> in social media, kindly submitted her survey responses as well as those of a strong climbing friend, Nelson <a href="https://www.instagram.com/aloeveraelephant/">@aloeveraelephant</a>[^seethemclimb]. I'll see how typical we all are and try to assess our relative strengths and weaknesses (we're nicely spread out in max V grade which makes for especially aesthetic plots!) Then, based on my findings (and taking into what I've learned in all my covid reading), I'll present a practical training assessment including strenth targets and ratios (aka, my winter plans). 


[^otherdata]: Other datasets exist, most notably the scrapped submissions from 8a.nu <a href="https://www.kaggle.com/dcohen21/8anu-climbing-logbook">downloadable</a> from kaggle.  <a href="https://latticetraining.com">Lattice Training</a> released an interesting finger strength vs V grade that we'll compare with. 

[^seethemclimb]: To see them climb, I highly recommend <a href="https://www.youtube.com/c/FearlessTofu">Megan's YouTube channel; you can see Nelson in 2 of her recent videos: in "<a href="https://www.youtube.com/watch?v=HrGscD-nyMc&t=270s">Friends try my moonboard</a>" wearing orange shorts and a blue tank top, and in "<a href="https://www.youtube.com/watch?v=Q2nP8j-FhSM">We try the FOREARM CHALLENGE</a>".
 

## Interlude: reading plots

If you see a bar chart, I'm counting climbers per value of V grade or number of years, or binned values (aka how many in each interval) as in the ape index chart where we count in 1cm .

If you see a scatter plot (lots of dots), each point is one climber from the dataset with coordinates of eg. height (on the vertical axis) versus V grade (on the horizontal axis). I'll always superpose a line that shows the average (height) over climbers (at each V grade). 

Pink is for female climbers; blue for male; purple is for all climbers.

## About the Climbers in the Dataset

The climbers surveyed include 80 women and 514 men. The women are on average lighter (58kg / 72kg), shorter (165cm /  179cm), have a shorter ape index by more than 1cm, have been climbing 4 months less, climb 15min less per week, train 20min less per week, are weaker in all measures except they can hold an L-sit longer (45s / 35s); they climb 1-2 V grades lower but their hardest grade is closer to the grade they can send 90-100% of the time. Higher V grade climbers are more likely to climb outside (nearly everyone in this dataset climbs inside).


<script type="text/javascript">

$(document).ready(function(){
  $('#carousel_stats, #carousel_strengths, #carousel_del_s, #carousel_preds, #carousel_feats, #carousel_del_y, #carousel_del_s_s2').carousel({
  interval: false
  });     
  
});

</script>
<div id="wrapper">

<div id="carousel_stats" class="carousel slide">
  <div class="carousel-inner">
    <div class="item active">
      <img src="{{ "/assets/images/climbing/histogram_by_grade.png" | relative_url }}">
      <p class="caption">V6 is the most common grade&colon; a peak in the men's, but more of a bump in the women’s distribution (and have a second bump at V9). Lattice Training noticed this and called it a milestone grade. Megan is left of that second bump so clearly she’ll get a V9 imminently; Nelson sits in the blue V11 bar; and I’m just shy of the first pink bump so by similar logic I should get a V6 soon! Note that these are Megan and my indoor grades; <a href="https://www.youtube.com/watch?v=PLRYD1q6VrQ">Megan's outdoor hardest climb</a> was a V7 while mine was a V3. This discrepancy may be a known <a href="https://boulderingboss.com/indoor-vs-outdoor-bouldering-is-there-a-difference-in-v-grades/">trend in gym route grading</a>.</p>
  </div>
  <div class="item">
    <img src="{{ "/assets/images/climbing/histogram_by_inoutdoor.png" | relative_url }}">
    <p class="caption">If we break down those grades by who climbs indoors vs outdoors we find that most strong climbers (also) climb outside whereas the majority of beginners only climb inside. I started with outdoors only and came inside to increase volume. For those that started inside, I strongly suggest trying bouldering on real rock. It’ll challenge your route reading infinitely more, the footwork is almost always harder and the variety of grips you’ll practise is endless.</p>
  </div>
  <div class="item">
    <img src="{{ "/assets/images/climbing/histogram_by_year.png" | relative_url }}">
    <p class="caption">Majority of climbers are in their first 4 years of climbing. Megan has been climbing 6 years; Nelson, 5. For modelling purposes later, I put myself down for ~5-10 years to take out the many skipped years since I started climbing in grad school. </p>
  </div>
  <div class="item">
    <img src="{{ "/assets/images/climbing/height.png" | relative_url }}">
    <p class="caption">Higher V grade male climbers then to be shorter; but higher V grade female climbers then to be taller. At 5’1”, Megan is the shortest in this dataset at V8&colon; clearly height is not holding her back!</p>
  </div>
  <div class="item">
    <img src="{{ "/assets/images/climbing/apeindex.png" | relative_url }}">
    <p class="caption">There are more climbers with +ve index than -ve and I wonder if this generalizes to non-climbers. I sit at -4cm while both Megan and Nelson have an ape index of +4cm. Kai Lightner has a stupendous ape index of +18cm; at 190cm tall, that's a >2m arm span!</p>
  </div>    
  <div class="item">
    <img src="{{ "/assets/images/climbing/bmi.png" | relative_url }}">
    <p class="caption">BMI is crude scaling of weight and height (about as accurate as the physics joke "approximate the cow by a sphere"). It doesn’t differentiate muscle with fat and muscle is 20% heavier per volume than fat. It seems the trend vs V grade in men is to drop in BMI (from >25 to 22) while in women the trend is actually to increase (from <18 to ~21). Possibly, the optimal BMI is 21-22 for both genders[^probmi].</p>
  </div>    
  <div class="item">
    <img src="{{ "/assets/images/climbing/hoursclimbing.png" | relative_url }}">
    <p class="caption">The highest V grade climbers climb roughly twice as much per week as the beginners. This is as much about what a person can handle and still recover (skin not least of all). </p>
  </div>
  <div class="item">
    <img src="{{ "/assets/images/climbing/hourstraining.png" | relative_url }}">
    <p class="caption">Beginners don’t train at all, nor should they necessarily, while the highest V grade climbers average 5-8 hours per week (this includes both climbing-specific training and general strength training). Ignore the women’s regression going negative: don’t worry, they can’t actually <em>untrain</em>.</p>
  </div>
</div>
<a class="carousel-control left" href="#carousel_stats" data-slide="prev">&lsaquo;</a>
<a class="carousel-control right" href="#carousel_stats" data-slide="next">&rsaquo;</a>
</div>
</div>

[^probmi]: <a href="https://www.reddit.com/r/climbharder/comments/el9pow/climbing_height_vs_weight_from_mani/">The BMI of the pros</a> are more typically borderline or outright underweight (defined as 18.5). Hopefully these are their "performance weights" and not their "training/recovery weight". There's a <a href="https://www.youtube.com/watch?v=aSepsUJKdHs&t=1225s">segment in this video</a> where Alex Huber talks about getting down from his training 68kg down to 9a climbing weight 62kg (he's 176cm so that's going from a bmi of 22 down to 20). 


## Strength by Grade

Blah blah.

<div id="wrapper">
<div id="carousel_strengths" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/halfcrimp.png" | relative_url }}">
        <p class="caption">Often touted to be the most predictive of strength metrics, the maximum weight a climber can add to a 10s hang on an 18mm[^18mm] edge normalized by the climber’s weight. Both Megan and Nelson seem to outperform given their finger strength (they're less strong than others of the same grade). Despite differences in protocol, the trends here agree fairly well with a <a href="https://www.instagram.com/p/B9zNGplJMyG/">post from Lattice Training</a> (cf. ~1.3 for V5, ~1.45 for V8 and ~1.6 for V11). Quite possibly, finger strength is the one metric you can never be strong in. In another <a href="https://latticetraining.com/2017/09/07/9c-adam-ondra-alex-megos/">post</a>, Lattice Training estimates that to climb 9c one must be able to add 110% their bodyweight (atop their bodyweight, making 210% total strength) to climb 9c. Alex Megos can add 132% to his 7s/20mm hangs!</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/openhand.png" | relative_url }}">
        <p class="caption">The equivalent for open hand grips is noisier&colon; fewer climbers reported open hand strength. Now both Megan and Nelson are stronger than others at their V grade while I’m the least strong in mine (generally climbers didn't often report any weighted metrics that involved weight removed; maybe all those that didn't answer were more likely not not manage body weight alone?) In <a href="https://www.v-publishing.co.uk/books/climbing/beastmaking/">Beastmaking</a>, the author suggests that hand anatomy plays a role in which grip a climber favours. Full- and half-crimp place more strain on the finger pulleys and open-hand[^openinjuries] transfers better to slopers&colon; I know what I need to train!</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/5reppullups.png" | relative_url }}">
        <p class="caption">While finger strength didn’t show a big gender difference, the normalized weight added to 5 pull-ups is 10-20% more at a given grade for male climbers. Either the women make due with less pull up strength or they default to problems that don’t require it. I’m pleased to see both Megan and Nelson climb hard given pulling strength.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/lsit.png" | relative_url }}">
        <p class="caption">If this looks random, it’s because less than a quarter of people submitted their L-sit time (and, actually, a further 9 climbers are cut off; L-sit times went as high as 10min including one woman at V3 who held for nearly 5min!) One issue may be that if you google  “L-sit” you get the standard, much harder sitting version and the one climbers refer to is actually the “hanging L-sit” (in my own climbing group, some hadn't even heard of them). Also, many climbers suspiciously answered an even 30s and 60s. Were they just guessing or did they get bored and drop early. Even though going from a hanging L-sit to a front lever is a harsh jump, the 9c climbing test progression is clearly better than one fixed exercise. Just as they allowed a progression of tucked knees for the L-sit, I’d suggest also using a <a href="https://www.gymclimber.com/front-lever-progression-for-climbers/">progression to front level</a>.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/pull_pushups.png" | relative_url }}">
        <p class="caption">For any given grade, the male climbers seem to do twice as many pull-ups or push-ups as the women (a further eight male climbers are cut off in the right plot, one claiming 286 push-ups!) From the trends, it looks like more modest goals of max 20 pull-ups and max 30 push-ups are better for climbing (and we'll see later than the models agree). For the boulderer, unweighted pull-ups are essentially an endurance test. The 5-rep weighted tests power endurance, far more relevant to bouldering. If we add a single-rep weighted pull-up to the assessment, we can measure pure strength as well.</p>
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_strengths" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_strengths" data-slide="next">
      &rsaquo;
    </a>
  </div>

</div>


[^18mm]: Though more commonly, an edge size of 20mm is used both because it is ever so slightly safer while being just as effective a training size, and 20 is a round number in the metric world (even in the imperial world, 3/4” ~ 19mm, the thickness of blahx1 lumber); and the hold is only 5-7s. 10s is very long!

[^openinjuries]: Open hand grips can lead to overuse injuries in the form of <a href="https://theclimbingdoctor.com/rock-climbing-finger-tenosynovitis/">finger tendon tenosynovitis</a>.

What about differences in strength metrics: how should the two grips compare for finger strength? How does finger strength compare with pulling strength? 

<div id="wrapper">
<div id="carousel_del_s" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active" style="height: 550px">
        <img src="{{ "/assets/images/climbing/delta_fingers.png" | relative_url }}">
        <p class="caption">Half crimp and open hand strength are typically equal. Considering the merits of both, I think I can stand to train my open hand to catch up to my crimp while Megan and Nelson (who I’ve seen use crimps in videos!) may do well to train their half crimp to catch up to their open hand.</p>
      </div>
      <div class="item" style="height: 550px">
        <img src="{{ "/assets/images/climbing/pull_finger.png" | relative_url }}" style="max-height: 75%;">
        <p class="caption">Here I subtracted the finger strength (whichever was higher) from the 5-rep pulling strength. At higher V-grades, finger strength begins to exceed pulling strength for both women and men. When training, at first if you are weak in all aspects, it makes sense to increase your pulling strength to keep up or exceed your finger strength since it is safer and faster to gain. As you get stronger fingers, let your pulling strength lag behind (unless you want to climb steep, compression climbs all day, then, by all means, continue to get more pulling strength). As with all strength training, it’s important to constantly adapt all strength gains into climbing gains before working to get any stronger still. Two climbers were cropped to better see the trend: they had excess pulling strength of 3 body weights!</p>
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_del_s" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_del_s" data-slide="next">
      &rsaquo;
    </a>
  </div>
</div>

## Bouldering Predictions

With a dataset of nearly 600 climbers, I could train a model[^models] to predict the hardest V grade each climber had reached given their strength metrics and training habits. Shockingly, the model was better than expected with some regression to the mean (that is, low V grade climbers were predicted high, while high V grade climbers were predicted low) with typical errors ~1-2 V grades. 

[^models]: Several in fact, of various kinds: I started with linear regression, went to 2-4 layer dense neural networks before finally settling on random forests (which, of course, are usually best for this kind of tabular data). I trained many of each kind and chose the model type that gave the most consistent feature importance estimates. 


<div id="wrapper">
<div id="carousel_preds" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/pred_max.png" | relative_url }}" style="max-height: 100%;">
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/pred_max_recent.png" | relative_url }}" style="max-height: 100%;">
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/pred_doable.png" | relative_url }}" style="max-height: 100%;">
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_preds" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_preds" data-slide="next">
      &rsaquo;
    </a>
  </div>
</div>


<p class="caption">This small model was trained holding out a random 30 climbers including Megan, Nelson and I, shown in green: it generalizes well to this unseen data. The model is biased to predicting high for lower V grade climbers and low for higher V grade climbers (known as regressing to the mean) which makes my higher than true and Nelson’s lower than true predictions less concerning (aka, maybe I’m not underperforming by the full 1.5 V grades; but Nelson should still feel complimented for out climbing the predictions based on his metrics!)</p>


In predicting each of the reported bouldering grades, the model can be assessed for how important it found each feature of the climber. In nearly every model I trained for every grade, the most important feature is number of years climbed. After all: 

>     Climbing is the best training for climbing
>       ~ according to basically everyone

But commonly the number of pull-ups were appear more important than the actual pull-up strength. Surely in bouldering, number of pull-ups is more an an endurance feat while 5-rep is roughly strength endurance (single rep max weighted pull-ups would better assess pure strength). If most boulders feature 5 moves, this should be the most important (pull-up) feature. The reason I think they come reversed is that 3/4 of climbers reported number of pull-ups while less than half reported weighted ones. There's just more information in the former for the model to learn from.
That said, it's astonishing that half crimp strength was the most common second most used feature when only 35% of climbers reported it!


<div id="wrapper">
<div id="carousel_feats" class="carousel slide">
  <div class="carousel-inner">
    <div class="item active" style="height: 750px">
      <img src="{{ "/assets/images/climbing/feats_max.png" | relative_url }}" style="max-height: 100%;">
    </div>
    <div class="item" style="height: 750px">
      <img src="{{ "/assets/images/climbing/feats_max_recent.png" | relative_url }}" style="max-height: 100%;">
    </div>
    <div class="item" style="height: 750px">
      <img src="{{ "/assets/images/climbing/feats_doable.png" | relative_url }}" style="max-height: 100%;">
    </div>
  </div>
  <a class="carousel-control left" href="#carousel_feats" data-slide="prev">
    &lsaquo;
  </a>
  <a class="carousel-control right" href="#carousel_feats" data-slide="next">
    &rsaquo;
  </a>
  </div>
</div>


<p class="caption">As found by the model, the most important aspect of a climber to guess their highest V grade is how long they’ve been climbing! Next we see half crimp strength dominate, followed by BMI and max pull up reps where lower and higher are not strictly better. The effect size of each aspect depends on the particular climber’s profiles. NB: the scale is relative but meaningless.</p>

<div id="wrapper">
<div id="carousel_del_y" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/del_y_max.png" | relative_url }}" style="max-height: 100%;">
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/del_y_max_recent.png" | relative_url }}" style="max-height: 100%;">
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/del_y_doable.png" | relative_url }}" style="max-height: 100%;">
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_del_y" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_del_y" data-slide="next">
      &rsaquo;
    </a>
  </div>
</div>

<p class="caption">Change no habits, even if continuing various kinds of training, if you get no stronger and just climb another year and you’ll improve by 0.5 to nearly 2 V grades in your first 4 years.</p>


<div id="wrapper">
<div id="carousel_del_s_s2" class="carousel slide">
  <div class="carousel-inner">
    <div class="item active" style="height: 750px">
      <p class="figtitle">Predicting max V grade</p>
      <img src="{{ "/assets/images/climbing/del_s_max.png" | relative_url }}" style="max-height: 370px;">
      <img src="{{ "/assets/images/climbing/del_s2_max.png" | relative_url }}" style="max-height: 355px;">
    </div>
    <div class="item" style="height: 750px">
      <p class="figtitle">Predicting max recent V grade</p>
      <img src="{{ "/assets/images/climbing/del_s_max_recent.png" | relative_url }}" style="max-height: 370px;">
      <img src="{{ "/assets/images/climbing/del_s2_max_recent.png" | relative_url }}" style="max-height: 355px;">
    </div>
    <div class="item" style="height: 750px">
      <p class="figtitle">Predicting ~doable V grade</p>
      <img src="{{ "/assets/images/climbing/del_s_doable.png" | relative_url }}" style="max-height: 370px;">
      <img src="{{ "/assets/images/climbing/del_s2_doable.png" | relative_url }}" style="max-height: 355px;">
    </div>
  </div>
  <a class="carousel-control left" href="#carousel_del_s_s2" data-slide="prev">
    &lsaquo;
  </a>
  <a class="carousel-control right" href="#carousel_del_s_s2" data-slide="next">
    &rsaquo;
  </a>
  </div>
</div>

<p class="caption">The predicted grade shift for increased strength metrics all follow a similar pattern: there are no gains (and sometimes expected losses!) for increasing strength at the lowest levels. I interpret this as the usual advice from trainers and climbers alike: to improve at climbing, at first, focus on climbing. You will naturally get stronger. Once a minimal strength is reached (10s hangs are possible on a 20mm edge; can do 5 pull ups and 10 push ups; can do a hanging L-sit) then increasing them further yields greater gains. Once a certain strength is reached however, the gains saturate. The data sets the upper limits at hangs with body weight added, 5-rep pull-ups with less than half body weight added, 20 pull-ups, 30 push-ups, 37s of hanging L-sit (chosen so arbitrarily precise because that is Megan’s L-sit time!). </p>

It’s tricky to assess the expected V grade change with BMI change as it affects all the normalized strength metrics. Clearly the denominator (weight) changes directly as BMI is proportional to weight, and if the BMI drop is only excess fat and superfluous muscle then we can imagine that the muscles can still support the original weight and the finger and pulling strengths will seem to increase by the weight lost. Of course, this is <em>not</em> a reasonable assumption in many climbers, especially in the lower BMI / % body fat range[^bodyweight]. If a BMI gain is only in muscles used in grip and pull strengths, then even though the weight increases, the strength gains should keep up or even exceed the added weight. For BMIs under 20, the expected V grade increases if BMI increases by 0.5. Lowering BMI by 0.5 only increased V grade prediction through adjusted strength metrics.

[^bodyweight]: This is an entire topic on its own and not one I'm well placed to talk about. For some people it’s rather clear that we can lose some fat to get into better climbing condition (whether our goal actually demand it is yet another matter); for others, the margin is getting very slim. Read the recent thread on weight, diet and training by professional boulderer Staša Gejo <a href="https://www.instagram.com/gejostasa/">@gejostasa</a> starting with <a href="https://www.instagram.com/p/CUQabPzMvuU/">this one</a>.


Using myself as an example to clarify these strength adjustments, I weigh a little under 140lbs and am 168 cm / 5’6.5” tall. I can currently add 25.5 lbs to my half crimp hangs; 25 lbs to my 5-rep pull-ups; and have to take away 25.5 lbs to do open hand hangs. My BMI goes down by 0.5 if my weight drops by 3 lbs[^3lbs]. If my strength doesn’t change, I’ll be able to hang and pull with 28.5 / 28 / -22.5 lbs. With those 4 updated metrics (BMI and the three normalized strengths; note that we’re still ignoring any changes in pull ups, push ups or L-sits), the model predicts I can push my bouldering ~2.5 V grades higher (the comparison +0.5 BMI drops my V grade by a mere 0.13 assuming no strength adjustments necessary). If that sounds overly optimistic, I agree: the model is telling me that others with that BMI and those strength metrics climb V9 (the model originally predicted high for me); but they may also generally have more technique and mobility, and losing weight won’t magically help me with either. 

[^3lbs]: I had a lazy second half of my 30s and my weight drifted from a lean and muscular 130 lbs to a soft and weak 140 lbs. Training this summer so far has unsoftened me somewhat and strengthened me oodles with weight dropping just a little. All to say, it’s not unreasonable to think I have 3 lbs of excess fat. 

... gender changes?


## What if...


For fun next, I’ll have the model recommend modified profiles for Megan, Nelson and I to reach the next V grade. The model is under-predicting for Nelson by over 2 V grades and over-predicting about the same for me, so I’ll be comparing before and after model predictions (and ignoring our actual climbing grades). Keep in mind that assumes the “wisdom of the crowd” in this dataset is accurate; one substitution I’ll make is to switch campus board to system board training. It’s more climbing specific and can be used just as effectively to develop power. 

Megan: 1 year later, climbing 6 hours a week with no additional training, she only needs to increase her half crimp strength by 10% and the model predicts she’ll reach the next V grade!

Nelson: 1 year later, climbing an extra hour per week and adding 1 hr of training, max hangs 2x / week, if he increases both grip strengths by 10%, the model anticipates a V grade improvements.

Lara: 1 year later, still climbing 6 hours a week and training for 1 hr, starting 2x / week max hangs[^onearmhangs], if I increase both half crimp and open hand strength another 10% of body weight the model predicts I push one more V grade.

[^onearmhangs]: Actually, model predicts that if I hang one-armed I get an even greater return. Strangely, it did not have the same expected change for Nelson or Megan. Yes, my left is weaker but how did the model know that I'm imbalanced? Are all V-middling climbers imbalanced? Kidding aside, it means that climbers otherwise like me but only climb a little harder train one-armed &mdash; maybe <a href="https://www.youtube.com/watch?v=IUOm2IHylpA">farmer crimps</a>? 

## A Better Bouldering Assessment

add mobility metrics
add 1 rep pull-up
progression for core
add or modify hangs to 5s or 7s
add hang endurance test? some number of 7/3 repeaters, what weight can be added?
track indoor, system board and outdoor grades
keep:
5 rep pull-ups
number of pull-ups, push-ups


## Further Reading and Other Resources

