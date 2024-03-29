---
layout: post
use_math: false
use_carousel: true
title:  "Assess Yourself for Better Bouldering"
subtitle: "Data-Backed Training Advice"
tags: ["machine learning", "climbing"]
date:   2021-12-15
summary: Analysis of a climbing survey dataset to test the wisdom of the crowd in how best to improve at climbing and assess training progress. 

---

<script type="text/javascript">
$(document).ready(function(){
  $('#carousel_intros').carousel();
  $('#carousel_stats, #carousel_strengths, #carousel_del_s, #carousel_preds, #carousel_d_preds, #carousel_grades').carousel(
    {interval: false}
    );  
});
</script>


This summer, I got stronger with some "<span class="float-notes">base<span>Base training is meant to increase training volume slowly, improve general fitness, and lay a good foundation for sport-specific training. A better base leads into more effective training (theoretically).</span></span>" training, pull-ups, push-ups and core circuits, and <span class="float-notes">broke<span>I've reached 3-hex multiple times through my climbing years never with any training, just through climbing; with training, I went from 4 to 10 pull-ups / 10 to 15 push-ups / 7 to 30s in a hanging L-sit; from struggling on half the 3-hexes to reliably getting a few 4-hexes. I should mention that I've been this strong and fit before but never climbing at the grade! So climbing practice over the many years has meant I mostly just need to be stronger (this time).</span></span> my 3-<a href="https://hiveclimbing.com/start-here/#explained">hex</a> (V2-V4) plateau. Instead of continuing with <span class="float-notes">climbing<span>Usually split to first build strength and then to build power.</span></span> specific training, I spent a few months adjusting to that new strength; aka, reaping the benefits. After a decade of being warned against <span class="float-notes">hangboarding<span>On the common fear of hangboarding, in Beastmaking, Ned Feehally writes, "[fingerboard training] is the safest way of training finger strength as it is very controlled, you can apply the load slowly and let go at any time".</span></span> and (worse) <span class="float-notes">campus boarding<span>On the ubiquity of campus boarding, Ned writes, "modern climbing walls have developed so far and become so good that the campus board seems massively dated;" instead, he suggests campusing routes and training on a system board.</span></span>&mdash;"you'll injure yourself!"&mdash;why not just continue with the same training? It works! 

The first two hints against this plan come from the <a href="https://gripped.com/indoor-climbing/how-close-are-you-to-climbing-5-15d/">9c "ultimate" climbing test</a> and the <a href="https://strengthclimbing.com/finger-strength-analyzer/">Climbing Finger Strength Analyzer 2.0</a>:
  * my "9c score" is <span class="float-notes">14<span>Which corresponds to a sport climbing grade of 7b ~ 5.12b but I don't sport climb...MEC translates that to ~V5.</span></span>, 6 coming from core alone
  * and my "upper body strength is *quite high* compared to [my] finger strength" when it is already <span class="float-notes">*lower*<span>Comparing max weighted 5 pull-ups with 10s 19mm half crimp maxhangs.</span></span> than my finger strength

Looks like my core and pulling training have already outpaced my finger training. 

<aside>
  <h3>Reading plots</h3>

  <p>If you see a bar chart, I'm counting climbers per value (eg. per V grade, per number of years, or per number of hours), or showing some amount per category.</p>

  <p>If you see a scatter plot, each circle is one climber from the dataset with coordinates of eg. height versus V grade. The superposed line shows the average (height) over climbers (at each V grade) or the trend line when the data is too noisy. </p>

  <p>Pink is for female climbers; blue for male; purple is for both pooled when the data is sparse.</p>

  <p>Most of the plots are in < carousels >: use the large arrows to scroll between them.</p>

  <p>Also: <span class="float-notes">hover over me<span>Many technical comments, asides, and personal anecdotes can be found associated with the double-dash underlined text. Skip them for a 12min read; read all to add another 7min; and since pictures are ~1000 words, with all the plots you get nearly another 2 hours!</span></span></p>
</aside>

Consider a parallel <span class="float-notes">story<span>Drawn from The Science and Practice of Strength Training</span></span> of a shot putter training to throw a 7kg shot. He trains to bench press more and more, 50kg then 150kg&mdash;it's improving his throws!&mdash;200kg, 300kg&mdash;and yet he can throw no further. He got stronger, yes, but what he needed was more power. 

But what is the ideal strength profile of a boulderer? How much finger strength? How much pulling strength? How much power? More is surely better but what is a good balance progressing from V-lo through V-mid to V-hi? What about push-ups, legs and endurance?  Surely it depends on my specific goals and likely on my height, arm span, and hand size also, but general estimates would still help guide my training. 




In this post, I'll analyse and model a <a href="https://docs.google.com/spreadsheets/u/0/d/1J6d45EqIlIsIqNdi2X-Zl-EGFxf9d9T3R_W55xrpEAs/edit">dataset</a> collected from a survey on Reddit, including many <span class="float-notes">strength<span>Half-crimp and open hand 10s max hangs on 18mm edge; 5-rep pull-up max weight; max hanging L-sit time; # pull-ups / push-ups.</span></span> metrics, <span class="float-notes">training<span>Training specifics included hangboard protocols (eg. repeaters, max hangs, min edges, one-armed protocols, etc.), grip types trained (eg. half crimp, open hand, etc.); endurance training protocols (4x4, threshold intervals, feet on campusing, etc.); non-specific training (upper body pulling and pushing, core, legs and antagonists); other activities (running, yoga, skiing, martial arts, etc); and the number of sessions and hours per week doing various kinds of training.</span></span> habits and basic climber <span class="float-notes">attributes<span>Height, weight, arm span, years climbing, indoors vs outdoors, and various bouldering and climbing grades.</span></span>. We'll see how these climbers balance and progress their strengths through the grades; how they train at each stage; and see that height and BMI both have a <span class="float-notes">sweet spot<span>Most aspects in a complex system have a 'sweet spot': any time there are competing factors at play, the optimum is somewhere in the middle when neither penalty is too extreme. Weight scales very loosely as a cube of height; muscles is quadratic in height. If this were the only factor at play, then, in bodyweight sports, shorter would be strictly better (think gymnastics): this would give a max strength scaling with weight with power 0.666, analysing world record athletes finds a power of 0.63 -- close! In climbing, reach is still important and increases with height linearly. Balancing the two opposing factors, we should find an optimal height and corresponding weight. BMI is weight over height *squared* so it too should increase for similarly strong athletes (in a bodyweight sport) with increasing height and it too will have an optimum by the same arguments.</span></span>, not too low, not too high. 

<em>What about <span class="float-notes">mobility<span>Mobility is the stability and strength through your full range of motion.</span></span>? Although certainly quantifiable, no mobility assessments are in the dataset I'll be using, so my analysis will not consider it, but more on this later.</em>



## Meet the Climbers


Special guests include: 
Megan, better known as @fearlesstofu in social media, and her strong climbing friend, Nelson <a href="https://www.instagram.com/aloeveraelephant/" target="__blank">@aloeveraelephant</a>. Our data points will be highlighted against the anonymous climbers in the survey to show our relative strengths and weaknesses; you can compare findings against examples of our climbing, Megan especially on her <a href="https://www.youtube.com/fearlesstofu">YouTube channel</a> or on <a href="https://www.instagram.com/fearlesstofu/" target="__blank">Instagram</a>.  


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
            <img src="{{ "/assets/images/climbing/lara.jpg" | relative_url }}" title="Me on the very wet Brothers Creek Erratic along the Baden Powell trail.">
          </div>
          <div class="float-child float-right">
            <h3>Lara, the author, <a href="https://www.instagram.com/lrthomps/" target="__blank">@lrthomps</a></h3>
            <p>See me <a href="https://www.instagram.com/p/CUi_e-5pTRs/" target="__blank">climb</a></p>
            <p>168cm tall<br> 
              -4cm ape index<br>
           22.4 BMI<br></p>
            <p>climbing 18 years<br> 
              bouldering ~7 years<br></p>
            <p>4-hex (V4-V6) at the Hive<br> V5 on the kilter board<br>V3 outside<br> 3-hex (V2-V4) / outdoor V1 are nearly always doable<br>
            <!-- 5.10c (trad), AD- alpine -->
          </p>
            <p>6-8 hrs climbing / week<br> 
              1-2 hr training / week<br>
              ran ~1200km in 2021<br>
            <!-- backcountry skiing soon! -->
          </p>
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
              V4 is nearly always doable indoors<br></p>
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


The survey included another 513 men and 77 women. V6 is the most common grade for these climbers who are typically in their first 4 years of climbing. Climbing grades rise with the number of years and plateau after around 5 years. Higher V grade climbers are more likely to <span class="float-notes">climb outside<span>Nearly everyone in this dataset climbs inside but about half of the 'strong' climbers also climb outside. I started with trad climbing and came indoors during thesis time. For those that started inside, I strongly suggest trying bouldering on real rock. It’ll challenge your route reading infinitely more, the footwork is almost always harder and the variety of grips you’ll practice is endless.</span></span>. The women's V grades cluster at V3, V5 and V9, familiar as common plateaus; generally, in the much larger and wider dataset at Lattice Training, these fall at <a href="https://latticetraining.com/2017/08/30/milestone-grades/">V6 and V8</a>.  

Higher V grade male climbers tend to be shorter while higher V grade female climbers tend to be taller; they asymptotically meet in the middle:

<blockquote><p>The ideal height is ~<span class="float-notes">170cm<span>Alex Megos, 173cm; Nalle Hukkataival, 173cm; Daniel Woods, 170cm; Stefano Ghisolfi, 170cm; Colin Duffy, 168cm. Akiyo Noguchi, 168cm; Janja Garnbret, 164cm; Shauna Coxsey, 163cm; Oriane Bertone, 164cm. But: Jimmy Webb, 183cm; Adam Ondra, 185cm; Jan Hojer, 188cm; Dean Potter, 196cm; and: Sean Bailey, 163cm; Brooke Raboutou, 158cm; Natalia Grossman, 157cm; Lynn Hill, 157cm; Ashima Shiraishi, 155cm; Laura Rogora, 152cm.</span></span> and +5-10 ape index.&mdash;<a href="https://youtu.be/8-5yuVuDFzU?t=2620">Adam Ondra</a></p></blockquote>

...though he discusses the merits of <span class="float-notes">short vs tall<span>Short climbers must learn creative solutions early for lack of reach and puts them on a path for better technique. Being tall isn't that big an advance -- it's the long arms that it comes with that are. Overall, some climbs suit short people better; others suit tall people better. Climb to your strengths!</span></span>, <span class="float-notes">long vs short arms<span>Long arms are good for their long reach but worse in every other aspect: harder lock-offs, harder underclings, require more leverage and more torque.</span></span>, and being a <span class="float-notes">little light<span>...for better endurance sport climbing</span></span> vs a <span class="float-notes">little more muscled<span>...to be a stronger boulderer.</span></span> <a href="https://www.youtube.com/watch?v=yFfkOM8RgAU" title="Adam Ondra #38: What is the best body type for climbing?">here</a>.

There are <span class="float-notes">more climbers with +ve<span>Apparently this generalizes to non-climbers: up to 5% longer is normal (the climbers here average 1% longer arm span than height). There are regional and gender differences, and shrinkage with age [Quanjer, 2014].</span></span> index than -ve. <span class="float-notes">BMI<span>BMI is a crude scaling of weight and height (about as accurate as when the physicist 'approximates the cow by a sphere'). It doesn’t differentiate muscle from fat and muscle is 20% heavier per volume than fat. That said, for many problems, the scaling works, and the cow may as well be a sphere.</span></span> trends downward with increasing V grade in men (from >25 to 22) while in women the trend tips slightly upward (from <18 to ~21). An optimal BMI for bouldering may be ~<span class="float-notes">21-22<span>Only two boulderers have climbed V17: Daniel Woods, 21.2; and Nalle Hukkataival, 22.7; I can't get (adult) numbers for any V15 female climbers (Ashima Shiraishi has climbed 2; Kaddi Lehman and Oriane Bertone have each climbed one); strong V14 climbers include Shauna Coxsey, 21.8; and Alex Puccio, 23.1. Others that are primarily boulderers that commonly make 'top 10' lists: Guiliano Cameroni, 19.6; Jimmy Webb, 23.3; Dai Koyomada, 21.3; Adam Ondra, 20.7.</span></span>.

The women are on average lighter (58kg vs 72kg), shorter (165cm vs  179cm), have >1cm shorter ape index, have been climbing 4 months less, climb 15min less per week, train 20min less per week, and are weaker in all measures except they can hold an L-sit 10s longer; they climb 1-2 V grades lower but their hardest grade is closer to the grade they can climb 90-100% of the time. 

The highest V grade climbers climb roughly twice as much per week as beginners. Beginners don’t train at all, while the highest V grade climbers train 5-8 hours per week on average.

In the carousel, you can <span class="float-notes">see<span>If you have trouble understanding these plots and you happen to also climb at the Hive, track me down and I might be able to help.</span></span> these statistics visually (click through to see all the figures).

<div id="wrapper">
  <div id="carousel_stats" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/histogram_by_grade.png" | relative_url }}">
        <p class="caption">Looking at the number of climbers by  max recent V grade, V6 / V3 are the most common grades for men / women, but we have climbers up to V14 / V9.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/histogram_by_inoutdoor.png" | relative_url }}">
        <p class="caption">If we break down those grades by who climbs indoors vs outdoors we find that most strong climbers (also) climb outside whereas the majority of beginners only climb inside. A few men only climb outside.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/histogram_by_year.png" | relative_url }}">
        <p class="caption">The number of climbers that have climbed more than 4 years drops off sharply. Megan has 6 years and Nelson has 5. For me, ~<a class="float-notes" title="2003, a low 5th class up the Tête Nord du Replat, and Bim bam boum in the Vercors; 2004, Lion's Way 5.6, Pigeon W Ridge 5.4, 1/2 of Bugaboo Spire, a trip to the Bugaboos; 2006-8, started leading trad up to 5.9, mountains up to AD-; 2010, end of Ph.D., bouldering in indoors, pushing trad to a single 5.10c, Exasperator, maybe now buried?; 2011-12, at MIT, bouldering & route-setting at an on-campus cooperative + outdoor bouldering / sport / trad / ice climbing; 2014, back in Van, learn to hand jam properly but visit Indian Creek twice and learn otherwise; 2018-now, bouldering regularly at the Hive; 2021, bouldering outside regularly for the first summer. So how many years are relevant to bouldering? 18yrs? 3yrs? Funny enough, both years fit the trend in the next plot; later, modelling will learn likewise not to differentiate heavily between 3 and >15 yrs of climbing.">3-18 years</a>. </p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/grade_by_year.png" | relative_url }}">
        <p class="caption">There's a wide spread of grades among climbers with the same number of years of climbing experience but the average grade by year shows an upward trend. The women's curve looks noisy because there aren't enough <a class="float-notes" title="The number of women climbing rose rapidly from almost none to 10% in the 2000s (using 8a.nu as a proxy) and another few percent since then. This survey was conducted on Reddit which compounds the issue: 62% of Reddit users are male, while the remaining 38% are female. Having 13% women respond is actually not bad.">respondents</a>.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/height.png" | relative_url }}">
        <p class="caption">A wide range of heights is common for the middling grades but the scatter funnels down to around 170cm. Adam Ondra and Ashima Shiraishi are strong outliers.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/apeindex.png" | relative_url }}">
        <p class="caption">Ape index trends higher with increasing grades but the scatter is 5x wider so I won't let my -4cm be an excuse (though my arm span is <em>shorter</em> than Ashima's!).</p>
      </div>    
      <div class="item">
        <img src="{{ "/assets/images/climbing/bmi.png" | relative_url }}">
        <p class="caption">Looking at BMI vs V grade, the men trend downward while the women trend slowly <em>upward</em>; the noise narrows just as height did.</p>
      </div>    
      <div class="item">
        <img src="{{ "/assets/images/climbing/hoursclimbing.png" | relative_url }}">
        <p class="caption">Left: Climbers by # of hours climbing per week is fairly noisy with 4/6 hours being the most common for women/men. Right: Climbers at higher grades climb more.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/hourstraining.png" | relative_url }}">
        <p class="caption">Left: Climbers by # of hours spent training (of all kinds) is noisier still with < 6/8 most likely for women/men. Right: Climbers at higher grades train more.</p>
      </div>
    </div>
    <a class="carousel-control left" href="#carousel_stats" data-slide="prev">&lsaquo;</a>
    <a class="carousel-control right" href="#carousel_stats" data-slide="next">&rsaquo;</a>
  </div>
</div>




## Not All Surveyed V Grades are the Same

Climbers submitted three different grades: max ever, recent max (in the last 3 months ), and the grade that's "doable" 90-100% of the time. Grading gets more complicated when we consider <a href="https://boulderingboss.com/indoor-vs-outdoor-bouldering-is-there-a-difference-in-v-grades/">indoor vs outdoor</a> (or moonboard vs kilter board for that matter).  

Max ever V grade is problematic: the climber may have sent it years ago and their current strength and habits aren't what they once were. The spread is as wide as 4 V grades for a climber of 15 years and, generally, <span class="float-notes">wider<span>Although a few climbers claimed the opposite: that their recent max is higher than their max ever. Presumably, they read the survey questions wrong and I reversed their grades.</span></span> at higher V grades. 

The doable grade is highly subjective.  Should we consider all styles? Or just the style we love and climb well. What about the reachy climbs if you’re short, or the overly compressed climbs if you’re tall? Just how peaky is your <a href="https://hiveclimbing.com/blog/climbing-pyramid/">climbing pyramid</a>? Do you always get beta from others before trying? The spread from doable grade to max ever is as wide as 5 V grades; on average, the spread is wider at the higher grades. Doable grade against max recent shows the same <span class="float-notes">widening<span>A few climbers claim higher doable grade than max recent, surely impossible. I filtered out the climbers that answered 'I don't boulder' for either question. If they're bouldering at all, they could have climbed at least one problem at their doable grade.</span></span> spread.  


<div id="wrapper">
  <div id="carousel_grades" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/max_recent.png" | relative_url }}">
        <p class="caption">When we compare max ever V grade to hardest in the last 3 months, the spread is as high as 4 V grades. The spread widens with more years climbing (tiny inset).</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/doable_max.png" | relative_url }}">
        <p class="caption">The doable V grade vs max ever V grade is funnel-shaped: the wider gaps are more common at higher grades. Megan may be underestimating or her height may disadvantage her on too many climbs.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/doable_recent.png" | relative_url }}">
        <p class="caption">Doable vs max recent V grade is again funnel-shaped. The few (blue) points above the dashed (1:1) line claimed a higher doable grade than max recent.</p>
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

All plots and analysis hereafter will consider only max recent V grade.

## How Strong are the Climbers?

Finger strength is the most correlated feature we have to climbing grade. The numbers are similar for men and women and <span class="float-notes">agree<span>Though Lattice Training uses 7s/20mm max hangs vs 10s/18mm max hangs gathered by this survey.</span></span> fairly well with the climbers from <a href="https://www.instagram.com/p/B9zNGplJMyG/" target="__blank">Lattice Training</a>: each V grade requires adding another 8% of body weight to max hangs; to climb 9c would require ~<span class="float-notes">1.1<span>That's a hang with 110% of bodyweight added, or 210% total weight.</span></span>. Silence, the first 9c, was put up by Adam Ondra with max hangs of 112%; Bibliographie, briefly the second 9c, was first climbed by Alex Megos whose max hangs are an astonishing 132%. 

While finger strength didn’t show a big gender difference, the normalized weight added to 5 pull-ups is <span class="float-notes">10-20% more<span>Either the women make do with less pulling strength or they prefer problems that don’t require it.</span></span> for male climbers at any given grade. Pulling strength increases with grade up to around <span class="float-notes">0.8<span>80% of bodyweight, in agreement with the pulling to finger strength ratio recommended by the Climbing Finger Strength Analyzer 2.0 (0.75) and the Lattice Training finger strength estimate of 1.1 to climb 9c, where 0.8 ~ 0.75*1.1.</span></span> at the highest grades. 
For any given grade, the male climbers seem to do twice as many pull-ups or push-ups as the women. Despite many over-achievers, more modest goals of 20-25 pull-ups and 30-40 push-ups seem sufficient for climbing. 
Less than 25% submitted their L-sit time and many <span class="float-notes">suspiciously<span>Were they just guessing or did they get bored and give up?</span></span> answered an even 30s and 60s and 12 with times exceeding the world record.

Here are the same metrics visually; like before, click through the carousel to see them all.

<div id="wrapper">
<div id="carousel_strengths" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/maxfinger.png" | relative_url }}">
        <p class="caption">Both Megan and Nelson seem to have more finger strength than their recent grade merits, but both fall perfectly on the trendline using their max ever V grades (8, 11).</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/5reppullups.png" | relative_url }}">
        <p class="caption">For 5-rep pull-up strength, the women trend a steady 0.2 (or 20% of bodyweight) below the men. Ideally, this strength should be less than finger strength and we'll see later that, in higher V grade climbers, it is.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/pull_pushups.png" | relative_url }}">
        <p class="caption">Number of pull-ups (left) and push-ups (right) by grade. A further eight male climbers are cut off in the right plot, one claiming 286 push-ups!</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/lsit.png" | relative_url }}">
        <p class="caption">Self-reported L-sit times went as high as 2h46m; 12 in total exceeded the world record of 1m29s (during COVID raised to 1m46s, not by a climber). Less than 25% reported. Be suspicious of conclusions based on it.</p>
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


<div style="
    width: 40%;
    padding: .5rem 0 0 .5rem;
    float: right">
<img src="{{ "/assets/images/climbing/grip-positions.png" | relative_url }}" 
style="max-height: 400px" >
<p class="caption">Reproduced with the permission of Lattice Training Ltd.</p>
</div>

What about differences in strength metrics: how does finger strength compare with pulling strength? And how do they compare as we get stronger? How do half crimp and open hand compare for finger strength?

When finger and pulling strength are still low, pulling strength exceeds finger strength in both women and men. As they increase, women quickly develop <span class="float-notes">far more<span>Megan has more than 6x finger strength than pulling strength!</span></span> stronger fingers; the men develop equal finger strength only when both are ~50% body weight. In the strongest climbers, finger strength settles at roughly double pulling strength.

The difference between <span class="float-notes">half crimp<span>Not to be confused with full crimp that engages the thumb.</span></span> and  <span class="float-notes">open hand<span>Not to be confused with 3 finger drag that drops the pinky.</span></span> max hangs may average out to zero but less than a third of <span class="float-notes">those<span>35% of climbers gave half crimp max hangs, 28% gave open hand max hangs while 25% gave both: which tips the balance another 10% in favour of half crimps. To compare, 46% gave their 5-rep pull-up max weight; 29% gave both weighted pull-ups and a max hang in either grip.</span></span> reporting both had them within <span class="float-notes">5%<span>The arbitrary metric used for acceptable left/right strength asymmetry seems like a reasonable buffer to use here.</span></span> of each other. In Beastmaking, Ned suggests that hand anatomy plays a role in which grip a climber favours. Full- and half-crimp are generally the stronger grip but open hand places less strain on the finger pulleys. 

<div id="wrapper">
<div id="carousel_del_s" class="carousel slide">
    <div class="carousel-inner">
      <div class="item ">
        <img src="{{ "/assets/images/climbing/delta_fingers.png" | relative_url }}">
        <p class="caption">The difference between open and half crimp strengths is very noisy but mostly averages out; there's a slight trend to stronger open hand in the stronger climbers (only 136/9 men/women provided both max hangs).</p>
      </div>
      <div class="item active">
        <img src="{{ "/assets/images/climbing/finger_by_pull.png" | relative_url }}">
        <p class="caption">The ratio of finger strength to 5-rep pull-ups plotted against finger strength (1:1, equal strengths, along the dashed line). Climbers in this plot provided both weighted pull-ups and a max hang in either grip (leaving only 233/16 men/women).</p>
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

With this dataset of nearly <span class="float-notes">600<span>Dropping a few with suspicious data including those claiming to have broken world records.</span></span> climbers, I could train a <span class="float-notes">model<span>Several in fact, of various kinds: I started with linear regression, went to 2-4 layer dense neural networks before settling on random forests then boosted trees (which, of course, are usually best for tabular data like this). I trained many of each kind, keeping various subsets of climber features, and settled on a model that gave consistent feature influences.</span></span> to predict the hardest recent V grade of each climber given their strength metrics and training habits. The model has only mild <span class="float-notes">regression to the mean<span>Low V grade climbers are predicted high, while high V grade climbers are predicted low.</span></span>, surprising since there were many metrics that weren't provided; typical errors were <2 V grades. 

<aside>
A simple way to assess feature importance is with correlation with grade (numbers are using only climbers that provide that feature). The model can better utilize a feature if more climbers provide it (percentage that did in brackets): 

<ul>
  <li>open hand strength, 0.64 (28%)</li>
  <li>half crimp strength, 0.59 (35%)</li>
  <li># pull-ups, 0.49 (78%)</li>
  <li>year, 0.43 (all)</li>
  <li>hrs climbing per week, 0.32 (all)</li>
  <li># hangboard/campus board sessions per week, 0.34/0.3 (all, 56%/26% do)</li>
  <li>L-sit time, 0.31 (31%)</li>
  <li>5-rep pull-up strength, 0.29 (46%)</li>
  <li>hrs training per week, 0.26 (all, 46% train endurance, 79% train strength)</li>
  <li># push-ups, 0.13 (61%)</li>
  <li>BMI, -0.13 (all) </li>
</ul>
</aside>

The <span class="float-notes">feature *importance*<span>Calculated by shuffling the values of that feature among all climbers and seeing how much worse the predictions are on average. The range each feature can take varies widely, and shuffling can give an entirely unreasonable shift in a given climber. Years vary from 0 to 15 and BMI from 15 to 30, and yet most of us can't wait a year to improve and fret over BMI increments of a few pounds. Compare that to hrs on the campus board per week that varies from 0 to 5 where half an hour can make a difference.</span></span> estimates how much the model relies on it for predictions; feature *influence* is the average gains for a standard small shift in that feature. 

By far the most important feature is how many years a climber has been climbing and, next in importance, is the number of hours climbing per week. After all: 

>   Climbing is the best training for climbing

The top strength metrics by any measure are the number of pull-ups, half crimp strength, and the number of hours campus board training per week. Campus board training is synonymous with training for <span class="float-notes">power<span>Power is a measure of the rate of force applied; think of <a href="https://www.youtube.com/watch?v=HFe4LyDihDQ" title="What is Contact Strength? (A Climbing Nerd’s Investigation) Part 1/3 from Hooper's Beta">contact strength</a> and how much harder it is to catch a bad hold in a lunge than to grab it statically, or think of the fast pulling strength to initiate that lunge.</span></span> so we can say:

>   Finger and pulling strength and power are the best predictors of climbing grade

Consistently important and somewhat influential, we find BMI. For climbers with BMI < 20 (>25), raising (lowering) BMI always increases the expected grade; in between, predictions go up or down depending on the individual. The largest prediction changes were for climbers that didn't provide many strength metrics; for the three of us that did, BMI influence was <span class="float-notes">tiny<span>I saw the largest gains: by lowering my BMI by 0.5 (aka, losing 3lbs), my predicted grade increases by 0.17.</span></span>. 

Both feature assessments entirely ignore the <span class="float-notes">correlation<span>And among all the other features too. Features that are strongly correlated: number of pull-ups and pull-up strength (0.50), number of pull-ups and number of push-ups (0.44), years climbing and half crimp strength (0.34), BMI and number of push-ups (0.24), etc.</span></span> of BMI to the strength metrics: being <span class="float-notes">lighter<span>Furthermore, the denominator in the normalized metrics further amplifies any weight loss.</span></span> makes all body-weight exercises easier; while having more muscle more than compensates for the added weight. There's a limit in both lines of thinking: we should only lose excess fat and muscle and keep a safe weight for optimal recovery; we should only gain muscle beneficial to climbing and carefully balance muscle strength. To quote Tomoa from <a href="https://www.v-publishing.co.uk/books/climbing/beastmaking/">Beastmaking</a>:

>   After trying to reinforce a specific skill or train a body part, it is found that it made the total balance of the body corrupted.  &mdash;Tomoa Narasaki

To estimate the maximum expected gains of each climber, we can add up all the positive influences. These gains diminish with grade; but, luckily (if true), Megan, Nelson and I have high estimated gains for our V grade.  

<div id="wrapper">
<div id="carousel_preds" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/d_per_gender.png" | relative_url }}" style='max-height: 300px;'>
        <p class="caption">The feature influence considers the change in expected grade for a shift in a given feature. An extra half hour on the campus board has the greatest effect.</p>
      </div>    
      <div class="item">
        <img src="{{ "/assets/images/climbing/feat_imp.png" | relative_url }}" style='max-height: 300px;'>
        <p class="caption">The <a href="https://christophm.github.io/interpretable-ml-book/feature-importance.html">permutation importance</a> of each feature gives the (normalized) increase in <a class="float-notes" title="Averaged over all climbers, the 30 held out climbers included.">mean</a> squared error when that feature is randomly shuffled. Given that the error nearly doubles, 'years' is a very important feature.</p>
      </div>
      <div class="item">
        <img src="{{ "/assets/images/climbing/max_gains.png" | relative_url }}" style='max-height: 300px;'>
        <p class="caption">With the step shifts used to assess feature influence, adding up the positive steps each climber can take defines their maximal gains. The gains per climber go down with grade.</p>
      </div>       
      <div class="item">
        <img src="{{ "/assets/images/climbing/pred.png" | relative_url }}" style='max-height: 300px;'>
        <p class="caption">This <a href="https://lightgbm.readthedocs.io/en/latest/">lightgbm</a> model was trained holding out a random 30 climbers (in green) including Megan, Nelson and me: that the test climbers are predicted as well as the others is a sign the model trained well.</p>
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


The influence of each feature depends on the profile of a given climber. Here are the gains by feature for Megan, Nelson and I as examples. Of course, we won't suddenly climb harder by <span class="float-notes">changing<span>The influence of changing training and getting stronger is not something this dataset can answer since it only has a single snapshot of each climber in their present state.</span></span> training habits; rather, these are the nearest profiles to us that the model expects to have the biggest jump in grade and we might expect good results if we emulate them (and we trust the model and the dataset). 

<div id="wrapper">
<div id="carousel_d_preds" class="carousel slide">
    <div class="carousel-inner">
      <div class="item active">
        <img src="{{ "/assets/images/climbing/d_megan.png" | relative_url }}" style="max-height: 200px">
        <p class="caption">The expected feature influence for Megan's <a class="float-notes" title="Her open hand strength is roughly twice her half crimp strength and 6.5x her pulling strength; her L-sit time is 38s; lately, she isn't training and climbing very little.">profile</a>: more pull-ups; power training; and increase both grips with emphasis on her dominant open hand grip.</p>
      </div>   
      <div class="item">
        <img src="{{ "/assets/images/climbing/d_nelson.png" | relative_url }}" style="max-height: 200px">
        <p class="caption">The expected feature influence for Nelson's <a class="float-notes" title="His open hand strength > half crimp strength > pulling strength but with better balance than either Megan or I; his L-sit time is 27s; lately, he doesn't train but climbs 10hrs per week.">profile</a>: biggest gains to strengthen his half crimp; start power training; and increase his L-sit time. The predicted gains from losing 1.5kg don't seem worth it.</p>
      </div>    
      <div class="item">
        <img src="{{ "/assets/images/climbing/d_lara.png" | relative_url }}" style="max-height: 200px">
        <p class="caption">The expected feature influence for my <a class="float-notes" title="My half crimp strength > pulling strength >> open hand strength; my L-sit time is 30s; lately, I do some training and climb 6-8hrs per week.">profile</a>: power training, more pull-ups, increase half crimp strength, climb more, increase 5-rep pull-up strength, lose 3lbs, and more push-ups. </p>
      </div>       
    </div>
    <a class="carousel-control left" href="#carousel_d_preds" data-slide="prev">
      &lsaquo;
    </a>
    <a class="carousel-control right" href="#carousel_d_preds" data-slide="next">
      &rsaquo;
    </a>
  </div>
</div>


## Your Data Next

We've studied these climbers and, although we haven't discovered an ideal training progression, rough strength scales emerged that agree with intuition and the training literature. Are you more like Megan with >6x stronger fingers than pulling strength? Or like the handful of climbers that can add nearly their full bodyweight to 5 pullups and yet only climb V4? Assess yourself to see your strength profile: how balanced is it and how does it compare to the grades you're climbing? As you progress, how does your climbing improve with increased strength? 

<aside>
  <h3>Ongoing data to collect</h3>

  <ul>
    <li>indoor, system board and outdoor grades: new milestones and <span class="float-notes">sends/attempts<span>Attempts are good to track, especially for problems eventually climbed, but not all attempts are equal. Sends are definitely more stable to track.</span></span> per session (as <span class="float-notes">sum(grades)<span>Maximize this to train for endurance.</span></span> and <span class="float-notes">avg(grades)<span>Maximize this to train for power and better technique. Best to increase sum(V) first with doable grades, then to hold that steady as try to increase avg(V).</span></span>)</li>
    <li>grade by the style of climb (slab, overhang, compression, dynamic)</li>
    <li>training sessions, protocol details, and how it felt</li>
    <li>day by day, how do you feel? tired, aching? strong!</li>
    <li>resting heart rate each morning</li>
    <li>sleep quality</li>
  </ul>
</aside>

Test as many aspects as you like, but do not <span class="float-notes">train<span>They fail to serve if you start to train to them specifically (max hangs being an exception), aka you overfit if you train to the test. For instance, 'core' is more than the muscles of your torso; it's the entire chain of muscles that lets you hold tension from hands to feet. Assessing with hanging L-sits doesn't cover the entire chain; the front lever comes closer, but neither covers the full variety of positions you'll hopefully get into bouldering.</span></span> to them. Assess once per training cycle to influence how you train in the next one; twice a year to monitor your progress if you're training by climbing. 

>  If you are still getting stronger and better by just climbing, then just climb! 

From one assessment to the next, look for trends in your response to different training stimuli. When you start to plateau with a given exercise, try a more advanced progression, if any, or just switch things up (eg. max hangs to repeaters). Monitor your load capacity and <span class="float-notes">increase<span>If training gets you fitter and hence capable of more training (hurray!) or you're sleeping and eating better, and practicing active recovery.</span></span>/<span class="float-notes">decrease<span>Because other stressors in life come up, or you have more opportunity to go climbing! Or you have a trail race coming up that you also have to train for.</span></span> as necessary. It's safer to aim low and recover well for each session than to aim high and risk injury and overtraining.

<div class='nolist'>

<p><span class='orange'>Max hangs</span> in half crimp, open hand, on a sloper, pinching, etc.:
7-10s on a 20mm edge. One arm or two depends on how much weight you need to add; at some point, it makes more sense to take a little weight off and assess one-armed, with the added benefit of checking for left/right asymmetries. </p>

<p><span class="orange">Mobility</span>:
<span class="float-notes">hamstrings<span>Forward bend though it isolates the hamstrings better on the floor and, with a strap, pull your leg straight and measure the angle it makes with the floor. 60-70° is tight; 90° is ok; 105° is awesome.</span></span>; <span class="float-notes">ankles<span>How far past your toes can your knee reach; aim for at least 5", higher is better.</span></span>; <span class="float-notes">hip turnout<span>How close to the wall can your body get with knees frogged, thighs parallel to the floor; hip bones should be at most 10" from the wall, closer is better.</span></span>; <span class="float-notes">high step<span>How high can you step with your body about a foot from the wall? Make sure not to lean sideways!</span></span>; <a href="https://www.youtube.com/watch?v=gsz3BLAkkQ4" title="Can You Pass These Simple Shoulder Mobility Tests? (Recommendations for Climbers!) from Hooper's Beta">shoulders</a></p>

<p><span class="orange">Pull-ups</span>: 
Unweighted pull-ups are to endurance as weighted single reps are to strength, as 5-rep weighted pull-ups are to strength endurance. Aim for 5-rep strength around 80% of single rep strength, and single rep strength 75-100% of finger strength. </p>

<p><span class="orange">Core</span>: 
(on the floor) forearm plank; (hanging from a bar) knees tucked, or legs straight (L-sit); then front lever progression: knees tucked, one leg extended, legs wide, both legs extended. Pick the hardest 1-2 you can do 5-30s.</p>

<p><span class="orange">Power</span>:
explosive pull-ups / muscle-ups for pulling power; assess your <a href="https://www.youtube.com/watch?v=HFe4LyDihDQ" title="What is Contact Strength? (A Climbing Nerd’s Investigation) Part 1/3 from Hooper's Beta">contact strength</a> with system board climbs that challenge it, or on a <a href="https://mojagear.com/campus-board-training-with-eric-horst/">campus board</a>. Maybe your gym has hangboard with a time-resolved force meter.</p>

<p><span class="orange">Legs</span>:
<span class="float-notes">Jump taps<span>Chalk your hands and see how high you can tap a brick wall; count the bricks to measure distance.</span></span>; toe the <span class="float-notes">four corners<span>Balance on one foot and with the other nudge a small object as far forward as you can without putting weight into that foot. Then to the back, then the left and the right. It requires good balance which tests the stable leg (and core) in many positions.</span></span>; pistol squats (surely just a few are enough).</p>

<p><span class="orange">Push-ups</span>:
Useful for mantelling but stop at 20-40. Don't neglect the other <a href="https://www.youtube.com/watch?v=bEaqJ4Cc1Fo" title="Killer Home Shoulder Circuit for Rock Climbers (LONG) // from Gumby to Sharma from Hooper's Beta">antagonists</a>.</p>
</div>



Assess your strengths and train your weakest aspects. Finger strength? Pull-ups? Body tension? Steep compression climbs? Scary slab climbs? All/none of them? Which are most crucial for your next goal? What are the <span class="float-notes">lowest<span>Usually the big muscles respond the fastest to training. Any weakness that you've never trained will likely see fast improvement once you start.</span></span> hanging fruit or which take the <span class="float-notes">longest<span>Finger strength develops slowly and is arguably the most important. Mobility may come easily for you but it's hard-won tiny gains for me; you can never be too mobile (but you can be too flexible).</span></span> and should be ongoing?

<hr>


<div class='endnotes' style="color: #29627e; ">
  <div style="
      width: 60%;
      padding: .5rem 0 0 .5rem;
      float: right">
  <img src="{{ "/assets/images/climbing/grade_vs_year_8a_wt_AS_AO.png" | relative_url }}" 
  style="max-height: 450px" >
  <p class="caption">As a quick comparison, with only mild data massaging, the grade vs <span class="float-notes">adjusted<span>Somewhat skewed as the data is actually years on 8a.nu that I adjusted using the trend of grade vs years on 8a.nu; this should still underestimate the number of years climbing since the only data I have on each climber begins when they join the site. Some join from the start, others wait until their first V10.</span></span> years climbing. The trends are reassuringly similar to ours. Each climber now has one point per year that they posted to <a href="https://www.8a.nu">8a.nu</a>.</p>
  </div>

  <h3>ML Conclusions</h3>

  <p>We have a single snapshot of each climber, not their individual progression, certainly not the interventions (aka, the training) they undertook to progress in their climbing. That means our models are merely descriptive and cannot make "causal" conclusions. Still, we can expect that, if not on an individual level, then at least in aggregate, the (mean) V6 climber progresses into a V9 climber, and might progress into a V12 climber, so that the model is at least a progressive description. </p>

  <p>A model is only as good as the dataset it learns from: while ours clearly found stronger climbers climbed harder grades, it found that all forms of endurance, <a href="https://www.youtube.com/watch?v=_XONhxQ-Gbk" title="Super easy leg training to climb better in the cave AND on slab - Hooper's Beta Ep. 8">leg</a>, core, and mobility training  <em>lowered</em> expected grade. These are the biases and habits of these climbers, at best a snapshot of training advice from a decade ago; certainly not how the <a href="https://www.youtube.com/channel/UCx3XxWczzWgm1bLmgdeQJMw" title="Tomoa / Akiyo / Ikedai on YouTube">elite</a> <a href="https://www.youtube.com/channel/UC84S_JcTHwx_NBu84qWH0Xg" title="Ross & Tim on YouTube">climbers</a> <a href="https://www.youtube.com/channel/UCZ4_7FcmF_Kahg05ppmzL7g" title="Sofya Yokoyama on YouTube">train</a> today.</p>


  <p>Other datasets exist, most notably the scrapped submissions from 8a.nu <a href="https://www.kaggle.com/dcohen21/8anu-climbing-logbook">downloadable</a> from Kaggle.  I have plans to test a graph neural network to look for climbing cliques, correlated climb progressions, etc. </p>
</div>

## Resources and References


<div class='endnotes'>
  <p><a href="https://latticetraining.com">Lattice Training</a> released an interesting <a href="https://www.instagram.com/p/B9zNGplJMyG/" target="__blank">finger strength vs V grade</a> that compared well with our climbers. They offer a free <a href="https://latticetraining.com/product/my-fingers/">finger assessment</a> if you want to compare your finger strength against their dataset (and add to it). A <a href="https://www.youtube.com/watch?v=AuOkMElNgtU" title="Tom Vs. Joe who is the strongest || Lattice training symposium ft. Tom Randall">video</a> with the Bobats showed them going through a thorough Lattice Training assessment that included various measures of strength, power, endurance, and mobility. </p>

  <p>The Substr8 Climbing Performance <a href="https://www.substr8climbing.com/athletic-assessment">assessment</a> includes the plank, max hangs, number of pull-ups, and an interesting test of strength endurance: do 3 inclined ring pull-ups at 45&deg; every 10s for as long as possible (up to 6min), "resting" in between but always inclined.</p>

  <p>Steve Bechtel at <a href="https://www.climbstrong.com">Climb Strong</a> has a good intro to <a href="https://www.climbstrong.com/education-center/quantifying-bouldering-sessions/">Quantifying Bouldering Sessions</a>, including monitoring sum/average of the grades sent per session, mentioned in the text, and "session density", sum(V)/duration of session, as a quick measure of load.</p> 

  <p>Sorely missing in my analysis and poorly treated in most training books: improving your mobility for climbing (and life) may actually yield the greatest gains. Climbing specific routines from <a href="https://latticetraining.com">Lattice Training</a> (<a href="https://www.youtube.com/watch?v=lvErtoi9NCY">overview</a>, <a href="https://www.youtube.com/watch?v=tf_FkzgLHp0">shoulders</a> and <a href="https://www.youtube.com/watch?v=FIXJZhQz4V8">lower body</a>) and <a href="https://www.hoopersbeta.com/">Hooper's Beta</a> (<a href="https://www.youtube.com/watch?v=ZhyBhad0zRM">shoulders</a>, <a href="https://www.youtube.com/watch?v=f86QMiSMaZ4">hips</a> and <a href="https://www.youtube.com/watch?v=_yk_EMQDM_Q">lower body</a>); or if you prefer a program, I'm in level 2/3 of <a href="https://www.youtube.com/user/Calisthenicmovement">Calisthenic Movement</a>'s <a href="https://www.calimove.com/p/mobility">mobility program</a> and very pleased with my progress and how well it goes with climbing.</p>

  <h3>Books and Papers</h3>
  <p><a href="https://www.v-publishing.co.uk/books/climbing/beastmaking/">Beastmaking</a>: a fingers-first approach to becoming a better climber, by Ned Feehally. Certainly biased toward climbing foremost, supplemented with hangboard and system board training, he explains from grip outward how to train strength, power, core and footwork. Although he emphasizes the importance of mobility, he doesn't cover this well.</p>

  <p><a href="https://us.humankinetics.com/products/science-and-practice-of-strength-training-3rd-edition">The Science and Practice of Strength Training</a> is a wonderful, (nearly fully) self-contained book on strength training intended for coaches and trainers to learn how personalize training for individuals. Discusses strength vs power in detail; strength scaling with weight; strength through muscle systems about a joint (or multiple joints). Pleases my inner physicist and yet the math is fairly straightforward and should be alright for most.</p>

  <p><a href="https://www.patagonia.ca/product/training-for-the-new-alpinism/BK695.html">Training for the New Alpinism</a> by Steve House and Scott Johnston. For anyone interested in self-coaching for, possibly, multiple disciplines (aka, trail running and bouldering), this book explains the physiology of endurance vs strength training and the phases of each training cycle. The athlete tales are great reads and the (mountain) photos are spectacular. </p>

  <p><a href="https://erj.ersjournals.com/content/44/4/905">All-age relationship between arm span and height in different ethnic groups</a>, Philip H. Quanjer, et. al. European Respiratory Journal 2014 44: 905-912</p>

</div>
