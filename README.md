WhatsApp Automation Workflows with n8n
Two powerful n8n workflows that bring weather updates and news directly to WhatsApp - one interactive bot and one automated morning briefing service.

📋 Table of Contents
Overview
Workflows
Prerequisites
Installation
Configuration
Usage
API Keys Required
Troubleshooting
Contributing
License
🔍 Overview
This repository contains two WhatsApp automation workflows built with n8n:

Interactive WhatsApp Bot - Responds to user commands for weather and news
Morning Briefing - Automatically sends daily weather and news updates
Both workflows use Twilio for WhatsApp messaging, OpenWeatherMap for weather data, and NewsAPI for news headlines.

📁 Workflows
Workflow 1: WhatsApp Interactive Bot
File: WhatsApp Interactive Bot.json

Description: An interactive WhatsApp bot that responds to user messages with real-time weather and news information.

Trigger: Webhook (receives incoming WhatsApp messages via Twilio)

Key Features:

Responds to "weather" command with current Raleigh weather
Responds to "news" command with top 3 US news headlines
Automatic message parsing and routing
Error handling for malformed requests
How it works:

User sends a WhatsApp message to your Twilio number
Webhook receives the message
JavaScript code parses the message content
Switch node routes to appropriate action (weather or news)
API calls fetch the requested data
Response is formatted and sent back via WhatsApp
Nodes Used:

Webhook (POST endpoint)
Code (JavaScript) - 3 nodes for parsing and formatting
HTTP Request - 2 nodes for API calls
Switch - Routes messages based on content
Merge - Combines different response paths
Twilio - Sends WhatsApp message response
Workflow 2: WhatsApp Morning Briefing
File: WhatsApp Morning Briefing.json

Description: Automatically sends a daily morning briefing with weather and news to WhatsApp at 7:08 AM.

Trigger: Schedule (Cron: 8 7 * * * - Daily at 7:08 AM)

Key Features:

Automated daily delivery at scheduled time
Combined weather and news in one message
Formatted with emojis for better readability
No user interaction required
How it works:

Schedule triggers workflow at 7:08 AM daily
Fetches current weather for Raleigh
Fetches top 3 US news headlines
Combines both into formatted message
Sends complete briefing via WhatsApp
Nodes Used:

Schedule Trigger (Cron expression)
HTTP Request - 2 nodes for APIs
Code (JavaScript) - Formats combined message
Twilio - Sends WhatsApp message
✅ Prerequisites
Before importing these workflows, ensure you have:

n8n installed (self-hosted or cloud)
Twilio account with WhatsApp enabled
Twilio phone number with WhatsApp capability
Account SID and Auth Token
API Keys:
OpenWeatherMap API key (free tier available)
NewsAPI key (free tier available)
WhatsApp Sandbox configured (for testing) or approved Twilio WhatsApp sender
🚀 Installation
Step 1: Clone or Download
Clone this repository or download the JSON files:

bash
git clone https://github.com/yourusername/whatsapp-n8n-workflows.git
Step 2: Import Workflows into n8n
For each workflow:

Open your n8n instance
Click on "Workflows" in the left sidebar
Click "Add workflow" → "Import from File"
Select the workflow JSON file
Click "Import"
Step 3: Get API Keys
OpenWeatherMap:

Sign up at https://openweathermap.org/api
Generate a free API key
Copy your API key
NewsAPI:

Sign up at https://newsapi.org/
Get your free API key
Copy your API key
Twilio:

Sign up at https://www.twilio.com/
Get your Account SID and Auth Token from the console
Set up WhatsApp Sandbox or get approved for production
⚙️ Configuration
1. Configure Twilio Credentials
In n8n:

Go to Credentials → Add Credential
Search for "Twilio"
Enter your:
Account SID
Auth Token
Save the credential
2. Update Workflow Settings
For WhatsApp Interactive Bot:

Webhook Node:
Note your webhook URL (will be shown when you open the node)
Configure this URL in your Twilio WhatsApp settings
HTTP Request Nodes:
Update weather API URL with your OpenWeatherMap API key:
     https://api.openweathermap.org/data/2.5/weather?q=YOUR_CITY&appid=YOUR_API_KEY&units=metric
Update news API URL with your NewsAPI key:
     https://newsapi.org/v2/top-headlines?country=us&pageSize=3&apiKey=YOUR_API_KEY
Twilio Node:
Update the "From" number (your Twilio WhatsApp number)
Update the "To" number (your WhatsApp number for testing)
Select your Twilio credentials
For WhatsApp Morning Briefing:

Schedule Trigger:
Adjust the cron expression if you want a different time
Default: 8 7 * * * (7:08 AM daily)
HTTP Request Nodes:
Update both API URLs with your API keys (same as above)
Twilio Node:
Update the "From" and "To" numbers
Select your Twilio credentials
Code Node (Optional):
Customize the message format
Change the city for weather
Adjust number of news articles
3. Configure Twilio Webhook (Interactive Bot Only)
Log into Twilio Console
Go to your WhatsApp Sandbox or WhatsApp sender
Under "When a message comes in", paste your n8n webhook URL:
   https://your-n8n-instance.com/webhook/whatsapp-bot
Set method to POST
Save configuration
📖 Usage
Interactive WhatsApp Bot
To use the bot:

Activate the workflow in n8n
Send a WhatsApp message to your Twilio number
Send keyword commands:
Type "weather" to get current weather
Type "news" to get top news headlines
Example conversation:

You: weather
Bot: 🌤️ Weather in Raleigh: 22°C, clear sky

You: news
Bot: 📰 Top News:

1. [Headline 1]

2. [Headline 2]

3. [Headline 3]
Morning Briefing
Automated delivery:

Activate the workflow in n8n
The briefing will automatically send daily at 7:08 AM
No action needed from you!
Manual test:

Open the workflow
Click "Execute Workflow" to test immediately
Example briefing message:

🌅 Good Morning!

📍 Weather in Raleigh
22°C - clear sky

📰 Top News Today:
1. [Headline 1]

2. [Headline 2]

3. [Headline 3]

Have a great day! 🚀
🔑 API Keys Required
Service	Purpose	Free Tier	Get Key
OpenWeatherMap	Weather data	✅ Yes	https://openweathermap.org/api
NewsAPI	News headlines	✅ Yes (100 req/day)	https://newsapi.org/
Twilio	WhatsApp messaging	⚠️ Trial available	https://www.twilio.com/
Note: Replace the API keys in the workflow files with your own keys. The keys in the files are examples only.

🛠️ Troubleshooting
Webhook not receiving messages:

Verify webhook URL is correctly configured in Twilio
Ensure workflow is activated in n8n
Check n8n execution logs for errors
API requests failing:

Verify your API keys are correct and active
Check API rate limits (NewsAPI free tier: 100 requests/day)
Ensure the city name in weather API is correct
WhatsApp messages not sending:

Confirm Twilio credentials are properly configured
Verify phone numbers are in correct format (+1234567890)
Check if you're still in Twilio sandbox mode (requires WhatsApp template approval)
Scheduled workflow not running:

Verify workflow is activated
Check cron expression is correct
Review n8n's execution history
🎨 Customization Ideas
Change location: Update the city in weather API calls
Different news sources: Change country or category in NewsAPI
Add more commands: Extend the Switch node with new options
Multiple recipients: Add more phone numbers to send briefings
Different schedule: Modify cron expression for different times
Add quotes: Include daily motivational quotes
Weather alerts: Add conditions to send alerts for extreme weather
🤝 Contributing
Contributions welcome! Feel free to:

Add new features
Improve error handling
Add more command options
Create pull requests
📝 License
MIT License - Feel free to use and modify these workflows for your needs.

🆘 Support
n8n Documentation: https://docs.n8n.io/
n8n Community: https://community.n8n.io/
Twilio WhatsApp Docs: https://www.twilio.com/docs/whatsapp
⚠️ Important Notes
Twilio Costs: WhatsApp messages may incur charges after trial period
API Limits: Free tiers have daily request limits
Privacy: Protect your API keys and credentials
Phone Numbers: Update all phone numbers before deploying
Created with: n8n
Last Updated: October 2025
Requires n8n version: 1.0+

# n8n-workflows
