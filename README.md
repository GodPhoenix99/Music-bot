python

import discord

import asyncio

from discord.ext import commands

import youtube_dl

bot = commands.Bot(command_prefix='!') # set the bot's command prefix

# function to download and extract audio from a YouTube URL

def play_song(url):

    with youtube_dl.YoutubeDL() as ydl:

        info = ydl.extract_info(url, download=False)

        url = info['formats'][0]['url']

    return discord.PCMVolumeTransformer(discord.FFmpegPCMAudio(url))

@bot.command()

async def join(ctx):

    channel = ctx.message.author.voice.channel

    await channel.connect()

@bot.command()

async def leave(ctx):

    await ctx.voice_client.disconnect()

@bot.command()

async def skip(ctx):

    ctx.voice_client.stop()

@bot.command()

async def play(ctx, url):

    await ctx.send(f"Playing {url}")

    ctx.voice_client.play(play_song(url), after=lambda e: print(f'Player error: {e}') if e else None)

bot.run(MTA5NTAzODY0ODE4Mjg5ODgyOQ.GhUZKs.IvwwBgSdrf2-wixdzVx3RioCVu8XlAqv6Ugtv8) # replace with your bot token
