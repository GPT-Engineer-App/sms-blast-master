# sms-blast-master

Sure, here's the complete Python script for a bulk SMS sender using Twilio:

```python
import os
import random
import tkinter as tk
from twilio.rest import Client
from phonenumbers import parse, format_number, PhoneNumberFormat

# Twilio account SID and auth token (replace with your credentials)
account_sid = 'your_account_sid'
auth_token = 'your_auth_token'
twilio_phone_number = 'your_twilio_phone_number'

# Message generator
def generate_message():
    messages = [
        "This is a test message.",
        "Hello from Twilio!",
        "Your verification code is 123456.",
        # Add more messages
    ]
    return random.choice(messages)

# Phone number formatter and verifier
def format_phone_number(phone_number):
    try:
        parsed_number = parse(phone_number, "US")
        formatted_number = format_number(parsed_number, PhoneNumberFormat.E164)
        return formatted_number
    except:
        return None

# Create Twilio client
client = Client(account_sid, auth_token)

# User interface
class BulkSMSApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Bulk SMS App")
        self.root.geometry("400x300")
        self.phone_numbers = []

        self.phone_label = tk.Label(self.root, text="Phone Numbers:")
        self.phone_label.pack()
        self.phone_entry = tk.Entry(self.root)
        self.phone_entry.pack()

        self.add_button = tk.Button(self.root, text="Add", command=self.add_phone_number)
        self.add_button.pack()
        self.send_button = tk.Button(self.root, text="Send SMS", command=self.send_sms)
        self.send_button.pack()

    def add_phone_number(self):
        phone_number = self.phone_entry.get()
        formatted_number = format_phone_number(phone_number)
        if formatted_number:
            self.phone_numbers.append(formatted_number)
            self.phone_entry.delete(0, tk.END)
            print(f"Phone number added: {formatted_number}")
        else:
            print("Invalid phone number format.")

    def send_sms(self):
        for phone_number in self.phone_numbers:
            message = client.messages.create(
                body=generate_message(),
                from_=twilio_phone_number,
                to=phone_number
            )
            print(f"Message sent to: {phone_number}")

# Run the application
root = tk.Tk()
app = BulkSMSApp(root)
root.mainloop()
```

To use this script, replace the placeholder values with your actual Twilio credentials and phone numbers. You can then run the script to use the bulk SMS sender.

## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with .

- Vite
- React
- shadcn-ui
- Tailwind CSS

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/sms-blast-master.git
cd sms-blast-master
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
