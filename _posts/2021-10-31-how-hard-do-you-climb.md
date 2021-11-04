---
layout: post
use_math: false
use_carousel: true
title:  "A Better Assessment for Better Bouldering"
subtitle: "Data Backed Training Advice"
tags: ["machine learning", "climbing"]
date:   2021-10-31
summary: Analysis of a climbing survey dataset to test the wisdom of the crowd in how best to improve at climbing and assess training progress. 

---

<script type="text/javascript">
$(document).ready(function(){
  $('#carousel_intros').carousel();
  $('#carousel_stats, #carousel_strengths, #carousel_del_s, #carousel_preds, #carousel_grades').carousel(
    {interval: false}
    );  
});
</script>

During COVID, people were rushing to <a href="https://www.bbc.com/news/entertainment-arts-53637305">Netflix</a> and <a href="https://www.statista.com/statistics/1106313/youtube-usage-increase-due-to-coronavirus-home-usa/">YouTube</a>, but they also signed up with <a href="https://www.cnbc.com/2020/11/05/peloton-says-recent-spike-in-covid-19-cases-lockdowns-boosting-sales.html">Peloton</a>, and were <a href="https://runningmagazine.ca/the-scene/stravas-year-in-sport-report-tells-the-story-of-running-during-covid-19/">running and biking more than ever</a>. While the climbing gym was closed during early lockdown, <abbr class="float-notes" title="Before COVID, I nearly never used YouTube and the recommended videos for me were stuck at music videos I watched over a decade ago.">I started watching</abbr> oodles of climbing videos on YouTube and have barely slowed down since (spoiler alert: <a href="https://www.youtube.com/fearlesstofu">fearless tofu</a>, a YouTuber that I highly recommend, is in the dataset!). Also in 2020, I ran more than twice as far than in any other year; I started regular training with intervals, hills (my favourite), and long slow runs, that summer breaking my 10km PR by 2.5min. When bouldering resumed it was natural to ask what could training do for my climbing?

After a <abbr class="float-notes" title="A weekly intensive core series (30-45min) followed by max strength training for pull-ups and push-ups (5 sets of 5 reps of progressively difficult variations).">summer of training</abbr>, I started getting "<a href="https://hiveclimbing.com/start-here/#explained">4-hex</a>" routes regularly (V4-V6), a V5 on the <abbr class="float-notes" title="Writing this post is what pushed me to try V5 at all! When the models said I was underperforming I had to consider: am I not trying hard often enough? And yes, if I try hard, I can climb harder!">kilter board</abbr>, started getting outdoor V2s more easily and got my first granite <abbr class="float-notes" title="&hellip;followed by another three V3s while visiting the Okanagan! I guess the edgier basalt columns and gneiss rock are closer to indoor bouldering. For local granite, I need to work on sloper strength and tricky mantels!">V3</abbr>, Green Eggs and Sam. A tweaked <a href="https://theclimbingdoctor.com/pulley-injuries-explained-part-1/">A2 pulley</a> got me on the hangboard with "no hang" repeaters for rehab; once healed, I eased into max hangs.

My Garmin tracks my runs and resting heart rate (to track recovery), so, of course, I was all my training sessions but only to note sets and reps and when I reached harder grades&mdash;no assessements. But what assessment is most relevant to climbing? Number of pull-ups? How small an edge I can hang from? Or how steep a sloper? 

The <a href="https://gripped.com/indoor-climbing/how-close-are-you-to-climbing-5-15d/">9c "ultimate" climbing test</a> has been <abbr class="float-notes" title="If I feel ambitious and bored someday, I'll compile results">all over</abbr> <a href="https://www.youtube.com/watch?v=UOBB4wkTdxQ">social media</a> for over a year. Measure your max finger strength, max (single) pull-up strength, core strength (up to a 30sec front lever) and endurance (hanging from a bar) to estimate your highest <abbr class="float-notes" title="The gap between your actual grade and this predicted grade can apparently be attributed to lack of technique and/or mobility, poor strategy or poor mental aspects. Aka, everything we can't really measure. When the climber outclimbs the estimate it’s often down to mobility and style specialization, eg. slab climbers with superb finger strength but missing pull-up and core strength.">achievable grade</abbr>. I get a very lopsided score of 15, dominated nearly entirely by core strength. Should the scores be more equal? Does a 6 in one really make up for a 2 in another? Does that atrocious endurance hang actually assess anything for bouldering? Another <a href="https://www.substr8climbing.com/athletic-assessment">climbing assessment</a> has a more climbing specific endurance test: do 3 inclined ring pull-ups at 45&deg; every 10s for as long as possible (up to 6min), "resting" in between always inclined. This might still be more relevant for route climbing.


<aside>
  <h3>Reading plots</h3>

  <p>If you see a bar chart, I'm counting climbers per value (eg. the V grade or the number of years), or binned values (how many in each interval) as in the ape index chart where we group climbers in ~2cm increments (eg. just over 175 climbers have an ape index between 0 to +2cm).</p>

  <p>If you see a scatter plot (lots of circles), each point is one climber from the dataset with coordinates of eg. height (on the vertical axis) versus V grade (on the horizontal axis). I'll always superpose a line that shows the average (height) over climbers (that climb at each V grade). </p>

  <p>Pink is for female climbers; blue for male; purple is for all climbers.</p>

  <p>Most of the plots are in carousels: use the large arrows to scroll between them.</p>
</aside>

The <a href="https://strengthclimbing.com/finger-strength-analyzer/">Climbing Finger Strength Analyzer 2.0</a> considers finger strength and pull-up strength to estimate your V grade. I got a V4 estimate with a 51% probability of climbing V5 and the assessment that my "upper body strength is quite high compared to [my] finger strength" and to stop training it in favour of improving finger strength. 


Lattice Training has a free <a href="https://latticetraining.com/product/my-fingers/">finger assessment</a>: given your finger strength in your preferred grip (half crimp or open hand) for a 7sec on a 20mm hang, they'll "compare your data to [their] models so you can find out how your finger strength compares to other similar climbers". After submitting my half crimp finger strength, weight and highest V grade within the last two years:

> Your score of 121.8% bodyweight held makes you in the expected range for your bouldering grade. We would expect people at your grade, weight and gender to be scoring around the level you achieved.

Are finger strength and pull-up strength enough? Half crimp or open hand? What edge size and how long a hang? 5sec/20mm (9c test), 7sec/20mm (Lattice) or 10sec/18mm (this survey)? How many pull-up reps? Just one (9c test) or 5 (this survey)? Core strength might be crucial, but how best is it assessed? There are many complaints about going from a 20sec hanging L-sit to a 5sec front lever in the 9c test. 

I would be remiss to ignore the importance of mobility and, sadly, no mobility assessments are in the dataset I'll be using. In an actual <a href="https://www.youtube.com/watch?v=AuOkMElNgtU">Lattice Training assessment</a>, of course, they have tests of mobility: ankles (how far past your toes can your knee reach&mdash;aim for at least 5", higher is better); hips (how close to the wall can your body get with knees frogged&mdash;hip bones should be at most 10" from the wall, closer is better); and shoulders (arms above the head should pull beside the ears, ideally past them). The GB climbing team assessment, <a href="https://youtu.be/HRz65aplK7w?t=219">previewed by Hannah Morris</a>, tests shoulder mobility in the same way, hip mobility also in the same way but lying down, but ankle mobility entirely differently. They check how deeply you can squat with feet together; then, as a progression, if you can balance in and out of a pistol squat on each side. Because Hannah and her boyfriend weren't more flexible, we didn't see the full mobility progressions in the GB tests. 

While it's fun to <abbr class="float-notes" title="Around my finger strength (25% of body weight), to get the wording &ldquo;your pull-up strength is on par with your finger strength&rdquo; for 1-rep pull-ups the weight added should be 125% of my 10s/20mm max hangs; in comparison, for 5-rep pull-ups the weight should only be around 75%. If I could hang 50kg atop 60kg, the 1-rep on-par is 100% (equal to finger strength) while the 5-rep on-par hasn't changed (is still 75% of finger strength).">reverse-engineer</abbr> the trends behind the <a href="https://strengthclimbing.com/finger-strength-analyzer/">Climbing Finger Strength Analyzer 2.0</a>, to fully explore what to assess in a boulderer, I'll analyse and model a <a href="https://docs.google.com/spreadsheets/u/0/d/1J6d45EqIlIsIqNdi2X-Zl-EGFxf9d9T3R_W55xrpEAs/edit">dataset</a> that includes many strength metrics, training habits and basic climber attributes. We'll see how to balance a strength profile; what progression of strength to expect going from V-lo through V-med to V-hi; what training exercises are best to improve; and see that height and BMI both have a sweet spot, not too low, not too high. 




## Meet the Climbers (in the Dataset)


Special guests include: 
Megan, better known as <a href="https://www.instagram.com/fearlesstofu/" target="__blank">@fearlesstofu</a> in social media, and her strong climbing friend, Nelson <a href="https://www.instagram.com/aloeveraelephant/" target="__blank">@aloeveraelephant</a>. Our data points will be highlighted against the masses surveyed anonymously to show our relative strengths and weaknesses.  


<style>

a.carousel-control{
  color:  #b5b9b7;;
}
.float-container {
  width: 100%; margin: auto
}
.float-child {
  width:  50%;
  float:  left;
  padding: 5px;
  font-style: italic;
  font-size: 10pt;
  color: #333333;
}

.float-left {
  width: 60%;
}
.float-right {
  width: 40%;
}

.float-child img {
  display: inline; max-width: 100%; max-height: 100%;
}

</style>

<div id="wrapper">
  <div id="carousel_intros" class="carousel slide">
    <div class="carousel-inner">
      <div class="item ">
        <div class="float-container">
          <div class="float-child float-left ">
            <img src="{{ "/assets/images/climbing/me.jpg" | relative_url }}" title="Me on the very wet Brothers Creek Erratic along the Baden Powell trail.">
          </div>
          <div class="float-child float-right">
            <h3>Lara, <a href="https://www.instagram.com/lrthomps/" target="__blank">lrthomps</a></h3>
            <p>See me <a href="https://www.instagram.com/p/CUi_e-5pTRs/" target="__blank">climb</a></p>
            <p>168cm tall<br> 
              -4cm ape index<br>
           22.7 BMI<br></p>
            <p>climbing 18 years<br> 
              bouldering ~7 years<br></p>
            <p><a href="https://hiveclimbing.com/start-here/#explained">4-hex</a> at the Hive<br> V5 on the kilter board<br> V3 outside<br> 3-hex / <abbr class="float-notes" title="Though I need to find more slab V1s in granite to see if I can consistently climb them">granite V1</abbr> are nearly always doable<br></p>
            <p>6 hrs climbing / week<br> 
              1 hr training / week<br>
            1-2 hangboarding / week<br>
            running<br>
          backcountry skiing soon!</p>
            <p>+30lbs half crimp<br> 
              +4lbs open hand<br> 
              +25lbs 5rep pull-ups<br> 
              10 pull-ups<br> 
              19 push-ups<br> 
            30s hanging L-sit</p>
          </div>
        </div>
      </div>
      <div class="item active">
        <div class="float-container">
          <div class="float-child float-left ">
            <img src="{{ "/assets/images/climbing/megan.jpg" | relative_url }}" title="Megan on her first outdoor V6: Fat Tire in South Lake Tahoe">
          </div>
          <div class="float-child float-right">
            <h3>Megan, <a href="https://www.instagram.com/fearlesstofu/" target="__blank">@fearlesstofu</a></h3>
            <p>See her climb on <a href="https://www.youtube.com/fearlesstofu">YouTube</a></p>
            <p>156cm tall<br>
              neutral ape index<br>
              20.8 BMI<br></p>
            <p>climbing ~6 years<br></p>
            <p>V8 indoors<br>
            V6 indoors in the last 3 months<br>
              <a href="https://www.youtube.com/watch?v=95YO-N2b48o">V7 outside</a><br> 
              V4 is nearly always doable<br></p>
            <p>2 hrs / week on a <a href="https://www.instagram.com/fearlessmooncake/" target="__blank">moonboard</a></p>
            <p>+12kg half crimp<br> 
              +26.26kg open hand<br> 
              +4kg 5rep pull-ups<br> 
              10 pull-ups<br> 
              14 push-ups<br> 
            38s hanging L-sit</p>
          </div>
        </div>
      </div>
      <div class="item ">
        <div class="float-container">
          <div class="float-child float-left ">
            <img src="{{ "/assets/images/climbing/nelson.jpg" | relative_url }}" title="Nelson on a V6 in Columbia, CA called Triple Cracks">
          </div>
          <div class="float-child float-right">
            <h3>Nelson, <a href="https://www.instagram.com/aloeveraelephant/" target="__blank">@aloeveraelephant </a></h3>
            <p>See him in "<a href="https://www.youtube.com/watch?v=HrGscD-nyMc&t=270s">Friends...</a>" and in "<a href="https://www.youtube.com/watch?v=Q2nP8j-FhSM">We try...</a>"</p>
            <p>175cm tall<br>
              +4cm ape index<br>
              22.5 BMI<br></p>
            <p>climbing ~5 years<br>
            climbs outdoors "maybe 2x / year"</p>
            <p>V11<br>
            V8, in the last 3 months<br> 
              V7 is nearly always doable<br></p>
            <p>10 hrs climbing / week<br>
            no other training<br></p>
            <p>+36kg half crimp<br> 
              +48kg open hand<br> 
              +28kg 5rep pull-ups<br> 
              18 pull-ups<br> 
              24 push-ups<br> 
            27s hanging L-sit</p>
          </div>
        </div>
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_intros" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_intros" data-slide="next">
      &rsaquo;
    </a>
  </div>
</div>


[^otherquestions]: Training specifics such as hangboard protocols (eg. repeaters, max hangs, min edges and one-armed protocols) as well as grip types trained (eg. half crimp, open hand and others not modeled as they were too noisy); 


The survey included another 513 men and 77 women. V6 is the most common grade and most climbers are in their first 4 years of climbing. Climbing grades rise with number of years climbing and plateau after around 5 years. Higher V grade climbers are more likely to <abbr class="float-notes" title="I started with outdoors only and came inside to increase volume. For those that started inside, I strongly suggest trying bouldering on real rock. It’ll challenge your route reading infinitely more, the footwork is almost always harder and the variety of grips you’ll practice is endless.">climb outside</abbr> (nearly everyone in this dataset climbs inside). The distribution of grades is peaked in the women's profile at V3, V5 and V9, familiar as common plateaus. Lattice Training saw this pervasively in their data and call them <a href="https://latticetraining.com/2017/08/30/milestone-grades/">milestone grades</a> (though they see these most prominently at V6 and V8). Megan sits comfortably below the last milestone grade (plateau) so she can cruise into it in time while I've just left the first plateau to land in the <abbr class="float-notes" title="Unless I go by the Lattice Training milestone grades then I'll be cruising into V6s, indoors at least">second</abbr>. 

Higher V grade male climbers then to be shorter; but higher V grade female climbers then to be taller. There are <abbr class="float-notes" title="I wonder if this generalizes to non-climbers">more climbers with +ve</abbr> index than -ve. <abbr class="float-notes" title="BMI is crude scaling of weight and height (about as accurate as when the physicist 'approximates the cow by a sphere'). It doesn’t differentiate muscle from fat and muscle is 20% heavier per volume than fat. That said, for many problems, the cow may as well be a sphere.">BMI</abbr> trends downward with increasing V grade in men (from >25 to 22) while in women the trend upward (from <18 to ~21). Maybe there's an optimal BMI ~21-22 for most climbers.

The women are on average lighter (58kg vs 72kg), shorter (165cm vs  179cm), have a shorter ape index by more than 1cm, have been climbing 4 months less, climb 15min less per week, train 20min less per week, and are weaker in all measures except they can hold an L-sit 10s longer; they climb 1-2 V grades lower but their hardest grade is closer to the grade they can send 90-100% of the time. 

The highest V grade climbers climb roughly twice as much per week as the beginners. Beginners don’t train at all, nor should they necessarily, while the highest V grade climbers average 5-8 hours per week.

Let’s look at these statistics visually (click through the carousel to see all the figures).

<div id="wrapper">
  <div id="carousel_stats" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/histogram_by_grade.png" | relative_url }}">
        <p class="caption">Looking at the number of climbers by V grade (highest within the last 3 months), we that V6 / V3 for men/women are the most common grades, but we have climbers up to V14 / V9.</p>
    </div>
    <div class="item">
      <img src="{{ "/assets/images/climbing/histogram_by_inoutdoor.png" | relative_url }}">
      <p class="caption">If we break down those grades by who climbs indoors vs outdoors we find that most strong climbers (also) climb outside whereas the majority of beginners only climb inside.</p>
    </div>
    <div class="item">
      <img src="{{ "/assets/images/climbing/histogram_by_year.png" | relative_url }}">
      <p class="caption">Now by # of years climbing, we find Megan at 6 years and Nelson at 5. For modelling purposes, I put myself down for 7 years to take out the many years I didn't climb. </p>
    </div>
    <div class="item">
      <img src="{{ "/assets/images/climbing/grade_by_year.png" | relative_url }}">
      <p class="caption">In V grade versus # years climbing, we see a huge spread but the averages by year are clearer. The women's curve is still noisy because there aren't enough respondents. </p>
    </div>
    <div class="item">
      <img src="{{ "/assets/images/climbing/height.png" | relative_url }}">
      <p class="caption">At 5’1”, Megan is the shortest in this dataset climbing V6 recently&colon; clearly height is not holding her back. Next to Laura Rogara (148cm) she's pretty tall.</p>
    </div>
    <div class="item">
      <img src="{{ "/assets/images/climbing/apeindex.png" | relative_url }}">
      <p class="caption">Ape index trends higher with increasing grades but the scatter is more 5x wider so I won't let my -4cm be an excuse. A V7 climber has a -60cm ape index (not shown).</p>
    </div>    
    <div class="item">
      <img src="{{ "/assets/images/climbing/bmi.png" | relative_url }}">
      <p class="caption">Looking at BMI vs V grade, the men trend downward but stay on average above 20; the women have a weak <em>upward</em> trend always averaging just above 21.</p>
    </div>    
    <div class="item">
      <img src="{{ "/assets/images/climbing/hoursclimbing.png" | relative_url }}">
      <p class="caption">Left: Climbers by # of hours climbing per week is fairly noisy with 6 hours being most common. Right: More hours climbing for climbers at higher grades.</p>
    </div>
    <div class="item">
      <img src="{{ "/assets/images/climbing/hourstraining.png" | relative_url }}">
      <p class="caption">Left: Climbers by # of hours spent training (both climbing-specific and general strength training). Right: More hours training for climbers at higher grades. Ignore the women’s regression going negative: don’t worry, they can’t actually <em>untrain</em>.</p>
    </div>
  </div>
  <a class="carousel-control left" href="#carousel_stats" data-slide="prev">&lsaquo;</a>
  <a class="carousel-control right" href="#carousel_stats" data-slide="next">&rsaquo;</a>
  </div>
</div>




## Not All Surveyed V Grades are the Same

Climbers submitted three different grades: highest ever, highest in the last 3 months, and grade they can send 90-100% of the time. The first is problematic because it may have been years ago and the climber’s current strength and current habits don’t reflect how they were then. Indeed <abbr class="float-notes" title="In fact, a few climbers claimed the opposite: that their recent max is higher than their max ever. Presumably they read the survey questions wrong and I reversed their grades.">comparing</abbr> highest ever to highest recently, the spread is as high as 4 V grades for a climber of 15 years. 

The <abbr class="float-notes" title="Doable meaning climbable 90-100% of the time">“doable” grade</abbr> is highly subjective. Should we consider all styles? Or just the style we love and climb well. What about the reachy climbs if you’re short, or the overly compressed climbs if you’re tall? Just how peaky is your <a href="https://hiveclimbing.com/blog/climbing-pyramid/">climbing pyramid</a>? The spread from doable grade to highest ever is as wide as 5 V grades for some climbers; on average, the spread is wider at the higher grades. 

Doable grade vs max recent shows similar features. A few climbers claim <abbr class="float-notes" title="This should be impossible since I filtered out the climbers than answered 'I don't boulder' for either question. Surely they could have climbed at least one problem at their doable grade.">higher</abbr> doable grade than max recent. This emphasizes how "subjective" this question is on the survey.


<div id="wrapper">
  <div id="carousel_grades" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/max_recent.png" | relative_url }}">
        <p class="caption">When we compare max ever V grade to hardest in the last 3 months, the spread is as high as 4 V grades and the trend is larger spread for more years climbing (not shown).</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/doable_max.png" | relative_url }}">
        <p class="caption">The doable V grade vs highest ever V grade is funnel-shaped: the wider gaps are more common at higher grades. Megan may be underestimating or her height may disadvantage her on too many climbs.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/doable_recent.png" | relative_url }}">
        <p class="caption">Doable vs max recent V grade is again funnel-shaped. The blue points above the dashed (1:1) line claimed higher doable grade than max recent.</p>
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_grades" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_grades" data-slide="next">
      &rsaquo;
    </a>
  </div>
</div>

We may be chasing that hardest ever, or aiming to be well rounded and want to maximize that "climbable" grade, neither grade is consistent in this dataset enough for the analysis. Grading gets more complicated when we consider indoor vs outdoor (or moonboard vs kilter board for that matter). For Megan and I, I'm using our <a href="https://boulderingboss.com/indoor-vs-outdoor-bouldering-is-there-a-difference-in-v-grades/">higher indoor grades</a> since it's' most likely what climbers did when surveyed. 

## How Strong are the Climbers?

Now we know a little about the climbers informing this post in all the ways except the ones that we’re all most interested in: how strong are they? 

Often touted to be the most predictive of strength metrics, finger strength is given by the maximum weight a climber can add to a 5-10s <abbr class="float-notes" title="Of course, as a climber gets stronger a two-armed hang on such a large edge can mean adding more than body weight again. In that case, to assess finger strength it makes more sense to hang one-armed. An additional benefit is to find any left/right asymmetries.">hang</abbr> on an 18mm-20mm edge normalized by the climber’s weight (this survey asked for 10s/18mm hangs). The <abbr class="float-notes" title="Among men or women, the trend is about the same.">trend</abbr> agrees fairly well with a <a href="https://www.instagram.com/p/B9zNGplJMyG/" target="__blank">post</a> from Lattice Training (with 7s/20mm hangs): each V grade requires another 8% of body weight for the hangs. In another <a href="https://latticetraining.com/2017/09/07/9c-adam-ondra-alex-megos/">post</a>, they estimate a necessary <abbr class="float-notes" title="That's a hang with 110% of bodyweight added: poor back!">1.1</abbr> finger strength to climb 9c. Alex Megos can add 132% to his 7s/20mm hangs and has climbed multiple <abbr class="float-notes" title="But I wouldn't say he's underperforming given that he's a sport climber who first onsighted 9a and first to climb Bibliographie, 9b+.">V15s</abbr>. <abbr class="float-notes" title="Also more of a sport climber, Adam is the first and only one to climb 9c: Silence, a route he put up in Norway.">Adam Ondra</abbr> manages V16 while only capable of 112% hangs. His technique, speed and surreal mobility certainly highlight that (finger) strength is not all that matters.

While finger strength didn’t show a big gender difference, the normalized weight added to 5 pull-ups is <abbr class="float-notes" title="Either the women make due with less pull up strength or they default to problems that don’t require it.">10-20% more</abbr> at a given grade for male climbers. (5-rep) Pull-up strength increases with grade up to around <abbr class="float-notes" title="Where 0.8 ~ 0.75*1.1, in agreement with the recommended scaling I extracted from the Climbing Finger Strength Analyzer 2.0">0.8</abbr> (of bodyweight) at the highest grades. 

For any given grade, the male climbers seem to do twice as many pull-ups or push-ups as the women. From the trends, it looks like more modest goals of 20-25 pull-ups and 30-40 push-ups are better for climbing (we'll see later than the models agree). For the boulderer, unweighted pull-ups are essentially an endurance test. The 5-rep weighted pull-ups test power endurance, while a single-rep weighted pull-up is a better test of pure strength.

Less than a quarter of people submitted their L-sit time. One issue may be that if you google  “L-sit” you get the standard, much harder sitting version and the one climbers refer to is actually the “hanging L-sit” (in my own climbing group, some hadn't heard of either). Also, many climbers suspiciously answered an even 30s and 60s. Were they just guessing or did they get bored and give up? Even though going from a hanging L-sit to a front lever is a harsh jump, the 9c climbing test progression is clearly better than one fixed exercise. Just as they allowed a progression of tucked knees for the L-sit, why not also use a <a href="https://www.gymclimber.com/front-lever-progression-for-climbers/">progression to front level</a>.


I’ll plot these metrics and, like before, click through the carousel to see them all.

<div id="wrapper">
<div id="carousel_strengths" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/maxfinger.png" | relative_url }}">
        <p class="caption">Both Megan and Nelson seem to have more finger strength than their recent grade merits, but, in fact, both fall perfectly on the trendline using their max ever V grades (8, 11).</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/5reppullups.png" | relative_url }}">
        <p class="caption">For 5-rep pull-up strength, the women trend a steady 0.2 below the men. At every grade, this strength should be less than finger strength.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/pull_pushups.png" | relative_url }}">
        <p class="caption">Number of pull-ups (left) and push-ups (right) by grade. A further eight male climbers are cut off in the right plot, one claiming 286 push-ups!</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/lsit.png" | relative_url }}">
        <p class="caption">A further 9 climbers are cut off; L-sit times went as high as 10min including one female V3 climber who held for nearly <abbr class="float-notes" title="Just hanging from the bar that long is 9/10 points for endurance on the 9c test. 10min is off the charts!">5min</abbr>!</p>
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



What about differences in strength metrics: how should the two grips compare for finger strength? How does finger strength compare with pulling strength? And how should finger strength and pulling strength compare as we get stronger?

<div id="wrapper">
<div id="carousel_del_s" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/delta_fingers.png" | relative_url }}">
        <p class="caption">Half crimp and open hand strength are typically equal. In <a href="https://www.v-publishing.co.uk/books/climbing/beastmaking/">Beastmaking</a>, the author suggests that hand anatomy plays a role in which grip a climber favours. Full- and half-crimp are generally the stronger grip but place more strain on the finger pulleys and open-hand transfers better to slopers. Considering the merits of both, I think I can stand to train my open hand to catch up to my crimp while Megan and Nelson may do well to train their half crimp to catch up to their open hand. Another point to keep in mind here, 35% of climbers gave half crimp max hangs, 28% gave open hand max hangs while 25% gave both: which tips the balance another 10% in favour of half crimps. To compare, 46% gave their 5-rep pull-up max weight.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/finger_by_pull.png" | relative_url }}">
        <p class="caption">Instead of considering the progression of strength by grade, let's look at finger strength (whichever is higher) over 5-rep pulling strength as a function of finger strength; aka, how should the two metrics develop together. When both are still low, pulling strength exceeds finger strength for both women and men; but as they get stronger, women typically get far more finger strength than pulling strength. Megan has more than 6x the finger to pulling strength! The men tend to increase both with their finger strength starting to exceed pulling strength only once they've reach roughly 50% body weight. The trend seems to roll over beyond that with finger:pulling strength ~5:3.</p>
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

With a dataset of nearly 600 climbers, I could train <abbr class="float-notes" title="Several in fact, of various kinds: I started with linear regression, went to 2-4 layer dense neural networks before finally trying on random forests then boosted trees (which, of course, are usually best for this kind of tabular data). I trained many of each kind and settled on the model type that gave the most consistent feature importance estimates.">a model</abbr> to predict the hardest V grade each climber had reached given their strength metrics and training habits. Shockingly, the model was better than expected with some regression to the mean (that is, low V grade climbers were predicted high, while high V grade climbers were predicted low) with typical errors ~1-2 V grades. 

In predicting each of the reported bouldering grades, the model can be assessed for how important it found each feature of the climber. In nearly every model I trained for every grade, the most important feature is number of years climbed. After all: 

>   Climbing is the best training for climbing

Strangely, the number of pull-ups often appeared more important than the actual pull-up strength. Surely in bouldering, number of pull-ups is more of an endurance feat while 5-rep max weight is a measure of strength endurance (single rep max weighted pull-ups would better assess pure strength). If most boulders feature 5 moves, this should be the most important (pull-up) feature. The reason I think they come reversed is that 3/4 of climbers reported number of pull-ups while less than half reported weighted ones: there's just more information in the former for the model to learn from.
That said, it's astonishing that half crimp strength was the most common second most used feature when only 35% of climbers reported it!

<img src="{{ "/assets/images/climbing/feats_max_recent.png" | relative_url }}">

<p class="caption">As found by the model, the most important aspect of a climber to guess their highest V grade is how long they’ve been climbing! BMI is next in importance: the predicted grade only increases for climbers with BMI &le; 19; Megan, Nelson and my predictions all go up if we increase out BMI by 0.5 (not by much though). Next we see hours climbing, max pull up reps and half crimp strength. This is <a href="https://christophm.github.io/interpretable-ml-book/feature-importance.html">permutation importance</a> so the score is the (normalized) increase in mean squared error over all climbers (the 30 held out climbers included) when each feature is random shuffled.</p>

<div id="wrapper">
<div id="carousel_preds" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/pred_max_recent.png" | relative_url }}" >
        <p class="caption">This (<a href="https://lightgbm.readthedocs.io/en/latest/">lightgbm</a>) model was trained holding out a random 30 climbers (in green) including Megan, Nelson and I: that the test climbers are predicted as well as the others is a sign the model trained well. The slight bias to predict high for lower V grade climbers and low for higher V grade climbers (known as regressing to the mean) isn't too surprising since there is a lot of missing data (unmeasured weighted hangs for instance). Megan, Nelson and I are very well predicted; reassuring since the model had all our strength metrics.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/del_y_max_recent.png" | relative_url }}" >
        <p class="caption">Change no habits, even if continuing various kinds of training, if you get no stronger and just climb another year and you’ll improve by 0.5 to 1.5 V grades in your first 5 years.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/del_s_max_recent.png" | relative_url }}" >
        <p class="caption">The predicted grade shift for increased strength metrics all follow a similar pattern: there are no gains (and sometimes expected losses!) for increasing strength at the lowest levels. I interpret this as the usual advice from trainers and climbers alike: to improve at climbing, at first, focus on climbing. You will naturally get stronger. Once a minimal strength is reached (10s hangs on a 20mm edge, 5 pull-ups, 10 push-ups, 5s hanging L-sit) then increasing them further yields greater gains. Once a certain strength is reached however, the gains saturate. The data sets the upper limits at hangs with body weight added, 5-rep pull-ups with less than half body weight added, 20 pull-ups, 30 push-ups, 30s of hanging L-sit. Note that this dataset is realistic limited to climbing up to V10 (very few climbers climbed harder); but <a href="https://www.instagram.com/p/B9zNGplJMyG/" target="__blank">Lattice Training reports</a> less than that finger strength for bouldering V15!</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/del_s2_max_recent.png" | relative_url }}" >
        <p class="caption">The predicted grade shift for increased strength metrics all follow a similar pattern: there are no gains (and sometimes expected losses!) for increasing strength at the lowest levels. I interpret this as the usual advice from trainers and climbers alike: to improve at climbing, at first, focus on climbing. You will naturally get stronger. Once a minimal strength is reached (10s hangs on a 20mm edge, 5 pull-ups, 10 push-ups, 5s hanging L-sit) then increasing them further yields greater gains. Once a certain strength is reached however, the gains saturate. The data sets the upper limits at hangs with body weight added, 5-rep pull-ups with less than half body weight added, 20 pull-ups, 30 push-ups, 30s of hanging L-sit. Note that this dataset is realistic limited to climbing up to V10 (very few climbers climbed harder); but <a href="https://www.instagram.com/p/B9zNGplJMyG/" target="__blank">Lattice Training reports</a> less than that finger strength for bouldering V15!</p>
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


<!-- It’s tricky to assess the expected V grade change with BMI change as it affects all the normalized strength metrics. Clearly the denominator (weight) changes directly as BMI is proportional to weight, and if the BMI drop is only excess fat and superfluous muscle then we can imagine that the muscles can still support the original weight and the finger and pulling strengths will seem to increase by the weight lost. Of course, this is <em>not</em> a reasonable assumption in many climbers, especially in the lower BMI / % body fat range[^bodyweight]. If a BMI gain is only in muscles used in grip and pull strengths, then even though the weight increases, the strength gains should keep up or even exceed the added weight. For BMIs under 20, the expected V grade increases if BMI increases by 0.5. Lowering BMI by 0.5 only increased V grade prediction through adjusted strength metrics.

[^bodyweight]: This is an entire topic on its own and not one I'm well placed to talk about. For some people it’s rather clear that we can lose some fat to get into better climbing condition (whether our goal actually demand it is yet another matter); for others, the margin is getting very slim. Read the recent thread on weight, diet and training by professional boulderer Staša Gejo <a href="https://www.instagram.com/gejostasa/" target="__blank">@gejostasa</a> starting with <a href="https://www.instagram.com/p/CUQabPzMvuU/" target="__blank">this one</a>. Of course, the pros[^probmi] have a different commitment level than most of us and, in general, we won't push our bodies as hard.


[^probmi]: <a href="https://www.reddit.com/r/climbharder/comments/el9pow/climbing_height_vs_weight_from_mani/">The BMI of the pros</a> are more typically borderline or outright underweight (defined as 18.5). Hopefully these are their "performance weights" and not their "training/recovery weight". There's a <a href="https://www.youtube.com/watch?v=aSepsUJKdHs&t=1225s">segment in this video</a> where Alex Huber talks about his "liquid diet" to drop from his training weight, 68kg, down to his 9a climbing weight, 62kg&mdash;he's 176cm so that's going from a bmi of 22 down to 20. 

Using myself as an example to clarify these strength adjustments, I weigh a little under 140lbs and am 168 cm / 5’6.5” tall. I can currently add 25.5 lbs to my half crimp hangs; 25 lbs to my 5-rep pull-ups; and have to take away 25.5 lbs to do open hand hangs. My BMI goes down by 0.5 if my weight drops by 3 lbs[^3lbs]. If my strength doesn’t change, I’ll be able to hang and pull with 28.5 / 28 / -22.5 lbs. With those 4 updated metrics (BMI and the three normalized strengths; note that we’re still ignoring any changes in pull ups, push ups or L-sits), the model predicts I can push my bouldering ~2.5 V grades higher (the comparison +0.5 BMI drops my V grade by a mere 0.13 assuming no strength adjustments necessary). If that sounds overly optimistic, I agree: the model is telling me that others with that BMI and those strength metrics climb V9 (the model originally predicted high for me); but they may also generally have more technique and mobility, and losing weight won’t magically help me with either. 

[^3lbs]: I had a lazy second half of my 30s and my weight drifted from a lean and muscular 130 lbs to a soft and weak 140 lbs. Training this summer so far has unsoftened me somewhat and strengthened me oodles with weight dropping just a little. All to say, it’s not unreasonable to think I have 3 lbs of excess fat. 

... gender changes? -->


## What if...


For fun next, I’ll have the model recommend modified profiles for Megan, Nelson and I to reach the next V grade. The model is under-predicting for Nelson by over 2 V grades and over-predicting about the same for me, so I’ll be comparing before and after model predictions (and ignoring our actual climbing grades). Keep in mind that assumes the “wisdom of the crowd” in this dataset is accurate; one substitution I’ll make is to switch campus board to system board training. It’s more climbing specific and can be used just as effectively to develop power. 

Megan: 1 year later, climbing 6 hours a week with no additional training, she only needs to increase her half crimp strength by 10% and the model predicts she’ll reach the next V grade!

Nelson: 1 year later, climbing an extra hour per week and adding 1 hr of training, max hangs 2x / week, if he increases both grip strengths by 10%, the model anticipates a V grade improvements.

Lara: 1 year later, still climbing 6 hours a week and training for 1 hr, starting 2x / week <abbr class="float-notes" title="Actually, model predicts that if I hang one-armed I get an even greater return. Strangely, it did not have the same expected change for Nelson or Megan. Yes, my left is weaker but how did the model know that I'm imbalanced?">max hangs</abbr>, if I increase both half crimp and open hand strength another 10% of body weight the model predicts I push one more V grade.


## Training Progression

Track: 
* add mobility metrics
* add 1 rep pull-up
* progression for core
* add or modify hangs to 5s or 7s
* add hang endurance test? some number of 7/3 repeaters, what weight can be added?
* track indoor, system board and outdoor grades
* 5 rep pull-ups
* number of pull-ups, push-ups


Aim for max 5-rep pull-up strength following finger strength ~3 or 4:5  
Aim for max single rep pull-up strength surpassing 5-rep strength 5:4 (according to the finger strength analyzer; a small departure from the inherent scaling implied by the 9c test)


## Further Reading and Other Resources

Other datasets exist, most notably the scrapped submissions from 8a.nu <a href="https://www.kaggle.com/dcohen21/8anu-climbing-logbook">downloadable</a> from kaggle.  <a href="https://latticetraining.com">Lattice Training</a> released an interesting <a href="https://www.instagram.com/p/B9zNGplJMyG/" target="__blank">finger strength vs V grade</a> that we'll compare with. 