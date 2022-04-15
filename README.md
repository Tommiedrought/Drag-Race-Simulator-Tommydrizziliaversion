# Drag-Race-Simulator-Tommydrizziliaversion
"use strict";
//mini-challenge stuff:
class MiniChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["wigs with "] = 0] = "wigs with ";
            desc1[desc1["a quiz about "] = 1] = "a quiz about ";
            desc1[desc1["nails with "] = 2] = "nails with ";
            desc1[desc1["a competition about "] = 3] = "a competition about ";
            desc1[desc1["a song about "] = 4] = "a song about ";
            desc1[desc1["make-up tutorials with "] = 5] = "make-up tutorials with ";
            desc1[desc1["make a quick look about "] = 6] = "make a quick look about ";
            desc1[desc1["a photoshoot about "] = 7] = "a photoshoot about ";
        })(desc1 || (desc1 = {}));
        let desc2;
        (function (desc2) {
            desc2[desc2["the pitcrew."] = 0] = "the pitcrew.";
            desc2[desc2["a partner."] = 1] = "a partner.";
            desc2[desc2["noodles."] = 2] = "noodles.";
            desc2[desc2["hip pads."] = 3] = "hip pads.";
            desc2[desc2["balls."] = 4] = "balls.";
            desc2[desc2["past Drag Race contestants"] = 5] = "past Drag Race contestants";
            desc2[desc2["a celebrity."] = 6] = "a celebrity.";
        })(desc2 || (desc2 = {}));
        //reading and puppet challenges:
        if (totalCastSize >= 10 && currentCast.length == 7 && !all_stars || currentCast.length == totalCastSize && (all_stars || lipsync_assassin)) {
            description.innerHTML = "The library is open! In today's mini-challenge, the queens will read eachother!";
        }
        else if (totalCastSize != 5 && currentCast.length == 5) {
            description.innerHTML = "Bring in the puppets! The queens will parody eachother using puppets!";
        }
        else {
            description.innerHTML = "In today's mini-challenge, the queens will do " + desc1[randomNumber(0, 7)] + desc2[randomNumber(0, 6)];
        }
    }
    rankPerformances() {
        let screen = new Scene();
        if (randomNumber(0, 100) <= 90) {
            let winner = currentCast[randomNumber(0, currentCast.length - 1)];
            screen.createImage(winner.image, "royalblue");
            screen.createBold(`${winner.getName()} won the mini-challenge!`);
        }else {
            let winner = randomNumber(0, currentCast.length - 1);
            let second;
            do{
                second = randomNumber(0, currentCast.length - 1);
            }while (second == winner);
            screen.createImage(currentCast[winner].image, "royalblue");
            screen.createImage(currentCast[second].image, "royalblue");
            screen.createBold(`${currentCast[winner].getName()} and ${currentCast[second].getName()} won the mini-challenge!`);
        }
        
    }
}
//challenge modifiers:
let actingChallengeCounter = 0;
let comedyChallengeCounter = 0;
let marketingChallengeCounter = 0;
let danceChallengeCounter = 0;
let designChallengeCounter = 0;
let improvChallengeCounter = 0;
var isDesignChallenge = false;
let rusicalCounter = false;
let ballCounter = false;
let talentShowCounter = false;
let girlGroupCounter = false;
let makeoverCounter = false;
let snatchCounter = false;
let rumixCounter = false;
let lastChallenge = '';
function miniChallenge() {
    let miniChallengeScreen = new Scene();
    miniChallengeScreen.clean();
    miniChallengeScreen.createHeader("Mini-challenge!");
    miniChallengeScreen.createParagraph("", "Description");
    document.body.style.backgroundImage = "url('image/werkroom.webp')";
    let challenge = new MiniChallenge();
    challenge.generateDescription();
    challenge.rankPerformances();
    //deal with maxi chalenges:
    let challenges = ["actingChallenge()", "comedyChallenge()", "danceChallenge()", "designChallenge()", "improvChallenge()", "marketingChallenge()"];
    //remove from possible challenges list:
    if (actingChallengeCounter == 3)
        challenges.splice(challenges.indexOf("actingChallenge()"), 1);
    if (comedyChallengeCounter == 3)
        challenges.splice(challenges.indexOf("comedyChallenge()"), 1);
    if (marketingChallengeCounter == 3)
        challenges.splice(challenges.indexOf("marketingChallenge()"), 1);
    if (danceChallengeCounter == 2)
        challenges.splice(challenges.indexOf("danceChallenge()"), 1);
    if (designChallengeCounter == 3)
        challenges.splice(challenges.indexOf("designChallenge()"), 1);
    if (improvChallengeCounter == 3)
        challenges.splice(challenges.indexOf("improvChallenge()"), 1);
    createChallenge(challenges, miniChallengeScreen);
}
//GENERAL CHALLENGES:
let team1 = [];
let team2 = [];
let team3 = [];
let isTeamChallenge = false;
class ActingChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["theather piece about "] = 0] = "theather piece about ";
            desc1[desc1["parody film about "] = 1] = "parody film about ";
            desc1[desc1["commercial about "] = 2] = "commercial about ";
            desc1[desc1["60's inspired film about "] = 3] = "60's inspired film about ";
            desc1[desc1["80's inspired film about "] = 4] = "80's inspired film about ";
        })(desc1 || (desc1 = {}));
        let desc2;
        (function (desc2) {
            desc2[desc2["crime."] = 0] = "crime.";
            desc2[desc2["phone apps."] = 1] = "phone apps.";
            desc2[desc2["social media."] = 2] = "social media.";
            desc2[desc2["cancel culture."] = 3] = "cancel culture.";
            desc2[desc2["gayness."] = 4] = "gayness.";
            desc2[desc2["celebrities."] = 5] = "celebrities.";
            desc2[desc2["the future."] = 6] = "the future.";
            desc2[desc2["the rainbow."] = 7] = "the rainbow.";
        })(desc2 || (desc2 = {}));
        description.innerHTML = "The queens will act in a " + desc1[randomNumber(0, 4)] + desc2[randomNumber(0, 6)];
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++) {
            currentCast[i].getActing();
        }
        sortPerformances(currentCast);
    }
}
function actingChallenge() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new ActingChallenge();
    challenge.generateDescription();
    if (randomNumber(0, 100) >= 50 && currentCast.length > 6 && currentCast.length <= 15 && !isTeamChallenge && (top3 || top4)){
        isTeamChallenge = true;
        teamMaking();
        challenge.rankPerformances();
    } else {
        challenge.rankPerformances();
    }
    queensPerformances();
    actingChallengeCounter++;
    isDesignChallenge = false;
    episodeChallenges.push("Acting");
}
class ComedyChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        let whatChallengeIs = randomNumber(0, 1);
        (function (desc1) {
            desc1[desc1["a comedy routine about "] = 0] = "a comedy routine about ";
            desc1[desc1["a roast about "] = 1] = "a roast about ";
        })(desc1 || (desc1 = {}));
        let desc2;
        (function (desc2) {
            desc2[desc2["love."] = 0] = "love.";
            desc2[desc2["sex."] = 1] = "sex.";
            desc2[desc2["crime."] = 2] = "crime.";
            desc2[desc2["school."] = 3] = "school.";
            desc2[desc2["a popular TV series."] = 4] = "a popular TV series.";
            desc2[desc2["Drag Race."] = 5] = "Drag Race.";
            desc2[desc2["Past Drag Race Contestants."] = 6] = "Past Drag Race Contestants.";
            desc2[desc2["comedy."] = 7] = "comedy.";
        })(desc2 || (desc2 = {}));
        description.innerHTML = "The queens will participate in " + desc1[whatChallengeIs] + desc2[randomNumber(0, 7)];
        if (whatChallengeIs == 0) {
            episodeChallenges.push("Stand Up");
        } else {
            episodeChallenges.push("Roast");
        }
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getComedy();
        sortPerformances(currentCast);
    }
}
function comedyChallenge() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new ComedyChallenge();
    challenge.generateDescription();
    challenge.rankPerformances();
    queensPerformances();
    comedyChallengeCounter++;
    isDesignChallenge = false;
}
class MarketingChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        let whatChallengeIs = randomNumber(0, 1);
        (function (desc1) {
            desc1[desc1["a parody commercial about "] = 0] = "a parody commercial about ";
            desc1[desc1["a parody trailer about "] = 1] = "a parody trailer about ";
        })(desc1 || (desc1 = {}));
        let desc2;
        (function (desc2) {
            desc2[desc2["love."] = 0] = "love.";
            desc2[desc2["sex."] = 1] = "sex.";
            desc2[desc2["crime."] = 2] = "crime.";
            desc2[desc2["school."] = 3] = "school.";
            desc2[desc2["a popular TV series."] = 4] = "a popular TV series.";
            desc2[desc2["Drag Race."] = 5] = "Drag Race.";
            desc2[desc2["Past Drag Race Contestants."] = 6] = "Past Drag Race Contestants.";
            desc2[desc2["comedy."] = 7] = "comedy.";
        })(desc2 || (desc2 = {}));
        description.innerHTML = "The queens will participate in " + desc1[whatChallengeIs] + desc2[randomNumber(0, 7)];
        if (whatChallengeIs == 0) {
            episodeChallenges.push("Commercial");
        } else {
            episodeChallenges.push("Marketing");
        }
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getMarketing();
        sortPerformances(currentCast);
    }
}
function marketingChallenge() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new MarketingChallenge();
    challenge.generateDescription();
    if (randomNumber(0, 100) >= 60 && currentCast.length > 6 && currentCast.length <= 15 && !isTeamChallenge && (top3 || top4)){
        isTeamChallenge = true;
        teamMaking();
        challenge.rankPerformances();
    } else {
        challenge.rankPerformances();
    }
    queensPerformances();
    marketingChallengeCounter++;
    isDesignChallenge = false;
}
class DanceChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["the history of disco."] = 0] = "the history of disco.";
            desc1[desc1["RuPaul's biography."] = 1] = "RuPaul's biography.";
            desc1[desc1["rival dance clubs."] = 2] = "rival dance clubs.";
            desc1[desc1["Drag Race."] = 3] = "Drag Race.";
        })(desc1 || (desc1 = {}));
        description.innerHTML = "The queens will participate in a dance number about " + desc1[randomNumber(0, 3)];
        if (randomNumber(0, 100) >= 50) {
            episodeChallenges.push("Dance");
        } else {
            episodeChallenges.push("Choreo");
        }
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getDance();
        sortPerformances(currentCast);
    }
}
function danceChallenge() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new DanceChallenge();
    challenge.generateDescription();
    if (randomNumber(0, 100) >= 70 && currentCast.length > 6 && currentCast.length <= 15 && !isTeamChallenge && (top3 || top4)){
        isTeamChallenge = true;
        teamMaking();
        challenge.rankPerformances();
    } else {
        challenge.rankPerformances();
    }
    queensPerformances();
    danceChallengeCounter++;
    isDesignChallenge = false;
}
class DesignChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["trash."] = 0] = "trash.";
            desc1[desc1["random items."] = 1] = "random items.";
            desc1[desc1["dollar store items."] = 2] = "dollar store items.";
            desc1[desc1["a specific color scheme."] = 3] = "a specific color scheme.";
            desc1[desc1["items inspired by past Drag Race contestants."] = 4] = "items inspired by past Drag Race contestants.";
            desc1[desc1["bags."] = 5] = "bags.";
            desc1[desc1["wigs."] = 6] = "wigs.";
            desc1[desc1["winter items."] = 7] = "winter items.";
            desc1[desc1["summer items."] = 8] = "summer items.";
        })(desc1 || (desc1 = {}));
        if (currentCast.length == 6 && makeoverCounter == false && team == false && currentCast != firstCast && currentCast != secondCast && !uk3Premiere && !s9Premiere && !conjoinedQueens) {
            description.innerHTML = "It's the makeover challenge! The queens will make everyday people their drag sisters!";
        }
        else if (currentCast.length == totalCastSize && (uk3Premiere || s9Premiere) && !s9PremiereCheck && !uk3PremiereCheck) {
            description.innerHTML = "The queens will bring it to the runway and serve not one but two looks!";
        }
        else
            description.innerHTML = "The queens will do outfits with " + desc1[randomNumber(0, 8)];
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getDesign();
        sortPerformances(currentCast);
    }
}
function designChallenge() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new DesignChallenge();
    challenge.generateDescription();
    challenge.rankPerformances();
    isDesignChallenge = true;
    queensPerformances();
    designChallengeCounter++;
    if (currentCast.length == 6 && makeoverCounter == false && team == false && currentCast != firstCast && currentCast != secondCast && !uk3Premiere && !s9Premiere && !conjoinedQueens) {
        episodeChallenges.push("Makeover");
        makeoverCounter = true;
    }
    else if (currentCast.length == totalCastSize && (uk3Premiere || s9Premiere) && !s9PremiereCheck && !uk3PremiereCheck){
        episodeChallenges.push("Runway");
    }
    else if (currentCast.length == totalCastSize - 1 && s9Premiere && !s9PremiereCheck)
        episodeChallenges.push("Runway");
    else
        episodeChallenges.push("Design");
}
class ImprovChallenge {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        let whatChallengeIs = randomNumber(0, 12);
        (function (desc1) {
            desc1[desc1["political debate."] = 0] = "political debate.";
            desc1[desc1["celebrity interview."] = 1] = "celebrity interview.";
            desc1[desc1["modern morning TV show."] = 2] = "modern morning TV show.";
            desc1[desc1["late-night TV show."] = 3] = "late-night TV show.";
            desc1[desc1["new Bossy Rossy episode."] = 4] = "new Bossy Rossy episode.";
            desc1[desc1["suggestive kids TV show."] = 5] = "suggestive kids TV show.";
            desc1[desc1["Bitchelor show."] = 6] = "Bitchelor show.";
            desc1[desc1["Jersey Justice show."] = 7] = "Jersey Justice show.";
            desc1[desc1["diva worship talk show."] = 8] = "diva worship talk show.";
            desc1[desc1["talent show for people with little talent."] = 9] = "talent show for people with little talent.";
            desc1[desc1["drag queen spoof of the celebrity gossip and drama television show."] = 10] = "drag queen spoof of the celebrity gossip and drama television show.";
            desc1[desc1["pageant, the Miss Loose Jaw Pageant."] = 11] = "pageant, the Miss Loose Jaw Pageant.";
            desc1[desc1["intimate chat show called Pink Table Talk."] = 12] = "intimate chat show called Pink Table Talk.";
        })(desc1 || (desc1 = {}));
        description.innerHTML = "The queens will improvise in a " + desc1[whatChallengeIs];
        if (whatChallengeIs == 0) {
            episodeChallenges.push("Political Debate");
        } else if (whatChallengeIs == 4) {
            episodeChallenges.push("The Bossy Rossy Show");
        } else if (whatChallengeIs == 6) {
            episodeChallenges.push("The Bitchelor");
        } else {
            episodeChallenges.push("Improv");
        }
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getImprov();
        sortPerformances(currentCast);
    }
}
function improvChallenge() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new ImprovChallenge();
    challenge.generateDescription();
    if (randomNumber(0, 100) >= 50 && currentCast.length > 6 && currentCast.length <= 15 && !isTeamChallenge && (top3 || top4)){
        isTeamChallenge = true;
        teamMaking();
        challenge.rankPerformances();
    } else {
        challenge.rankPerformances();
    }
    queensPerformances();
    improvChallengeCounter++;
    isDesignChallenge = false;
}
//SPECIAL CHALLENGES:
class SnatchGame {
    generateDescription() {
        let description = document.querySelector("p#Description");
        description.innerHTML = "Today's challenge is... SNATCH GAME!! The queens will do funny celebrity impersonations!";
        if (randomNumber(0, 100) >= 95) {
            episodeChallenges.push("Snatch Game of Love");
        } else {
            episodeChallenges.push("Snatch Game");
        }
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getSnatch();
        sortPerformances(currentCast);
    }
}
function snatchGame() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new SnatchGame();
    challenge.generateDescription();
    challenge.rankPerformances();
    queensPerformances();
    isDesignChallenge = false;
    snatchCounter = true;
}
class Rusical {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc;
        (function (desc) {
            desc[desc["Social Media: The Unverified Rusical."] = 0] = "Social Media: The Unverified Rusical.";
            desc[desc["Halftime Headliners."] = 1] = "Halftime Headliners.";
            desc[desc["CindeRulla: The Rusical."] = 2] = "CindeRulla: The Rusical.";
            desc[desc["Under the Big Top."] = 3] = "Under the Big Top.";
            desc[desc["West End Wendys - The Rusical."] = 4] = "West End Wendys - The Rusical.";
            desc[desc["RuPaul's music carreer."] = 5] = "RuPaul's music carreer.";
            desc[desc["Shade: The Rusical."] = 6] = "Shade: The Rusical.";
            desc[desc["Glamazonian Airways."] = 7] = "Glamazonian Airways.";
            desc[desc["Bitch Perfect."] = 8] = "Bitch Perfect.";
            desc[desc["HERstory of the World'."] = 9] = "HERstory of the World'.";
            desc[desc["Kardashians: The Rusical."] = 10] = "Kardashians: The Rusical.";
            desc[desc["VH1 Divas Live."] = 11] = "VH1 Divas Live.";
            desc[desc["PharmaRusical."] = 12] = "PharmaRusical.";
            desc[desc["Cher: The Unauthorized Rusical."] = 13] = "Cher: The Unauthorized Rusical.";
            desc[desc["Trump: The Rusical."] = 14] = "Trump: The Rusical.";
            desc[desc["Madonna: The Unauthorized Rusical."] = 15] = "Madonna: The Unauthorized Rusical.";
            desc[desc["Máxima - The Rusical."] = 16] = "Máxima - The Rusical.";
            desc[desc["Rats: The Rusical."] = 17] = "Rats: The Rusical.";
        })(desc || (desc = {}));
        description.innerHTML = "Today's challenge is... THE RUSICAL!! The queens were tasked to take part in " + desc[randomNumber(0, 17)];
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getRusical();
        sortPerformances(currentCast);
    }
}
function rusical() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new Rusical();
    challenge.generateDescription();
    challenge.rankPerformances();
    queensPerformances();
    isDesignChallenge = false;
    rusicalCounter = true;
    episodeChallenges.push("Rusical");
}
class Ball {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["Executive realness, "] = 0] = "Executive realness, ";
            desc1[desc1["Party night, "] = 1] = "Party night, ";
            desc1[desc1["Summer, "] = 2] = "Summer, ";
            desc1[desc1["Elegant, "] = 3] = "Elegant, ";
            desc1[desc1["Sweet 16, "] = 4] = "Sweet 16, ";
            desc1[desc1["Black and white, "] = 5] = "Black and white, ";
            desc1[desc1["Winter, "] = 6] = "Winter, ";
        })(desc1 || (desc1 = {}));
        let desc2;
        (function (desc2) {
            desc2[desc2["Antique, "] = 0] = "Antique, ";
            desc2[desc2["Rainbow, "] = 1] = "Rainbow, ";
            desc2[desc2["Rich, "] = 2] = "Rich, ";
            desc2[desc2["Space, "] = 3] = "Space, ";
            desc2[desc2["Wild, "] = 4] = "Wild, ";
            desc2[desc2["Water, "] = 5] = "Water, ";
            desc2[desc2["Swimsuit, "] = 6] = "Swimsuit, ";
        })(desc2 || (desc2 = {}));
        let desc3;
        (function (desc3) {
            desc3[desc3["Ice queen."] = 0] = "Ice queen.";
            desc3[desc3["Futuristic."] = 1] = "Futuristic.";
            desc3[desc3["Fire."] = 2] = "Fire.";
            desc3[desc3["Princess."] = 3] = "Princess.";
            desc3[desc3["Jewels."] = 4] = "Jewels.";
            desc3[desc3["Flowers."] = 5] = "Flowers.";
            desc3[desc3["Evening Gown Extravaganza."] = 6] = "Evening Gown Extravaganza.";
        })(desc3 || (desc3 = {}));
        description.innerHTML = "Today's challenge is... THE BALL! The queens will bring three looks to the runway! The themes are: " + desc1[randomNumber(0, 6)] + desc2[randomNumber(0, 6)] + desc3[randomNumber(0, 6)];
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getBall();
        sortPerformances(currentCast);
    }
}
function ball() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new Ball();
    challenge.generateDescription();
    challenge.rankPerformances();
    isDesignChallenge = true;
    queensPerformances();
    ballCounter = true;
    episodeChallenges.push("Ball");
}
class Rumix {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["Read U Wrote U."] = 0] = "Read U Wrote U.";
            desc1[desc1["Category Is."] = 1] = "Category Is.";
            desc1[desc1["Kitty Girl."] = 2] = "Kitty Girl.";
            desc1[desc1["American."] = 3] = "American.";
            desc1[desc1["Super Queen."] = 4] = "Super Queen.";
            desc1[desc1["Queens Everywhere."] = 5] = "Queens Everywhere.";
            desc1[desc1["Rock It (To The Moon)."] = 6] = "Rock It (To The Moon).";
            desc1[desc1[" I Made It / Mirror Song / Losing is the New Winning."] = 7] = " I Made It / Mirror Song / Losing is the New Winning.";
            desc1[desc1["Clap Back."] = 8] = "Clap Back.";
            desc1[desc1["U Wear It Well."] = 9] = "U Wear It Well.";
            desc1[desc1["A Little Bit of Love."] = 10] = "A Little Bit of Love.";
            desc1[desc1["Lucky."] = 11] = "Lucky.";
            desc1[desc1["I'm a Winner, Baby."] = 12] = "I'm a Winner, Baby.";
            desc1[desc1["This Is Our Country."] = 13] = "This Is Our Country.";
            desc1[desc1["Hey Sis, It's Christmas."] = 14] = "Hey Sis, It's Christmas.";
            desc1[desc1["Queen of the North."] = 15] = "Queen of the North.";
        })(desc1 || (desc1 = {}));
        description.innerHTML = "Today's challenge is... the rumix! The queens will make a verse and a choreography for " + desc1[randomNumber(0, 15)];
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getRumix();
        sortPerformances(currentCast);
    }
}
function rumix() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new Rumix();
    challenge.generateDescription();
    challenge.rankPerformances();
    queensPerformances();
    isDesignChallenge = false;
    episodeChallenges.push("Rumix");
    rumixCounter = true;
}
class GirlGroup {
    generateDescription() {
        let description = document.querySelector("p#Description");
        let desc1;
        (function (desc1) {
            desc1[desc1["Break Up (Bye Bye)"] = 0] = "Break Up (Bye Bye)";
            desc1[desc1["Drag Up Your Life"] = 1] = "Drag Up Your Life";
            desc1[desc1["Sitting on a Secret"] = 2] = "Sitting on a Secret";
            desc1[desc1["Don't Funk it Up"] = 3] = "Don't Funk it Up";
            desc1[desc1["Everybody Say Love"] = 4] = "Everybody Say Love";
            desc1[desc1["You Don't Know Me"] = 5] = "You Don't Know Me";
            desc1[desc1["I'm That Bitch"] = 6] = "I'm That Bitch";
            desc1[desc1["I'm in Love!"] = 7] = "I'm in Love!";
            desc1[desc1["Not Sorry Aboot It"] = 8] = "Not Sorry Aboot It";
            desc1[desc1["Condragulations "] = 9] = "Condragulations";
            desc1[desc1["Phenomenon"] = 10] = "Phenomenon";
            desc1[desc1["UK Hun?"] = 11] = "UK Hun?";
            desc1[desc1["Queens Down Under"] = 12] = "Queens Down Under";
            desc1[desc1["Divas"] = 13] = "Divas";
            desc1[desc1["Show Up Queen"] = 14] = "Show Up Queen";
            desc1[desc1["B.D.E (Big Drag Energy)"] = 15] = "B.D.E (Big Drag Energy)";
            desc1[desc1["Bye Flop"] = 16] = "Bye Flop";
            desc1[desc1["Superstar"] = 17] = "Superstar";
            desc1[desc1["So Much Better Than You"] = 18] = "So Much Better Than You";
            desc1[desc1["Can I Get An Amen?"] = 19] = "Can I Get An Amen?";
            desc1[desc1["Oh No She Betta Don't!"] = 20] = "Oh No She Betta Don't!";
        })(desc1 || (desc1 = {}));
        description.innerHTML = "The remaining queens will record vocals and perform in a Girl Group number for the original song " + desc1[randomNumber(0, 20)] + ".";
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getRumix();
        sortPerformances(currentCast);
    }
}
function girlgroup() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new GirlGroup();
    challenge.generateDescription();
    if (randomNumber(0, 100) >= 50 && currentCast.length > 6 && currentCast.length <= 15 && !isTeamChallenge && (top3 || top4) && episodeCount > 3) {
        isTeamChallenge = true;
        teamMaking();
        challenge.rankPerformances();
    } else {
        challenge.rankPerformances();
    }
    queensPerformances();
    isDesignChallenge = false;
    episodeChallenges.push("Girl Group");
    if (((s12Premiere || porkchopPremiere) && episodeCount <= 2)) {
        girlGroupCounter = false;
    } else {
        girlGroupCounter = true;
    }
}
class TalentShow {
    generateDescription() {
        let description = document.querySelector("p#Description");
        description.innerHTML = "In this first challenge, the queens will prove themselves in a talent show, where they bring all they've got!";
    }
    rankPerformances() {
        for (let i = 0; i < currentCast.length; i++)
            currentCast[i].getTalentShow();
        sortPerformances(currentCast);
    }
}
function talentshow() {
    let challengeScreen = new Scene();
    challengeScreen.clean();
    challengeScreen.createHeader("Maxi-challenge!");
    challengeScreen.createParagraph("", "Description");
    let challenge = new TalentShow();
    challenge.generateDescription();
    queenTalents();
    challenge.rankPerformances();
    isDesignChallenge = true;
    queensPerformances();
    episodeChallenges.push("Talent Show");
    if (s14Premiere && episodeCount == 2 || (lipsync_assassin || all_stars)) {
        talentShowCounter = true;
    }
}
//performance:
function queensPerformances() {
    let performanceScreen = new Scene();
    performanceScreen.createHorizontalLine();
    performanceScreen.createBigText("Queens' performances...");
    let slay = currentCast.filter(function (queen) { return queen.performanceScore < 6; });
    let great = currentCast.filter(function (queen) { return queen.performanceScore >= 6 && queen.performanceScore < 16; });
    let good = currentCast.filter(function (queen) { return queen.performanceScore >= 16 && queen.performanceScore < 26; });
    let bad = currentCast.filter(function (queen) { return queen.performanceScore >= 26 && queen.performanceScore < 31; });
    let flop = currentCast.filter(function (queen) { return queen.performanceScore >= 31 && queen.performanceScore < 50; });
    createPerformanceDesc(slay, great, good, bad, flop);
    if (isDesignChallenge == true || episodeChallenges[episodeChallenges.length - 1] == "Design")
        performanceScreen.createButton("Proceed", "judging()");
    else
        performanceScreen.createButton("Proceed", "runway()", "button2");
}
function teamMaking() {
    let screen = new Scene();
    team1 = [];
    team2 = [];
    team3 = [];
    let twoOrThree = false;
    let castTeams = currentCast.slice(); 
    shuffle(castTeams);
    if (castTeams.length <= 8) {
        team1 = castTeams.splice(0, Math.floor(castTeams.length / 2));
        team2 = [...castTeams];
    }
    else if (castTeams.length >= 9) {
        team1 = castTeams.splice(0, Math.floor(castTeams.length / 3));
        team2 = castTeams.splice(0, Math.floor(castTeams.length / 2));
        team3 = [...castTeams];
        twoOrThree = true;
    }
    screen.createBigText("Team 1");
    for (let i = 0; i < team1.length; i++) {
        screen.createImage(team1[i].image, "blue");
    }
    screen.createBigText("Team 2");
    for (let i = 0; i < team2.length; i++) {
        screen.createImage(team2[i].image, "pink");
    }
    if (twoOrThree) {
        screen.createBigText("Team 3");
        for (let i = 0; i < team3.length; i++) {
            screen.createImage(team3[i].image, "green");
        }
    }
}
//runway:
function runway() {
    let runwayScreen = new Scene();
    runwayScreen.createHorizontalLine();
    let button2 = document.querySelector("button#button2");
    button2.remove();
    runwayScreen.createBigText("Runway!");
    let desc;
    (function (desc) {
        desc[desc["feathers."] = 0] = "feathers.";
        desc[desc["fascinator."] = 1] = "fascinator.";
        desc[desc["pink."] = 2] = "pink.";
        desc[desc["purple."] = 3] = "purple.";
        desc[desc["caftan."] = 4] = "caftan.";
        desc[desc["trains."] = 5] = "trains.";
        desc[desc["yellow."] = 6] = "yellow.";
        desc[desc["white."] = 7] = "white.";
        desc[desc["black."] = 8] = "black.";
        desc[desc["ugly dress."] = 9] = "ugly dress.";
        desc[desc["naughty."] = 10] = "naughty.";
        desc[desc["crazy sexy cool."] = 11] = "crazy sexy cool.";
        desc[desc["country."] = 12] = "country.";
        desc[desc["phoenix."] = 13] = "phoenix.";
        desc[desc["silver."] = 14] = "silver.";
        desc[desc["2 in 1."] = 15] = "2 in 1.";
        desc[desc["surprise!"] = 16] = "surprise!";
        desc[desc["gold."] = 17] = "gold.";
        desc[desc["blue."] = 18] = "blue.";
        desc[desc["fish"] = 19] = "fish";
        desc[desc["butch."] = 20] = "butch.";
        desc[desc["amazon"] = 21] = "amazon";
    })(desc || (desc = {}));
    runwayScreen.createParagraph("The queens will bring it to the runway!");
    if (currentCast.length > 4)
        runwayScreen.createParagraph("The theme is: " + desc[randomNumber(0, 21)]);
    else if (currentCast.length == 3 && top3 || currentCast.length == 5 && top4 || currentCast.length == 4 && (all_stars || lipsync_assassin) || currentCast.length == 2 && team)
        runwayScreen.createParagraph("The theme is... best drag!");
    for (let i = 0; i < currentCast.length; i++)
        currentCast[i].getRunway();
    let slay = currentCast.filter(function (queen) { return queen.runwayScore < 6; });
    let great = currentCast.filter(function (queen) { return queen.runwayScore >= 6 && queen.runwayScore < 16; });
    let good = currentCast.filter(function (queen) { return queen.runwayScore >= 16 && queen.runwayScore < 26; });
    let bad = currentCast.filter(function (queen) { return queen.runwayScore >= 26; });
    createRunwayDesc(slay, great, good, bad);
    if (currentCast.length > 4)
        runwayScreen.createButton("Proceed", "judging()");
    else if (currentCast.length == 4 && porkchopPremiere && premiereCounter < 3)
        runwayScreen.createButton("Proceed", "judging()");
    else if (currentCast.length == 4 && (top3 || team))
        runwayScreen.createButton("Proceed", "judging()");
    else if (currentCast.length == 3 && team)
        runwayScreen.createButton("Proceed", "judging()");
    else if (currentCast.length == 3 && (top3))
        runwayScreen.createButton("Proceed", "finaleJudging()");
    else if (currentCast.length == 2 && (top3))
        runwayScreen.createButton("Proceed", "finaleJudging()");
    else if (currentCast.length == 4 && (allstars3Finale))
        runwayScreen.createButton("Proceed", "finaleJuryAS()");
    else if (currentCast.length == 4 && (all_stars || lipsync_assassin))
        runwayScreen.createButton("Proceed", "finaleASJudging()");
    else if (currentCast.length == 2 && team)
        runwayScreen.createButton("Proceed", "finaleTeamJudging()");
}
//helper functions
////create next challenge
function createChallenge(challenges, miniChallengeScreen) {
    for (let i = 0; i < currentCast.length; i++){
        currentCast[i].episodesOn++;
    }
    //first design challenge for normal seasons
    if (currentCast.length == totalCastSize && top3 && episodeCount == 1 && s6Premiere == false || currentCast.length == totalCastSize && top4 && episodeCount == 1 && s6Premiere == false || currentCast.length == totalCastSize && team || sweatshop || currentCast == firstCast && s6Premiere || currentCast == secondCast && s6Premiere)
        miniChallengeScreen.createButton("Proceed", "designChallenge()");
    //girl group challenge for s12 or porkchop premiere
    else if (premiereCounter <= 2 && (s12Premiere || porkchopPremiere))
        miniChallengeScreen.createButton("Proceed", "girlgroup()");
    //uk3 premiere
    else if (currentCast.length == totalCastSize && uk3Premiere && !uk3PremiereCheck)
        miniChallengeScreen.createButton("Proceed", "designChallenge()");
    else if (currentCast.length == totalCastSize - 1 && s9Premiere && !s9PremiereCheck)
        miniChallengeScreen.createButton("Proceed", "designChallenge()");
    //talent show for all stars and s14 premiere
    else if (currentCast.length == totalCastSize && !talentShowCounter && (all_stars || lipsync_assassin) || currentCast == firstCast && s14Premiere || currentCast == secondCast && s14Premiere)
        miniChallengeScreen.createButton("Proceed", "talentshow()");
    //snatch game for +10 cast
    else if (totalCastSize >= 10 && currentCast.length == 9 && !team && snatchCounter == false || totalCastSize >= 6 && currentCast.length == 5 && team)
        miniChallengeScreen.createButton("Proceed", "snatchGame()");
    //snatch game for -10 cast
    else if (totalCastSize < 10 && currentCast.length == (totalCastSize - 1) && !team && snatchCounter == false)
        miniChallengeScreen.createButton("Proceed", "snatchGame()");
    //the ball for the third competitive episode for lsftc seasons
    else if (currentCast.length == totalCastSize - 3 && top4 && !ballCounter)
        miniChallengeScreen.createButton("Proceed", "ball()");
    //same but if above condition doesn't apply (example: snatch game needs to happen before the ball)
    else if (currentCast.length == totalCastSize - 4 && (top4 || (all_stars || lipsync_assassin) && randomNumber(0, 100) < 30) && !ballCounter || currentCast.length == 3 && team)
        miniChallengeScreen.createButton("Proceed", "ball()");
    //Girl Group
    else if (currentCast.length == 8 && !girlGroupCounter && (top3 || top4 || lipsync_assassin))
        miniChallengeScreen.createButton("Proceed", "girlgroup()");
    //rusical
    else if (currentCast.length > 6 && randomNumber(0, 20) >= 19 && !rusicalCounter || currentCast.length > 5 && randomNumber(0, 20) >= 19 && team && !rusicalCounter)
        miniChallengeScreen.createButton("Proceed", "rusical()");
    //makeover
    else if (currentCast.length == 6 && (top3 || top4) && makeoverCounter == false || currentCast.length == 6 && randomNumber(0, 15) == 15 && (all_stars || lipsync_assassin) && makeoverCounter == false)
        miniChallengeScreen.createButton("Proceed", "designChallenge()");
    //rumix
    else if (currentCast.length == 5 && !rumixCounter && top4 && (!smackdown || returningQueen == true || chocolateBarTwistCheck))
        miniChallengeScreen.createButton("Proceed", "rumix()");
    //ball for top3 seasons
    else if (currentCast.length == 4 && top3 && !ballCounter)
        miniChallengeScreen.createButton("Proceed", "ball()");
    //if no conditions apply, create random challenge
    else {
        let currentChallenge = challenges[randomNumber(0, challenges.length - 1)];
        if (currentChallenge == lastChallenge && currentCast.length != totalCastSize) {
            while (currentChallenge == lastChallenge) {
                currentChallenge = challenges[randomNumber(0, challenges.length - 1)];
            }
            lastChallenge = currentChallenge;
            miniChallengeScreen.createButton("Proceed", currentChallenge);
        }
        else {
            lastChallenge = currentChallenge;
            miniChallengeScreen.createButton("Proceed", currentChallenge);
        }
    }
}
////create performance descriptions CREATE NEW DESCRIPTIONS FOR THIS
function createPerformanceDesc(slay, great, good, bad, flop) {
    let screen = new Scene();
    if (slay.length !== 0) {
        for (let i = 0; i < slay.length; i++)
            screen.createImage(slay[i].image, "darkblue");
        screen.createBold("", "slay");
        let slayText = document.getElementById("slay");
        for (let i = 0; i < slay.length; i++)
            slayText.innerHTML += `${slay[i].getName()}, `;
        slayText.innerHTML += "slayed the challenge!";
    }
    if (great.length !== 0) {
        for (let i = 0; i < great.length; i++)
            screen.createImage(great[i].image, "royalblue");
        screen.createBold("", "great");
        let greatText = document.getElementById("great");
        for (let i = 0; i < great.length; i++)
            greatText.innerHTML += `${great[i].getName()}, `;
        greatText.innerHTML += "had a great performance!";
    }
    if (good.length !== 0) {
        for (let i = 0; i < good.length; i++)
            screen.createImage(good[i].image);
        screen.createBold("", "good");
        let goodText = document.getElementById("good");
        for (let i = 0; i < good.length; i++)
            goodText.innerHTML += `${good[i].getName()}, `;
        goodText.innerHTML += "had a good performance.";
    }
    if (bad.length !== 0) {
        for (let i = 0; i < bad.length; i++)
            screen.createImage(bad[i].image, "pink");
        screen.createBold("", "bad");
        let badText = document.getElementById("bad");
        for (let i = 0; i < bad.length; i++)
            badText.innerHTML += `${bad[i].getName()}, `;
        badText.innerHTML += "had a bad performance...";
    }
    if (flop.length !== 0) {
        for (let i = 0; i < flop.length; i++)
            screen.createImage(flop[i].image, "tomato");
        screen.createBold("", "flop");
        let flopText = document.getElementById("flop");
        for (let i = 0; i < flop.length; i++)
            flopText.innerHTML += `${flop[i].getName()}, `;
        flopText.innerHTML += "flopped the challenge...";
    }
    CheckForSpecialEvents(slay, great, good, bad, flop);
}
let floppers = false;
let floppersCheck = false;
let slayers = false;
let slayersCheck = false;
let bottom6WayLipsync = false;
let bottom6WayLipsyncCheck = false;
let s14LaLaPaRUZa = false;
let s14LaLaPaRUZaCheck = false;

function CheckForSpecialEvents(slay, great, good, bad, flop) {
    if (slay.length === 0 && great.length === 0 && currentCast.length >= 8 && !floppersCheck && randomNumber(0, 100) >= 80 && !conjoinedCheck)
        floppers = true;
    if (slay.length == currentCast.length && !slayersCheck && !conjoinedCheck)
        slayers = true;
    else if (slay.length + great.length == currentCast.length && !slayersCheck && randomNumber(0, 100) >= 70 && !conjoinedCheck)
        slayers = true;
    if (flop.length + bad.length >= 5 && flop.length + bad.length < 7 && currentCast.length >= 9 && !bottom6WayLipsyncCheck && randomNumber(0, 100) >= 70 && !conjoinedCheck)
        bottom6WayLipsync = true;
    if (flop.length + bad.length >= 7 && great.length + slay.length + good.length > 0 && currentCast.length > 7 && currentCast.length < 10 &&!s14LaLaPaRUZaCheck && randomNumber(0, 100) >= 70 && !conjoinedCheck)
        s14LaLaPaRUZa = true;
}
function createRunwayDesc(slay, great, good, bad) {
    let screen = new Scene();
    if (slay.length !== 0) {
        for (let i = 0; i < slay.length; i++) {
            screen.createImage(slay[i].image, "darkblue");
            slay[i].runwayScore = 10;
        }
        screen.createBold("", "slayR");
        let slayText = document.getElementById("slayR");
        for (let i = 0; i < slay.length; i++)
            slayText.innerHTML += `${slay[i].getName()}, `;
        slayText.innerHTML += "slayed the runway!";
    }
    if (great.length !== 0) {
        for (let i = 0; i < great.length; i++) {
            screen.createImage(great[i].image, "royalblue");
            great[i].runwayScore = 5;
        }
        screen.createBold("", "greatR");
        let greatText = document.getElementById("greatR");
        for (let i = 0; i < great.length; i++)
            greatText.innerHTML += `${great[i].getName()}, `;
        greatText.innerHTML += "had a great runway!";
    }
    if (good.length !== 0) {
        for (let i = 0; i < good.length; i++) {
            screen.createImage(good[i].image);
            good[i].runwayScore = 0;
        }
        screen.createBold("", "goodR");
        let goodText = document.getElementById("goodR");
        for (let i = 0; i < good.length; i++)
            goodText.innerHTML += `${good[i].getName()}, `;
        goodText.innerHTML += "had a good runway.";
    }
    if (bad.length !== 0) {
        for (let i = 0; i < bad.length; i++) {
            screen.createImage(bad[i].image, "pink");
            bad[i].runwayScore = -3;
        }
        screen.createBold("", "badR");
        let badText = document.getElementById("badR");
        for (let i = 0; i < bad.length; i++)
            badText.innerHTML += `${bad[i].getName()}, `;
        badText.innerHTML += "had a bad runway...";
    }
}
function addQueen() {
    let name = document.getElementById("queenName").value.trim();
    let acting = document.getElementById("actingStat").valueAsNumber;
    let comedy = document.getElementById("comedyStat").valueAsNumber;
    let dance = document.getElementById("danceStat").valueAsNumber;
    let design = document.getElementById("designStat").valueAsNumber;
    let improv = document.getElementById("improvStat").valueAsNumber;
    let runway = document.getElementById("runwayStat").valueAsNumber;
    let lipsync = document.getElementById("lipsyncStat").valueAsNumber;
    let image = document.getElementById("url").value.trim();
    if ((acting || comedy || dance || design || improv || runway || lipsync) < 0 || (acting || comedy || dance || design || improv || runway || lipsync) > 15) {
        window.alert("Queens' stats must be between 0 and 15!");
        return;
    }
    if (name == "" || isNaN((acting || comedy || dance || design || improv || runway || lipsync))) {
        window.alert("One of the boxes is empty!");
        return;
    }
    let extension = image.substring(image.lastIndexOf(".") + 1).toLowerCase();
    let noimagemaybe = false;
    if (extension == "png" || extension == "jpg" || extension == ""){
        console.log("Good file");
        if (image == ""){
            image = "noimage";
            noimagemaybe = false;
        }else {
            noimagemaybe = true;
        }
    } else {
        window.alert("Invalid image extension! Use jpg or png instead!");
        document.getElementById("url").value = "";
        return;
    }
    let customQueen = new Queen(name, acting, comedy, dance, design, improv, runway, lipsync, image, noimagemaybe);
    let sameName = false;
    for (let i = 0; i < allCustomQueens.length; i++)
        if (allCustomQueens[i].getName() == customQueen.getName()) {
            window.alert(`There's already a queen with the name ${customQueen.getName()}! Please use another name.`);
            sameName = true;
            break;
        }
    if (sameName == false) {
        allCustomQueens.push(customQueen);
        customQueen.customqueen = true;
        let announce = document.getElementById("announce-new");
        announce.innerHTML = `${customQueen.getName()} added to the queen list!`;
        localStorage.setItem("customQueens", JSON.stringify(allCustomQueens));
        setTimeout(() => {
            document.location.reload();
        }, 1500);
    }
}
function customQueenSelectList() {
    let select = document.getElementById("custom-remove");
    for (let i = 0; i < allCustomQueens.length; i++) {
        let option = document.createElement("option");
        option.innerHTML = allCustomQueens[i].getName();
        option.value = i.toString();
        select.appendChild(option);
    }
}
function removeCustomQueen() {
    let select = document.getElementById("custom-remove");
    let index = parseInt(select.options[select.selectedIndex].value);
    let announce = document.getElementById("announce-remove");
    announce.innerHTML = `${allCustomQueens[index].getName()} removed from the queen list!`;
    allCustomQueens.splice(index, 1);
    localStorage.setItem("customQueens", JSON.stringify(allCustomQueens));
    setTimeout(() => {
        document.location.reload();
    }, 1500);
}
function editCustomQueen(){
    let editButton = document.getElementById("edit");
    let addButton = document.getElementById("add");
    let select = document.getElementById("custom-remove");
    let index = parseInt(select.options[select.selectedIndex].value);
    addButton.setAttribute("hidden", "hidden");
    editButton.removeAttribute("hidden");
    document.getElementById("queenName").value = allCustomQueens[index].getName();
    document.getElementById("actingStat").value = allCustomQueens[index]._actingStat;
    document.getElementById("comedyStat").value = allCustomQueens[index]._comedyStat;
    document.getElementById("danceStat").value = allCustomQueens[index]._danceStat;
    document.getElementById("designStat").value = allCustomQueens[index]._designStat;
    document.getElementById("improvStat").value = allCustomQueens[index]._improvStat;
    document.getElementById("runwayStat").value = allCustomQueens[index]._runwayStat;
    document.getElementById("lipsyncStat").value = allCustomQueens[index]._lipsyncStat;
    document.getElementById("url").value = allCustomQueens[index].image;
}
function updateCustomQueen(){
    let select = document.getElementById("custom-remove");
    let index = parseInt(select.options[select.selectedIndex].value);
    let name = document.getElementById("queenName").value.trim();
    let acting = document.getElementById("actingStat").valueAsNumber;
    let comedy = document.getElementById("comedyStat").valueAsNumber;
    let dance = document.getElementById("danceStat").valueAsNumber;
    let design = document.getElementById("designStat").valueAsNumber;
    let improv = document.getElementById("improvStat").valueAsNumber;
    let runway = document.getElementById("runwayStat").valueAsNumber;
    let lipsync = document.getElementById("lipsyncStat").valueAsNumber;
    let image = document.getElementById("url").value.trim();
    if ((acting || comedy || dance || design || improv || runway || lipsync) < 0 || (acting || comedy || dance || design || improv || runway || lipsync) > 15) {
        window.alert("Queens' stats must be between 0 and 15!");
        return;
    }
    if (name == "" || isNaN((acting || comedy || dance || design || improv || runway || lipsync))) {
        window.alert("One of the boxes is empty!");
        return;
    }
    let extension = image.substring(image.lastIndexOf(".") + 1).toLowerCase();
    let noimagemaybe = false;
    if (extension == "png" || extension == "jpg" || extension == ""){
        console.log("Good file");
        if (image == ""){
            image = "noimage";
            noimagemaybe = false;
        }else {
            noimagemaybe = true;
        }
    } else {
        window.alert("Invalid image extension! Use jpg or png instead!");
        document.getElementById("url").value = "";
        return;
    }
    let customQueen = new Queen(name, acting, comedy, dance, design, improv, runway, lipsync, image, noimagemaybe);
    allCustomQueens.splice(index, 1);
    allCustomQueens.push(customQueen);
    customQueen.customqueen = true;
    customQueen.custom = true;
    let announce = document.getElementById("announce-new");
    announce.innerHTML = `${customQueen.getName()} updated!`;
    localStorage.setItem("customQueens", JSON.stringify(allCustomQueens));
    setTimeout(() => {
        document.location.reload();
    }, 1500);
}
function randomizeStats() {
    let stats = document.getElementsByClassName("stats");
    for (let i = 0; i < stats.length; i++) {
        stats[i].value = randomNumber(0, 15).toString();
    }
}
let premiereCounter = 0;
let firstCast = [];
let secondCast = [];
function doublePremiere() {
    if (premiereCounter == 0)
        if (s6Premiere || s12Premiere || s14Premiere) {
            shuffle(currentCast);
            firstCast = currentCast.splice(0, Math.floor(currentCast.length / 2));
            secondCast = [...currentCast];
            slayersCheck = true;
        }
    if (premiereCounter == 0) {
        currentCast = firstCast;
        for (let i = 0; i < secondCast.length; i++)
            secondCast[i].addToTrackRecord("");
        premiereCounter++;
        slayersCheck = true;
        newEpisode();
    }
    else if (premiereCounter == 1) {
        currentCast = secondCast;
        for (let i = 0; i < firstCast.length; i++)
            firstCast[i].addToTrackRecord("");
        premiereCounter++;
        slayersCheck = true;
        newEpisode();
    }
    else if (premiereCounter == 2 && s14Premiere) {
        currentCast = [...firstCast, ...secondCast];
        for (let i = 0; i < eliminatedCast.length; i++){
            let queen = eliminatedCast[i];
            if (disqOrDept) {
                if (queen.QueenDisqOrDept){
                    console.log(queen);
                }else{
                    queen.trackRecord.splice(queen.trackRecord.indexOf("ELIM"), 1, " ELIM");
                    currentCast.push(queen);
                    eliminatedCast.splice(eliminatedCast.indexOf(queen), 1);
                    i--;
                }
            }
            else{
                queen.trackRecord.splice(queen.trackRecord.indexOf("ELIM"), 1, " ELIM");
                currentCast.push(queen);
                eliminatedCast.splice(eliminatedCast.indexOf(queen), 1);
                i--;
            }
        }
        premiereCounter++;
        chocolateBarTwistCheck = false;
        slayersCheck = false;
        newEpisode();
    }
    else if (premiereCounter == 2) {
        currentCast = [...firstCast, ...secondCast];
        premiereCounter++;
        slayersCheck = false;
        newEpisode();
    }
}
function porkchopLipsyncs() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("It's time...");
    screen.createParagraph("After the queens enter the workroom, it's time for them to lip-sync... for their lives!");
    for (let i = 0; i < Math.floor(totalCastSize / 2); i++) {
        screen.createHorizontalLine();
        let queen1 = currentCast[randomNumber(0, currentCast.length - 1)];
        currentCast.splice(currentCast.indexOf(queen1), 1);
        let queen2 = currentCast[randomNumber(0, currentCast.length - 1)];
        currentCast.splice(currentCast.indexOf(queen2), 1);
        if (currentCast.length == 1) {
            let queen3 = currentCast[randomNumber(0, currentCast.length - 1)];
            currentCast.splice(currentCast.indexOf(queen3), 1);
            screen.createImage(queen1.image, "royalblue");
            screen.createImage(queen2.image, "royalblue");
            screen.createImage(queen3.image, "royalblue");
            screen.createBold(`${queen1.getName()}, ${queen2.getName()} and ${queen3.getName()} will lipsync...`);
            lsSong();
            let lipSync = [queen1, queen2, queen3];
            for (let i = 0; i < lipSync.length; i++) {
                lipSync[i].getASLipsync();
            }
            lipSync.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
            queen1 = lipSync[0];
            queen2 = lipSync[1];
            queen3 = lipSync[2];
            screen.createImage(queen1.image, "green");
            screen.createBold(`${queen1.getName()}, shantay you stay!`);
            screen.createImage(queen2.image, "orange");
            screen.createImage(queen3.image, "orange");
            screen.createBold(`${queen2.getName()} and ${queen3.getName()}, you're getting the porkchop...`);
            queen1.addToTrackRecord(" WIN ");
            queen2.addToTrackRecord("LOSS");
            queen3.addToTrackRecord("LOSS");
            firstCast.push(queen1);
            secondCast.push(queen2, queen3);
        }
        else {
            screen.createImage(queen1.image, "royalblue");
            screen.createImage(queen2.image, "royalblue");
            screen.createBold(`${queen1.getName()} and ${queen2.getName()} will lipsync...`);
            lsSong();
            let lipSync = [queen1, queen2];
            for (let i = 0; i < lipSync.length; i++) {
                lipSync[i].getASLipsync();
            }
            lipSync.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
            queen1 = lipSync[0];
            queen2 = lipSync[1];
            screen.createImage(queen1.image, "green");
            screen.createBold(`${queen1.getName()}, shantay you stay!`);
            screen.createImage(queen2.image, "orange");
            screen.createBold(`${queen2.getName()}, you're getting the porkchop...`);
            queen1.addToTrackRecord(" WIN ");
            queen2.addToTrackRecord("LOSS");
            firstCast.push(queen1);
            secondCast.push(queen2);
        }
    }
    screen.createHorizontalLine();
    screen.createBigText("The porkchop queens will vote out one of their group...");
    screen.createBold("The queens vote...");
    for (let i = 0; i < secondCast.length; i++) {
        secondCast[i].lipstick = secondCast[randomNumber(0, secondCast.length - 1)];
        while (secondCast[i].lipstick.getName() == secondCast[i].getName()) {
            secondCast[i].lipstick = secondCast[randomNumber(0, secondCast.length - 1)];
        }
        secondCast[i].lipstick.votes++;
        screen.createParagraph(`${secondCast[i].getName()} voted for ${secondCast[i].lipstick.getName()}!`);
    }
    screen.createHorizontalLine();
    screen.createBold("The results are in..!");
    for (let i = 0; i < secondCast.length; i++) {
        screen.createBold(`${secondCast[i].getName()}: ${secondCast[i].votes.toString()} votes`);
    }
    screen.createHorizontalLine();
    let queen = secondCast.sort((a, b) => b.votes - a.votes)[0];

    if (secondCast[0].votes == secondCast[1].votes) {
        screen.createBold("It is a tie, the queens must revote between " + secondCast[0].getName() + " and " + secondCast[1].getName() + "!!");
        secondCast[0].votes = 0;
        secondCast[1].votes = 0;
        for (let i = 0; i < secondCast.length; i++) {
            secondCast[i].lipstick = secondCast[randomNumber(0, 1)];
            while (secondCast[i].lipstick.getName() == secondCast[i].getName()) {
                secondCast[i].lipstick = secondCast[randomNumber(0, 1)];
            }
            secondCast[i].lipstick.votes++;
            screen.createParagraph(`${secondCast[i].getName()} voted for ${secondCast[i].lipstick.getName()}!`);
        }
        screen.createHorizontalLine();
        screen.createBold("The results are in..!");
        screen.createBold(`${secondCast[0].getName()}: ${secondCast[0].votes.toString()} votes`);
        screen.createBold(`${secondCast[1].getName()}: ${secondCast[1].votes.toString()} votes`);
        let tiebreaker = secondCast.sort((a, b) => b.votes - a.votes)[0];
        queen = tiebreaker;
        screen.createHorizontalLine();
    }
    screen.createBold(`The queen that's getting the porkchop is... ${queen.getName()}!`);
    firstCast.push(queen);
    secondCast.splice(secondCast.indexOf(queen), 1);
    queen.trackRecord.pop();
    queen.addToTrackRecord("LOSS ")
    episodeChallenges.push("Porkchop Lipsyncs");
    for (let i = 0; i < secondCast.length; i++) {
        secondCast[i].votes = 0;
    }
    screen.createButton("Proceed", "doublePremiere()");
}
function doublePremiereJudging() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("Bring back my girls!");
    screen.createBold("Ladies, I've made some decisions...");
    document.body.style.backgroundImage = "url('image/stage.webp')";
    screen.createImage(topQueens[0].image, "cyan");
    screen.createImage(topQueens[1].image, "cyan");
    screen.createBold(`${topQueens[0].getName()}, ${topQueens[1].getName()}, condragulations, you're the Top 2 of the week!`);
    screen.createParagraph("Nobody is going home tonight!");
    screen.createHorizontalLine();
    screen.createBold("The Top 2 will now lip-sync... for the win!");
    lsSong();
    for (let i = 0; i < topQueens.length; i++) {
        topQueens[i].getASLipsync();
    }
    topQueens.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    screen.createImage(topQueens[0].image, "royalblue");
    screen.createBold(`${topQueens[0].getName()}, you're a winner baby!`);
    topQueens[0].addToTrackRecord("WIN");
    topQueens[0].favoritism += 5;
    topQueens[0].ppe += 2;
    topQueens[1].addToTrackRecord("TOP2");
    topQueens[1].favoritism += 2;
    topQueens[1].ppe += 1.5;
    screen.createButton("Proceed", "doublePremiere()");
}
function uk3PremiereJudging() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("Bring back my girls!");
    screen.createBold("Ladies, I've made some decisions...");
    document.body.style.backgroundImage = "url('image/stage.webp')";
    screen.createImage(topQueens[2].image, "lightblue");
    topQueens[2].addToTrackRecord("HIGH");
    topQueens[2].favoritism += 1;
    topQueens[2].ppe += 4;
    screen.createParagraph("", "highs");
    let highs = document.getElementById("highs");
    highs.innerHTML += `${topQueens[2].getName()}, `;
    highs.innerHTML += "good job this week, you're safe.";
    topQueens.splice(2, 1);
    screen.createImage(topQueens[0].image, "cyan");
    screen.createImage(topQueens[1].image, "cyan");
    screen.createBold(`${topQueens[0].getName()}, ${topQueens[1].getName()}, condragulations, you're the Top 2 of the week!`);
    screen.createHorizontalLine();
    screen.createBold("The Top 2 will now lip-sync... for the win!");
    lsSong();
    for (let i = 0; i < topQueens.length; i++) {
        topQueens[i].getASLipsync();
    }
    topQueens.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    screen.createImage(topQueens[0].image, "royalblue");
    screen.createBold(`${topQueens[0].getName()}, you're a winner baby!`);
    topQueens[0].addToTrackRecord("WIN");
    topQueens[0].favoritism += 5;
    topQueens[0].ppe += 5;
    topQueens[1].addToTrackRecord("TOP2");
    topQueens[1].favoritism += 2;
    topQueens[1].ppe += 4.5;
    topQueens.splice(0, 2);
    screen.createHorizontalLine();
    screen.createBold("Now...");
    if (bottomQueens.length >= 3) {
        for (let i = 0; i < bottomQueens.length; i++)
            screen.createImage(bottomQueens[i].image, "tomato");
        screen.createParagraph("", "bottom3");
        let bottom3 = document.getElementById("bottom3");
        for (let i = 0; i < bottomQueens.length; i++)
            bottom3.innerHTML += bottomQueens[i].getName() + ", ";
        bottom3.innerHTML += "you're the bottoms of the week...";
    }
    //do the same, but for the bottom queens:
    if (bottomQueens.length == 3) {
        for (let i = 0; i < topQueens.length; i++)
            bottomQueens[i].performanceScore -= (bottomQueens[i].runwayScore - bottomQueens[i].favoritism);
        bottomQueens.sort((a, b) => (a.performanceScore - b.performanceScore));
        bottomQueens[0].addToTrackRecord("LOW");
        screen.createImage(bottomQueens[0].image, "pink");
        screen.createBold(bottomQueens[0].getName() + "... you are safe.");
        bottomQueens[0].unfavoritism += 1;
        bottomQueens[0].ppe += 2;
        bottomQueens.splice(0, 1);
    }
    for (let i = 0; i < bottomQueens.length; i++)
        screen.createImage(bottomQueens[i].image, "tomato");
    screen.createBold("", "btm2");
    let btm2 = document.getElementById("btm2");
    for (let i = 0; i < bottomQueens.length; i++) {
        btm2.innerHTML += bottomQueens[i].getName() + ", ";
    }
    btm2.innerHTML += "I'm sorry my dears but you are up for elimination.";
    screen.createButton("Proceed", "lipSync()");
}
let currentCast = [];
let eliminatedCast = [];
let fullCast = [];
let safeQueens = [];
let topQueens = [];
let bottomQueens = [];
let top2 = [];
let doubleShantay = false;
let doubleSashay = false;
let episodeChallenges = [];
let episodeCount = 0;
let returningQueen = false;
let noDouble = false;
let chocolateBarTwist = false;
let chocolateBarTwistCheck = false;
let chocolateBarTwistChoosable = false;
let s6Premiere = false;
let s12Premiere = false;
let s14Premiere = false;
let porkchopPremiere = false;
let firstPremiere = false;
let secondPremiere = false;
let uk3Premiere = false;
let s9Premiere = false;
//challenge seasons
let sweatshop = false;
let chaos = false;
function newEpisode() {
    safeQueens = [];
    topQueens = [];
    bottomQueens = [];
    top2 = [];
    episodeCount++;
    let queensRemainingScreen = new Scene();
    if (s9Premiere && episodeCount == 1) {
        lateQueen = currentCast[randomNumber(0, currentCast.length - 1)];
        console.log(lateQueen);
        currentCast.splice(currentCast.indexOf(lateQueen), 1);
        lateQueen.addToTrackRecord('');
    }
    if (episodeCount == 1 || premiereCounter <= 2 && (s12Premiere || porkchopPremiere || s6Premiere || s14Premiere ) || episodeCount == 1 && (uk3Premiere || s9Premiere)) {
        queensRemainingScreen.clean();
        queensRemainingScreen.createHeader("Full cast");
        for (let i = 0; i < currentCast.length; i++) {
            queensRemainingScreen.createImage(currentCast[i].image);
            queensRemainingScreen.createBold(currentCast[i].getName());
        }
    }
    else {
        contestantProgress();
    }
    if (currentCast.length == totalCastSize && team == true)
        queensRemainingScreen.createButton("Proceed", "teamsScreen()");
    else if (currentCast.length > 4)
        queensRemainingScreen.createButton("Proceed", "miniChallenge()");
    else if (currentCast.length == 4 && porkchopPremiere && premiereCounter < 3)
        queensRemainingScreen.createButton("Proceed", "miniChallenge()");
    else if (currentCast.length == 4 && canFinale)
        queensRemainingScreen.createButton("Proceed", "canadaS2Finale()");
    else if (currentCast.length == 4 && (top3 || team))
        queensRemainingScreen.createButton("Proceed", "miniChallenge()");
    else if (currentCast.length == 4 && top4 || ukvstwFinale)
        queensRemainingScreen.createButton("Proceed", "finaleLS()");
    else if (currentCast.length == 4 && (all_stars || lipsync_assassin))
        queensRemainingScreen.createButton("Proceed", "finaleAS()");
    else if (currentCast.length == 3 && team)
        queensRemainingScreen.createButton("Proceed", "miniChallenge()");
    else if (currentCast.length == 2 && team)
        queensRemainingScreen.createButton("Proceed", "finaleTeam()");
    else
        queensRemainingScreen.createButton("Proceed", "finale()");
    //add an empty placement on eliminated queen's track records
    for (let i = 0; i < eliminatedCast.length; i++)
        eliminatedCast[i].addToTrackRecord('');
}
function reSimulate() {
    //add eliminated queens again to cast and clean it
    for (let i = 0; i < eliminatedCast.length; i++) {
        currentCast.push(eliminatedCast[i]);
    }
    if (top4) {
        finalLS = [];
        firstLS = [];
        secondLS = [];
    }else if (canFinale){
        finalLS = [];
        firstLS = [];
        secondLS = [];
    }else if(ukvstwFinale){
        finalLS = [];
        firstLS = [];
        secondLS = [];
    }
    currentCast.sort((a, b) => a.getName().toLowerCase().localeCompare(b.getName().toLowerCase()));
    eliminatedCast = [];
    firstCast = [];
    secondCast = [];
    fullCast = [];
    premiereCounter = 0;
    episodeCount = 0;
    onFinale = false;
    onTop4Finale = false;
    totalCastSize = currentCast.length;
    disqOrDept = false;
    //clean track records
    for (let i = 0; i < currentCast.length; i++) {
        currentCast[i].trackRecord = [];
        currentCast[i].favoritism = 0;
        currentCast[i].unfavoritism = 0;
        currentCast[i].finaleScore = 0;
        currentCast[i].votes = 0;
        currentCast[i].ppe = 0;
        currentCast[i].episodesOn = 0;
        currentCast[i].QueenDisqOrDept = false;
        currentCast[i].chocolate = false;
    }
    //clean challenges
    episodeChallenges = [];
    actingChallengeCounter = 0;
    comedyChallengeCounter = 0;
    marketingChallengeCounter = 0;
    danceChallengeCounter = 0;
    designChallengeCounter = 0;
    improvChallengeCounter = 0;
    rusicalCounter = false;
    ballCounter = false;
    talentShowCounter = false;
    girlGroupCounter = false;
    rumixCounter = false;
    makeoverCounter = false;
    snatchCounter = false;
    doubleShantay = false;
    doubleSashay = false;
    returningQueen = false;
    floppers = false;
    floppersCheck = false;
    slayers = false;
    slayersCheck = false;
    bottom6WayLipsync = false;
    bottom6WayLipsyncCheck = false;
    s14LaLaPaRUZa = false;
    s14LaLaPaRUZaCheck = false;
    assasintable = [];
    assasinlipstick = [];
    twinsMakeover = [];
    conjoinedCheck = false;
    s9PremiereCheck = false;
    uk3PremiereCheck = false;
    chocolateBarTwistCheck = false;
    lateQueen = '';
    //refill lip-sync songs and lsa
    lsSongs = allLsSongs;
    allQueens = allQueensCopy;
    if (chocolateBarTwist) {
        if (chocolateBarTwistChoosable){
            chooseGoldenBar();
        }else {
            giveChocolate();
        }
    }
    else if (s6Premiere || s12Premiere || s14Premiere)
        doublePremiere();
    else if (porkchopPremiere)
        porkchopLipsyncs();
    else
        newEpisode();
}
let firstLS = [];
let secondLS = [];
let finalLS = [];
let onFinale = false;
let onTop4Finale = false;

function finaleLS() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The grand finale!");
    screen.createImage(currentCast[0].image, "royalblue");
    screen.createImage(currentCast[1].image, "royalblue");
    screen.createImage(currentCast[2].image, "royalblue");
    screen.createImage(currentCast[3].image, "royalblue");
    screen.createParagraph("Our Top 4 will participate in a lip-sync smackdown for the crown! The preliminaries will now be decided...");
    screen.createHorizontalLine();
    for (let i = 0; i < 2; i++) {
        let q1 = currentCast[randomNumber(0, currentCast.length - 1)];
        firstLS.push(q1);
        currentCast.splice(currentCast.indexOf(q1), 1);
        let q2 = currentCast[randomNumber(0, currentCast.length - 1)];
        secondLS.push(q2);
        currentCast.splice(currentCast.indexOf(q2), 1);
    }
    screen.createBigText("The preliminaries will be: ");
    screen.createImage(firstLS[0].image, "darkblue");
    screen.createImage(firstLS[1].image, "darkblue");
    screen.createBold(firstLS[0].getName() + " vs. " + firstLS[1].getName());
    screen.createParagraph("and");
    screen.createImage(secondLS[0].image, "darkred");
    screen.createImage(secondLS[1].image, "darkred");
    screen.createBold(secondLS[0].getName() + " vs. " + secondLS[1].getName());
    episodeChallenges.push("Finale");
    screen.createButton("Proceed", "finaleLipSyncs()");
}
let finaleof4gurl = false;
function finaleLipSyncs() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The Lip-Syncs...");
    screen.createParagraph(firstLS[0].getName() + " and " + firstLS[1].getName() + " lip-sync...");
    lsSong();
    for (let i = 0; i < firstLS.length; i++) {
        firstLS[i].getLipsync();
    }
    firstLS.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    if (firstLS[0].lipsyncScore == firstLS[1].lipsyncScore && firstLS[0].lipsyncScore > 6 && firstLS[1].lipsyncScore > 6) {
        screen.createImage(firstLS[0].image, "silver");
        screen.createImage(firstLS[1].image, "silver");
        screen.createBold(firstLS[0].getName() + ", " + firstLS[1].getName() + ", shantay you both stay.");
        finalLS.push(firstLS[0]);
        finalLS.push(firstLS[1]);
        isThisA3Way = true;
    } else if (chocolateBarTwist  && !chocolateBarTwistCheck) {
        screen.createImage(firstLS[0].image, "silver");
        screen.createBold(firstLS[0].getName() + ", shantay you stay.");
        screen.createBold(firstLS[1].getName() + ", now your fate rests in the hands of the drag gods.");
        screen.createBold("If you have the golden chocolate bar, you will be safe.");
        finalLS.push(firstLS[0]);
        if (chocolateBarCheck(firstLS[1]) == true) {
            screen.createImage("image/ChocolateBarWithTicket.webp", "gold");
            screen.createImage(firstLS[1].image, "gold");
            screen.createBold("You've got the GOLD BAR!!!! The gods have spoken!");
            screen.createBold(firstLS[1].getName() + "!! Condragtulations, you are safe to slay another day and you move on into the final lipsync!!");
            firstLS[1].unfavoritism += 3;
            finalLS.push(firstLS[1]);
            chocolateBarTwistCheck = true;
            isThisA3Way = true;
        } else {
            screen.createImage("image/ChocolateBarWithNoTicket.webp", "brown");
            screen.createBold("It's chocolate.");
            firstLS[1].addToTrackRecord("LOST 1ST ROUND");
            eliminatedCast.unshift(firstLS[1]);
            screen.createImage(firstLS[1].image, "sienna");
            screen.createBold(firstLS[1].getName() + ", sashay away...");
        }
    } 
    else {
        finalLS.push(firstLS[0]);
        firstLS[1].addToTrackRecord("LOST 1ST ROUND");
        eliminatedCast.unshift(firstLS[1]);
        screen.createImage(firstLS[0].image, "silver");
        screen.createBold(firstLS[0].getName() + ", shantay you stay.");
        screen.createImage(firstLS[1].image, "sienna");
        screen.createBold(firstLS[1].getName() + ", sashay away...");
    }
    screen.createHorizontalLine();
    screen.createParagraph(secondLS[0].getName() + " and " + secondLS[1].getName() + " lip-sync...");
    lsSong();
    for (let i = 0; i < secondLS.length; i++) {
        secondLS[i].getASLipsync();
    }
    secondLS.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    if (secondLS[0].lipsyncScore == secondLS[1].lipsyncScore && secondLS[0].lipsyncScore > 6 && secondLS[1].lipsyncScore > 6) {
        screen.createImage(secondLS[0].image, "silver");
        screen.createImage(secondLS[1].image, "silver");
        screen.createBold(secondLS[0].getName() + ", " + secondLS[1].getName() + ", shantay you both stay.");
        finalLS.push(secondLS[0]);
        finalLS.push(secondLS[1]);
        if (!isThisA3Way) {
            isThisA3Way = true;
        } else {
            finaleof4gurl = true;
        }
    } else if (chocolateBarTwist  && !chocolateBarTwistCheck) {
        screen.createImage(secondLS[0].image, "silver");
        screen.createBold(secondLS[0].getName() + ", shantay you stay.");
        screen.createBold(secondLS[1].getName() + ", now your fate rests in the hands of the drag gods.");
        screen.createBold("If you have the golden chocolate bar, you will be safe.");
        finalLS.push(secondLS[0]);
        if (chocolateBarCheck(secondLS[1]) == true) {
            screen.createImage("image/ChocolateBarWithTicket.webp", "gold");
            screen.createImage(secondLS[1].image, "gold");
            screen.createBold("You've got the GOLD BAR!!!! The gods have spoken!");
            screen.createBold(secondLS[1].getName() + "!! Condragtulations, you are safe to slay another day and you move on into the final lipsync!!");
            secondLS[1].unfavoritism += 3;
            chocolateBarTwistCheck = true;
            finalLS.push(secondLS[1]);
            if (!isThisA3Way) {
                isThisA3Way = true;
            } else {
                finaleof4gurl = true;
            }
        } else {
            screen.createImage("image/ChocolateBarWithNoTicket.webp", "brown");
            screen.createBold("It's chocolate.");
            secondLS[1].addToTrackRecord("LOST 2ND ROUND");
            eliminatedCast.unshift(secondLS[1]);
            screen.createImage(secondLS[1].image, "sienna");
            screen.createBold(secondLS[1].getName() + ", sashay away...");
        }
    }  
    else {
        finalLS.push(secondLS[0]);
        secondLS[1].addToTrackRecord("LOST 2ND ROUND");
        eliminatedCast.unshift(secondLS[1]);
        screen.createImage(secondLS[0].image, "silver");
        screen.createBold(secondLS[0].getName() + ", shantay you stay.");
        screen.createImage(secondLS[1].image, "sienna");
        screen.createBold(secondLS[1].getName() + ", sashay away...");
    }
    screen.createButton("Proceed", "finalLipSync()");
}
function finalLipSync() {
    onTop4Finale = true;
    onFinale = true;
    chocolateBarTwistCheck = true;
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The end...");
    if (finaleof4gurl) {
        screen.createBold(finalLS[0].getName() + ", " + finalLS[1].getName() + ", " + finalLS[2].getName() + " and " + finalLS[3].getName() + " will lip-sync for the crown...!");
        screen.createImage(finalLS[0].image);
        screen.createImage(finalLS[1].image);
        screen.createImage(finalLS[2].image);
        screen.createImage(finalLS[3].image);
        lsSong();
        screen.createHorizontalLine();
        screen.createBold("Ladies, I've made my decision. The Next Drag Superstar is...");
        for (let i = 0; i < finalLS.length; i++)
            finalLS[i].getFinale();
        finalLS.sort((a, b) => b.finaleScore - a.finaleScore);
        let winner = 0;
        if (randomNumber(0, 100) >= 95) {
            winner = randomNumber(1, 3);
        }
        screen.createImage(finalLS[winner].image, "yellow");
        screen.createBigText(finalLS[winner].getName() + "!!");
        screen.createBold("Now prance, my queen!");
        finalLS[winner].addToTrackRecord("WINNER");
        for (let i = 0; i < finalLS.length; i++) {
            if (!(finalLS.indexOf(finalLS[i]) == winner)) {
                finalLS[i].addToTrackRecord("LOST 3RD ROUND");
                eliminatedCast.unshift(finalLS[i]);
            }
        }
        if (winner == 0) {
            finalLS.splice(1, 3);
        } else if (winner == 1) {
            finalLS.splice(2, 2);
            finalLS.splice(0, 1);
        } else if (winner == 2) {
            finalLS.splice(0, 2);
            finalLS.splice(1, 1);
        } else if (winner == 3) {
            finalLS.splice(0, 3);
        }
    } else if (isThisA3Way) {
        screen.createBold(finalLS[0].getName() + ", " + finalLS[1].getName() + " and " + finalLS[2].getName() + " will lip-sync for the crown...!");
        screen.createImage(finalLS[0].image);
        screen.createImage(finalLS[1].image);
        screen.createImage(finalLS[2].image);
        lsSong();
        screen.createHorizontalLine();
        screen.createBold("Ladies, I've made my decision. The Next Drag Superstar is...");
        for (let i = 0; i < finalLS.length; i++)
            finalLS[i].getFinale();
        finalLS.sort((a, b) => b.finaleScore - a.finaleScore);
        let winner = 0;
        if (randomNumber(0, 100) >= 95) {
            winner = randomNumber(1, 2);
        }
        screen.createImage(finalLS[winner].image, "yellow");
        screen.createBigText(finalLS[winner].getName() + "!!");
        screen.createBold("Now prance, my queen!");
        finalLS[winner].addToTrackRecord("WINNER");
        for (let i = 0; i < finalLS.length; i++) {
            if (!(finalLS.indexOf(finalLS[i]) == winner)) {
                finalLS[i].addToTrackRecord("LOST 3RD ROUND");
                eliminatedCast.unshift(finalLS[i]);
            }
        }
        if (winner == 0) {
            finalLS.splice(1, 2);
        } else if (winner == 1) {
            finalLS.splice(2, 1);
            finalLS.splice(0, 1);
        } else if (winner == 2) {
            finalLS.splice(0, 2);
        }
    } else {
        screen.createBold(finalLS[0].getName() + " and " + finalLS[1].getName() + " will lip-sync for the crown...!");
        screen.createImage(finalLS[0].image);
        screen.createImage(finalLS[1].image);
        lsSong();
        screen.createHorizontalLine();
        screen.createBold("Ladies, I've made my decision. The Next Drag Superstar is...");
        for (let i = 0; i < finalLS.length; i++)
            finalLS[i].getFinale();
        finalLS.sort((a, b) => b.finaleScore - a.finaleScore);
        if (finalLS[0].finaleScore == finalLS[1].finaleScore && randomNumber(0, 100) >= 50) {
            screen.createBold("For the FIRST TIME in Drag Race herstory, you are both winners, baby");
            screen.createImage(finalLS[0].image, "yellow");
            screen.createImage(finalLS[1].image, "yellow");
            screen.createBigText(finalLS[0].getName() + " and " + finalLS[1].getName() + "!!");
            screen.createBold("Now prance, my queens!");
            finalLS[0].addToTrackRecord("WINNER");
            finalLS[1].addToTrackRecord("WINNER");
            eliminatedCast.unshift(finalLS[1]);
            finalLS.splice(1, 1);
        }else{
            let winner = 0;
            if (randomNumber(0, 100) >= 95) {
                winner = 1;
            }
            screen.createImage(finalLS[winner].image, "yellow");
            screen.createBigText(finalLS[winner].getName() + "!!");
            screen.createBold("Now prance, my queen!");
            finalLS[winner].addToTrackRecord("WINNER");
            for (let i = 0; i < finalLS.length; i++) {
                if (!(finalLS.indexOf(finalLS[i]) == winner)) {
                    finalLS[i].addToTrackRecord("LOST 3RD ROUND");
                    eliminatedCast.unshift(finalLS[i]);
                    finalLS.splice(i, 1);
                }
            }
        }
    }
    isThisA3Way = false;
    finaleof4gurl = false;
    currentCast.push(finalLS[0]);
    screen.createButton("Proceed", "contestantProgress()");
}
function finale() {
    //sort queens by finale score:
    for (let i = 0; i < currentCast.length; i++) {
        currentCast[i].getFinale();
    }
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The grande finale!");
    for (let i = 0; i < currentCast.length; i++)
        screen.createImage(currentCast[i].image);
    currentCast.sort((a, b) => (b.finaleScore - a.finaleScore));
    screen.createParagraph("Our Top 3 will participate in a music video for RuPaul's newest single!");
    screen.createButton("Proceed", "runway()", "button2");
}
function finaleTeam() {
    //sort queens by finale score:
    for (let i = 0; i < currentCast.length; i++) {
        currentCast[i].getFinale();
    }
    currentCast.sort((a, b) => (b.finaleScore - a.finaleScore));
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The grande finale!");
    screen.createParagraph("Our Top 4 will participate in a music video for RuPaul's newest single!");
    screen.createImage(currentCast[0].QueenB.image, "black");
    screen.createImage(currentCast[1].QueenB.image, "black");
    screen.createImage(currentCast[0].QueenA.image, "black");
    screen.createImage(currentCast[1].QueenA.image, "black");
    screen.createButton("Proceed", "runway()", "button2");
}
let isThisA3Way = false;
function finaleJudging() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The final minutes...");
    screen.createBold("Ladies, it's time to decide The Next Drag Superstar, and...");
    if (randomNumber(0, 100) <= 90){
        screen.createImage(currentCast[2].image, "sienna");
        screen.createBold(currentCast[2].getName() + ", I'm sorry my dear but it's not your time. I must ask you to sashay away...");
        currentCast[2].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[2]);
        currentCast.splice(2, 1);
        screen.createHorizontalLine();
        screen.createImage(currentCast[0].image, "silver");
        screen.createImage(currentCast[1].image, "silver");
        screen.createBold(currentCast[0].getName() + " and " + currentCast[1].getName() + ", this is your last chance to prove yourself. It's time for you to lipsync.. for the CROWN!!");
        lsSong();
    } else {
        screen.createBold("For the first time in Drag Race herstory, we are breaking all the rules!");
        screen.createHorizontalLine();
        screen.createImage(currentCast[0].image, "silver");
        screen.createImage(currentCast[1].image, "silver");
        screen.createImage(currentCast[2].image, "silver");
        screen.createBold(currentCast[0].getName() + ", " + currentCast[1].getName() + " and " + currentCast[2].getName() + ", the three of you will lipsync for your lives!!");
        lsSong();
        isThisA3Way = true;
    }
    screen.createButton("Proceed", "finaleFinale()");
}
function finaleTeamJudging() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The final minutes...");
    screen.createBold("Ladies, it's time to decide The Next Drag Superstar, and...");
    screen.createBold(currentCast[1].getName() + ", I'm sorry my dears but it's not your time. I must ask you both to sashay away...");
    screen.createHorizontalLine();
    currentCast[1].QueenA.addToTrackRecord("ELIMINATED");
    currentCast[1].QueenB.addToTrackRecord("ELIMINATED");
    eliminatedCast.unshift(currentCast[1].QueenA);
    eliminatedCast.unshift(currentCast[1].QueenB);
    currentCast.splice(1, 1);
    if (randomNumber(0, 100) <= 50) {
        currentCast.push(currentCast[0].QueenA);
        currentCast.push(currentCast[0].QueenB);
    }
    else {
        currentCast.push(currentCast[0].QueenB);
        currentCast.push(currentCast[0].QueenA);
    }
    if (randomNumber(0, 100) <= 80) {
        currentCast[0].QueenB.finaleScore += 1;
    }
    currentCast.splice(0, 1);
    screen.createBold(currentCast[0].getName() + " and " + currentCast[1].getName() + ", this is your last chance to prove yourself. It's time for you to lipsync.. for the CROWN!!");
    lsSong();
    screen.createButton("Proceed", "finaleFinale()");
}
function finaleFinale() {
    onFinale = true;
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The end.");
    screen.createBold("Ladies, I've made my decision. The Next Drag Superstar is...");
    chocolateBarTwistCheck = true;
    if (currentCast[0].finaleScore == currentCast[1].finaleScore && randomNumber(0, 100) >= 90) {
        screen.createBold("For the FIRST TIME in Drag Race herstory, you are both winners, baby");
        screen.createImage(currentCast[0].image, "yellow");
        screen.createImage(currentCast[1].image, "yellow");
        screen.createBigText(currentCast[0].getName() + " and " + currentCast[1].getName() + "!!");
        screen.createBold("Now prance, my queens!");
        if (!allstars3Finale && !ukvstwFinale && !top2finaleAS && (all_stars || lipsync_assassin) || isThisA3Way) {
            currentCast[2].addToTrackRecord("RUNNER UP");
            eliminatedCast.unshift(currentCast[2]);
            currentCast.splice(2, 1);
        }
        currentCast[0].addToTrackRecord("WINNER");
        currentCast[1].addToTrackRecord("WINNER");
        eliminatedCast.unshift(currentCast[1]);
        currentCast.splice(1, 1);
    }else{
        screen.createImage(currentCast[0].image, "yellow");
        screen.createBigText(currentCast[0].getName() + "!!");
        screen.createBold("Now prance, my queen!");
        currentCast[0].addToTrackRecord("WINNER");
        currentCast[1].addToTrackRecord("RUNNER UP");
        eliminatedCast.unshift(currentCast[1]);
        currentCast.splice(1, 1);
        if (!allstars3Finale && !ukvstwFinale && !top2finaleAS && (all_stars || lipsync_assassin) || isThisA3Way) {
            currentCast[1].addToTrackRecord("RUNNER UP");
            eliminatedCast.unshift(currentCast[1]);
            currentCast.splice(1, 1);
        }
    }
    isThisA3Way = false;
    top2finaleAS = false;
    episodeChallenges.push("Finale");
    screen.createButton("Proceed", "contestantProgress()");
}
function finaleAS() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The grand finale!");
    for (let i = 0; i < currentCast.length; i++)
        screen.createImage(currentCast[i].image);
    //sort queens by finale score:
    for (let i = 0; i < currentCast.length; i++) {
        currentCast[i].getFinale();
    }
    currentCast.sort((a, b) => (b.finaleScore - a.finaleScore));
    screen.createParagraph("Our Top 4 will create verses and choreography for a new original song!");
    screen.createButton("Proceed", "runway()", "button2");
}
let top2finaleAS = false;
function finaleASJudging() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The final minutes...");
    screen.createBold("Ladies, it's time to decide The Next Drag Superstar, and...");
    if (randomNumber(0, 100) <= 90) {
        screen.createImage(currentCast[3].image, "sienna");
        screen.createBold(currentCast[3].getName() + ", I'm sorry my dear but it's not your time. I must ask you to sashay away...");
        currentCast[3].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[3]);
        currentCast.splice(3, 1);
        screen.createHorizontalLine();
        for (let i = 0; i < currentCast.length; i++)
            screen.createImage(currentCast[i].image, "silver");
        screen.createBold(currentCast[0].getName() + ", " + currentCast[1].getName() + ", " + currentCast[2].getName() + ", this is your last chance to prove yourself. It's time for you to lipsync.. for the CROWN!!");
        lsSong();
    } else {
        screen.createImage(currentCast[2].image, "sienna");
        screen.createImage(currentCast[3].image, "sienna");
        screen.createBold(currentCast[2].getName() + ", " + currentCast[3].getName() + ", I'm sorry my dears but it's not your time. I must ask you both to sashay away...");
        currentCast[2].addToTrackRecord("ELIMINATED");
        currentCast[3].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[3]);
        eliminatedCast.unshift(currentCast[2]);
        currentCast.splice(2, 2);
        for (let i = 0; i < currentCast.length; i++)
            screen.createImage(currentCast[i].image, "silver");
        screen.createBold(currentCast[0].getName() + ", " + currentCast[1].getName() + ", this is your last chance to prove yourself. It's time for you to lipsync.. for the CROWN!!");
        lsSong();
        top2finaleAS = true;
    }
    screen.createButton("Proceed", "finaleFinale()");
}
function finaleJuryAS() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("The jury!");
    screen.createParagraph("The eliminated queens are coming back, back, back again!");
    screen.createHorizontalLine();
    let voting = [];
    for (let i = 0; i < currentCast.length; i++){
        screen.createImage(currentCast[i].image);
        currentCast[i].votes = 0;
    }
    screen.createBold("After the Top 4 All Stars had their meetings with the eliminated queens... The eliminated queens vote!!");
    for (let i = 0; i < eliminatedCast.length; i++) {
        voting = [...currentCast];
        eliminatedCast[i].lipstick = voting[randomNumber(0, voting.length - 1)];
        eliminatedCast[i].lipstick.votes += 2;
        voting.splice(voting.indexOf(eliminatedCast[i].lipstick), 1);
        screen.createImage(eliminatedCast[i].image , "black");
        screen.createImage(eliminatedCast[i].lipstick.image , "yellow");
        screen.createParagraph(`${eliminatedCast[i].getName()} voted for ${eliminatedCast[i].lipstick.getName()}! As their first option.`);
        eliminatedCast[i].lipstick = voting[randomNumber(0, voting.length - 1)];
        eliminatedCast[i].lipstick.votes += 1;
        screen.createImage(eliminatedCast[i].image , "black");
        screen.createImage(eliminatedCast[i].lipstick.image , "silver");
        screen.createParagraph(`${eliminatedCast[i].getName()} voted for ${eliminatedCast[i].lipstick.getName()}! As their second option.`);
    }
    screen.createHorizontalLine();
    screen.createBold("The results are in..!!");
    for (let i = 0; i < currentCast.length; i++) {
        screen.createBold(`${currentCast[i].getName()}: ${currentCast[i].votes.toString()} points`);
    }
    screen.createHorizontalLine();
    let queen = currentCast.sort((a, b) => b.votes - a.votes)[0];
    let queen1 = currentCast.sort((a, b) => b.votes - a.votes)[1];
    if (currentCast[1].votes == currentCast[2].votes) {
        screen.createBold("It is a tie, the queens must revote between " + currentCast[1].getName() + " and " + currentCast[2].getName() + "!!");
        let ogvote = currentCast[1].votes;
        currentCast[1].votes = 0;
        currentCast[2].votes = 0;
        for (let i = 0; i < eliminatedCast.length; i++) {
            voting = [currentCast[1], currentCast[2]];
            eliminatedCast[i].lipstick = voting[randomNumber(0, voting.length - 1)];
            eliminatedCast[i].lipstick.votes += 1;
            screen.createImage(eliminatedCast[i].image , "black");
            screen.createImage(eliminatedCast[i].lipstick.image , "yellow");
            screen.createParagraph(`${eliminatedCast[i].getName()} voted for ${eliminatedCast[i].lipstick.getName()}! to be in the finale!`);
        }
        screen.createHorizontalLine();
        screen.createBold("The results are in..!");
        for (let i = 0; i < voting.length; i++) {
            screen.createBold(`${voting[i].getName()}: ${voting[i].votes.toString()} points`);
        }
        let tiebreaker = voting.sort((a, b) => b.votes - a.votes)[0];
        screen.createBold(`${tiebreaker.getName()} moves into the finale!!`);
        tiebreaker.votes = ogvote;
        voting[1] = ogvote;
        queen1 = tiebreaker;
    }
    screen.createBold(`${queen.getName()} and ${queen1.getName()} are the Top 2 of the season!!`);
    if (queen1 == currentCast[1]) {
        currentCast[2].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[2]);
        currentCast[3].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[3]);
        currentCast.splice(2, 2);
    } else {
        currentCast[1].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[1]);
        currentCast[3].addToTrackRecord("ELIMINATED");
        eliminatedCast.unshift(currentCast[3]);
        currentCast.splice(1, 3);
        currentCast.push(queen1);
    }
    currentCast.sort((a, b) => (b.finaleScore - a.finaleScore));
    screen.createButton("Proceed", "finaleFinale()");
}
function canadaS2Finale() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("Our Top 4 is about to become a Top 3...");
    screen.createImage(currentCast[0].image, "royalblue");
    screen.createImage(currentCast[1].image, "royalblue");
    screen.createImage(currentCast[2].image, "royalblue");
    screen.createImage(currentCast[3].image, "royalblue");
    screen.createBold(currentCast[0].getName() + ", " + currentCast[1].getName() + ", " + currentCast[2].getName() + ", " + currentCast[3].getName() + ", you will all be competing in a lipsync batte royale!!");
    screen.createHorizontalLine();
    for (let i = 0; i < 2; i++) {
        let q1 = currentCast[randomNumber(0, currentCast.length - 1)];
        firstLS.push(q1);
        currentCast.splice(currentCast.indexOf(q1), 1);
        let q2 = currentCast[randomNumber(0, currentCast.length - 1)];
        secondLS.push(q2);
        currentCast.splice(currentCast.indexOf(q2), 1);
    }
    screen.createBigText("The lipsyncs will be: ");
    screen.createImage(firstLS[0].image, "darkblue");
    screen.createImage(firstLS[1].image, "darkblue");
    screen.createBold(firstLS[0].getName() + " vs. " + firstLS[1].getName());
    screen.createParagraph("and");
    screen.createImage(secondLS[0].image, "darkred");
    screen.createImage(secondLS[1].image, "darkred");
    screen.createBold(secondLS[0].getName() + " vs. " + secondLS[1].getName());
    episodeChallenges.push("Lipsync For The Finale");
    screen.createButton("Proceed", "canadaS2LipSyncs()");
}
function canadaS2LipSyncs() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("Let the battle begin!!");
    screen.createBold(firstLS[0].getName() + " and " + firstLS[1].getName() + " will lip-sync for the finale...!");
    lsSong();
    for (let i = 0; i < firstLS.length; i++) {
        firstLS[i].getLipsync();
    }
    firstLS.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    finalLS.push(firstLS[1]);
    firstLS[0].addToTrackRecord("TOP 3<br><small>Win round 1</small>");
    screen.createImage(firstLS[0].image, "silver");
    screen.createBold(firstLS[0].getName() + ", shantay you stay. We will see you at the finale!!");
    currentCast.unshift(firstLS[0]);
    screen.createImage(firstLS[1].image, "sienna");
    screen.createBold(firstLS[1].getName() + ", you will have one more chance to redeem yourself...");
    screen.createHorizontalLine();
    screen.createParagraph(secondLS[0].getName() + " and " + secondLS[1].getName() + " lip-sync...");
    lsSong();
    for (let i = 0; i < secondLS.length; i++) {
        secondLS[i].getASLipsync();
    }
    secondLS.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    finalLS.push(secondLS[1]);
    secondLS[0].addToTrackRecord("TOP 3<br><small>Win round 2</small>");
    screen.createImage(secondLS[0].image, "silver");
    screen.createBold(secondLS[0].getName() + ", shantay you stay. We will see you at the finale!!");
    currentCast.unshift(secondLS[0]);
    screen.createImage(secondLS[1].image, "sienna");
    screen.createBold(secondLS[1].getName() + ", you will have one more chance to redeem yourself...");
    screen.createHorizontalLine();
    screen.createParagraph(finalLS[0].getName() + " and " + finalLS[1].getName() + " lip-sync...");
    lsSong();
    for (let i = 0; i < finalLS.length; i++) {
        finalLS[i].getASLipsync();
    }
    finalLS.sort((a, b) => (b.lipsyncScore - a.lipsyncScore));
    if (finalLS[1].chocolate) {
        if (chocolateBarTwist  && !chocolateBarTwistCheck) {
            finalLS[1].addToTrackRecord("TOP 3<br><small>Win round 3</small>");
            screen.createImage(finalLS[1].image, "silver");
            screen.createBold(finalLS[1].getName() + ", shantay you stay. We will see you at the finale!!");
            currentCast.unshift(finalLS[1]);
            screen.createBold(finalLS[0].getName() + ", now your fate rests in the hands of the drag gods.");
            screen.createBold("If you have the golden chocolate bar, you will be safe.");
            screen.createImage("image/ChocolateBarWithNoTicket.webp", "brown");
            screen.createBold("It's chocolate.");
            screen.createBold(finalLS[0].getName() + ", sashay away...");
            finalLS[0].addToTrackRecord("ELIM");
            finalLS[0].unfavoritism += 5;
            eliminatedCast.unshift(finalLS[0]);
        } else {
            finalLS[1].addToTrackRecord("TOP 3<br><small>Win round 3</small>");
            screen.createImage(finalLS[1].image, "silver");
            screen.createBold(finalLS[1].getName() + ", shantay you stay. We will see you at the finale!!");
            currentCast.unshift(finalLS[1]);
            eliminatedCast.unshift(finalLS[0]);
            screen.createImage(finalLS[0].image, "sienna");
            screen.createBold(finalLS[0].getName() + ", sashay away...");
            finalLS[0].addToTrackRecord("ELIM");
        }
    } else {
        if (chocolateBarTwist  && !chocolateBarTwistCheck) {
            finalLS[0].addToTrackRecord("TOP 3<br><small>Win round 3</small>");
            screen.createImage(finalLS[0].image, "silver");
            screen.createBold(finalLS[0].getName() + ", shantay you stay. We will see you at the finale!!");
            currentCast.unshift(finalLS[0]);
            screen.createBold(finalLS[1].getName() + ", now your fate rests in the hands of the drag gods.");
            screen.createBold("If you have the golden chocolate bar, you will be safe.");
            screen.createImage("image/ChocolateBarWithNoTicket.webp", "brown");
            screen.createBold("It's chocolate.");
            eliminatedCast.unshift(finalLS[1]);
            screen.createImage(finalLS[1].image, "sienna");
            screen.createBold(finalLS[1].getName() + ", sashay away...");
            finalLS[1].addToTrackRecord("ELIM");
        } else {
        finalLS[0].addToTrackRecord("TOP 3<br><small>Win round 3</small>");
        screen.createImage(finalLS[0].image, "silver");
        screen.createBold(finalLS[0].getName() + ", shantay you stay. We will see you at the finale!!");
        currentCast.unshift(finalLS[0]);
        eliminatedCast.unshift(finalLS[1]);
        screen.createImage(finalLS[1].image, "sienna");
        screen.createBold(finalLS[1].getName() + ", sashay away...");
        finalLS[1].addToTrackRecord("ELIM");
        }
    }
    episodeCount++;
    for (let i = 0; i < eliminatedCast.length; i++)
        eliminatedCast[i].addToTrackRecord('');
    screen.createButton("Proceed", "finale()");
}
function contestantProgress() {
    let screen = new Scene();
    screen.clean();
    screen.createHeader("Contestant Progress");
    document.body.style.backgroundImage = "url('image/bg.png')";
    let main = document.querySelector("div#MainBlock");
    let centering = document.createElement("center");
    let trackRecords = document.createElement("table");
    trackRecords.setAttribute("id", "trackRecord");
    if (totalCastSize >= 12 && totalCastSize < 15)
        trackRecords.setAttribute("style", "font-size: 85%;");
    if (totalCastSize >= 15)
        trackRecords.setAttribute("style", "font-size: 75%");
    let header = document.createElement("tr");
    trackRecords.appendChild(header);
    let th = document.createElement("th");
    th.innerHTML = "Queen";
    th.setAttribute("style", "background-color: #e9dfe9; font-weight: bold; width: 170px;");
    header.appendChild(th);
    let th_i = document.createElement("th");
    th_i.innerHTML = "Photo";
    th_i.setAttribute("style", "background-color: #e9dfe9; font-weight: bold; width: 60px;");
    header.appendChild(th_i);
    for (let i = 0; i < episodeChallenges.length; i++) {
        let th = document.createElement("th");
        th.innerHTML = episodeChallenges[i];
        th.setAttribute("style", "background-color: #e9dfe9; font-weight: bold; width: 75px;");
        header.appendChild(th);
    }
    let th_2 = document.createElement("th");
    th_2.innerHTML = "PPE";
    th_2.setAttribute("style", "background-color: #e9dfe9; font-weight: bold; width: 35px;");
    header.appendChild(th_2);
    let winner = document.createElement("tr");
    let name = document.createElement("td");
    name.setAttribute("style", "background-color: #f5ebf5; font-weight: bold; height: 50px;");
    if (onFinale) {
        let winnerQueen;
        if (!top4) {
            if (ukvstwFinale){
                winnerQueen = finalLS[0];
            }else{
                winnerQueen = currentCast[0];
            }
        }
        else if (onTop4Finale)
            winnerQueen = finalLS[0];
        else
            winnerQueen = currentCast[0];
        name.innerHTML = winnerQueen.getName();
        winner.appendChild(name);
        let photo = document.createElement("td");
        photo.setAttribute("style", "background: url("+ winnerQueen.image +"); background-size: 106px 106px; background-position: center;");
        winner.appendChild(photo);
        for (let i = 0; i < winnerQueen.trackRecord.length + 1; i++) {
            let placement = document.createElement("td");
            placement.innerHTML = winnerQueen.trackRecord[i];
            if (placement.innerHTML == "WIN") {
                placement.setAttribute("style", "font-weight: bold; background-color: royalblue; color: white;");
            }
            else if (placement.innerHTML == "TOP2") {
                placement.setAttribute("style", "background-color: deepskyblue;");
            }
            else if (placement.innerHTML == "TOP 3<br><small>Win round 1</small>") {
                placement.setAttribute("style", "font-weight: bold; background-color: #ffd100; color: #000;");
            }
            else if (placement.innerHTML == "TOP 3<br><small>Win round 2</small>") {
                placement.setAttribute("style", "font-weight: bold; background-color: #ffae00; color: #000;");
            }
            else if (placement.innerHTML == "TOP 3<br><small>Win round 3</small>") {
                placement.setAttribute("style", "font-weight: bold; background-color: #ff7c00; color: #000;");
            }
            else if (placement.innerHTML == "LOW") {
                placement.setAttribute("style", "background-color: pink;");
            }
            else if (placement.innerHTML == "HIGH") {
                placement.setAttribute("style", "background-color: lightblue;");
            }
            else if (placement.innerHTML == "HIGH TEAM") {
                placement.setAttribute("style", "background-color: aquamarine;");
            }
            else if (placement.innerHTML == "BTM2 ") {
                placement.setAttribute("style", "background-color: #FA8072;");
            }
            else if (placement.innerHTML == "BTM2" || placement.innerHTML == "BTM3" || placement.innerHTML == "BTM4" || placement.innerHTML == "BTM5" || placement.innerHTML == "BTM6" || placement.innerHTML == "BTM") {
                placement.setAttribute("style", "background-color: tomato;");
            }
            else if (placement.innerHTML == " BTM2") {
                placement.setAttribute("style", "background-color: hotpink;");
            }
            else if (placement.innerHTML == "CHOC") {
                placement.setAttribute("style", "font-weight: bold; background-color: #fcea7c;");
            }
            else if (placement.innerHTML == "ELIM") {
                placement.setAttribute("style", "font-weight: bold; background-color: red;");
            }
            else if (placement.innerHTML == "ELIM ") {
                placement.setAttribute("style", "font-weight: bold; background-color: #FC4545;");
            }
            else if (placement.innerHTML == " ELIM") {
                placement.setAttribute("style", "font-weight: bold; background-color: deeppink;");
            }
            else if (placement.innerHTML == " ELIM ") {
                placement.setAttribute("style", "font-weight: bold; background-color: darkred; color:white");
            }
            else if (placement.innerHTML == "WINNER") {
                placement.setAttribute("style", "font-weight: bold; background-color: yellow;");
                if (allstars3Finale)
                    placement.innerHTML += " <br><small> (" + winnerQueen.votes + " points) </small>";
            }
            else if (placement.innerHTML == "RUNNER UP") {
                placement.setAttribute("style", "font-weight: bold; background-color: silver;");
            }
            else if (placement.innerHTML == "ELIMINATED") {
                placement.setAttribute("style", "font-weight: bold; background-color: sienna;");
            }
            else if (placement.innerHTML == "LOST 1ST ROUND") {
                placement.setAttribute("style", "font-weight: bold; background-color: #FF7C00;");
            }
            else if (placement.innerHTML == "LOST 2ND ROUND") {
                placement.setAttribute("style", "font-weight: bold; background-color: #FFAE00;");
            }
            else if (placement.innerHTML == "LOST 3RD ROUND") {
                placement.setAttribute("style", "font-weight: bold; background-color: #FFD100;");
            }
            else if (placement.innerHTML == "") {
                placement.setAttribute("style", "background-color: gray");
            }
            else if (placement.innerHTML == "WIN ") {
                placement.setAttribute("style", "font-weight: bold; background-color: deepskyblue;");
            }
            else if (placement.innerHTML == "  WIN") {
                placement.setAttribute("style", "font-weight: bold; background-color: #2238B4; color: white;");
            }
            else if (placement.innerHTML == "WIN+RTRN") {
                placement.setAttribute("style", "font-weight: bold; background-color: forestgreen; color: white;");
            }
            else if (placement.innerHTML == "SAFE") {
                placement.setAttribute("style", "background-color: white;");
            }
            else if (placement.innerHTML == "SAFE ") {
                    placement.setAttribute("style", "background-color: palegreen; color:#000;");
            }
            else if (placement.innerHTML == " SAFE ") {
                    placement.setAttribute("style", "background-color: #7D1935; color:#000;");
            }
            else if (placement.innerHTML == " SAFE") {
                placement.setAttribute("style", "background-color: magenta; color:white;");
            }
            else if (placement.innerHTML == "SAFE<br><small>Round 1</small>") {
                placement.setAttribute("style", "background-color: lightcoral; color: white;");
            }
            else if (placement.innerHTML == "SAFE<br><small>Round 2</small>") {
                placement.setAttribute("style", "background-color: indianred; color: white;");
            }
            else if (placement.innerHTML == "SAFE<br><small>Round 3</small>") {
                placement.setAttribute("style", "background-color: crimson; color: white;");
            }
            else if (placement.innerHTML == "RUN") {
                    placement.setAttribute("style", "background-color: magenta; color:white;");
            }
            else if (placement.innerHTML == "RUN ") {
                    placement.setAttribute("style", "background-color: #D3FFB5; color:#000; font-weight: bold;");
            }
            else if (placement.innerHTML == "OUT") {
                placement.setAttribute("style", "background-color: forestgreen; color:white;");
            }
            else if (placement.innerHTML == "OUT ") {
                    placement.setAttribute("style", "background-color: purple; color:white;");
            }
            else if (placement.innerHTML == " WIN") {
                placement.setAttribute("style", "font-weight: bold; background-color: darkblue; color: white;");
            }
            else if (placement.innerHTML == "DISQ") {
                placement.setAttribute("style", "font-weight: bold; background-color: black; color: white;");
            }
            else if (placement.innerHTML == "DEPT") {
                placement.setAttribute("style", "font-weight: bold; background-color: plum;");
            }
            else if (placement.innerHTML == "QUIT") {
                placement.setAttribute("style", "font-weight: bold; background-color: palevioletred;");
            }
            else if (placement.innerHTML == "WIN+QUIT") {
                placement.setAttribute("style", "font-weight: bold; background-color:#5920d4;");
            }
            else if (placement.innerHTML == "RTRN") {
                placement.setAttribute("style", "font-weight: bold; background-color: magenta;");
            }
            else if (placement.innerHTML == "RTRN ") {
                placement.setAttribute("style", "font-weight: bold; background-color: orange;");
            }
            else if (placement.innerHTML == " WIN ") {
                placement.setAttribute("style", "background-color: lightskyblue;");
            }
            else if (placement.innerHTML == "LOSS") {
                placement.setAttribute("style", "background-color: #ff9e9e;");
            }
            else if (placement.innerHTML == "LOSS ") {
                placement.setAttribute("style", "background-color: orange;");
            }
            else if (placement.innerHTML == "undefined") {
                placement.setAttribute("style", "font-weight: bold; background-color: lightgray;");
                placement.innerHTML = (winnerQueen.ppe / (winnerQueen.episodesOn)).toFixed(2);
            }
            winner.appendChild(placement);
        }
        trackRecords.appendChild(winner);
    }
    if (!onFinale) {
        for (let i = 0; i < currentCast.length; i++) {
            let contestant = document.createElement("tr");
            let name = document.createElement("td");
            name.setAttribute("style", "font-weight: bold;");
            name.innerHTML = currentCast[i].getName();
            name.setAttribute("style", "background-color: #f5ebf5; font-weight: bold; height: 50px;");
            contestant.appendChild(name);
            let photo = document.createElement("td");
            photo.setAttribute("style", "background: url("+ currentCast[i].image +"); background-size: 106px 106px; background-position: center;");
            contestant.appendChild(photo);
            for (let k = 0; k < currentCast[i].trackRecord.length + 1; k++) {
                let placement = document.createElement("td");
                placement.innerHTML = currentCast[i].trackRecord[k];
                if (placement.innerHTML == "WIN") {
                    placement.setAttribute("style", "font-weight: bold; background-color: royalblue; color: white;");
                }
                else if (placement.innerHTML == "TOP2") {
                    placement.setAttribute("style", "background-color: deepskyblue;");
                }
                else if (placement.innerHTML == "TOP 3<br><small>Win round 1</small>") {
                    placement.setAttribute("style", "font-weight: bold; background-color: #ffd100; color: #000;");
                }
                else if (placement.innerHTML == "TOP 3<br><small>Win round 2</small>") {
                    placement.setAttribute("style", "font-weight: bold; background-color: #ffae00; color: #000;");
                }
                else if (placement.innerHTML == "TOP 3<br><small>Win round 3</small>") {
                    placement.setAttribute("style", "font-weight: bold; background-color: #ff7c00; color: #000;");
                }
                else if (placement.innerHTML == "LOW") {
                    placement.setAttribute("style", "background-color: pink;
