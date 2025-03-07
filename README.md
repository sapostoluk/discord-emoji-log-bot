# Discord Emoji Log Bot

[![Discord](https://discordapp.com/api/guilds/258167954913361930/embed.png)](https://discord.gg/WjEFnzC) [![Twitter Follow](https://img.shields.io/twitter/follow/peterthehan.svg?style=social)](https://twitter.com/peterthehan)

An old Discord bot that logs user emoji usage. Updated to work with v13 of [peterthehan's create-discord-bot](https://github.com/peterthehan/create-discord-bot), and also added an isCustom column to the emoji log.

## Fork Updates

I know this repo this is forked from is archived, but it still seemed like a great solution for tracking emoji use on a Discord server. As such, I've made the necessary changes to get this working with v13 of [peterthehan's create-discord-bot repo](https://github.com/peterthehan/create-discord-bot). This really only involved updating the text message type check and changing the bot folder from /widgets to /bots. Updating the message event to messageCreate event wasn't necessary, but it was an easy update that should help futureproof a bit.

I also added an isCustom column to the emojis sheet, which is minor but nice for easy filtering when determining which emoji should be removed on a server. 

## Warnings, FYI

> Be aware that while the Google Sheets API has a free tier, it has limits in place. You can read more about the API limits [here](https://developers.google.com/sheets/api/limits) and the document limits [here](https://support.google.com/drive/answer/37603).

> Given that a Google Sheets document supports up to 5000000 cells and the main `logs` table has 5 columns, that gives us appromixately 1000000 rows. If we assume a rate of 500 logs per day, that gives us approximately 5.5 years before we have to consider archiving rows.

## Google Sheets Setup

1. Follow the [setup instructions](https://theoephraim.github.io/node-google-spreadsheet/#/getting-started/authentication?id=service-account) found in the project [google-spreadsheet](https://github.com/theoephraim/node-google-spreadsheet) to create a Google Sheets API Service Account.

   > Take note of the client email associated with the Service Account. Additionally, you will have downloaded a credentials JSON file after following through the instructions. You will need these in the next section.

2. Create a Google Sheets document in your Google Drive.

3. Click the green `Share` button and share the file with the client email associated with the Service Account.

   > Make sure the Service Account has edit access to this file or the bot will not be able to log data!

## Setup

1. Follow the instructions in [create-discord-bot](https://github.com/peterthehan/create-discord-bot).

2. Copy the `client_email` and `private_key` values in the credentials JSON file into your `.env` file:

   ```
   CLIENT_EMAIL=client_email_value_here
   PRIVATE_KEY=private_key_value_here
   ```

3. Download this widget and move the `src-discord-emoji-log-bot` folder into the [src/bots/](https://github.com/peterthehan/create-discord-bot/tree/master/app/src/bots) folder created in step 1.

   > `npm i -s emoji-regex@^9.2.2 google-spreadsheet@^^3.1.15` to install this widget's dependencies.

4. Open [config.js](https://github.com/peterthehan/discord-emoji-log-bot/blob/master/src-discord-emoji-log-bot/config.js) to configure your own settings:

   ```js
   module.exports = {
     sheetId: "1CrvJ3Zuec5F7dF5ez_nPOJ5auZVfPrXz_W8GG2o0PZM",
     guildChannelMap: {
       "258167954913361930": {
         channelsToIgnore: [],
       },
     },
   };
   ```

   Add as many rules as you want to configure for other servers.

   - `sheetId` is the id of the Google Sheets document found in the URL: [https://docs.google.com/spreadsheets/d/SHEET_ID_FOUND_HERE/edit](https://docs.google.com/spreadsheets/d/SHEET_ID_FOUND_HERE/edit).
   - `guildChannelMap` is a key-value map between server id and channel ids.
     - `channelsToIgnore` are the text channel ids the bot will not log user emoji usage from.

5. `npm start` to run the bot.

## Design

<div align="center">
  <img
    src="https://raw.githubusercontent.com/peterthehan/discord-emoji-log-bot/master/assets/schema.png"
    alt="schema"
  />
</div>

Visit for more help or information!

<a href="https://discord.gg/WjEFnzC">
  <img src="https://discordapp.com/api/guilds/258167954913361930/embed.png?style=banner2" title="Discord Server"/>
</a>
