import os
import threading
from flask import Flask
import discord
from discord.ext import commands

# Fake website so Render Free Web Service stays happy
app = Flask(__name__)
@app.route('/')
def home():
    return "Bot is alive!"

def run_web():
    port = int(os.environ.get("PORT", 10000))
    app.run(host="0.0.0.0", port=port)

threading.Thread(target=run_web, daemon=True).start()

intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix="!", intents=intents)

@bot.event
async def on_ready():
    print(f"Logged in as {bot.user} - Bot is online!")

@bot.command()
async def hello(ctx):
    await ctx.send(f"Hello {ctx.author.mention}! I'm alive 👋")

@bot.command()
async def ping(ctx):
    await ctx.send(f"Pong! {round(bot.latency * 1000)}ms")

TOKEN = os.getenv("DISCORD_TOKEN")
bot.run(TOKEN)
