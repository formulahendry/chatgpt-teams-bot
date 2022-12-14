# How to use this ChatGPT Teams Bot app

This is a ChatGPT Teams Bot app to let you chat with ChatGPT in Microsoft Teams.

![ChatGPT](./images/chatgpt-chat.png)

## Prerequisites

- A ChatGPT account
- [NodeJS](https://nodejs.org/en/) (**version >= 18**) (Tested on Node.js 18.12.1)
- An M365 account. If you do not have M365 account, apply one from [M365 developer program](https://developer.microsoft.com/en-us/microsoft-365/dev-program)
- Latest stable version of [Teams Toolkit Visual Studio Code Extension](https://aka.ms/teams-toolkit) (Tested on version 4.1.3)

## Set up ChatGPT token

On December 11, 2022, OpenAI added some additional Cloudflare protections which make it more difficult to access the unofficial API.

You'll need a valid OpenAI "session token" and Cloudflare "clearance token" in order to use the API.

1. Go to https://chat.openai.com/chat and log in or sign up.
1. Open dev tools.
1. Open `Application` > `Cookies`.
   ![ChatGPT cookies](./images/chatgpt-session-token.png)
1. Copy the value for `__Secure-next-auth.session-token`. This will be your `CHATGPT_SESSION_TOKEN`.
1. Copy the value for `cf_clearance`. This will be your `CLEARANCE_TOKEN`.
1. Copy the value of the `user-agent` header from any request in your `Network` tab. (Or type `navigator.userAgent` in Console of your dev tools) This will be your `USER_AGENT`.
1. Create a `.env.teamsfx.local` file under `bot` folder, and set the above value in `.env.teamsfx.local` file:
    ```
    CHATGPT_SESSION_TOKEN=xxxxxxxxxx
    CLEARANCE_TOKEN=xxxxxxxxxx
    USER_AGENT=xxxxxxxxxx
    ```

## Debug

- From Visual Studio Code: Start debugging the project by hitting the `F5` key in Visual Studio Code. 
- Alternatively use the `Run and Debug Activity Panel` in Visual Studio Code and click the `Run and Debug` green arrow button.

## Restrictions

**Please read carefully**

- You must use `node >= 18` at the moment. I'm using `v18.12.1` in my testing.
- Cloudflare `cf_clearance` **tokens expire after 2 hours**, so right now we recommend that you refresh your `cf_clearance` token every hour or so.
- Your `user-agent` and `IP address` **must match** from the real browser window you're logged in with to the one you're using for `ChatGPTAPI`.
  - This means that only local-debug is supported for now. You currently can't log in with your laptop and then run the bot on a server or proxy somewhere.
- You should not be using this account while the bot is using it, because that browser window may refresh one of your tokens and invalidate the bot's session.

## Further reading

- [chatgpt-api Node SDK](https://github.com/transitive-bullshit/chatgpt-api): it is a 3rd-party ChatGPT npm used in this Teams bot. 
