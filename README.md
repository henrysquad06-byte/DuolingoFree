# Free Duolingo Super Subscription (aka Plus)

**DuolingoFree** is a web service that automates the referral flow to obtain free Duolingo Plus (Super) time.

All a user needs to do is provide a referral link obtained from the Duolingo app — the service will register a new user using that referral link and you receive one week of subscription for each successful referral.

## Requirements

This project is designed to run in containers and requires the following services:

- Docker
- docker-compose
- traefik (you should already have Traefik configured in your environment)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/henrysquad06-byte/DuolingoFree.git
cd DuolingoFree
```

2. Copy the example docker-compose file:

```bash
mv docker-compose.example.yml docker-compose.yml
```

3. Open and edit `docker-compose.yml`. For the `migrate` service set the following environment variables (or leave defaults):

- `DJANGO_SUPERUSER_USERNAME` — admin username
- `DJANGO_SUPERUSER_PASSWORD` — admin password
- `DJANGO_SUPERUSER_EMAIL` — admin email address

For the `gunicorn` service, add the appropriate Traefik labels and make sure to set the host where the service should be available.

For the `celery` service, provide environment variables for Telegram notifications:

- `TELEGRAM_BOT_TOKEN` — your bot token
- `TELEGRAM_CHAT_ID` — the chat id (note: chat ids for groups often start with a `-`)

## Running

If everything is configured properly, build and start the services:

```bash
docker-compose build
docker-compose up -d
```

The web service will be available on the host configured for the `gunicorn` service.

## Notes and configuration

- Do not commit secrets (tokens, passwords) to the repository. Use environment variables or a `.env` file that is listed in `.gitignore`.
- Adjust ports, Traefik rules, and other deployment details to match your infrastructure.

## Useful links

- [Project overview and description (in Russian)](https://egorovegor.ru/duolingo-plus/)
- [How does Duolingo's referral program work?](https://support.duolingo.com/hc/ru/articles/4404225309581-How-does-the-referral-program-work-)
- [How to check subscription status (Duolingo support)](https://support.duolingo.com/hc/ru/articles/4404225723021-Как-проверить-статус-подписки-)


If you want, I can also:
- Translate the rest of the project docs or comments into English,
- Add example environment files and a sample Traefik configuration,
- Create a brief quick-start that matches the actual project entrypoint (tell me which file starts Django or Gunicorn, or I can inspect the code and update the README accordingly).
