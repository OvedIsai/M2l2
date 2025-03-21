
import discord
import random, os
import requests

from discord.ext import commands
intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix='!', intents=intents)

@bot.event
async def on_ready():
    print(f'We have logged in as {bot.user}')

@bot.command()
async def hello(ctx):
    await ctx.send(f'Hola, soy {bot.user}!')

@bot.command()
async def hola(ctx):
    await ctx.send(f'Hola, a todos de la reunion soy {bot.user} y estoy para resolver cualquier problema  que tenga mi dueño!')

@bot.command()
async def  saludamoises(ctx):
    await ctx.send(f'hola moises soy {bot.user}!')

@bot.command()
async def  aquetededicas(ctx):
    await ctx.send(f'um a ya y me dedico a estar con mi dueño cuando me necesite para con probar un comando!')


@bot.command()
async def  saludajuanda(ctx):
    await ctx.send(f'hola juanda soy {bot.user}!')

@bot.command()
async def mem(ctx):
    # ¡Vamos a elegir una imagen al azar de la carpeta "images"!
    img_name = random.choice(os.listdir('images'))
    with open(f'images/{img_name}', 'rb') as f:
        # ¡Vamos a almacenar el archivo de la biblioteca Discord convertido en esta variable!
        picture = discord.File(f)
    # A continuación, podemos enviar este archivo como parámetro.
    await ctx.send(file=picture)

@bot.command()
async def pet(ctx):
    # URL de la API de imágenes de perros
    url = 'https://dog.ceo/api/breeds/image/random'
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        dog_image_url = data['message']  # URL de la imagen del perro
        # Enviar la imagen al canal
        await ctx.send(dog_image_url)
    else:
        await ctx.send('Lo siento, no pude obtener una imagen de perro en este momento.')
bot.run('TOKEN BOT')
