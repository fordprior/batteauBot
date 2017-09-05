# batteauBot
An alexa skill in Node.js

## prerequisites
Nothing local. Just fire up your Amazon Dev Console (for the skill code) & your AWS Console (for the triggering code).

## concept
Alexa has access to a core library of skills + extras you can turn on via Amazon.com. Available skills are "awoken" with something called an `invocation` ("Alexa, ask WeatherBot..."), then directed with `utterances` ("...is it going to rain in Baltimore this weekend?"). These utterances engage blocks of code called `intents`, which churn out a response. You can also insert `slots` to capture variables within utterances, use those variables to develop a more complex dialog model, and do a zillion other crazy things. But that's the gist.

## what I did
Nobody knows about batteaux, which is a shame. So I wrote a little skill (1) to answer a couple of stock questions people might ask; and (2) for fun, to spout off a random fact about batteaux.

## how I did it
I combined the instructions from 2 tutorials: fact[https://github.com/alexa/skill-sample-nodejs-fact] and how-to[https://github.com/alexa/skill-sample-nodejs-howto]. I also did some custom javascript to hack through issues.

# the code

The Node code pasted into my Lambda function:
```json
'use strict';
var Alexa = require('alexa-sdk');

//=========================================================================================================================================
//TODO: The items below this comment need your attention.
//=========================================================================================================================================

//Replace with your app ID (OPTIONAL).  You can find this value at the top of your skill's page on http://developer.amazon.com.  
//Make sure to enclose your value in quotes, like this: var APP_ID = "amzn1.ask.skill.bb4045e6-b3e8-4133-b650-72923c5980f1";
var APP_ID = "amzn1.ask.skill.5fe48205-2852-49be-86eb-0561840bb24e";

var SKILL_NAME = "Batteau Bot";
var ANSWER_WHAT_IS = "A bateau is a type of wooden boat which was used for commercial navigation of North America's inland waterways during the 17 and 18 hundreds. In modern times, it used recreationally by an active community of hobbyists";
var ANSWER_HOW_BUILD = "Bateau are made by hammering a bunch of wood together. There are several steps. First, a dozen u-shaped ribs are constructed and mounted to a central king plank, which functions much like a spine. Next, the hull is covered with smaller planks from end to end. Lastly, the bow and stern are mounted and the boat is caulked to prevent leaks. If you have ever built a bateau yourself, the brevity of this answer will likely offend you.";
var ANSWER_WHO_USES = "Prior to colonization, bateau were used by French fur traders. During the colonial era, they were used by African American slaves. In modern times, they are used recreationally by renaissance rednecks throughout the Virginia piedmont.";
var GET_FACT_MESSAGE = "Here's your fact: ";
var HELP_MESSAGE = "You can ask me a question, say, tell me a batteau fact, or, you can say exit.";
var HELP_REPROMPT = "What can I help you with?";
var STOP_MESSAGE = "Goodbye!";

//=========================================================================================================================================
//TODO: Replace this data with your own.  You can find translations of this data at http://github.com/alexa/skill-sample-node-js-fact/data
//=========================================================================================================================================
//NOTE: I took out my massive list of facts here to make this easier to read. They were listed in this data variable.
var data = [
        "A fact.",
        "Another fact.",
        "One last fact."
];

//=========================================================================================================================================
//Editing anything below this line might break your skill.  
//=========================================================================================================================================
exports.handler = function(event, context, callback) {
    var alexa = Alexa.handler(event, context);
    alexa.APP_ID = APP_ID;
    alexa.registerHandlers(handlers);
    alexa.execute();
};

var handlers = {
    'LaunchRequest': function () {
        this.emit('GetNewFactIntent');
        this.emit('AnswerWhatIs');
        this.emit('AnswerWhoUses');
        this.emit('AnswerHowBuild');
    },
    
    'GetNewFactIntent': function () {
        var factArr = data;
        var factIndex = Math.floor(Math.random() * factArr.length);
        var randomFact = factArr[factIndex];
        var speechOutput = GET_FACT_MESSAGE + randomFact;
        this.emit(':tellWithCard', speechOutput, SKILL_NAME, randomFact)
    },
    
    'AMAZON.HelpIntent': function () {
        var speechOutput = HELP_MESSAGE;
        var reprompt = HELP_REPROMPT;
        this.emit(':ask', speechOutput, reprompt); },
    
    'AMAZON.CancelIntent': function () { this.emit(':tell', STOP_MESSAGE); },
        
    'AnswerWhoUses': function () { this.emit(':tell', ANSWER_WHO_USES); },    
    
    'AnswerWhatIs': function () { this.emit(':tell', ANSWER_WHAT_IS); },
    
    'AnswerHowBuild': function () { this.emit(':tell', ANSWER_HOW_BUILD); }
};
```

My intent code:
```json
{
  "intents": [
    {
      "name": "AMAZON.CancelIntent",
      "samples": []
    },
    {
      "name": "AMAZON.HelpIntent",
      "samples": []
    },
    {
      "name": "AMAZON.StopIntent",
      "samples": []
    },
    {
      "name": "AnswerHowBuild",
      "samples": [
        "how do you build a bateau",
        "how do you construct a bateau",
        "how do you make a bateau",
        "how are bateau made",
        "how are bateau built",
        "how are bateau constructe",
        "how does building a bateau work",
        "what goes into building a bateau"
      ],
      "slots": []
    },
    {
      "name": "AnswerWhatIs",
      "samples": [
        "what is a bateau",
        "what's a bateau",
        "what the hell is a bateau",
        "tell me what a bateau is",
        "tell us what a bateau is"
      ],
      "slots": []
    },
    {
      "name": "AnswerWhoUses",
      "samples": [
        "who uses a bateau",
        "who actually uses a bateau",
        "who rides in a bateau",
        "who uses it"
      ],
      "slots": []
    },
    {
      "name": "GetNewFactIntent",
      "samples": [
        "Tell me a bateau fact",
        "Tell me something about bateau",
        "Give me  a bateau fact",
        "tell us a bateau fact",
        "tell me a fact",
        "tell us a fact",
        "tell us something",
        "drop some knowledge",
        "tell us something about bateau",
        "tell me a fact about bateau",
        "tell us a fact about bateau",
        "tell me something else",
        "drop some more knowledge",
        "tell me more",
        "tell me another fact",
        "tell me another bateau fact",
        "tell me more bateau facts",
        "tell us more bateau facts",
        "give us another bateau fact",
        "give me another bateau fact",
        "share a bateau fact"
      ],
      "slots": []
    }
  ]
}
```

Good luck!
