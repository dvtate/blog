# Corki Discord Bot Development Timeline

This post is a brief overview of the history of the [Corki Discord Bot](https://corki.js.org) I created as well as an explanation of why it's no longer in operation.

## 2016
### Telegram Bot
  In 2016, I threw together a [Telegram](https://telegram.org) chatbot for my
[highschool robotics team](https://robobibb.github.io) and hosted it on my home
server. In addition to coordinating team communications, the bot became somewhat
of a swiss army knife with ever more functionality.

## 2017
  I continued making Telegram bots for more than just my robotics team, but
eventually started using Discord as well.
### Corki Mains Discord
  In 2017, I joined the Corki Mains Discord server -- a community centered around
the videogame League of Legends (LoL). The server had a bot,
[Oriana bot](https://orianna.molenzwiebel.xyz), which is the most popular League of
Legends focused Discord bot, however it was misconfigured and didn't work. The server
owner was unable to fix the configuration due to mixture of bugs, bad UI, and him not
caring enough. By the end of the year, I had created my own Discord bot with plans to
replace Orianna Bot.

## 2018
  I started out adding many of the features from my old Telegram bots, but my goal
was feature parity with Orianna Bot. I added lots of LoL-related features and other
things to make it user-friendly.

  With a strong start, I presented the bot to the server owner, and he added it to the
server. The bot immediately started getting used, and everyone was happy and sharing
ideas on how to make it better.
### Features
  By the end of the year I had alternatives to many of Oriana's features, although
many were admittedly rough around the edges. One key feature I added was a web-portal,
allowing users to do many actions with an interface that's easier to work with than
text-based commands. This web portal also opened the door to broader moderation
functionality which became useful for moderators.

## 2019
### Discord Server Takeover
The Corki Mains Server Owner hadn't been seen for several months starting in late 2018.
The moderators were doing a lot to manage the community but didn't have administrator
priveleges needed to perform many tasks so they sent several messages to the unresponsive
server owner requesting help and/or permissions.

Eventually, the server owner did come back online, with his friends, but instead of
helping, they raided the server posting spam and even NSFW material. Acting fast to save
the community, a moderator created a new server without the previous server owner. I
used Corki Bot to direct message everyone in the old server an invite link to join the
new server. Making sure to skip over the bad actors. After this, the old server only had
inactive users so I continued to use it to test new bot features.

### Discord Bot Lists
  With the bot approaching feature parity with Orianna Bot, I put it on [top.gg](https://top.gg)
and another bot directory. After filling in the forms the bot gained over 40k new users
almost overnight.

### Orianna Rewrite
  Orianna Bot was eventually rewritten, fixing its UI and even added some of the original
features I added to Corki bot. At this point Corki was no longer Competitive with Orianna
bot but because I now had users it made sense to continue development.

### AutoRoles
  One of Orianna Bot's features was that it automatically assigned Discord guild roles
based on user rank and mastery points. I had previously created a system for this but it
was buggy. I decided that instead of simply cloning this feature I should make a generic
system that would use user-defined conditions. Having just finished making a programming
language, I decided to make a language-based rule engine to do this. I quickly got the
system working and deployed to the Corki Mains server. I had plans to make a 
user-friendly editor for the conditions but out of the blue I got a call from an old
friend asking me to work on her startup. I spent most of the rest of the year at that
startup making a similar system which bought and sold stocks instead of assigning and
removing guild roles.

## 2020 - 2022
  During this time, only basic maintenance was done with the bot in terms of code.
### Discord Bot Verification
  Discord warned about requiring verification for popular bots (like Corki). I requested
verification to prevent my bot getting shutdown. After a long time in review, my bot was
[mistakenly rejected](https://github.com/discord/discord-api-docs/discussions/3971) by
Discord. I submitted an appeal and complained to support, getting no response for over a
year. Eventually my bot crossed a threshold and Discord restricted it. After communication
with Discord support, the issue was resolved and my bot was verified and working again.

## 2023
### The Beginning of the End
  At this point I realized that although my bot still worked, it was in desperate need of
a rewrite. Additionally with Discord wanting me to use a different system for commands
and other APIs continuing to change, continuing development looked like a difficult task.
With that in mind, I reached out to the developer of Orianna bot to transfer users' LoL
data over.

## 2024
### The End
  Despite Corki Bot being functionally obsolete, I kept it online and it did still have users.
My plan was to keep it online until it stopped working. However, Discord requested a bunch of
legal documents in order to renew my bot's verification. To me it wasn't worth the security
risk of putting these on the internet. Eventually Discord revoked my access token and Corki
was dead.

## Conclusion
Developing, maintaining and hosting Corki Bot taught me a lot and with it peaking at well over 200,000 users it's one of the projects I'm most proud of.
