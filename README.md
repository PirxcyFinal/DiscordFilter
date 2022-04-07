# PirxcyPinger
Use This To Upload Files To PirxcyPinger

[![Downloads](https://pepy.tech/badge/PirxcyPinger)](https://pepy.tech/project/PirxcyPinger)
[![Downloads](https://pepy.tech/badge/pirxcypinger/week)](https://pepy.tech/project/pirxcypinger)
[![Downloads](https://pepy.tech/badge/pirxcypinger/month)](https://pepy.tech/project/pirxcypinger)
[![Requires: Python 3.x](https://img.shields.io/pypi/pyversions/PirxcyPinger.svg)](https://pypi.org/project/PirxcyPinger/)
[![Version: 0.0.2](https://img.shields.io/pypi/v/PirxcyPinger.svg)](https://pypi.org/project/PirxcyPinger/)

### Setup:
``pip3 install PirxcyPinger``

[Examples](https://github.com/PirxcyFinal/PirxcyPinger/tree/main/Examples "github.com/PirxcyFinal/PirxcyPinger/tree/main/Examples")

```python
import DiscordFilter
import asyncio
import discord

from discord.ext import commands


filter = DiscordFilter.filter(blacklist_file="blacklist.json")
bot = commands.Bot(command_prefix="!")

async def update_blacklist():
  while True:
    update = await filter.update_blacklist()
    if update == True:#If a new update was recieved.
      print(f"Updated {filter.blacklist_file}")
    await asyncio.sleep(300)#Wait 5min Then check for update again.

@bot.event
async def event_ready():
  bot.loop.create_task(update_blacklist)#Set a background task to check for updates every 5min.

@bot.event
async def on_message(message):
  if filter.is_filtered(message) == True: #if the message is filtered
    await message.delete()#deletes the filtered message

@bot.command()
async def hello(ctx):
  await ctx.reply("Hello!")

bot.run('token')
```
