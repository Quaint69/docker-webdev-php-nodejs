# What is it

A Docker Compose setup for running multiple databases and development environments — Alpine-leaning for minimal storage footprint:

* **Development Environments:** PHP, Node.js (Javascript/Typescript)
* **Databases:** MariaDB/MySQL, PostgreSQL, MongoDB, SQLite
* **Web-based DB tools:** phpMyAdmin, pgAdmin, Mongo Express, PHPLiteAdmin
* **Cached data:** speeds up Node/npm and PHP/composer installs for faster dev

---

## Services

### Databases

| Service       | Image                        | Access                                         | Login           |
| ------------- | ---------------------------- | ---------------------------------------------- | --------------- |
| MariaDB/MySQL | mariadb:10.11                | [http://localhost:1000](http://localhost:1000) | root / 11111111 |
| phpMyAdmin    | phpmyadmin:fpm-alpine        | [http://localhost:1001](http://localhost:1001) | root / 11111111 |
| PostgreSQL    | postgres:16-alpine           | [http://localhost:1002](http://localhost:1002) | root / 11111111 |
| pgAdmin       | dpage/pgadmin4:latest        | [http://localhost:1003](http://localhost:1003) | root / 11111111 |
| MongoDB       | mongo:7                      | [http://localhost:1004](http://localhost:1004) | root / 11111111 |
| Mongo Express | mongo-express:latest         | [http://localhost:1005](http://localhost:1005) | admin / pass    |
| PHPLiteAdmin  | vtacquet/phpliteadmin:latest | [http://localhost:1006](http://localhost:1006) | no login        |

### Development Environments

| Service | Image              | Access                                         | Notes                                                                                                                    |
| ------- | ------------------ | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| PHP     | php:8.3-cli-alpine | [http://localhost:1090](http://localhost:1090) | Code in `/php/index.php`                                                                                                 |
| Node.js | node:24-alpine     | [http://localhost:1091](http://localhost:1091) | Code in `/node/app.js` — auto-stubs an HTTP server on :1091 if missing                                                   |

> **Node.js & React/Next.js users:** To expose your app on port 3333, modify `package.json`:
>
> ```json
> "scripts": {
>   "dev": "next dev -H 0.0.0.0 -p 3333"
> }
> ```

---

## Cached Data Benefits

* **Composer cache:** faster PHP dependency installs
* **Node modules:** keeps installed packages for quick Node/npm startup
* **NPM cache:** speeds up repeated installs and avoids redownloading

---

## How to Run

```bash
docker compose up -d
```
* PHP → `/php`, write your `index.php`, browse http://localhost:1090
* Node → `/node`, app.js is auto-created if missing (starts an HTTP server on :1091)
* Node modules install in the container via `docker exec -it node-1 sh` → `npm install ...`

---

## Storage Notes

Where possible, images use Alpine Linux variants to keep the footprint small:
- **phpmyadmin:fpm-alpine** instead of the default Debian-based image
- **php:8.3-cli-alpine**, **node:24-alpine**, **postgres:16-alpine**
- phpMyAdmin is also on Alpine via the `fpm-alpine` tag
- Services without official Alpine tags (MariaDB, MongoDB, pgAdmin) run on their default base

*Good luck!*