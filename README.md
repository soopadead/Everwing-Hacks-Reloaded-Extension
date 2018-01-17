# Everwing-Hacks
Hacks for the everwing game.

These codes are for people that understund some programing.

The security of the today systems should be strong. We as users demand that the systems we use should be secure to protect our data. For educational reasons we try to see, how easy it is to change the system's data (like in this example Everwing Game's data). When a game is so unsecure, it makes a player's ingame achivements and items useless.

We use these cheat codes as an example of how a supposed well crafted game like Everwing, with fancy sprites and game modes, has no security at all. By using this cheats your account may be banned.

## Use our extension
You can easily run the hack codes by installing our extension
https://dinodevs.github.io/Everwing-Hacks/

## Apply the hacks
To apply the hacks you have to open the developer console of your browser.

Detailed guide with photos [here](docs/guide.md).

To do that:
 - Click F12 on the everwing game page (or, right click the page and select "inspect element")
    - This will open the developer's tools on most major browsers. From here web developers tests and debug the web aplications they create. If your browser don't have dev tools, you can use firebug (https://getfirebug.com/)
 - Click the "Console" tab if you are not already there
    - The console tab is a javascript console. Here, we can write javascript code and run it on the active page.
 - Click the down arrow next to the "top"
 - On the drop down, sellect "index.html" (it should be on the bottom)
    - This will set the active javascript window to the game window, so that the code we run will run on the game window and not on the messenger window.

## Hack Codes
Now paste any of the codes bollow to hack the game.

### Unlock All Players
```javascript
var names = ["fiona", "sophia", "coin", "magnet", "lenore", "jade", "arcana", "lyra", "trixie"];
for (var i = 0; i < names.length; i++) {
	if(GC.app.mvc.models.CharactersModel.characters[names[i]].state == "locked")
		GC.app.client.runFunction("purchaseCharacter", { characterID: names[i], isFree: true });
}
```

### Maximize All Players' Levels
```javascript
var names = ["fiona", "sophia", "coin", "magnet", "lenore", "jade", "arcana", "lyra", "trixie"];
var level = 1;
var maxlevel = 50;
var state = null;
for (var i = 0; i < names.length; i++) {
	if(GC.app.mvc.models.CharactersModel.characters[names[i]].state == "locked")
    		GC.app.client.runFunction("purchaseCharacter", { characterID: names[i], isFree: true });
	level = GC.app.mvc.models.CharactersModel.characters[names[i]].level;
	maxlevel = GC.app.mvc.models.CharactersModel.characters[names[i]].maxLevel;
	state = GC.app.mvc.models.CharactersModel.characters[names[i]].state;
	console.log("Level : " + level + " Max Level : " + maxlevel + " state : " + state);
	if(state == "idle" || state == "equiped") {
		if(state == "idle") {
			GC.app.client.runFunction("equipCharacter", {characterName : names[i]});
			console.log("equiping : " + names[i]);
		}
		for (x = level; x < maxlevel; x++) {
			console.log("upgrading : " + names[i] + " x : " + x);
			GC.app.client.runFunction("purchaseCharacterUpgrade", {characterID : names[i], isFree : true});
		}
	}
}
```

### Get a sidekick

Get a random sidekick
```javascript
var gacha = GC.app.client.schemaAPI.getTable("gachaConfig").rows;
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : gacha[Math.floor(Math.random() * gacha.length)].type});
```

Get a random event sidekick
```javascript
var events = GC.app.client.schemaAPI.getTable("sidekicksEvents").rows;
var sidekickEvents = [];
for(var i = events.length - 1; i>=0; i--){
	if (events[i].sidekicks) sidekickEvents.push(events[i].name);
}
if(sidekickEvents.length > 0){
	GC.app.client.runFunction("sidekickEventGacha", {eventID : sidekickEvents[Math.floor(Math.random() * sidekickEvents.length)]});
}
else{console.log("No events.");}
```

Get a smart sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "smart"});
```

Get a common sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "common"});
```

Get a bronze sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "bronze"});
```

Get a silver sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "silver"});
```

Get a gold sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "gold"});
```

Get a magical sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "magical"});
```

Get a legendary sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "legendary"});
```
Get a mythic sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "mythic"});
```

Get a bossraid sidekick
```javascript
GC.app.client.runFunction("sidekickGacha", {isFree : true, gachaType : "bossraid"});
```

### Fake a game run

First apply this function
```javascript
var playFakeGame = function(data) {
	// Fake game data
	var data = data || {};
	data.score = data.score || 10 + Math.round(Math.random()*10);
	data.seconds = data.seconds || 10 + Math.round(Math.random()*10);
	data.coins = data.coins || 0;
	data.trophies = data.trophies || 0;
	data.energy = data.energy || 0;
	data.xp = data.xp || 0;
	data.sidekick_xp = data.sidekick_xp || 0;
	// Get sidekicks
	var sidekicks = {};
	var sidekicks_db = window.GC.app.gameView.sidekicksModel.sidekicksList;
	for(var i=0; i<sidekicks_db.length; i++){
		if(sidekicks_db[i].state == "equippedLeft"){sidekicks.left = sidekicks_db[i];}
		else if(sidekicks_db[i].state == "equippedRight"){sidekicks.right = sidekicks_db[i];}
	}
	// App reference
	var app = window.GC.app;
	// Send command
	app.mvc.commandMap.GamePlayedCommand.prototype.execute.apply({mvc :app.mvc,finishCommand : function(e, $){}},
	[{
		playerID : app.gameModel.player.id,
		secondsElapsed : data.seconds,
		killedBy : "Meteor SINGLE " + (Math.round(Math.random()*3) + 1),
		background : "ocean",
		score : data.score,
		commonEarned : data.coins,
		premiumEarned : data.trophies,
		energyEarned : data.energy,
		playerXP : data.xp,
		sidekickXP : data.sidekick_xp,
		sidekickLeftID : (sidekicks.left) ? sidekicks.left.id : null,
		sidekickRightID : (sidekicks.right) ? sidekicks.right.id : null,
	}]);
}
```

Then call it with the amount of resources you need.

Get 15.000 coints
```javascript
playFakeGame({coins : 15000});
```
Get 1.500 trophies
```javascript
playFakeGame({trophies : 1500});
```
Get 9.999 player XP points
```javascript
playFakeGame({xp : 9999});
```
Get 9.999 sideckick XP points
```javascript
playFakeGame({sidekick_xp : 9999});
```

There are limits on the resources you can get, for example you can't get 999.999 coins with 1 fake game.
