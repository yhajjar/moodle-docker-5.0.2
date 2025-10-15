# Moodle Docker
### Recommended Specs
```txt
CPU: 4 Core
RAM: 8 GB
Storage: 30 GB
Versi OS:  Ubuntu 20.04
```

## Setup VPS dan Docker:
install docker https://docs.docker.com/engine/install/ubuntu/ 

berikan hak pada docker ```usermod -aG docker $USER```

## Setup Moodle
- Clone repo
```bash
git clone https://github.com/Derkora/moodle-docker
cd moodle-docker
```
- Ubah .env
```bash
cp .env.example .env
```
- Buat docker image moodle (opsional)
```bash
cd ver/5.0-nginx
docker build -t derkora/moodle:5.0-nginx .
```
- Run Docker
```bash
docker compose up -d
```

# Setup Web
masuk ke http://IP-VPS ikuti langkah ini di web
- language "Next"
- Confirm paths "Next"
- Choose database driver "MariaDB"
- Database settings
    - Database host moodle_db
    - Database name moodle
    - Database user ${MOODLE_DATABASE_USER}
    - Database Password ${MOODLE_DATABASE_PASSWORD}
- Installation - Moodle ... "Continue aja"
- Nunggu instalasi (agak lama)
- Masukin user admin dan moodle sesuai kebutuhan

## Deploying on Coolify
1. Push this repository (with the updated `docker-compose.yml`) to a Git provider that is connected to your Coolify instance.
2. In Coolify, create a new project, choose **Docker Compose**, select the repository and branch, and set the compose path to `docker-compose.yml`.
3. Add the following environment variables in the Coolify service settings (they can be added from `.env.example` or directly in the UI):
   - `MYSQL_ROOT_PASSWORD`
   - `MOODLE_DATABASE_USER`
   - `MOODLE_DATABASE_PASSWORD`
4. Expose port `80` for the Moodle service and, if you plan to use a custom domain, assign it in Coolify (Coolify will handle HTTPS).
5. Deploy the stack. The default Docker volumes (`moodle_data`, `moodledata`, and `moodle_db_data`) are created automatically and persist across redeploys.
6. After the containers are healthy, browse to the assigned domain/URL and finish Moodle's web installer using the same database credentials you configured above.
