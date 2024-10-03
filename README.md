# InstaBot
#Instagram bot for auto reply message using python..
from instabot import Bot
import time

# Initialize the bot
bot = Bot()

# Login to your Instagram account
USERNAME = 'username'  # Your Instagram username
PASSWORD = 'password'  # Your Instagram password
bot.login(username=USERNAME, password=PASSWORD)

# Function to check for new messages and respond
def respond_to_messages():
    inbox = bot.get_inbox()
    for thread in inbox:
        # Check if there's a new message in the thread
        if thread['messages'][-1]['user_id'] != bot.user_id:
            sender = thread['users'][0]['username']
            # Responding with a message
            response_message = "Thanks for reaching out! I'll get back to you soon."
            bot.send_message(response_message, [sender])
            print(f'Message sent to {sender}: "{response_message}"')

if __name__ == '__main__':
    print("Listening for messages...")
    while True:
        respond_to_messages()
        time.sleep(30)  # Check for new messages every 30 seconds
