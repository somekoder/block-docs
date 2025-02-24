# Quickstart
## Docker

In the example below, we are deploying the authentication block using docker compose and default values for configuration.

![GitHub Release](https://img.shields.io/github/v/release/somekoder/block-auth-api?include_prereleases)

## Quickstart
```yaml
services:
  auth-api:
    image: ghcr.io/somekoder/auth-api:latest
    # image: ghcr.io/somekoder/auth-api-snapshot:latest # For snapshots
    ports:
      - 8080:8080
    environment:
      JWT_SECRET: "secret" # Make this a long secure string
      DATABASE_USER: $DATABASE_USER
      DATABASE_PASSWORD: $DATABASE_PASSWORD
      DATABASE_URL: database # Referring to the database below
      DATABASE_NAME: $DATABASE_NAME

  database:
    image: postgres
    restart: always
    shm_size: 128mb
    environment:
      POSTGRES_PASSWORD: $DATABASE_PASSWORD
      POSTGRES_USER: $DATABASE_USER
      POSTGRES_DB: $DATABASE_NAME
    ports:
      - 5432:5432
    volumes:
      - /path/to/database:/var/lib/postgresql/data
```

## Environment Variables

Below is a list of configurations that can be changed using environment variables.

| Variable                     | Description                                         | Default                                             |
|------------------------------|-----------------------------------------------------|-----------------------------------------------------|
| `DATABASE_URL`               | IP address or URL of the database                   |                                                     |
| `DATABASE_USER`              | Username for the database user                      |                                                     |
| `DATABASE_PASSWORD`          | Password for the database user                      |                                                     |
| `DATABASE_NAME`              | Name of the database                                |                                                     |
| `JWT_SECRET`                 | Secret for generating and verifying JSON web tokens |                                                     |
| `JWT_ISSUER`                 | Issuer attached to the JSON web tokens              | `issuer`                                            |
| `JWT_AUDIENCE`               | Audience attached to the JSON web tokens            | `user`                                              |
| `JWT_EXPIRES_IN`             | Milliseconds in which tokens expire                 | `600000 # 10 mins`                                  |
| `REFRESH_EXPIRES_IN`         | Milliseconds in which refresh tokens expire         | `2629746000 # 1 month`                              |
| `PASSWORD_MIN_LENGTH`        | Minimum number of characters for password           | `8`                                                 |
| `PASSWORD_MAX_LENGTH`        | Maximum number of characters for password           | `32`                                                |
| `PASSWORD_REQUIRE_NUMBER`    | Passwords require a numerical character             | `true`                                              |
| `PASSWORD_REQUIRE_SPECIAL`   | Passwords require a special character               | `true`                                              |
| `PASSWORD_REQUIRE_LOWERCASE` | Require at least one lowercase letter               | `true`                                              |
| `PASSWORD_REQUIRE_UPERCASE`  | Require at least one uppercase letter               | `true`                                              |
| `EMAIL_REGEX`                | Regex used for validating emails                    | `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$` |