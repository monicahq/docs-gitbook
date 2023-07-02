# Setup Telegram

Users can setup Telegram to receive notifications. This is a bit tricky to set up from an instance's administration point of view if you want to test locally.

First of all, you need to setup a Telegram bot to be able to receive notifications. Then you need to configure Monica with the right .env variables. Finally, you need to send the webhook URL to Telegram so Telegram can communicate with your local setup.

#### First, create your Telegram bot

Follow the first steps described in [https://docs.microsoft.com/en-us/azure/bot-service/bot-service-channel-connect-telegram?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-channel-connect-telegram?view=azure-bot-service-4.0) so you can create a bot. Note that **you will need the token that Telegram will send you right after creating your bot**.

#### Fill in your Telegram .env variables

Locate the .env file and fill these three variables that are about Telegram.

```shell
TELEGRAM_BOT_TOKEN=393828013:AAEaw8ewefwhKIdkW2E
TELEGRAM_BOT_URL=https://t.me/monicahq_bot
TELEGRAM_BOT_WEBHOOK_URL=lkjl2kjl2k3232IOWEJFkek
```

The _bot token_ is given by Telegram after you create the bot.

The _bot URL_ is the URL of your bot. It's derivated from the name of your bot (for us, it's `monicahq_bot`), prefixed by `https://t.me/`. The name of your bot is the username that you've chosen upon the creation of your bot.&#x20;

The _webhook URL_ is not an URL per se. It's a random string, as long as possible, that will be used to sign the webhooks sent by Telegram. You have to defined it yourself.

#### Setup Telegram

We now need to inform Telegram which webhook URL it should use to send notifications.

{% hint style="info" %}
If you need to configure Telegram for development purposes, your Monica instance will likely not have an external URL. You would have to use either [ngrok](https://ngrok.com/) or [Expose](https://expose.dev/) to have a public URL that Telegram will use to send you notifications. If you use one of these, simply use the URL they give you in the `public url` parameter below.
{% endhint %}

The structure of the webhook URL should be as follow

```bash
https://[PUBLIC URL].'/telegram/webhook/'.[TELEGRAM_BOT_WEBHOOK_URL]
```

Let's assume your public URL is https://app.monicahq.com (our instance). If we take this URL and the .env variables set above, the webhook URL will be:

```
https://app.monicahq.com/telegram/webhook/lkjl2kjl2k323oIOWEJFkek
```

Now, we need to inform Telegram of this webhook URL. Telegram needs this structure:

```
https://api.telegram.org/bot[TELEGRAM_BOT_TOKEN]/setWebhook?url=[https://[PUBLIC URL].'/telegram/webhook/'.[TELEGRAM_BOT_WEBHOOK_URL]]
```

In our case, we would have this URL

```
https://api.telegram.org/bot393828013:AAEaw8ewefwhKIdkW2EIy23ksVY51XQqsV7o_3M/setWebhook?url=https://app.monicahq.com/telegram/webhook/lkjl2kjl2k323oIOWEJFkek
```

Simply copy and paste the URL above in your browser and Telegram should send you this JSON back.

```json
{"ok":true,"result":true,"description":"Webhook was set"}
```

That means your URL is registered, and Telegram will work.
