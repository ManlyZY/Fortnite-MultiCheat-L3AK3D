# WinRar Password: kol2233

 # fortnitepy

[![Supported py versions](https://img.shields.io/pypi/pyversions/fortnitepy.svg)](https://pypi.org/project/fortnitepy/)
[![Current pypi version](https://img.shields.io/pypi/v/fortnitepy.svg)](https://pypi.org/project/fortnitepy/)
[![Donate link](https://img.shields.io/badge/paypal-donate-blue.svg)](https://www.paypal.me/terbau)

Asynchronous library for interacting with Fortnite and EpicGames' API and XMPP services.

**Note:** This library is still under developement so breaking changes might happen at any time.

**Some key features:**
- Full support for Friends.
- Support for XMPP events including friend and party messages + many more.
- Support for Parties.
- Support for Battle Royale stats.

# Documentation
https://fortnitepy.readthedocs.io/en/latest/

# Installing
```
# windows
py -3 -m pip install -U fortnitepy

# linux
python3 -m pip install -U fortnitepy
```

# Basic usage
```py
import fortnitepy
import json
import os

from fortnitepy.ext import commands

email = 'email@email.com'
password = 'password1'
filename = 'device_auths.json'

def get_device_auth_details():
    if os.path.isfile(filename):
        with open(filename, 'r') as fp:
            return json.load(fp)
    return {}

def store_device_auth_details(email, details):
    existing = get_device_auth_details()
    existing[email] = details

    with open(filename, 'w') as fp:
        json.dump(existing, fp)

device_auth_details = get_device_auth_details().get(email, {})
bot = commands.Bot(
    command_prefix='!',
    auth=fortnitepy.AdvancedAuth(
        email=email,
        password=password,
        prompt_authorization_code=True,
        prompt_code_if_invalid=True,
        delete_existing_device_auths=True,
        **device_auth_details
    )
)

@bot.event
async def event_device_auth_generate(details, email):
    store_device_auth_details(email, details)

@bot.event
async def event_ready():
    print('----------------')
    print('Bot ready as')
    print(bot.user.display_name)
    print(bot.user.id)
    print('----------------')

@bot.event
async def event_friend_request(request):
    await request.accept()

@bot.command()
async def hello(ctx):
    await ctx.send('Hello!')

bot.run()
```

# Authorization
How to get a one time authorization code:
1. Log into the epic games account of your choice [here](https://www.epicgames.com/id/logout?redirectUrl=https%3A//www.epicgames.com/id/login%3FredirectUrl%3Dhttps%253A%252F%252Fwww.epicgames.com%252Fid%252Fapi%252Fredirect%253FclientId%253D3446cd72694c4a4485d81b77adbb2141%2526responseType%253Dcode).
2. Copy the hex part from the url that shows up as showcased by the image below:

![Authorization Code](https://raw.githubusercontent.com/Terbau/fortnitepy/dev/docs/resources/images/authorization_code.png)

# Credit
Thanks to [Kysune](https://github.com/SzymonLisowiec), [iXyles](https://github.com/iXyles), [Vrekt](https://github.com/Vrekt) and [amrsatrio](https://github.com/Amrsatrio) for ideas and/or work that this library is built upon.

Also thanks to [discord.py](https://github.com/Rapptz/discord.py) for much inspiration code-wise.

# Need help?
If you need more help feel free to join this [discord server](https://discord.gg/rnk869s).

DISCLAIMER!

THIS IS OUTDATED SINCE THE BATTLE EYE LAUNCH! Feel free to reuse any code you can recycle. I would not advise to inject this in it's current State. Will only result in crashes and/or bans.

Aimbot

    Line of sight check
    FoV check
    Aimlock to (Close Head, far Body)
    Autofire

Player ESP

    Health
    Shield
    Distance

Item ESP

    Name
    Rarity
    Distance

Extras

    Nospread & Norecoil
    Instant Reload
    Airdrop ESP
    Radar - WORK IN PROGRESS

Controles

    Hold Mouse5 - Aimlock
    Mouse4 - Toggle Autofire
    F6 - Toggle Instant Reload
    F7 - Toggle Nospread & Norecoil
    F8 - Toggle Chams
    F9 - Toggle ESP
    Num_8 - Increase HS_Range
    Num_2 - Decrease HS_Range
    Num_6 - Increase FoV
    Num_4 Decrease FoV


How To Use

    Compile as Release x64 or download dll
    Rename dll
    Inject dll during MainMenue
    Change Settings as pleased
    Have Fun


Known issues

    Toggeling Nospread & Norecoil or Instantreload after equipping the weapon won't work
    Game might crash when quitting
    Some People crash when pressing the aimkey - fixed by - use same injector and same settings as below
    ITEM ESP Distance scales wrong - seems fixed
    Small FOV tends to make problems in really close combat - fixed by increasing FoV


Thanks and Rep to:

    SevenSeasSinbad - for the base
    Zoomy500 - Original Code, chams, and D3d11 hook
    Randshot - Nospread & Norecoil fix
    liquidace - Instant Reload idea
    TJ888 - SDK

    if I should have mentioned you but didn`t please let me know


Links

    GitHub - https://github.com/Griizz/Fortnite-Hack
    Download dll new - https://www.unknowncheats.me/forum/d...=file&id=21405
    Download dll old - https://www.unknowncheats.me/forum/d...=file&id=21402
    How to Compile Source1 - How to compile a dll AKA how to use michaelsoft visual studio
    How to Compile Source2 - how 2 compile a dll pt. 2 AKA how to use gathub


Thank you all. This is my first release, so some feedback would be appreciated.

ScreenShots
ESP - http://imageshack.com/a/img923/7017/gEuvP8.png
ESP - http://imageshack.com/a/img924/4885/JJVb0b.png
Injector Settings - http://imageshack.com/a/img924/4295/t8MZyX.png


![Fortnite REST Api Client banner](https://raw.githubusercontent.com/weeco/fortnite-client/develop/git-banner.jpg)

# Fortnite REST Client
[![Build Status](https://travis-ci.org/weeco/fortnite-client.svg?branch=master)](https://travis-ci.org/weeco/fortnite-client)
[![npm](https://img.shields.io/npm/v//fortnite-client.svg)](https://www.npmjs.com/package/fortnite-client)
[![codecov](https://codecov.io/gh/weeco/fortnite-client/branch/master/graph/badge.svg)](https://codecov.io/gh/weeco/fortnite-client)

A promise based REST client for querying ingame data (such as stats) against the official Fortnite game servers. A valid Fortnite account is required to access these endpoints.

### Features

- [x] Promise based methods to get any Fortnite player's stats
- [x] Fully OOP and typesafe
- [x] Throws exceptions if exceeding predefined timeouts or 4xx / 5xx status codes in response.
- [x] Written in TypeScript (provides always up to date type definitions
- [x] Covers all publicly accessible endpoints
- [x] Integration tests
- [x] No token capturing or similiar needed, just pass your username/pass into the config

**And coming up on the roadmap...**

- [ ] Event for incoming friend requests :raising_hand:
- [ ] Sending messages to friends :e-mail:
- [ ] Event for incoming friend messages :inbox_tray:

## Table of contents
- [Fortnite REST Client](#fortnite-rest-client)
    - [Features](#features)
  - [Table of contents](#table-of-contents)
  - [Getting started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
    - [Basic usage](#basic-usage)
  - [Class FortniteClient](#class-fortniteclient)
    - [Instantion](#instantion)
    - [Available endpoints](#available-endpoints)
  - [Class LauncherClient](#class-launcherclient)
    - [Instantion](#instantion)
    - [Available endpoints](#available-endpoints)
  - [Contributors](#contributors)
  - [License](#license)

## Getting started
### Prerequisites
- [Node.js 8.0+](http://nodejs.org)
- Valid Fortnite account (email and password)
- Launcher & Client token (can both be sniffed using Fiddler)

### Installation
`$ npm install --save fortnite-client`

_**Note:** Typescript definitions are included, there is no need for installing types from the Definetely Typed Repo._

### Basic usage
Typescript (2.0+):

```typescript
import { FortniteClient, IFortniteClientCredentials, Lookup, PlayerStats } from 'fortnite-client';

const credentials: IFortniteClientCredentials = {
  email: 'weeco91@gmail.com',
  password: 'my-strong-password'
};
const api: FortniteClient = new FortniteClient(credentials);

async function bootstrap(): Promise<void> {
  try {
    await api.login();
    const ninjaLookup: Lookup = await api.lookup('ninja');
    const ninjaStats: PlayerStats = await api.getBattleRoyaleStatsById(ninjaLookup.id);
    console.log(ninjaStats.toJson());
  } catch (err) {
    console.error(err);
  }
}

bootstrap();
```

Javascript (requires ES6+):

```javascript
const FortniteClient = require('fortnite-client').FortniteClient;

const credentials = {
  email: 'weeco91@gmail.com',
  password: 'my-strong-password'
};
const api = new FortniteClient(credentials);

async function bootstrap() {
  try {
    await api.login();
    const ninjaLookup = await api.lookup('ninja');
    const ninjaStats = await api.getBattleRoyaleStatsById(ninjaLookup.id);
    console.log(ninjaStats.toJson());
  } catch (err) {
    console.error(err);
  }
}

bootstrap();
```

## Class FortniteClient
The class FortniteClient offers all available endpoints as promise based functions. Each function returns a Promise which resolves to a class instances (e. g. PlayerStats). In order to serialize the data to JSON you can just call the instance's `toJson()` method, which will return an object.

### Instantion
When creating an instance of FortniteClient you can pass a couple options which are described below:

```typescript
/**
 * Creates a new fortnite client instance.
 * @param credentials The account's credentials which shall be used for the REST requests.
 * @param options Library specific options (such as a response timeout until it throws an exception).
 */
constructor(credentials: IFortniteClientCredentials, options?: IFortniteClientOptions);

export interface IFortniteClientOptions {
  /**
   * Timeout for awaiting a response until it fails. Defaults to 5000 milliseconds.
   */
  timeoutMs?: number;
  /**
   * Tunnel requests through a proxy of your choice. If you want to inspect requests with Fiddler you have to
   * setup the proxy here.
   */
  proxy?: IProxyOptions;
}

export interface IProxyOptions {
  host: string;
  port: number;
}

```

### Available endpoints

| Route                                                                                                                                      | Returns                        |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------ |
| `static CHECK_STATUS()`                                                                                                                    | Promise\<ICheckStatus[]>       |
| `static GET_GAME_NEWS()`                                                                                                                   | Promise\<IGameNews>            |
| `login()`                                                                                                                                  | Promise\<void>                 |
| `getBattleRoyaleStatsById(userId: string, timeWindow: TimeWindow, convertJSONOutput: boolean=true)`                                        | Promise\<IPlayerStats>          | IStatsItem[]> |
| `getStore(locale: string = 'en-US')`                                                                                                       | Promise\<IStore>               |
| `getLeaderboards(leaderboardType: LeaderboardType, platform: Platform, groupType: GroupType, timeWindow: TimeWindows, limit: number = 50)` | Promise\<ILeaderboards>        |
| `lookup(username: string)`                                                                                                                 | Promise\<ILookup>              |
| `lookupByIds(accountIds: string[])`                                                                                                        | Promise\<Map<string, ILookup>> |

## Class LauncherClient
The class LauncherClient offers some of the endpoints (which I considered as useful) made by the Epic Games Launcher.

### Instantion
When creating an instance of LauncherClient you can pass a couple options which are the same as described in [FortniteClient Instantion](#instantion).

### Available endpoints

| Route                | Returns                    |
| -------------------- | -------------------------- |
| `buildInformation()` | Promise\<BuildInformation> |

## Contributors
SkYNewZ (https://github.com/SkYNewZ) - Primarily helped with the Git setup including Travis CI & Code coverage reports

Contributions to the code or documentation are welcome. If you want to add a new feature please open an issue before.

## License
The MIT License (MIT)

Copyright (c) 2018 Weeco

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# Fortnite AES Archive
A repository that contains almost *every* main PAK AES Key for Fortitude Offence Resistance Tech (FORTnite)

### Latest Available Version/Key
| Version |                                Key                                 |
|:-------:|:------------------------------------------------------------------:|
|  22.30  | 0xA1CDA4AD9A8A3B32AB87DD3501B3D906DA57C91FA599FFF5F15A35F3416DCF3C |

If you find an undocumented AES key, feel free to open a pull request and I will accept it.

Dynamic keys are kinda dead as I think other repos do a great job documenting those, namely https://github.com/kem0x/Fortnite-Aes-Keys-Archive,  https://github.com/Tectors/Archive, and https://fortnitecentral.gmatrixgames.ga/api/v1/aes

## Table Of Contents
- [Main AES Keys](https://github.com/dippyshere/fortnite-aes-archive/tree/master/archive/main.md)
- [Dynamic AES Keys](https://github.com/dippyshere/fortnite-aes-archive/tree/master/archive/dynamic)

## Credits
- Blenux for their [Pastebin](https://pastebin.com/raw/SCWdTWbj)
- FunGames BenBot
- 0x41414141
- Bizzfarts
- JunctionNinja
- Kem0x
- Kian738
- Lucas7Yoshi
- VastBlast
- GhostScissors
- https://fortnitecentral.gmatrixgames.ga/api/v1/aes

# fortnite-basic-api
[![npm version](https://img.shields.io/npm/v/fortnite-basic-api.svg)](https://npmjs.com/package/fortnite-basic-api)
[![npm downloads](https://img.shields.io/npm/dm/fortnite-basic-api.svg)](https://npmjs.com/package/fortnite-basic-api)
[![license](https://img.shields.io/npm/l/fortnite-basic-api.svg)](https://github.com/iXyles/fortnite-basic-api/blob/master/LICENSE)

__Basic Fortnite API for stats and server status built with async/await__

Inspired by other repos about Fortnite API's as:

- https://github.com/SzymonLisowiec/node-epicgames-client

- https://github.com/qlaffont/fortnite-api

Which I previously used fortnite-api but have gotten issues with unhandledrejections which causing issues in other projects. Therefore I rebuilt with focus on Async/await to resolve the issues and adding support for V2 API endpoint.
If you've a question feel free to create an issue - PS: No I'll not add party support. If you may want that sort of functionallity look into - https://www.npmjs.com/package/fnbr instead :)

- Generate device id from exchange example: https://github.com/iXyles/fortnite-basic-api/blob/master/example-test/generatedeviceauth.js 
- Login with regular creds and use device auth example: https://github.com/iXyles/fortnite-basic-api/blob/master/example-test/deviceauth.js 

Example usage: 
```js
const { Client, Communicator, FriendStatus } = require('fortnite-basic-api');

// Creation of the Client, autokill will kill the session when client is disposed.
// If you are not giving any tokens it will use the default ones that are needed.
// If you got rate limited (captcha_invalid) you can use an exchangeCode to generate a deviceauth.
// You get the exchangeCode at https://www.epicgames.com/id/login?redirectUrl=https%3A%2F%2Fwww.epicgames.com%2Fid%2Fapi%2Fexchange.
// Remember that you must be logged in with the account you want at https://epicgames.com
// AND BE CAREFUL! The generated code bypasses all 2FA logins & credentials, so do not share it.
const client = new Client({
  email: process.env.FORTNITE_EMAIL, // PLEASE USE ENV VARIABLES!
  password: process.env.FORTNITE_PASSWORD, // PLEASE USE ENV VARIABLES!
  // You should not have to update any of the tokens.
  launcherToken: 'MzRhMDJjZjhmNDQxNGUyOWIxNTkyMTg3NmRhMzZmOWE6ZGFhZmJjY2M3Mzc3NDUwMzlkZmZlNTNkOTRmYzc2Y2Y=',
  fortniteToken: 'ZWM2ODRiOGM2ODdmNDc5ZmFkZWEzY2IyYWQ4M2Y1YzY6ZTFmMzFjMjExZjI4NDEzMTg2MjYyZDM3YTEzZmM4NGQ=',
  autokill: true,
});

// Creation of communicator
const communicator = new Communicator(client);

// Example of usage
(async () => {
  // Perform the login process of the "client"
  console.log(await client.authenticator.login());

  // Setup communicator events
  communicator.events.on('session:started', async () => {
    console.log('XMPP Client is fully connected');
    console.log('Add friend: ', await communicator.friendship.addFriend('iXyles')); // example of how to add a friend
    console.log(await communicator.friendship.getFriends()); // get current friends
    console.log(await communicator.friendship.getIncomingFriendRequests()); // incoming
    console.log(await communicator.friendship.getOutgoingFriendRequests()); // outgoing
  });

  communicator.events.on('friend:request', async (friendrequest) => {
    if (friendrequest.friendStatus === FriendStatus.INCOMING) {
      console.log(friendrequest, await friendrequest.accept());
    }
  });

  communicator.events.on('reconnect', async (failure) => {
    if (failure) {
      console.log(failure); // reason to why it failed, currently only if token update failed
    }
  });

  communicator.events.on('friend:added', async (friend) => {
    console.log(`You're now friend with: ${friend.accountId}`);
  });

  communicator.events.on('friend:reject', async (friend) => {
    console.log(`You got rejected the friend request by: ${friend.accountId}`);
  });

  communicator.events.on('friend:removed', async (friend) => {
    console.log(`You're now unfriended with: ${friend.accountId}`);
  });

  communicator.events.on('friend:abort', async (friend) => {
    console.log(`Friendrequest aborted with: ${friend.accountId}`);
  });

  communicator.events.on('friend:presence', (friend) => {
    console.log(friend.presence);
  });

  communicator.events.on('friend:message', async (friend) => {
    console.log(await friend.getStatus());
    console.log('message', await friend.sendMessage('Send something back'));
  });

  // Then connect it
  console.log(await communicator.connect());

  // Since everything is async based, we can query everything parallel how ever we want with await
  const parallel = await Promise.all([
    // Supports both name & id
    client.stats.getV2Stats('iXyles'),
    client.stats.getV2Stats('96afefcb12e14e7fa1bcfab1189eae55'),

    // Or maybe just lookup?
    client.lookup.accountLookup('iXyles'),
    client.lookup.accountLookup('96afefcb12e14e7fa1bcfab1189eae55'),

    // or maybe a couple at a time?
    client.lookup.accountLookup(['iXyles', '96afefcb12e14e7fa1bcfab1189eae55']),

    client.getServerStatus(),
    client.getBRNews('es'), // insert a different language code if wanted
    client.getBRStore(),
    client.getPVEInfo(),
    client.getBREventFlags(),

    // or maybe the current logged in user accountId
    client.authenticator.accountId,
  ]);

  (parallel).forEach((result) => {
    console.log(result);
  });

  // Node will die and print that the session has been killed if login was successful
})();
```

# License
MIT License

Copyright (c) 2019-2021 iXyles

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

# Fortnite-Injector
simple fortnite injector, enjoy !!

driver include




















## Fortnite Discord RPC

An unofficial rich presence that let you to have Fortnite RPC regardless of the platform on which you play. Made with pypresence and fortnitepy

![preview](https://media.discordapp.net/attachments/838192486547324938/838206225325752340/unknown.png)

![preview playing](https://media.discordapp.net/attachments/838192486547324938/838282084437983232/unknown.png)


### Setup

**Install Python 3.7/3.8:**
https://www.python.org/downloads
Make sure `tcl/tk and IDLE` is enabled before installing

**Install required packages:**
* Windows:
Run `install.bat`

* Other:
Run the command `python3 -m pip install -r requirements.txt`

**Make an epic account to monitore your status**

For this step you can use an unused epic account
You can create an account in [this link](https://www.epicgames.com/id/logout?redirectUrl=https%3A//www.epicgames.com/id/login)

**Run the program**
* Windows:
Run `start.bat`

* Other:
Run the command `python3 main.py`

**Setup**

The first time you start the program you will be prompted to enter your epic games display name and log in to the account to be used to monitor your status.
You only have to wait for a text like this to appear:
```
Login to https://www.epicgames.com/id/login?redirectUrl=https%3A%2F%2Fwww.epicgames.com%2Fid%2Fapi%2Fredirect%3FclientId%3D3446cd72694c4a4485d81b77adbb2141%26responseType%3Dcode and paste the response:
```
Open that link in your browser, login with the bot account **NOT YOUR MAIN**.
You will see a text like this:
![Text example](https://media.discordapp.net/attachments/838192486547324938/856967743471747072/unknown.png)

Copy all and paste it in the console
![Paste example](https://media.discordapp.net/attachments/838192486547324938/856968391041220638/unknown.png)

Hit enter and if you did it correctly and the code didn't expire yet you are ready!

If for some reason you get an error saying that the code is not valid just refresh the page where you got the data and copy all again.


**Add the monitor account as friend**

You may get a message indicating that you are not a friend of the bot. This means you will have to add it by epic games. If you are already a friend of the bot simply ignore this step

**Ready!**

Now you will have your RPC ready, as long as you do not close your discord and you have the program open! Enjoy


**Command line arguments**

Just some command line arguments that can be usefull for you:

```
--delete-device-auth | Deletes created device auth (You will need to do authentication again after this)
--no-update-check | Skips the update check
```


**Note**

There is a possibility that the credentials of the monitor account may be invalid unexpectedly. In that case you will just have to restart and perform the authentication again.

---

If you need help you can send me a private message on twitter `@CodeBayGamerJJ` or add me as a friend on Discord `Bay#7210`

#### Use code BayGamerJJ in the item shop to support me <3 #EpicPartner

# UEDumper
This can probably dump the SDK for any Unreal Engine Game (Educational Purpose Only)
Note: We released this early, for now it's working perfect for fortnite (lower than u4.25?), but we will add more support later!

Current Bugs: You can not compile the files due to issues with including, very rare errors when calculating the padding, very few offsets are still hardcoded

# Usage

### Set the build settings  
Example of DUMP_OBJECT_NAMES  
Output path: D:\5.41-CL-4363240\FortniteGame\Binaries\Win64\SDK\  
Dumped 99158 objects in 636.12 ms  
  
Example of SEARCH_OFFSETS and PRINT_OFFSETS  
Memory base: 00007FF77AA20000  
ProcessEvent: 00007FF77C24D530  
StaticFindObject: 00007FF77C274780  
GObjects: 00007FF77FE45940  
....
  
1. Inject the dll into your game
2. If all offsets are found automatically you will need to do nothing, otherwise you will need to get them manually
3. Go to the game path and copy your SDK
4. To use it in a project check out the examples, not all packages are included, just add the ones you need to Core.hpp

# Features
✔️ Dump all Object names  
✔️ Create a SDK  
  
# Details  
✔️ Getting the real UPROPERTY Specifiers  
✔️ Automatically find most (often all) offsets

# TODO:
Check all functions if they contain the offset for a property
Add support for newer ue4 versions
 
More coming soon

# Fortnite stats for LaMetric

![LaMetric Fortnite](https://raw.githubusercontent.com/pgrimaud/lametric-fortnite/master/images/fortnite.png)

# How it works ?

- Launch your LaMetric app
- Install the app ["Fortnite"](https://apps.lametric.com/apps/fortnite/6390)
- Configure parameters

![LaMetric Fortnite](https://raw.githubusercontent.com/pgrimaud/lametric-fortnite/master/images/fortnite-app.png)

![LaMetric Fortnite GIF](https://raw.githubusercontent.com/pgrimaud/lametric-fortnite/master/images/fortnite.gif)

# Feedback

If you need help, [create an issue](https://github.com/pgrimaud/lametric-fortnite/issues) or contact us on [Twitter](http://twitter.com/pgrimaud_)

# More info

Based on [Fortnite Tracker](https://fortnitetracker.com)

This is a template for creating your own scheduled Fortnite Item Shop and BR News twitter bot using python and heroku.

Requirements
--------
* __heroku__
   * [account](https://www.heroku.com/) and [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install): _for hosting python app and keeping it running_

Instructions
--------
0. Click the "Use this template" button and create your own repo

1. Create a new heroku app on the [Heroku Dashboard](https://herokuapp.com/) by clicking on ```New``` and selecting ```New App```.
   * Select your server and confirm its creation.
   * Make sure your Heroku account is connected to your github account via the ```Deploy``` tab.
   * Enable automatic deploys and select your repository.
   * Click on ```Deploy Branch``` to ensure a copy of the repo is initialized and ready on heroku.
   * Go to the ```Resources``` tab and make sure that the dyno worker is ___switched off!___ This is a very important step on creating this bot, so keep that in mind.

2. __Verify your Heroku account__
   * This is needed because of Heroku's requirements, and you need to verify your acccount if you want to use add-ons, which is required for this program.
   * Go to [this page](http://heroku.com/verify) and enter your credit card details
      - Don't worry! Your card will never be charged for this program and will only serve as Verification of your Heroku account.
   * You do not need a paid plan for this. I use the free version of Heroku since we'll only use this once or twice a day.

3. Create a [new twitter account](https://twitter.com/). (If you already have one, please use your twitter account instead and skip straight to step 3.)
    * Use your current email to create the account by adding [a tag](http://en.wikipedia.org/wiki/Email_address#Address_tags).
       - Ex: _email@gmail.com_ => _email+twitterbot@gmail.com_
    * Confirm the email address associated with this new twitter account.

4. From your main twitter account (not the one you just created, unless this is your first twitter account!) create a [new twitter app](https://apps.twitter.com).
    * Apply for a Twitter developer account, and select ```Making a bot```. Enter the necessary details and submit your application.
    * This process may take a while, and it may not be instant.
    * After your application, create a bot by clicking on the ```Create an App``` button.
    * Enter the necessary details.
    * Under _Settings_ / _Application Type_:
        - Enable _"Read and Write"_
    * Under _Details_:
        - Click _"Create My Access Token"_

5. Create an `.env` file containing your twitter keys.
    * In your local repo, create a file called ```.env```, and then copy everything from [this paste](https://pastebin.com/PxJnKrFq)
    * Replace the placeholders with your credentials. You can only view it once on the twitter page until you close it, so copy everything to the ```.env``` file.
    * For [heroku](https://devcenter.heroku.com/articles/config-vars), use ```heroku-config``` to copy contents of ```.env``` to your heroku app.
        - Configure your heroku app by launching ```heroku git:remote -a [insert your heroku app name here]``` on the folder of your cloned Github repo.
        - Install heroku-config: ```heroku plugins:install heroku-config```.
        - Now run ```heroku config:push```.
            - NOTE: To update heroku environment variables later, run ```heroku config:push --overwrite```

__Okay, now here's the fun part:__

6. Personalize your message and background!
    * Change the ```twitterbot.sh``` URLs. The default settings have my branding on it, so you may need to replace the ```background``` URL to something different, or remove it entirely.
         - If you want to create your own backgrounds, please refer to the ```media``` folder for the image size and positioning.
         - The images I use are ```news.jpg``` and ```nitestats.jpg```. Change them to anything you like.
            - If you want to have weekly SAC reminders, the image I use is ```SAC_Reminder.png``` on the ```output``` folder.
         - To get the Image URL, go to the image you uploaded on your github repo and open it on a new tab.
    * Change the message and timezone on ```app.py``` and ```news.py```.
         -  __OPTIONAL__: If you want weekly SAC reminders, change ```sac.py``` as well.
         - You can also remove the Timezones and its references if you don't want the time on your tweets.

7. Commit and push local changes to Github. Heroku will automatically update the remote files since you have Heroku connected.
    
8. On your Heroku app dashboard, go to the ```Resources``` tab and add the ```Advanced Scheduler``` add-on.
    * Make sure your Heroku account is verified for this!
    * Click on it, and create a new trigger.
    * Add a name, and make sure the command is ```bash twitterbot.sh```, and the timezone is UTC.
    * Make it a recurring trigger and select the ```Schedule Helper``` option.
    * Item shop resets every day at 12:00AM UTC. Save the trigger.
      - If you use ```sac.py```, do the same steps. Except this time, you must change the interval to weekly and the time to be Tuesdays at 8:00AM UTC.

Additional Info
---------
Please check out the [Nitestats Discord](https://discord.gg/tNmWbBy) for updates on the API. Please redirect all questions and bug reports about the API to this discord. Thank you!

## If this repo helped you out, Please consider using code "KuletXCore" on the Fortnite item shop or on the Epic Games Store! :)

# Fortnite Discord Bot

Simple discord bot that retrieves fortnite user stats

![](https://i.imgur.com/khZNKIG.png)

### Prerequisites

This script requires these libraries: [discord.py](https://github.com/Rapptz/discord.py) and [requests](https://github.com/requests/requests)

```
pip install discord.py
pip install requests
```

### Running the bot

In `bot.py`, replace the values of `BOT_TOKEN` and `FORTNITE_API_TOKEN` with your own API keys.

Discord Developers: [https://discordapp.com/developers/docs/intro](https://discordapp.com/developers/docs/intro)

Fortnite Tracker API: [https://fortnitetracker.com/site-api](https://fortnitetracker.com/site-api)

Run your bot with:

```
python bot.py
```

### Using the bot

Go to a Discord server with your bot, then type `!ping` to check that the bot is online and responding to your messages. The bot must have `VIEW_CHANNEL` and `SEND_MESSAGES` permissions in that Discord server in order to respond to you. 

Type `!stats <platform> <nickname>` to retrieve stats about user with nickname on a platform (pc, xbl, or psn)

The command prefix can be customzied by changing the value of `COMMAND_PREFIX` in `bot.py`.

## Hosting the bot on Heroku

The bot can be hosted for free by running the script on Heroku.

1) Install git and Heroku CLI.

2) Create `requirements.txt` by typing `pip freeze > requirements.txt`. This lets Heroku detect that you are running a Python app and have it install the required libraries.

3) Create a Procfile with `worker: python bot.py`.

4) Create a git repository with `git init`.

5) Create a heroku app and set config vars:

```
heroku login
heroku create
heroku config:set BOT_TOKEN=<insert token here>
heroku config:set FORTNITE_API_TOKEN=<insert token here>
```

6) Push to heroku:

```
git init
git add -A
git commit -m "Initial commit"
git push heroku master
```

6) Start the worker with `heroku ps:scale worker=1`.

7) Check logs with `heroku logs --tail`.


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details