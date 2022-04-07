# DiscordFilter
Use This To Detect Filtered words on discord (nitro scams etc)

[![Downloads](https://pepy.tech/badge/DiscordFilter)](https://pepy.tech/project/DiscordFilter)
[![Downloads](https://pepy.tech/badge/DiscordFilter/week)](https://pepy.tech/project/DiscordFilter)
[![Downloads](https://pepy.tech/badge/DiscordFilter/month)](https://pepy.tech/project/DiscordFilter)
[![Requires: Python 3.x](https://img.shields.io/pypi/pyversions/DiscordFilter.svg)](https://pypi.org/project/DiscordFilter/)
[![Version: 0.0.2](https://img.shields.io/pypi/v/DiscordFilter.svg)](https://pypi.org/project/DiscordFilter/)

### Setup:
``pip3 install DiscordFilter``


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
  bot.loop.create_task(update_blacklist())#Set a background task to check for updates every 5min.

@bot.event
async def on_message(message):
  if filter.is_filtered(message) == True: #if the message is filtered
    await message.delete()#deletes the filtered message

@bot.command()
async def hello(ctx):
  await ctx.reply("Hello!")

bot.run('token')
```
