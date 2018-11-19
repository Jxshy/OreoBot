import discord
from discord.ext import commands
from discord.ext.commands import Bot
import asyncio


bot = commands.Bot(command_prefix='O!')
token = ("NTEzODM5ODQwNTI2MDczODgx.DtN6qA.wiW-PwKOboidXeI2yA_465LbenU")


@bot.event
async def on_ready():
    print("Ready!")
    print(bot.user.name)
    

@bot.command(pass_context=True)
async def ping(ctx):
    await bot.say(":ping_pong: Ping!")
    print ("user has pinged")

@bot.command(pass_context=True)
async def kick(ctx, user: discord.Member):
    await bot.say("{} was kicked from the server!".format(user.name))
    await bot.kick(user)
    if user == "everyone":
        await bot.say("You cannot kick everyone!")

@bot.command(pass_context=True)
async def info(ctx, user: discord.Member):
    await bot.say("The users name is: {}".format(user.name))
    await bot.say("The users status is: {}".format(user.status))
    await bot.say("The user joined at: {}".format(user.joined_at))
    

@bot.command(pass_context=True)
async def serverinfo(ctx):
    embed = discord.Embed(name="{}'s info".format(ctx.message.server.name), description="Here's what I could find.", color=0x36393E)
    embed.set_author(name="Server Info")
    embed.add_field(name="Name", value=ctx.message.server.name, inline=True)
    embed.add_field(name="ID", value=ctx.message.server.id, inline=True)
    embed.add_field(name="Roles", value=len(ctx.message.server.roles), inline=True)
    embed.add_field(name="Members", value=len(ctx.message.server.members))
    embed.set_thumbnail(url=ctx.message.server.icon_url)
    await bot.say(embed=embed)

@bot.command(pass_context=True)
async def embed(ctx):
    embed = discord.Embed(title="test", description="my name jeff", color=0x00ff00)
    embed.set_footer(text="this is a footer")
    embed.set_author(name="hi")
    embed.add_field(name="This is a field", value="no it isn't", inline=True)
    await bot.say(embed=embed)

@bot.command(pass_context=True)
async def say(ctx, *, arg):
    await bot.say(arg)


@bot.command(pass_context=True)
async def invite(ctx):
    await bot.say("Here is the bot invite!   :link: https://discordapp.com/oauth2/authorize?client_id=513839840526073881&permissions=8&scope=bot")

bot.run(token)
