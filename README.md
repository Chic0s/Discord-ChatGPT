
# ChatGPT

Suite à la hype autour de ChatGPT, j'ai décidé de l'intégrer à un bot Discord.




## Badges

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)


## Installation

**Server:** Python

- pip install discord

- pip install wikipedia

- pip install openai


## Documentation

Pour utiliser le bot, rien de plus facile. 

Rendez-vous sur le site : https://discord.com/developers

Pour faire un bot et récupérer un token valide.


Concernant ChatGPT, rendez-vous : https://beta.openai.com

Attention ! Une action est payante et coute 0,004€. 
Openai vous offre 18$ pour tester l'API. 

Et voilà, il ne vous reste plus qu'à ajouter les tokens.

openai.api_key = 'TOKEN_OPENAI'

bot.run = 'TOKEN_DISCORD'


## Commande 

!aide = pour obtenir la commande principale

!chat <votre question> = pour obtenir une réponse de ChatGPT

!wiki <mot> = pour obtenir une définition

## Code 

```python

import discord
from discord import app_commands
from discord.ext import commands
import wikipedia

from config import Pass

import openai
openai.api_key = Pass.openai()

def generate_text(prompt):
  completions = openai.Completion.create(
  engine="text-davinci-002",
  prompt=prompt,
  max_tokens=1024,
  n=1,
  stop=None,
  temperature=0.5,
  )
  message = completions.choices[0].text 
  return message.strip()

bot = commands.Bot(command_prefix='!', intents=discord.Intents.all())

@bot.event
async def on_ready():
  print('bot OP')
  await bot.change_presence(activity=discord.Game("!aide"))


@bot.command()
async def aide(ctx):
  await ctx.send("Pour utiliser le bot ChatGPT, !chat <votre question>")
  await ctx.send("De plus, une option !wiki <votre definition>, permet d'avoir une description précise.")

@bot.command()
async def credit(ctx):
  await ctx.send("Fait par Chic0s#0001")

@bot.command()
async def chat(ctx, *,question):
  try:
    response = generate_text(question)
    await ctx.send(response)
  except:
   await ctx.send("Désolé la réponse est trop longue pour discord, pour plus d'informations : chat.openai.com/")

@bot.command()
async def wiki(ctx, *, question):
  wikipedia.set_lang("fr")
  try:
    result = wikipedia.summary(question, sentences=2)
  except:
    result = "Désolé, votre recherche n'a pas pu aboutir. Merci de rechercher un autre terme !"
  await ctx.send(result)

bot.run(Pass.discord())

```
        




## Editeur 

Chic0s
