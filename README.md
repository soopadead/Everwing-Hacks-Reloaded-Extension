https://dinodevs.github.io/Everwing-Hacks/

•
[[Get for Chromium]](https://github.com/DinoDevs/Everwing-Hacks/releases/download/v2.1.6/EverWingHacks.v2.1.6.crx)
•
[[Get for Firefox]](https://github.com/DinoDevs/Everwing-Hacks/releases/download/v2.1.6/EverWingHacks.v2.1.6.xpi)
•
[[Get for Opera]](https://github.com/DinoDevs/Everwing-Hacks/releases/download/v2.1.6/EverWingHacks.v2.1.6.nex)
•

(Not currently availiable on chrome store [issue here](../../issues/26))

# Everwing-Hacks
### Everwing finally patched most of the holes.

These codes were for people that understund some programing.

The security of the today systems should be strong. We as users demand that the systems we use should be secure to protect our data. For educational reasons we try to see, how easy it is to change the system's data (like in this example Everwing Game's data). When a game is so unsecure, it makes a player's ingame achivements and items useless.

We use these cheat codes as an example of how a supposed well crafted game like Everwing, with fancy sprites and game modes, has no security at all. By using this cheats your account may be banned.

## Use our extension
You can easily run the hack codes by installing our extension
https://dinodevs.github.io/Everwing-Hacks/

## Hack Codes

### Fake a game run

First apply this function
```javascript
var playFakeGame = function(d) {
	// Fake game data
	if (!d) return;
	var data = {};
	data.coinsEarned = d.coins || 0;
	data.eggTypeFound = d.egg || ""; // Dont play with this
	data.energyEarned = d.energy || 0;
	data.score = d.score || 0;
	data.sidekick1Key = "";
	data.sidekick2Key = "";
	data.xpEarned = d.xp || 0;
	var time = d.seconds * 1000 || 12000;
	d.times = d.times || 1;
	// Get sidekicks
	var sidekicks = window.GC.app.gameView.sidekicksModel.sidekicksList;
	for(var i=0; i<sidekicks.length; i++){
		if(sidekicks[i].state == "equippedLeft"){data.sidekick1Key = sidekicks[i].id;}
		else if(sidekicks[i].state == "equippedRight"){data.sidekick2Key = sidekicks[i].id;}
	}
	// Check eg type
	if (data.eggTypeFound.length > 0) {
		try{window.GC.app.mvc.models.ServerModel.client.schemaAPI.getTable("eggSlotConfig").getRow('common')}
		catch(e){console.log('Invalid egg type.');return;}
	}
	// Check if already running
	if (window.fakeGameIsRunning) {
		console.log('A fake game is already running.');
		return;
	}
	window.fakeGameIsRunning = true;
	// Start fake game
	window.GC.app.client.runFunction('gameStart', {});
	window.GC.app.mvc.sendNotification("RootDialogViewController.showSpinner");
	// Wait some time and send game end command
	setTimeout(function(){
		window.GC.app.mvc.sendNotification("RootDialogViewController.hideSpinner");
		window.GC.app.client.runFunction('gameComplete', data);
		window.fakeGameIsRunning = false;
		d.times --;
		if (d.times > 0) setTimeout(function(){playFakeGame(d);}, 0);
	}, time);
}
```

Then call it with the amount of resources you need. The more the resources you add the more time you should let the fake game run.

Get 500 coins (12 seconds)
```javascript
playFakeGame({coins : 500, seconds : 12});
```
Get 1000 coins (20 seconds)
```javascript
playFakeGame({coins : 1000, seconds : 20});
```
Get 2000 coins (35 seconds)
```javascript
playFakeGame({coins : 2000, seconds : 35});
```
Get 1 energy (12 seconds)
```javascript
playFakeGame({energy : 1, seconds : 12});
```
Get 1000 XP (12 seconds)
```javascript
playFakeGame({xp : 1000, seconds : 12});
```
Get 10×1000 XP (2 minutes)
```javascript
playFakeGame({xp : 1000, seconds : 12, times: 10});
```javascript
Get Ancient egg (12 seconds)
```javacript
playFakeGame({egg : 'ancientTutorial', seconds : 12});
```
