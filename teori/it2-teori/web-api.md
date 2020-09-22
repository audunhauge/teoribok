# Web API

## Web Animation API <a id="web-animation-api"></a>

Web Animation API lar oss lage og kontrollerer animasjoner med javascript.

\(denne artikkelen er oversatt fra MDN\)

### Møt Web Animation API <a id="m&#xF8;t-web-animation-api"></a>

Ved å bruke Web Animation API kan vi flytte interaktive animasjoner fra CSS til javascript. Vi kan endre varighet og avspillingshastighet dynamisk. Egenskaper som animeres kan også endres underveis.

### Nettlesere som støtter APIen <a id="nettlesere-som-st&#xF8;tter-apien"></a>

God støtte i chrome og firefox.

### CSS versjonen <a id="css-versjonen"></a>

Her er animasjonen for Alice som faller ned i kaninhullet.

Merk at bakgrunnen beveger seg, Alice roterer og fargen skifter fra svart til mørk burgunder.

Under en forenkla CSS for animasjonen

```text
#alice {
  animation: aliceTumbling infinite 3s linear;
}

@keyframes aliceTumbling {
  0% {
    color: #000;
    transform: rotate(0) translate3D(-50%, -50%, 0);    
  }
  30% {
    color: #431236;
  }
  100% {
    color: #000;
    transform: rotate(360deg) translate3D(-50%, -50%, 0);
  }
}
```

### Konvertering til javascript <a id="konvertering-til-javascript"></a>

Vi lager et array som inneholder informasjon om nøkkelrammene \(keyframes\).

```text
var aliceTumbling = [
  { transform: 'rotate(0) translate3D(-50%, -50%, 0)', color: '#000' },
  { color: '#431236', offset: 0.333},
  { transform: 'rotate(360deg) translate3D(-50%, -50%, 0)', color: '#000' }
];
```

Her bruker vi et array som inneholder flere objekter. Hvert objekt tilsvarer en keyframe i css, men vi trenger ikke eksplisit angi prosenten for hver nøkkelramme. Animasjonen blir delt i like deler avhengig av hvor mange nøkkelrammer du har oppgitt. En animasjon med tre rammer vil spille den midterste på 50% dersom du ikke overstyrer dette.

Når vi ønsker å spesifisere en offset, legger vi til

```text
offset: 0.333
```

slik at denne rammen spilles på 33%.

Vi må spesifisere minst to rammer, start og slutt.

### Styring av tid <a id="styring-av-tid"></a>

Vi må også lage et objekt som styrer tiden for animasjonen:

```text
var aliceTiming = {
  duration: 3000,
  iterations: Infinity
}
```

En del forskjeller mellom hvordan verdier angis i CSS og js:

* Varighet i ms i stedenfor sekunder
* iterations, ikke iteration-count.
* Infinity, ikke infinite
* easing er default linear \(ikke eas-in\).

Nå kan vi sette det hele sammen med Elemnet.animate\(\) metoden:

```text
let aliceAni = document.getElementById("alice").animate(
  aliceTumbling,
  aliceTiming
)
```

Og dermed begynner animasjone å spille \(implisitt play\(\) for animasjonen\).

Dersom du ikke ønsker å starte den med en gang, må du kjøre aliceAni.stop\(\).

Alle DOM elementer du kan animere med CSS kan animeres med animate\(\). Du kan også skrive animasjonen på denne måten:

```text
document.getElementById("alice").animate(
  [
    { transform: 'rotate(0) translate3D(-50%, -50%, 0)', color: '#000' },
    { color: '#431236', offset: 0.333},
    { transform: 'rotate(360deg) translate3D(-50%, -50%, 0)', color: '#000' }
  ], {
    duration: 3000,
    iterations: Infinity
  }
);
```

Her har vi ikke laga egne objekter for keyframes og timing.

### Styring av avspilling med play\(\), pause\(\), reverse\(\) og playbackRate <a id="styring-av-avspilling-med-play-pause-reverse-og-playbackrate"></a>

Den viktigste forskjellen på CSS animasjon og WAAPI er muligheten til å styre avspilling \(hastighet, retning, pauser osv\).

WAAPI gir oss flere nyttige metoder for å styre avspilling, vi skal se på play\(\) og pause\(\) som vi bruker til å styre vokse/krympe for Alice i spillet.

Playing the growing and shrinking game with Alice.

In this game, Alice has an animation that causes her to go from small to big which we control via a bottle and a cupcake. Both of these have their own animations.

Pausing and playing animations

We’ll talk more about Alice’s animation later, but for now, let’s look closer at the cupcake’s animation:

```text
var nommingCake = document.getElementById('eat-me_sprite').animate(
[
  { transform: 'translateY(0)' },
  { transform: 'translateY(-80%)' }   
], {
  fill: 'forwards',
  easing: 'steps(4, end)',
  duration: aliceChange.effect.timing.duration / 2
});
```

The Element.animate\(\) method will immediately run after it is called. To prevent the cake from eating itself up before the user has had the chance to click on it, we call Animation.pause\(\) on it immediately after it is defined, like so:

nommingCake.pause\(\); We can now use the Animation.play\(\) method to run it whenever we’re ready:

nommingCake.play\(\); Specifically, we want to link it to Alice’s animation, so she gets bigger as the cupcake gets eaten. We can achiveve this via the following function:

```text
var growAlice = function() {

  // Play Alice's animation.
  aliceChange.play();

  // Play the cake's animation.
  nommingCake.play();
}
```

When a user holds their mouse down or presses their finger on the cake on a touch screen, we can now call growAlice to make all the animations play:

```text
cake.addEventListener("mousedown", growAlice, false);
cake.addEventListener("touchstart", growAlice, false);
```

### Other useful methods <a id="other-useful-methods"></a>

In addition to pausing and playing, we can use the following Animation methods:

Animation.finish\(\) skips to the end of the animation. Animation.cancel\(\) aborts the animation and removes its effects. Animation.reverse\(\) sets the animation’s playback rate \(Animation.playbackRate to a negative value so it runs backwards. Let’s take a look at playbackRate first — a negative playbackRate will cause an animation to run in reverse. When Alice drinks from the bottle, she grows smaller. This is because the bottle changes her animation’s playbackRate from 1 to -1:

```text
var shrinkAlice = function() {
  aliceChange.playbackRate = -1;
  aliceChange.play();
}

bottle.addEventListener("mousedown", shrinkAlice, false);
bottle.addEventListener("touchstart", shrinkAlice, false);
```

In Through the Looking-Glass, Alice travels to a world where she must run to stay in place — and run twice as fast to move forward! In the Red Queen’s Race example, Alice and the Red Queen are running to stay in place \(check out the full code on Codepen\):

Alice and the Red Queen race to get to the next square in this game.

Because small children tire out easily, unlike automaton chess pieces, Alice is constantly slowing down. We've done this in the code by setting a decay on her animation’s playbackRate:

```text
setInterval( function() {

  // Make sure the playback rate never falls below .4
  if (redQueen_alice.playbackRate > .4) {
    redQueen_alice.playbackRate *= .9;    
  }

}, 3000);
```

But urging them on by clicking or tapping causes them to speed up by multiplying their playbackRate:

```text
var goFaster = function() {

  redQueen_alice.playbackRate *= 1.1;

}
document.addEventListener("click", goFaster);
document.addEventListener("touchstart", goFaster);
```

The background elements also have playbackRates that are impacted when you click or tap. What happens when you make Alice and the Red Queen run twice as fast? What happens when you let them slow down?

Getting information out of animationsEDIT Imagine other ways we could use playbackRate, like improving accessibility for users with vestibular disorders by letting them slow down animations across an entire site. That’s impossible to do with CSS without recalculating durations in every CSS rule, but with the Web Animations API, we could use the upcoming \(not supported in browsers yet!\) document.getAnimations\(\) method to loop over each animation on the page and halve their playbackRates like so:

```text
document.getAnimations().forEach(
  function (animation) {
    animation.playbackRate *= .5;
  }
);
```

With the Web Animations API, all you need to change is just one little property!

Another thing that’s tough to do with CSS Animations alone is creating dependencies on values provided by other animations. For instance, in the Growing and Shrinking Alice game example, you might have noticed something odd about the cake’s duration:

duration: aliceChange.effect.timing.duration / 2 To understand what’s happening here, let’s take a look at Alice’s animation:

```text
var aliceChange = document.getElementById('alice').animate(
  [
    { transform: 'translate(-50%, -50%) scale(.5)' },
    { transform: 'translate(-50%, -50%) scale(2)' }   
  ], {
    duration: 8000,
    easing: 'ease-in-out',
    fill: 'both'
  });
```

Alice’s animation has her going from half her size to twice her size over 8 seconds. Then we pause her:

```text
aliceChange.pause();
```

If we had left her paused at the beginning of her animation, she’d start at half her full size, like she’d drunk the entire bottle already! We want to set her animation’s “playhead” in the middle, so she’s already halfway done. We could do that by setting her Animation.currentTime to 4 seconds like so:

```text
aliceChange.currentTime = 4000;
```

But while working on this animation, we might change Alice’s duration a lot. Wouldn’t it be better if we set her currentTime dynamically, so we don’t have to make two updates at a time? We can in fact do so by referencing aliceChange’s Animation.effect property, which returns an object containing all the details of the effect\(s\) active on Alice:

```text
aliceChange.currentTime = aliceChange.effect.timing.duration / 2;
```

effect lets us access the animation’s keyframe and timing objects — aliceChange.effect.timing points to Alice’s timing object \(which is of type AnimationEffectTimingReadOnly\) — this contains her AnimationEffectTimingReadOnly.duration. We can divide her duration in half to get the midpoint for her animation’s timeline, setting her to be normal height. Now we can reverse and play her animation in either direction to make her grow smaller or larger!

And we can do the same thing when setting the cake and bottle durations:

```text
var drinking = document.getElementById('liquid').animate(
[
  { height: '100%' },
  { height: '0' }   
], {
  fill: 'forwards',
  duration: aliceChange.effect.timing.duration / 2
});
drinking.pause();
```

Now all three animations are linked to just one duration, which we can change easily from one place.

We can also use the Web Animations API to figure out the animation's current time. The game ends when you run out of cake to eat or empty the bottle. Which vignette players are presented with depends on how far along Alice was in her animation, whether she grew too big and can't get in the tiny door anymore or too small and cannot reach the key to open the door. We can figure out whether she's on the large end or small end of her animation by getting her animation's currentTime and dividing it by her activeDuration:

```text
var endGame = function() {

  // get Alice's timeline's playhead location
  var alicePlayhead = aliceChange.currentTime;
  var aliceTimeline = aliceChange.effect.activeDuration;

  // stops Alice's and other animations
  stopPlayingAlice();

  // depending on which third it falls into
  var aliceHeight = alicePlayhead/aliceTimeline;

  if (aliceHeight <= .333){
    // Alice got smaller!
    ...

  } else if (aliceHeight >= .666) {
    // Alice got bigger!
    ...

  } else {
    // Alice didn't change significantly    
    ...

  }
}
```

Note: getAnimations\(\) and effect are not fully supported as of this writing, but the polyfill does support them today. Callbacks and promisesEDIT CSS Animations and Transitions have their own event listeners, and these are also possible with the Web Animations API:

onfinish is the event handler for the finish event and can be triggered manually with finish\(\). oncancel is the event handler for the cancel event and can be triggers with cancel\(\). Here we set the callbacks for the cake, bottle, and Alice to fire the endGame function:

```text
// When the cake or runs out... 
nommingCake.onfinish = endGame;
drinking.onfinish = endGame;

// ...or Alice reaches the end of her animation
aliceChange.onfinish = endGame;
```

Prefer promises? The Web Animations API also specifies two promises: onfinish and oncancel.

These promises are not fully supported as of this writing.

### Conclusion <a id="conclusion"></a>

These are the basic features of the Web Animations API, most of which are already supported across the latest release versions of Firefox and Chrome. By now you should be ready to "jump down the rabbit hole" of animating in the browser and ready to write your own animation experiments! If you're using the API and want to share, try using the \#WAAPI hashtag. We will be watching and will write more tutorials to cover further features as support spreads!

