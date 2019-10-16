# ShadowStalkers
Bot made for my clan

const Discord = require('discord.js');
const client = new Discord.Client();
const auth = require('./auth.json');

client.on('ready', () => {   
     console.log('Logged in as ${client.user.tag!');
 });
 
 client.login(auth.token)
 
client.on('message', msg => {
  if (msg.content === 'SS support') {
    msg.reply('Please refer to our ticket area for any support you may need help with');
  }
});

client.on('guildMemberAdd', member => {
    const channel = member.guild.channels.find(ch => ch.name === 'welcome');
    channel.send(`thank you for joining, please head to our #verifcation-pool section for access to the rest of our server, ${member}`);
});

client.on('ready', () => {
  console.log('I am ready!');
});

client.on('message', message => {
  // Ignore messages that aren't from a guild
  if (!message.guild) return;

  if (message.content.startsWith('SS kick')) {
    const user = message.mentions.users.first();
    // If we have a user mentioned
    if (user) 
      const member = message.guild.member(user);
     
      if (member) {
      
        member.kick('Optional reason that will display in the audit logs').then(()
        }).catch(err => {
         
          message.reply('I was unable to kick the member');
          
          console.error(err);
        });
      } else {
        
        message.reply('That user isn\'t in this guild!');
      }
    // Otherwise, if no user was mentioned
    } else {
      message.reply('You didn\'t mention the user to kick!');
    }
  }
});

client.on('message', message => {

  if (!message.guild) return;

 
  if (message.content.startsWith('SS ban')) {
   
    const user = message.mentions.users.first();
    
    if (user) {
      
      const member = message.guild.member(user);
      
      if (member) {
        
        member.ban({
          reason: 'They were bad!',
        }).then(() => {
          
          message.reply(`Successfully banned ${user.tag}`);
        }).catch(err => {
          
          message.reply('I was unable to ban the member');
          // Log the error
          console.error(err);
        });
      } else {
        
        message.reply('That user isn\'t in this guild!');
      }
    } else {
   
      message.reply('You didn\'t mention the user to ban!');
    }
  }
});
// using these commands as a basis, i am trying to add a mute command to help moderate my current server //
