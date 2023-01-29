# GameJolt FNF Integration



### Scrivi questo nel terminale (..cmd/!)
``` cmd
haxelib git tentools https://github.com/TentaRJ/tentools.git
haxelib git systools https://github.com/haya3218/systools
haxelib run lime rebuild systools [windows, mac, linux]
```

se devi rilasciare il codice sorgente della mod con quest'integrazione, devi aggiungere queste cose nel 'Project.xml'.
### Metti questo in `Project.xml`:
```xml
<haxelib name="tentools" />
<haxelib name="systools" />
<ndll name="systools" haxelib="systools" />
```

### Dopo che lo hai fatto, puoi inserire il file `GameJolt.hx` nella cartella `source/` del tuo progetto!

# SETUP (GAMEJOLT):

Assicurati che aggiungi `import GameJolt;` all'inizio di `Main.hx`!

Per aggiungere i game's keys, hai bisogno di creare un file chiamato "GJKeys.hx" (posizione[della cartella]: ../source/GJKeys.hx).
<br>
In questo file, hai bisgno di aggiungere i GJKeys class con due variabili statiche, `id:Int` and `key:String`.

### PER CHI NON SA DOVE
L'ID e le API Key si trovano nella pagina GameJolt della tua MOD.
*To find your private key go to Dashboard -> Your Games -> YOUR GAME HERE -> Game API -> API Settings -> Private Key. Then Click "Show key".*

### `source/GJKeys.hx` esempio:
```hx
package;
class GJKeys
{
    public static var id:Int = 	0; // Put your game's ID here
    public static var key:String = ""; // Put your game's private API key here
}
```
### NON RENDERE PUBBLICI I TUOI ID E API KEY DEL GIOCO, PERCHE' CHIUNQUE POTREBBE MANDARE FALSE INFORMAZIONI!!!

# SETUP (TOASTS):

## **Thank you Firubii for the code for this! Please go check them out!**
**https://twitter.com/firubiii / https://github.com/firubii**

To setup toasts, you will need to do a few things.

Inside the Main class (Main.hx), you need to make a new variable called toastManager.

`Main.hx`
```haxe
public static var gjToastManager:GJToastManager;
```

Inside the setupGame function in the Main class, you will need to create the toastManager.
```haxe
gjToastManager = new GJToastManager();
addChild(gjToastManager);
```

TYSM Firubii for your help!

# USAGE:

## Make sure to put `import GameJolt.GameJoltAPI;` at the top of the file if you want to call a command!

```hx
import GameJolt.GameJoltAPI;
```

## These commands **must** be ran before starting the API. Place these in `TitleState.hx`:

```hx
GameJoltAPI.connect();
GameJoltAPI.authDaUser(FlxG.save.data.gjUser, FlxG.save.data.gjToken);
```

### Username and Token are grabbed from the default `FlxG.save` file. This file can be changed in `TitleState.hx`.

### Exiting the login menu will throw you back to Main Menu State. You can change this in the GameJoltLogin class inside GameJolt.hx.

### The session will automatically start on login and will be pinged every 30 seconds. If it isn't pinged within 120 seconds, the session automatically ends from GameJolt's side.

### You can open the login state by calling the GameJoltLogin state:
```hx
FlxG.switchState(new GameJoltLogin());
```

# PSYCH ENGINE SUPPORT STEP's

### 1.Install Tentools, Systools and rebuild systools
### 2.Setup GameJolt
### 3.Put the thing's on ```Main.hx``` and ```TitleState.hx```

### PS: You should have internet connection for login, just that

# CHANGABLE VARIABLES:

`GameJoltInfo.changeState:FlxUIState`
> The state you will call back to after hitting ESCAPE or CONTINUE

`GameJoltInfo.font:String`
> The font used in GameJoltLogin

`GameJoltInfo.fontPath:String`
> The font path used for the notifications

`GameJoltInfo.imagePath:String`
> The file path for the image in the notifications.

# COMMANDS AVAILABLE:

`GameJoltAPI.getStatus():Bool`
> Checking to see if the user has signed in. Returns a `bool` value. `true` if signed in, `false` if not signed in.

`GameJoltAPI.getuserInfo(username):String`
> Grabs the username and usertoken of the user and returns a `String`.<br>
> `username:Bool = true` -> `true` to grab username, `false` to grab usertoken.

`GameJoltAPI.getTrophy(trophyID);`
> `TrophyID:Int` -> ID of the trophy you want the player to earn.

`GameJoltAPI.checkTrophy(trophyID);`
> Returns a `bool` value of the achieved status. `True` for achieved, `false` for not achieved.<br>
> `TrophyID:Int` -> ID of the trophy you want to check.

`GameJoltAPI.pullTrophy(trophyID);`
> Returns a `Map<String,String>` of the trophy called for.<br>
> `TrophyID:Int` -> ID of the trophy you want to pull.

`GameJoltAPI.addScore(score:Int, tableID:Int, ?extraData:String);`
> Adds a score to a table on GameJolt.<br>
> `score:Int` -> The score to add. Will also count as the sorting value.<br>
> `tableID:Int` -> ID of the table.<br>
> `extraData:String` -> Exta data you want to add. Could be accuracy, who knows.

`GameJoltAPI.pullHighScore(tableID:Int)`
> Pulls the data from the highest score on the table. Will return a `Map<String,String>` value.<br>
> `tableID:Int` -> ID of the table.<br>
> Values returned -> `score, sort, user_id, user, extra_data, stored, guest, success`

# CREDITS:

- <a href = "https://github.com/brightfyregit">BrightFyre</a> - Testing and UI design
- <a href ="https://github.com/haya3218">Haya</a> - Systools fork
- <a href = "https://github.com/firubii">Firubii</a> - Toast system
