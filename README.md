# A beginner's guide to karaoke effects

## K-Timing

*Note: I assume that you have experience timing in Aegisub. If you don't, refer to [Doki's Timing Guide](https://yukisubs.files.wordpress.com/2016/10/doki_timing_guide.pdf) to get started before continuing on.*

### What is K-Timing? 

K-Timing is the act of timing syllables in a song such that they match up with when they're sung. There's a couple differences between K-Timing and regular timing. 

1. You will be timing to audio 90% of the time. While it's worth to sync to keyframes to avoid scene bleeds sometimes, you won't have to worry about it most of the time. 
2. You don't have to worry as much about CPS for lines, because it can be fixed later on with a good effect anyway. 
3. K-Timing doesn't mean that you're timing every syllable in a separate line (though you can if you're super M), but instead, you'll have the whole line timed by itself, followed by each syllable with a `\k` tag.

![Example K-Timed line](https://i.imgur.com/NRCZkCp.png)
*First line of SUPER NOVA K-Timed*

### Resources you'll need

- Aegisub (duh!)
- A song to K-Time
- Lyrics
- [FuwaFuwaTime Karaoke Timer](https://nanodesu.moe/karaoke-timer/) by gacha4life

### Instructions

1. Load the audio into FFT.
![TOKIMEKI Runners](https://i.imgur.com/CEa4QrM.png)
2. Input the lyrics. If you're using romaji lyrics, you can also use the Syllablize feature to attempt to auto-generate the syllables. If not, you'll have to manually do that, so bust out your favorite text editor and insert `|` between each syllable.
![Syllablized Lyrics](https://i.imgur.com/2O4ew8F.png)
3. Start timing! With the default controls, you can press `Play`, then tap `l` every time a syllable is about to be sung. If you've played rhythm games before, it's going to feel quite similar, except that there's no visual cues, so you'll have to rely entirely on your knowledge of the song to know when to tap.
![Timing Progress](https://i.imgur.com/L9fAJAQ.png)
4. If you need to, press `Backspace` to undo your work on the current line to start over and try again. Remember that you can also seek through the song to retry lines if you need to. The `Controls` tab should have more information on what you can do.
5. Once you're done timing, click on `Output Timing`, then select it all and copy. After that, open up an Aegisub window, then paste it in, and you'll have the timed lines and the `\k` tags for the syllables. And you're done! Maybe...?
![Example output](https://i.imgur.com/mQf2BnE.png)
![Aegisub](https://i.imgur.com/zbj8UXo.png)

### Cleaning up

Unless you have a song that's super straightforward and you managed to time perfectly, chances are that your timing is off in certain points (or all of it). No problem, that's what Aegisub is for! Load the song's audio in, then start inspecting the lines and syllables.

- Click on the mic icon on the far right of the list of icons under the audio graph preview on the right. This will open Aegisub's Karaoke Editor mode, where you'll be able to see the individual timings of each syllable relative to the audio. You can also use the Karaoke Editor to join together syllables, split syllables, and also modify their durations by clicking and dragging around the markers. Remember to commit before moving onto the next line!
![Silent Blaze Karaoke](https://i.imgur.com/qVAjGkl.png)
- For any lines that are wrongly timed, go ahead and retime them. Then, you can open Karaoke Editor and fix the syllable timings if they are off.
- Load a dummy video that's around the length of the song and give the timings a watch-over. The effect will be super basic but what's more important are the timings, so if you spot anything off, go back and fix them.
![Silent Blaze dummy video](https://i.imgur.com/0sCujIk.png)

After this all, congrats! You now have a song that's properly K-Timed and ready for karaoke effects.

### Other tips

- You don't have to time the entire song at once in FFT. You can time small sections and fix them as you go along if that's less stressful. `Output Timing` also will output timings even if only part of the song is done, so you can start cleaning up small sections first.
- You can fix also fix the syllables before timing in FFT as well. Changing the lyrics at any point in FFT resets all K-Timing done so far, so after you click `Syllablize`, copy the lyrics over to your favorite text editor, open up the song in your favorite music player, then add/delete `|` as needed.
- You can have blank `\k` tags or `\k` tags with only whitespace. If your effect will look better with them, then feel free to add them in (FFT supports blank/whitespace syllables too).

## Karaoke Templating

*Note: I assume that you have experience typesetting in Aegisub. If you don't, refer to [unanimated's Typesetting Guide](http://unanimated.hostfree.pw/ts/index.htm?i=2) to get started before continuing on.*

### What is Karaoke Templating?

Karaoke Templating is the art of giving fancy effects to your karaoke. Normally, it's done to the lyrics of the song, but if you're feeling fancy, you can add effects to the TL (if there's one) or anything, really.

If you've done typesetting before, then you should know what many of the override tags in Aegisub do. The real strength of karaoke templating is that you can specify what tags to apply to certain lines, syllables or characters, and also change the timings if you want, so it's much faster than manually typesetting each line.

### Resources you'll need

- Aegisub (duh!)
- K-Timed lyrics (if you don't have any yet, use [this](https://raw.githubusercontent.com/ahuei123456/KFX-Tutorial/master/files/silent%20blaze.ass) as an example)
- [Karaoke Templater documentation](https://aeg-dev.github.io/AegiSite/docs/3.2/automation/karaoke_templater/)
- [Lua documentation](https://www.lua.org/manual/5.2/) (Optional, but knowing Lua can enable a lot of nice effects)

### Starting off

So you've taken a brief look into the Karaoke Templater documentation, and immediately realize that you have no idea what's going on. Don't worry, that's perfectly normal, because it's a *lot* to read through. Let's start with the basics.

### Templates

Templates are the bread and butter of KFX. It's what lets you apply effects to your lines/syllables, and barring minor exceptions, every effect will have at least one template.

To create a template line, create a new line in Aegisub at the very top, then declare it as a `Comment`. After that, go to the `Effect` box, and type in `template`. Congrats, now you have a template! Set the style to be the same as your romaji lyrics, then click on `Automation -> Apply karaoke template`. 

![Empty Template Line](https://i.imgur.com/lPzLMfU.png)

You should see two things happen. First, all your romaji lines got commented, and they now have `karaoke` in the `Effect` field. Second, a whole bunch of lines popped up at the bottom, each with individual syllables timed to their original lines, some blank.

![template syl results](https://i.imgur.com/inD9tBT.png)

This is the first type of template that we'll be looking at, a syllable template. If you have `template` or `template syl` in the `Effect` field, then the line gets treated as syllable template, and all the text in the line will be prepended to every syllable (including tags!). Try it out. Type `{\fade(200, 200)}` into the text box, then do `Automation -> Apply karaoke template` again.

![fade template](https://i.imgur.com/g13kvMZ.png)

Scroll all the way down, and you'll see the syllables again. Except this time, the syllables will all have `{\fad(200, 200)}`, because it was in the template field. Congratulations, you've applied your first effect (even though it's a bit useless)!

![fade effect](https://i.imgur.com/crLXS4c.png)

There are two other main types of templates (three, but let's do two for now). First is `template line`, which prepends the text to each syllable in your line but in one whole line instead, stripped of all other tags. Next is `template char`, which prepends the text to each character of your line. Each has its use, and you'll need them for some effects, but for now, let's focus on `template syl`.

![template line](https://i.imgur.com/cYqNOEM.png)
![template line effect](https://i.imgur.com/Ko3Jv1J.png)

### Positioning using $-vars

After you applied the template, now you have each individual syllable in its own line. But, each syllable is timed the exact same, so unfortunately they'll all just stack with each other. So, we'll have to fix that with additional `\pos` tags. Thankfully, the Karaoke Templater has a way of generating the correct positions for the syllables.

In the same `template syl` line as above, add in `\pos($center, $middle)`. Then, do `Automation -> Apply karaoke template`, and take a look at all the generated lines. You'll see a `\pos` tag there, filled in with some magic numbers. If you render the subs (on a dummy or actual video), you'll see that all the text appears where it's supposed to instead of stacking on each other. Wow, magic! But how did that work?

![pos template](https://i.imgur.com/RrUJ5KJ.png)
![pos effect](https://i.imgur.com/Ff6P5P6.png)

The answer lies in the presence of `$center` and `$middle`, which are called `$-vars`, by virtue of having an `$` before its name. When the Karaoke Templater script runs, it replaces any instances of these `$-vars` with the corresponding data from the line/syllable/character that the variables are referring to. In this case, because we used a `template syl`, `$center` and `$middle` would refer to the center x and y positions of the syllable when it is rendered, respectively. You can find the full list of all the `$-vars` [here](https://aeg-dev.github.io/AegiSite/docs/3.2/automation/karaoke_templater/inline_variables/), which you can then use in your tags to generate effects.

### Re-timing and inline execution

Now, you have each syllable in its own line, and correctly positioned! But... there's no effect. All the syllables in a line are timed the exact same as the line, so even if you added any fancy effects, then it'll just apply to each syllable equally, so you might as well just have applied effects to the line as a whole without bothering with K-Timing. What gives?

There are two ways of fixing that. First, we could use `$-vars`, just like we just learned. If you look at the [documentation](https://aeg-dev.github.io/AegiSite/docs/3.2/automation/karaoke_templater/inline_variables/), you'll see some variables related to syllable timing, which you can use in your template. Let's give it a shot with our good friend the `\t`. Try adding this into your template: `\alpha&H00&\t($start, $end, \alpha&HFF&)`, then do `Automation -> Apply karaoke template` as usual. 

![t $var](https://i.imgur.com/vz7JoVk.png)

Oh hey, now there's an effect where each syllable slowly fades out after it's sung! That's an actual effect!

The second, and more powerful way, is to use `retime()`. Simply put, it allows you to change the timing of each syllable, so now the individual syllables are no longer bound by the line's timing. Type `!retime("syl", 0, 0)!{\pos($center, $middle)}` into the template line in place of what's there now, and do `Automation -> Apply karaoke template` again. 

![retime template](https://i.imgur.com/D3nHWQe.png)

Scroll down, and now you'll see each syllable with a different timing, as per its original `\k` tag. If you play the video, then each syllable now only appears at its specified timing, disappearing when the next one appears. It's a properly timed effect!

![effect](https://i.imgur.com/7Cx4SJ1.png)

There are two parts to the `retime()`. The first is the presence of the `!!` around it. Using the exclamation marks tells the Karaoke Templater script that the text between it is meant to be a code block, so the code in it is executed instead of being taken literally. For example, if you wanted to shift your syllables up and used `{\pos($center, $middle-100)}`, then you'll see that your tag becomes something like `{\pos(880, 1006-100)}`, because the `$-var` is just replaced literally, but the subtraction is not executed. 

![fail](https://i.imgur.com/5Ap0Gv2.png)

However, if you surround the subtraction with `!!` to make it `{\pos($center, !$middle-100!)}`, then the subtraction is properly executed, giving you `{\pos(676, 906)}`.

![correct template](https://i.imgur.com/AZAaNtN.png)
![pass](https://i.imgur.com/RynvHSb.png)

Second, let's take a look at the arguments passed to the `retime()`. Just like a regular override tag, `retime()` takes in arguments, or three. The first one, which was the `"syl"` you saw, specifies that the base timing for the generated syllable to be the timing of the syllable from the `\k` tag. The second and third arguments are the offsets for the start and end (in ms), respectively. For example, if you wanted a syllable to start 100ms before and end 100ms after its normal time, then you'd put in `!retime("syl", -100, 100)!`. You can then combine this with something like a `\fade(100,100)` to make the syllable fade in and out as well. 

![retime 100](https://i.imgur.com/vfk4X3I.png)
![retime fade fx](https://i.imgur.com/h5U5ukW.png)

There are other base timings that you can use if you want to modify the syllable timing differently, which can all be found [here](https://aeg-dev.github.io/AegiSite/docs/3.2/automation/karaoke_templater/code_execution_environment/).

### Code lines

*To-do*

### Try it out

Here's some examples of KFX. See if you can recreate them before taking a look at the templates that I've used!

*To-do*

