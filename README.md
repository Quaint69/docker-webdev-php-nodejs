# What is it

A Docker-compose setup for running multiple databases and development environments:

* **Development Environments:** PHP, Node.js (Javascript/Typescript)
* **Databases:** MariaDB, PostgreSQL, MongoDB, SQLite
* **Web-based DB tools:** phpMyAdmin, pgAdmin, Mongo Express, PHPLiteAdmin
* **Cached data:** speeds up Node/npm and PHP/composer installs for faster dev

---

## Services

### Databases

| Service       | Image                        | Access                                         | Login           |
| ------------- | ---------------------------- | ---------------------------------------------- | --------------- |
| MariaDB       | mariadb:10.11                | [http://localhost:1001](http://localhost:1000) | root / 11111111 |
| phpMyAdmin    | phpmyadmin:latest            | [http://localhost:1001](http://localhost:1001) | root / 11111111 |
| PostgreSQL    | postgres:16-alpine           | [http://localhost:1003](http://localhost:1003) | root / 11111111 |
| pgAdmin       | dpage/pgadmin4:latest        | [http://localhost:1003](http://localhost:1003) | root / 11111111 |
| MongoDB       | mongo:7                      | [http://localhost:1005](http://localhost:1005) | root / 11111111 |
| Mongo Express | mongo-express:latest         | [http://localhost:1005](http://localhost:1005) | admin / pass    |
| PHPLiteAdmin  | vtacquet/phpliteadmin:latest | [http://localhost:1006](http://localhost:1006) | no login        |

---

### Development Environments

| Service | Image              | Access                                         | Notes                                                                                                                    |
| ------- | ------------------ | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| PHP     | php:8.3-cli-alpine | [http://localhost:1090](http://localhost:1090) | Code in `/php/index.php`                                                                                                 |
| Node.js | node:24-alpine     | [http://localhost:1091](http://localhost:1091) | Code in `/node/app.js` or `/node/<your-react/nextjs-app>/app/page.tsx` if React/Next.js installed via `npm` in container |

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
docker-compose up -d
```

* Node → [http://localhost:1091](http://localhost:1091), [http://localhost:3333](http://localhost:3333) (React/Next.js after setting up `package.json`)
* Head to Docker.desktop > containers > name column, node-1 (click name) > exec column > npx create-next-app@latestnpm / or react equivalent

* Goodluck!
