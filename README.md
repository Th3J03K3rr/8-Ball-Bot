# 8-Ball-Bot
# This is the initial code for 8-Ball-Bot discord bot, currently inactive.
#The code is in beta stage for initial release.
#This code is mutable and will be updated later.

# import commands

import discord
import random
import time

# bundle of replies

eight_ball_replies = ["It is certain", "It is decidedly so", "Without a doubt", "Yes, definitely", "You may rely on it", "As I see it, yes", "Most likely", "Outlook good", "Yes", "Signs point to yes",
"Reply hazy try again", "Ask again later", "Better not tell you now", "Cannot predict now", "Concentrate and ask again",
"Don't count on it", "My reply is no", "My sources say no", "Outlook not so good", "Very doubtful"]

# bullet design

rr_bullet = random.randint(1, 6)
rr_count = 1

# client link

client = discord.Client()
client.login('email', 'password')

#event initiation

@client.event
def on_message(message):
 
    if message.content.lower().startswith('!calc '):
        client.send_message(message.channel, eval(message.content[6:]))
 
    if message.content.lower().startswith('!ping'):
        client.send_message(message.channel, 'Pong!')
 
    if message.content.lower().startswith('!roll'):
        values = message.content[6:].split(' ')
        client.send_message(message.channel, random.randint(int(values[0]), int(values[1])))
 
    if message.content.lower().startswith('!8ball'):
        client.send_message(message.channel, '[Magic 8 Ball] "' + message.content[7:] + '": ' + eight_ball_replies[random.randint(0, 19)])
 
    if message.content.lower().startswith('!rr'):
        global rr_bullet
        global rr_count
        client.send_message(message.channel, 'You spin the cylinder of the revolver with 1 bullet in it...')
        time.sleep(1)
        client.send_message(message.channel, '...you place the muzzle against your head and pull the trigger...')
        time.sleep(2)
        if rr_bullet == rr_count:
                client.send_message(message.channel, '...your brain gets splattered all over the wall.')
                rr_bullet = random.randint(1, 6)
                rr_count = 1
        else:
                client.send_message(message.channel, '...you live to see another day.')
                rr_count = rr_count + 1
 



@client.event
def on_ready():
    print('Logged in as')
    print(client.user.name)
    print(client.user.id)
    print('------')
 
client.run()
