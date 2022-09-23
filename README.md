# Setup for Workadventure

See https://github.com/thecodingmachine/workadventure

docker-compose.yml setting for a productive enviromnent


#### File docker-compose.yml

This is a copy of the current workadventure/contrib/docker/docker-compose.prod.yaml from https://github.com/thecodingmachine/workadventure (stand 2022/09/23) with two tiny modifications, the most obvious being the addition of `- CHAT_URL=//${CHAT_HOST}` in the environment of the front service.

#### File .env.prod.template

This is a copy of the current workadventure/contrib/docker/.env.prod.template from https://github.com/thecodingmachine/workadventure (stand 2022/09/23) with the only change of one variable for the directory where to store the letsencrypt certificates.

### Instructions:
* git clone this repository in a folder on your server.
```
git clone https://github.com/pmaneggia/wa-workadventure
```
* Make a copy of `.env.prod.template` in the same directory and rename it to .env (this file name is already in .gitignore).
* in `.env` change:
    * `DOMAIN=workadventure.localhost` into `DOMAIN=workadventure.<yourdomain>` or into `DOMAIN=workadventure.<yourIP>.nip.io` if you do not have a suitable domain yet (the usage of nip.io will help you circumvent the fact that you do not have any control on subdomains if you only have a public IP address for your server).
    * Similarly all the values of the variables in the list `Subdomains`, for example `FRONT_HOST=play.workadventure.localhost` into `FRONT_HOST=play.workadventure.<yourdomain>` or into `FRONT_HOST=play.workadventure.<yourIP>.nip.io`.
    * add a valid email address of yours at `ACME_EMAIL=`. This is necessary to obtain certificates from letsencrypt.

Ar this point it should be possibly to get running! Use
```
docker compose up -d
```
and you should be able to reach in short your own self hosted instance of workadventure under `play.workadventure.<yourdomain>` or `play.workadventure.<yourIP>.nip.io`.

Reminder: the `-d` option tells docker compose that you do not want to see the logs outputted in your terminal. Too access the log use `docker compose logs` or `docker logs <service>`. Use the flag `--follow` for a container/service if you want to see more than just a snapshot of the logs.