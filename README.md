# Run Strapi on Google Cloud Shell

This repo serves as a code container for the tutorial written on Hashnode.

## Prerequisites

- Google Account
- Any Chromium-based browser
- Ngrok Account

## Getting Started

- Navigate to [Google Cloud Shell](https://shell.cloud.google.com)
- In the Cloud Shell Terminal, clone the repo:
```bash
git clone https://github.com/Marktawa/strapi-cloud-shell
```
- Open the project directory:
```bash
cd strapi-cloud-shell
```

## Strapi Setup

- Change directory to Strapi project folder.
```bash
cd backend
```

- Install dependencies.
```bash
npm install
```

- Run Strapi app.
```bash
npm run develop
```

## Ngrok Setup

- In new Google Cloud Shell terminal tab, change directory to root project folder.
```bash
cd strapi-cloud-shell
```

- Add `ngrok` to the instance's path.
```bash
sudo cp ngrok /usr/local/bin
```

- Add your Ngrok authtoken.
```bash
ngrok config add-authtoken <Authtoken>
```
> **NOTE:** *Replace with your specific ngrok account Authtoken*

- Run ngrok to listen on Strapi app's port.
```bash
ngrok http 1337
```

## Authors

- [Mark Tawanda Munyaka](https://github.com/Marktawa)

## Extra

- You are welcome to make [issues and feature requests](https://github.com/Marktawa/strapi-aws-s3/issues).


