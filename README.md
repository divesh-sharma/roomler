# Roomler

> Roomler.Live - Live video conferencing & collaboration tool using WebRTC (Janus Gateway)

It's like Slack on Crack and Microsoft Teams on Steroids.
All that fully free and open source. 


[![Roomler Intro](https://img.youtube.com/vi/lzHeRwVDfPQ/0.jpg)](https://www.youtube.com/watch?v=lzHeRwVDfPQ)

# Features

## Multi party calls
* [x] Camera
* [x] Rich-text
* [x] Public Rooms

| MULTI PARTY CALLS       | POWERFUL CHAT           | ORGANIZED TEAMS         |
|-------------------------|-------------------------|-------------------------|
| <ul><li>[x] Video</li><li>[x] Audio</li><li>[x] Screen share</li><li>[x] Encrypted</li><li>[ ] Recording (soon...)</li></ul> | <ul><li>[x] Rich-text</li><li>[x] File sharing</li><li>[x] Emojis & Giphy's</li><li>[x] Mentions</li><li>[x] Reactions</li></ul> | <ul><li>[x] Public Rooms</li><li>[x] Private Rooms</li><li>[x] Hierarchy of Rooms</li><li>[x] User roles (moderator, member)</li><li>[x] Secure communication</li></ul> |



# Install packages
``` bash
# install dependencies
$ npm i
```

# Prerequisites
Before you run the app either in DEVELOPMENT, PRODUCTION mode or even run any of the TESTS, you need to setup couple of environment variables used in `/config/index.js`:

## Email setting
You have the following options to configure your app to send emails e.g. Activation link, Welcome email, Password change email etc.
1. SENDGRID account: `SENDGRID_API_KEY`
2. GMAIL account: `GMAIL_USER` and `GMAIL_PASSWORD`, but before sending your email using gmail you have to allow non secure apps to access gmail you can do this by going to your gmail settings [here](https://myaccount.google.com/lesssecureapps).
3. SMTP server you have access to: `SMTP_HOST`, `SMTP_PORT`, `SMTP_SECURE`, `SMTP_USER` and `SMTP_PASSWORD`

Please note that only one of those 3 options is needed to be properly setup in the exact order as above.

## Database setting
For running on localhost and you have MongodDB server instance also stared on localhost, this is not needed, otherwise your will need to provide the DB URL in the env variable `DB_CONN`

## DNS settings
Since you have the options to run two separate Fastify servers:
1. UI server (for rendering UI app using NuxtJS)
2. API server (for API calls)

then you might want to configure the environment variables `URL` for the UI and `API_URL` for the API server respectively.

On localhost, the default setting for these env variables is `URL=http://localhost:3000` and `API_URL=http://localhost:3001`


# Development

## Environment variables
Create `.env` file in the root folter: `roomler/.env`

```toml
HOST=localhost
JANUS_URL=wss://YOUR_JANUS_URL/janus_ws
SENDGRID_API_KEY=YOUR_SENDGRID_API_KEY
FACEBOOK_ID=YOUR_FACEBOOK_ID
FACEBOOK_SECRET=YOUR_FACEBOOK_SECRET
GOOGLE_ID=YOUR_GOOGLE_ID
GOOGLE_SECRET=YOUR_GOOGLE_SECRET
GITHUB_ID=YOUR_GITHUB_ID
GITHUB_SECRET=YOUR_GITHUB_SECRET
LINKEDIN_ID=YOUR_LINKEDIN_ID
LINKEDIN_SECRET=YOUR_LINKED_SECRET
TURN_URL=turn:YOUR_TURN_URL?transport=udp
TURN_USERNAME=YOUR_TURN_USERNAME
TURN_PASSWORD=YOUR_TURN_PASSWORD
GIPHY_API_KEY=YOUR_GIPHY_KEY
```


## Start in development mode

``` bash
# Start API server (localhost:3001)
$ npm run dev:api

# Start UI server (localhost:3000)
$ npm run dev:ui
```

# Production
## Start in production mode

``` bash
# build for production and launch server
$ npm run build
$ npm start
```

## Start using docker
```
docker run -d --name roomler \
    --hostname roomler \
    --restart always \
    -e API_URL=https://roomler.live \
    -p 8082:3000 \
    -e DB_CONN=YOUR_DB_CONN \
    -e WS_SCALEOUT_ENABLED=true \
    -e WS_SCALEOUT_HOST=redis \
    -e SENDGRID_API_KEY=YOUR_SEND_GRID_KEY \
    -e FACEBOOK_ID=YOUR_FACEBOOK_ID \
    -e FACEBOOK_SECRET=YOUR_FACEBOOK_SECRET \
    -e GOOGLE_ID=YOUR_GOOGLE_ID \
    -e GOOGLE_SECRET=YOUR_GOOGLE_SECRET \
    -e GITHUB_ID=YOUR_GITHUB_ID \
    -e GITHUB_SECRET=YOUR_GITHUB_SECRET \
    -e LINKEDIN_ID=YOUR_LINKEDIN_ID \
    -e LINKEDIN_SECRET=YOUR_LINKEDIN_SECRET \
    -e TURN_URL=YOUR_TURN_URL \
    -e TURN_USERNAME=YOUR_TURN_USERNAME \
    -e TURN_PASSWORD=YOUR_TURN_PASSWORD \
    -e GIPHY_API_KEY=YOUR_GIPHY_KEY \
    gjovanov/roomler
```


# Testing
## Run API tests

``` bash
# makes sure MongoDB is reachable based on /config/index.js (dbSettings)
$ npm run test:api
```

## Run E2E tests (TODO)

``` bash
# makes sure MongoDB is reachable based on /config/index.js (dbSettings)
# first start the API and UI servers in TEST envrionment
$ npm run start:test-e2e
# then run all E2E test
$ npm run test:e2e

```
