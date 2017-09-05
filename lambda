'use strict';

var Alexa = require('alexa-sdk');
var APP_ID = "amzn1.ask.skill.5fe48205-2852-49be-86eb-0561840bb24e";
var SKILL_NAME = "Batteau Bot";
var ANSWER_WHAT_IS = "A bateau is a type of wooden boat which was used for commercial navigation of North America's inland waterways during the 17 and 18 hundreds. In modern times, it used recreationally by an active community of hobbyists";
var ANSWER_HOW_BUILD = "Bateau are made by hammering a bunch of wood together. There are several steps. First, a dozen u-shaped ribs are constructed and mounted to a central king plank, which functions much like a spine. Next, the hull is covered with smaller planks from end to end. Lastly, the bow and stern are mounted and the boat is caulked to prevent leaks. If you have ever built a bateau yourself, the brevity of this answer will likely offend you.";
var ANSWER_WHO_USES = "Prior to colonization, bateau were used by French fur traders. During the colonial era, they were used by African American slaves. In modern times, they are used recreationally by renaissance rednecks throughout the Virginia piedmont.";
var GET_FACT_MESSAGE = "Here's your fact: ";
var HELP_MESSAGE = "You can ask me a question, say, tell me a batteau fact, or, you can say exit.";
var HELP_REPROMPT = "What can I help you with?";
var STOP_MESSAGE = "Goodbye!";

// NOTE: I took out my massive list of facts here to make this easier to read. They were listed in this data variable.
var data = [
        "A fact.",
        "Another fact.",
        "One last fact."
];

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
