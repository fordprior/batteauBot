# batteauBot
An alexa skill in Node.js. It's still in beta ([click here to test](https://skills-store.amazon.com/deeplink/tvt/9aed219785802408375323d0eebba27ce2f86fe2e0c302aabf95a365b3615366598a6cb74766481044b3dbad37973d8301ce80d4cf787ff4f99dc47f1045c379cb05ce1b03071c7f9abd2eeffccb915c5f8eba0990ee7447ecd5b55c7f18769c95ebda2361719a519d007d54a0c7d4)).

## prerequisites
Nothing local. Just fire up your Amazon Dev Console (for the skill code) & your AWS Console (for the triggering code).

## concept
Alexa has access to a core library of skills + extras you can turn on via Amazon.com. Available skills are "awoken" with something called an `invocation` ("Alexa, ask WeatherBot..."), then directed with `utterances` ("...is it going to rain in Baltimore this weekend?"). These utterances engage blocks of code called `intents`, which churn out a response. You can also insert `slots` to capture variables within utterances, use those variables to develop a more complex dialog model, and do a zillion other crazy things. But that's the gist.

## what I did
Nobody knows about batteaux, which is a shame. So I wrote a little skill (1) to answer a couple of stock questions people might ask; and (2) for fun, to spout off a random fact about batteaux.

## how I did it
I combined the instructions from 2 tutorials: [fact](https://github.com/alexa/skill-sample-nodejs-fact) and [how-to](https://github.com/alexa/skill-sample-nodejs-howto). I also did some custom javascript to hack through issues.

## the code
Paste the `lambda.js` file into the Lambda function you create, and then paste the `intents.json` file into the code editor within your Alexa model builder UI.

Good luck!
