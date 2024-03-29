---
layout: post
category: [cyber]
title: "How to hack an amusement park"
author: PixelSergey
permalink: /lintsi/
---

In the summer of 2019 I came to the realisation:
I haven't gone to an amusement park in years!
There was a new ride in my local park that seemed very fun,
so I decided to look it up on their page,
just to see what it was like.

![Stock image of a rollercoaster](https://upload.wikimedia.org/wikipedia/commons/0/0e/WV_banner_Far_North_suburbs_Demon_rollercoaster_at_Six_Flags_Great_America.jpg)

While browsing the amusement park's pages,
I spotted a small banner on the side of the screen
advertising their season pass deal.
Upon clicking it, I was enlightened with the following information:

- Season passes are available via a mobile app
- They cost ~200€ per season
- Upon purchase, a customer gets an activation code sent to their email,
which they use to activate the app
- To use the app, one has to register an account and take a profile photo
(which can only be changed with authorisation from the amusement park)
- Every day, a season pass owner can come to the amusement park,
where the cashier validates the pass and gives out a wristband for the day.

Anyone with a hacker mindset will feel the alarm bells going off in their head.
How exactly is this app verified by the cashier?
How exactly is the activation code verified by the app?
What kind of security does the app actually have?

## Exploitation

### Getting the app

The app could be freely downloaded from Google Play or the App Store.
Upon downloading it, I noticed a few more questionable things.
For one, my phone tried to autofill my `http://localhost` password
instead of my amusement park password, which I found quite weird.
It also didn't ask you to verify your email:
both `sauli.niinisto@suomi.fi` and `a@a.a` yielded valid user accounts.
The whole platform did not seem too robust.

I downloaded the app to my computer to analyse it further.

### Reversing the app

As I was analysing an APK file,
I thought that I had to decompile the internals
to raw Java code, which I could somehow modify and recompile...
As it turned out, the Java code didn't store any of the app's data.
Its only purpose was to load an `index.html` file from a nearby assets folder.
So, now, instead of decompiling binaries,
I could just unzip the APK file and get everything I needed from there.
Funnily enough, the source code was all in plain text, grouped together in one folder.

Alongside the `index.html` file, there was a JavaScript file
containing all of the program logic in (slightly obfuscated) plain text.
It had 160 lines, totalling 6,412,605 characters.
A quick run through a JavaScript beautifier extended the line count to 100687.
It was time for some analysis.

As I had almost no background in JavaScript and web-based app programming,
it was hard for me to start poking away at the app.
The lack of descriptive variable names did not make this feat easier.

I first thought to somehow exploit the "calls" the app did.
For example, the function to check your activation code would call

```js
r.call("checkActivationCode", t.state.activationCode, function(e, n) { /* SNIP */ });
```

where the omitted code in the curly braces would take the server's response `n`
and use it to determine what message to show the user.
My idea was to change this value `n` somehow,
but I could not find where it was set in the code.

I then realised that, instead of changing the return value,
I could simply change the code that handles the response.
This proved to be very effective. For example, the following code

```js
// Code snipped for brevity

r.call("checkActivationCode", t.state.activationCode, function(e, n) {
  "number" == typeof n ? (!1 === n ? t.setState({
    message: "Failure message in Finnish"
  }) : t.setState({
    message: "Success message in Finnish"
})
);
```

turned into

```js
// Code snipped for brevity

r.call("checkActivationCode", t.state.activationCode, function(e, n) {
  "number" == typeof n ? (!0 === n ? t.setState({
    message: "Failure message in Finnish"
  }) : t.setState({
    message: "Success message in Finnish"
})
);
```
_(Can you spot five differences? Hint: there's only one)_

Although I have grossly oversimplified the code here,
the idea remains: the app does no checking for the integrity of its code,
blindly trusts the server's responses, and, most importantly,
doesn't stop you from removing and editing chunks of its code to modify functionality.

### Finalising setup

To repack the app, I simply rezipped the APK files I had extracted
and then signed it with
[Android MultiTool](https://forum.xda-developers.com/showthread.php?t=2326604)
(what's the point in signing APKs if anyone can just do it themselves?)

I then installed it on my stock Android device,
where I then simply logged in as before and got exactly what I wanted:
the ticket activation screen.

## Aftermath

After finding the vulnerability,
I immediately reported it to the amusement park's development team.
They have since changed their SaaS provider,
rewritten the app entirely with a new non-JavaScript framework,
and added a QR code that the cashier scans before giving you a free ticket.

I received *two free day passes* as a bug bounty.

## Credits

- [Reverse engineering Android APKs](https://reverseengineering.stackexchange.com/a/19032)
- The amusement park clowns
- [How to exit vim](https://stackoverflow.com/questions/11828270/how-do-i-exit-the-vim-editor)
