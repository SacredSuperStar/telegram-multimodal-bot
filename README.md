# ChatGPT Telegram Bot with Image support

Forked from [this repo](https://github.com/altryne/chatGPT-telegram-bot)


https://user-images.githubusercontent.com/22678055/210846293-cc599952-2765-4e0d-94cf-90fe38dbf3b3.mp4




This is a Telegram bot that lets you chat with the [chatGPT](https://github.com/openai/gpt-3) language model using your local browser, and uses the [Carrot](https://www.banana.dev/blog/banana-launches-carrot) model to add image support to chatGPT. The bot uses Playwright to run chatGPT in Chromium, and can parse code and text, as well as send messages. It also includes a `/draw` command that allows you to generate pictures using stable diffusion. More features are coming soon.

## Features

- Chat with chatGPT from your Telegram on the go
- Send images to chatGPT and ask questions/talk about the image
- `/draw` pictures using stable diffusion (version 0.0.2)
- `/browse` give chatGPT access to Google (version 0.0.3)

## How to Install

### Step 1: Install Python and Miniconda

1. Go to the [Miniconda download page](https://docs.conda.io/en/latest/miniconda.html).
2. Click on the appropriate installer for your operating system.
3. Follow the prompts to complete the installation.

### Step 2: Create a conda environment

1. Open a terminal or command prompt.
2. Navigate to the directory where you want to create the environment.
3. Run `conda env create -f environment.yml` to create the environment.
4. Activate the newly created environment `conda activate chat`

### Step 3: Install Playwright

1. Open a terminal or command prompt.
2. Navigate to the directory where you installed Miniconda.
3. Run `playwright install` to download the necessary Chromium software.
4. Run `playwright install-deps` to download the necessary dependencies

### Step 4: Set up your Telegram bot

1. Set up your Telegram bot token and user ID in the `.env` file. See [these instructions](https://core.telegram.org/bots/tutorial#obtain-your-bot-token) for more information on how to do this.

> How to obtain telegram user id? Add telegram [userinfobot](https://t.me/useridinfobot) to your telegram contacts

2. Edit the `.env.example` file, rename it to `.env`, and place your values in the appropriate fields.
   
### Step 5: Set up your carrot model on Banana

1. Sign up at [app.banana.dev](https://app.banana.dev)

2. Go to the deploy tab, and select Carrot (Image QA) 
<img width="1122" alt="image" src="https://user-images.githubusercontent.com/22678055/210836280-15ea1240-4270-4512-ae04-74872b8bfd6c.png">

3. Go into the model card, and copy your model key
<img width="684" alt="image" src="https://user-images.githubusercontent.com/22678055/210836596-9f15d4f7-0d3e-4438-9935-bf1ff06a092d.png">

4. Define the banana model key and api key in the .env file

### Step 6: Set up your API keys

1. Copy the `.env.example` file and rename the copy to `.env`.
2. To use the `/draw` command, you will need to obtain an API key for stable diffusion. To do this, go to [Dream Studio Beta](https://beta.dreamstudio.ai/membership?tab=home) and sign up for a free membership.
3. SERP_API_KEY is optional. If you want to use the `/browse` command, you will need to obtain an API key for SERP. To do this, go to [SERP API](https://serpapi.com/) and sign up for a free account.

### Step 7: Run the server

1. Open a terminal or command prompt.
2. Navigate to the directory where you installed the ChatGPT Telegram bot.
3. Run `python server.py` to start the server.

### Step 8: Chat with your bot in Telegram

1. Open the Telegram app on your device.
2. Find your bot in the list of contacts (you should have already created it with @botfather).
3. Start chatting with your bot.

## If you're using Docker inside a server (headless mode)

You can use the docker image to launch your bot in a server (using playwright headless mode)

`docker-compose` example

```docker-compose
services:
  chatgpt-telegram-bot:
    image: ghcr.io/altryne/chatgpt-telegram-bot
    container_name: chatgpt-telegram-bot
    environment:
      - TELEGRAM_API_KEY=
      - TELEGRAM_USER_ID= #Use this with your user ID to restrict usage only to your account
      - BANANA_API_KEY = #For image captioning
      - BANANA_MODEL_KEY = #For image captioning
      - STABILITY_API_KEY= #use this if you want the bot to draw things with stability AI as well
      - SERP_API_KEY= #add this from serpapi if you want to enable the google search feature
      - OPEN_AI_EMAIL= #openai login email. Needed for autologin in headless mode
      - OPEN_AI_PASSWORD= #openai password. Needed for autologin in headless mode
```

## Credits

- Based on the [repo](https://github.com/altryne/chatGPT-telegram-bot) by [@Altryne](https://twitter.com/altryne/status/1598902799625961472) on Twitter
